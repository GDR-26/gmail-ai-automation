# Gmail AI Automation

> An AI-powered Gmail workflow that classifies incoming emails, applies the correct label, and drafts a professional reply — combining LLM reasoning with deterministic email automation.

---

## Overview

Gmail AI Automation reduces the repetitive work of triaging an inbox.

When a new email arrives, the system reads its subject and content, classifies it using GPT-4.1 Mini, applies the most relevant Gmail label, and drafts a professional reply for human review.

Unlike a fully autonomous agent, this workflow keeps a human in the loop at the final step. The AI reasons and proposes; a person still decides what gets sent.

---

## Highlights

* 📧 Automatic email classification on arrival
* 🏷️ Dynamic label retrieval and assignment
* ✍️ AI-generated HTML reply drafts
* 🧠 LLM reasoning paired with deterministic execution
* 🔄 Event-driven workflow triggered by Gmail itself

---

## Why I Built This

Email triage is repetitive in a specific way: every message needs to be read, categorized, and often replied to in a similar tone and structure.

That repetition makes it a good candidate for AI assistance, but a poor candidate for full automation. Sending a reply without review carries real risk, so the goal was narrower: remove the reading and drafting effort, while keeping a human as the final checkpoint before anything is sent.

This workflow explores how far a single classification and drafting step can go in reducing that overhead, without overextending the AI into actions that should remain under human control.

---

## Core Workflow

1. A new email arrives in Gmail.
2. The Gmail Trigger starts the workflow.
3. GPT-4.1 Mini reads the subject and body to determine intent.
4. The workflow retrieves the user's current Gmail labels dynamically.
5. The AI selects the most appropriate label from that list.
6. The workflow applies the selected label to the email.
7. The AI generates a professional HTML reply draft.
8. Gmail saves the draft for human review before sending.

---

## System Architecture

The workflow follows the same separation of concerns used across my AI automation projects:

> **AI reasons. Workflows execute.**

The language model is responsible for two things only: classifying the email and drafting a reply. Every other step — label retrieval, label application, and saving the draft — is handled by deterministic workflow logic rather than the model itself.

This keeps the system predictable: if something goes wrong, the failure is traceable to a specific step rather than buried inside an opaque AI decision.

---

## Architecture Decisions

### Why dynamic label retrieval instead of hardcoded label IDs?

Gmail labels are user-specific and can change over time. Retrieving them dynamically means the workflow adapts automatically rather than breaking when a label is renamed or added.

### Why GPT-4.1 Mini?

Email classification and reply drafting are well-defined, repetitive tasks that don't require maximum model capability. A smaller model keeps the cost per email low while remaining accurate enough for consistent classification.

### Why save a draft instead of sending automatically?

Replying on someone's behalf carries real consequences if the AI misreads context or tone. Saving a draft preserves the time-saving benefit of AI-generated replies while keeping a human as the final decision-maker.

---

## Engineering Challenges

### Reliable Classification Without Hardcoded Categories

Early versions risked tightly coupling the AI's classification output to a fixed label list. Retrieving labels dynamically at runtime solved this, letting the workflow stay in sync with however the user organizes their inbox.

### Balancing Reply Quality With Cost

Generating a thoughtful, professional reply for every incoming email could get expensive at scale. Using a smaller, cost-efficient model for both classification and drafting kept the workflow practical to run continuously.

---

## Tech Stack

| Layer               | Technology          |
| ------------------- | -------------------- |
| Workflow Automation | n8n                  |
| AI                  | OpenAI GPT-4.1 Mini  |
| Email                | Gmail API             |

---

## Lessons Learned

This project reinforced a principle I now apply across every AI automation I build: the AI should reason, not act unsupervised in places where mistakes are costly.

Classification and drafting are low-risk, high-value places for AI to operate. Sending an email on someone's behalf is not — at least not without a human checkpoint. Designing around that boundary made the workflow both useful and safe to run continuously.

---

## Connect

If you're interested in Applied AI, workflow automation, or building reliable AI-assisted systems, I'd be happy to connect.

* 💼 **LinkedIn:** https://linkedin.com/in/dhruva-reddy-gaddam
* 💻 **GitHub:** https://github.com/GDR-26
* 🌐 **Portfolio:** *Coming Soon*
