# Tiny Wins — AI-Powered Personal Growth Platform

> Every small win matters. Tiny Wins helps people recognize their daily achievements, reflect on their progress, and celebrate their personal growth.

---

## 1. Project Overview

**Tiny Wins** is an AI-powered personal growth platform designed to help individuals record their small daily achievements and turn them into a meaningful record of progress.

The platform combines achievement tracking, AI-powered reflection, and workflow automation to help users recognize their growth over time.

This project was developed as the Final Capstone Project for the **AI & Intelligent Automation Program**.

## 2. The Problem

People often overlook their small daily achievements because they seem insignificant at the moment.

Over time, these achievements may be forgotten, making it difficult to recognize personal progress, reflect on past experiences, or stay motivated.

Tiny Wins addresses this problem by providing a simple space where users can record their achievements, explore their progress, and receive personalized reflections.

## 3. Target Users

Tiny Wins is designed for individuals who:

- Want to build better personal growth habits.
- Want to track their daily achievements.
- Find it difficult to recognize their progress over time.
- Are interested in using AI for personal reflection and self-improvement.

## 4. Key Features

### Achievement Tracking
Users can record, manage, and organize their daily achievements in one place.

### AI Wins Assistant
An AI-powered assistant that answers questions based on the user's recorded achievements.

### Monthly Growth Reflection
AI-generated monthly reflections that summarize achievements, identify supported patterns, and suggest small next steps.

### Grow This Win
Helps users reflect on a selected achievement and explore practical ways to build on it.

### Win Garden
A visual representation of personal progress that connects recorded achievements with a simple growth indicator.

### Future Letters
Users can write letters to their future selves and schedule them to be delivered later through email.

### Telegram Integration
Users can link their Telegram accounts and interact with the platform through its Telegram integration.

## 5. Technology Stack

| Technology | Purpose |
|---|---|
| Lovable | Application development and user interface |
| Supabase | Authentication and database |
| Lovable AI Gateway | AI-powered features |
| n8n Cloud | Workflow automation and integrations |
| Gmail | Future letter delivery |
| Telegram Bot | Telegram integration and notifications |

## 6. How It Works

1. Users create an account and access their personal dashboard.
2. They record their daily achievements.
3. Their achievements are stored securely in Supabase.
4. AI features use the user's available achievement data to generate reflections and answer questions.
5. n8n handles scheduled workflows and external integrations, including future letter delivery and Telegram-related processes.
6. Users can revisit their achievements and explore their personal growth over time.

## 7. System Architecture

The solution combines a web application, database services, AI capabilities, and workflow automation.

See the architecture diagram:

`docs/system-architecture.png`

## 8. Project Deliverables

This repository contains the documentation and supporting materials prepared for the Final Capstone Project.

| Folder / File | Description |
|---|---|
| `docs/` | Client proposal, system architecture, and final report |
| `content/` | Brand brief, main content, supporting content, and prompts |
| `tests/` | Testing evidence and improvement examples |
| `assets/` | Project screenshots and visual materials |

## 9. Live Application & Source Code

**Application Source Repository:**

[View Tiny Wins on GitHub](https://github.com/heba-nedal/tiny-wins)

**Live Application:**  
[Try the website](https://tiny-win-by-heba.lovable.app/)

**Video Demonstration:**  
[Add the video demonstration link here]

## 10. Known Limitations

- AI-generated reflections depend on the information available in the user's recorded achievements.
- AI responses may require human review to ensure accuracy and relevance.
- Some automated workflows depend on external services and their availability.
- The Win Garden currently uses a static illustration with a data-based progress indicator rather than dynamically generated plant visuals.

## 11. Responsible AI

Tiny Wins is designed to use AI responsibly by:

- Grounding AI responses in the user's available achievement records.
- Avoiding unsupported personal assumptions and invented achievements.
- Protecting user data through authenticated access and database access controls.
- Keeping human review important when evaluating AI-generated content.

Further details are provided in the final report.

---

**Project:** Tiny Wins  
**Program:** AI & Intelligent Automation  
**Project Type:** Individual Capstone Project  
**Repository:** [heba-nedal/tiny-wins](https://github.com/heba-nedal/tiny-wins)
