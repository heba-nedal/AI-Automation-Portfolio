# Course Knowledge Assistant --- RAG-Powered AI Agent

> An AI-powered course assistant that answers questions using a
> knowledge base built from the *AI Automation Starter Guide (2026
> Edition)*, while also providing general context when a topic is not
> covered by the guide.

------------------------------------------------------------------------

## 🎯 Problem

### The Context

Course materials often contain many pages of explanations, concepts, and
examples. Learners may need to search through the material repeatedly to
find a specific detail or clarify a concept.

### The Problem

Manually searching a long PDF can take time, and a conventional chat
model may answer from general knowledge without making clear whether the
answer is supported by the course material.

### Why It Matters

A course-specific assistant can make learning materials easier to query
and can distinguish information found in the guide from topics the guide
does not cover.

------------------------------------------------------------------------

## 💡 Solution

The Course Knowledge Assistant combines n8n, a Supabase vector database,
embeddings, and an AI agent to answer questions about the course guide.

What does the system do?

1.  Watches a designated Google Drive folder for newly created knowledge
    files.
2.  Downloads and extracts text from PDF files, then splits the text
    into smaller chunks.
3.  Creates embeddings and stores the document chunks and metadata in
    Supabase.
4.  Receives chat questions, retrieves relevant knowledge through the
    Supabase Vector Store, and generates a response with Google Gemini.

------------------------------------------------------------------------

## 👤 Users

**Primary Users:**\
Learners studying AI automation and n8n, or anyone who needs to query
the course guide.

**User Need:**\
Ask questions in natural language and quickly learn whether the guide
contains the answer. When the guide does not cover a topic, the
assistant can explicitly say so and then provide a general explanation.

------------------------------------------------------------------------

## 🧠 How I Designed the Solution

I separated the system into two workflows so that knowledge preparation
and question answering can be maintained and tested independently.

-   **Knowledge ingestion:** handles file detection, downloading, PDF
    text extraction, chunking, embedding, and vector storage.
-   **RAG chat agent:** handles incoming questions, retrieves relevant
    chunks from the vector store, and generates the response.
-   **Source-aware behavior:** the assistant can state when a concept is
    not mentioned or defined in the guide, while still providing a
    general explanation when useful.

This design keeps document preparation separate from the interactive
question-answering experience.

------------------------------------------------------------------------

## ⚙️ How It Works

``` text
KNOWLEDGE INGESTION

Google Drive folder (new file)
          ↓
Google Drive Trigger (polls every minute)
          ↓
Edit Fields → Download File → Extract from PDF
          ↓
Default Data Loader → Recursive Character Text Splitter
          ↓
OpenAI Embeddings → Supabase Vector Store


QUESTION ANSWERING

User question
     ↓
When Chat Message Received
     ↓
AI Agent ───── Google Gemini Chat Model
     │
     ├──────── Simple Memory
     │
     └──────── Supabase Vector Store
                         ↑
                 OpenAI Embeddings
     ↓
Response to the user
```

------------------------------------------------------------------------

## 🤖 Role of AI

What does AI do in this solution?

-   **Google Gemini Chat Model** interprets the user's question and
    generates a natural-language answer.
-   **OpenAI Embeddings** converts document chunks and search queries
    into vector representations used for semantic retrieval.
-   **RAG retrieval** gives the agent access to relevant content stored
    in the Supabase Vector Store.
-   **Simple Memory** supports conversational context across questions
    in the same conversation.

### What AI Should NOT Do

-   It should not present a general explanation as though it came from
    the course guide when the guide does not cover the topic.
-   It should not claim that the guide contains information that was not
    found in the source.

The intended behavior for out-of-scope questions is to state the
limitation of the guide and then clearly provide a general explanation
if appropriate.

------------------------------------------------------------------------

## 🔄 Automation

What parts of the process are automated?

-   The Google Drive Trigger is configured to check the `Knowledge Base`
    folder every minute for newly created files.
-   The ingestion workflow downloads a file, extracts PDF text, splits
    it into chunks, and passes the document to the Supabase Vector Store
    with embeddings.
-   During chat, the AI Agent can use the vector store to retrieve
    relevant knowledge before composing an answer.

The trigger configuration is documented in [the Google Drive Trigger
screenshot](./screenshots/11-google-drive-trigger-settings.png). A
successful end-to-end automatic run for a newly added file is not
claimed here unless separately verified.

------------------------------------------------------------------------

## 🗂️ Data

### Input

-   A PDF course guide: *The AI Automation Starter Guide (2026 Edition)*
    by Giovanni Beggiato.
-   Natural-language questions submitted through the n8n chat interface.
-   Extracted text, document metadata, and embedding vectors used by the
    retrieval workflow.

### Output

-   Natural-language answers to user questions.
-   An explicit note when a topic is not mentioned or defined in the
    course guide, followed by a general explanation when appropriate.
-   Stored document chunks and their metadata and embeddings in the
    Supabase `documents` table.

The visible table schema contains `id`, `content`, `metadata`, and
`embedding`. The table overview screenshot shows an estimated 233 rows
at the time of capture.

------------------------------------------------------------------------

## 🛠️ Tools & Technologies

  -----------------------------------------------------------------------
  Tool                                Purpose
  ----------------------------------- -----------------------------------
  n8n                                 Orchestrates the
                                      knowledge-ingestion and chat-agent
                                      workflows

  Google Drive                        Stores source files and triggers
                                      ingestion when a new file is
                                      created

  Supabase Vector Store               Stores document chunks and supports
                                      similarity-based retrieval

  PostgreSQL / `vector` data type     Stores document fields and
                                      embedding vectors in Supabase

  OpenAI Embeddings                   Generates vector representations
                                      for semantic search

  Google Gemini Chat Model            Generates responses to user
                                      questions

  Recursive Character Text Splitter   Splits extracted text into smaller
                                      chunks

  Default Data Loader                 Passes extracted document content
                                      and metadata into the vector-store
                                      pipeline
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 🔑 Key Design Decisions

### Decision 1 --- Separate Ingestion from Question Answering

**Decision:**\
Build two separate n8n workflows: one for processing source files and
another for answering chat questions.

**Why:**\
This separates document preparation from the live question-answering
path and makes each workflow easier to inspect and maintain.

### Decision 2 --- Use a Vector Store and Embeddings

**Decision:**\
Store chunked course content in Supabase and connect it to OpenAI
Embeddings.

**Why:**\
Semantic retrieval can find relevant passages based on meaning, rather
than relying only on exact keyword matches.

### Decision 3 --- Be Transparent About Missing Source Information

**Decision:**\
When a topic is not covered by the guide, state that limitation and
provide a general explanation separately.

**Why:**\
This preserves transparency without unnecessarily withholding a useful
general explanation. The globalization test demonstrates this intended
behavior.

------------------------------------------------------------------------

## 🧪 Testing

### Test 1 --- Ask for the Course Name

**Input:**\
`what is the course name`

**Expected Result:**\
The assistant identifies the guide by its title and provides relevant
information from the course materials.

**Actual Result:**\
The assistant identified *The AI Automation Starter Guide (2026
Edition)*, named Giovanni Beggiato as its creator, and listed several
chapters covered by the guide.

**Status:** ✅ Pass

**Evidence:** [Course-name
answer](./screenshots/06-test-course-name-answer.png)

------------------------------------------------------------------------

### Test 2 --- Ask About a Topic Not Covered by the Guide

**Input:**\
`what does 'globalization' mean`

**Expected Result:**\
The assistant states that the term is not mentioned or defined in the
course materials, then provides a general explanation rather than
implying that the explanation came from the guide.

**Actual Result:**\
The assistant stated that globalization was not mentioned or defined in
the guide, then provided a general-context definition.

**Status:** ✅ Pass

**Evidence:** [Out-of-scope topic
response](./screenshots/07-test-unsupported-term-general-answer.png)

------------------------------------------------------------------------

### Test 3 --- Review the RAG Agent Execution

**Input:**\
A course-related chat question submitted through the n8n chat interface.

**Expected Result:**\
The chat trigger and AI Agent execute successfully, with the configured
model, memory, and vector-store connections available to the agent.

**Actual Result:**\
The supplied n8n execution screenshots show successful execution
indicators for the chat trigger and AI Agent, with the connected model,
memory, vector store, and embeddings components visible.

**Status:** ✅ Pass

**Evidence:** [Successful
execution](./screenshots/08-rag-agent-successful-execution.png) ·
[Execution overview](./screenshots/09-rag-agent-execution-overview.png)

------------------------------------------------------------------------

## 📸 Evidence

### Final Result

The chat screenshots show the assistant answering a course-related
question and handling a topic that is outside the guide's scope.

![Final Result --- Course-name
answer](./screenshots/06-test-course-name-answer.png)

![Out-of-scope question
response](./screenshots/07-test-unsupported-term-general-answer.png)

### Workflow --- RAG Agent

![RAG Agent workflow](./screenshots/05-rag-agent-workflow.png)

![RAG Agent successful
execution](./screenshots/08-rag-agent-successful-execution.png)

### Workflow --- Knowledge Ingestion

![Knowledge ingestion
workflow](./screenshots/10-knowledge-ingestion-workflow.png)

![Google Drive Trigger
settings](./screenshots/11-google-drive-trigger-settings.png)

### Supabase Knowledge Storage

![Supabase documents table
schema](./screenshots/02-vector-table-schema.png)

![Supabase table overview](./screenshots/03-database-table-overview.png)

![Stored document chunks and
embeddings](./screenshots/04-stored-document-chunks.png)

------------------------------------------------------------------------

## ⚠️ Challenges & Failures

No implementation failures were reported during development.

One important design consideration was how to respond when a user asks
about something outside the source material. In the globalization test,
the assistant explicitly stated that the guide did not mention or define
the term, then gave a general explanation. This is intended behavior,
not a failed test.

------------------------------------------------------------------------

## 📚 What I Learned

### Technical Lesson

I learned how to connect document ingestion, PDF text extraction, text
chunking, embeddings, a vector database, and an AI agent in n8n.

### Problem-Solving Lesson

Separating the ingestion and retrieval workflows makes the system easier
to reason about, inspect, and test. Testing both an in-scope question
and an out-of-scope topic also helps evaluate different aspects of the
assistant's behavior.

### AI Lesson

A useful knowledge assistant should communicate the boundary between
source-grounded information and general model knowledge. Retrieval is
important, but transparent response behavior is also part of making an
AI system trustworthy.

------------------------------------------------------------------------

## 🔮 Future Improvements

If I continued developing this project, I would:

-   Add explicit source references or retrieved passage previews to
    answers, so users can verify where information came from.
-   Expand the test set to cover paraphrased questions, ambiguous
    questions, and topics only partially covered by the guide.
-   Add clearer monitoring and duplicate-file handling to the ingestion
    workflow.
-   Evaluate retrieval quality and tune chunk size and overlap using a
    consistent test set.
-   Add a dedicated user-facing interface if the assistant needs to be
    shared outside the n8n workspace.

------------------------------------------------------------------------

## 🔗 Project Links

**Live Demo:** Not provided; the assistant is currently demonstrated
through the n8n chat interface.

**Workflow:** Implemented in n8n. A shareable workflow URL was not
provided.

**Repository:** No GitHub repository for this project.

------------------------------------------------------------------------

## 👩‍💻 Author

**Heba Nedal**

[LinkedIn](https://www.linkedin.com/in/heba-n-ismail-b836b2377/) · [GitHub](https://github.com/heba-nedal)


