# Project Implementation Guide: Agentic Banking Platform

## 1. Executive Summary
The Agentic Banking Platform is a next-generation AI system designed to handle complex banking queries through a multi-agent orchestration framework. It transforms static policy documents and rigid loan logic into a conversational, transparent experience.

## 2. System Architecture
The platform utilizes a **Hub-and-Spoke** architecture:
- **Orchestrator**: The central brain (using high-reasoning models) that plans and synthesizes.
- **Expert Agents**: Specialized units (Policy RAG, Loan Specialist) that handle domain-specific data retrieval and computation.
- **Data Layer**: Secure storage for policy PDFs and decision matrices.

### 2.1 Layered Design
1. **Presentation Layer**: Vanilla JS Frontend with a custom "Agent Thought Graph" for real-time reasoning visualization.
2. **Orchestration Layer**: FastAPI backend managing state and model dispatching.
3. **Agent Layer**: Independent logic for Intent Classification, Task Decomposition, and Domain Expertise.
4. **Knowledge Layer**: S3/Local storage for ground-truth banking data.

## 3. Technical Stack
- **Language**: Python 3.10+ (Backend), JavaScript ES6 (Frontend).
- **Frameworks**: FastAPI (API), IBM Plex Mono (Typography).
- **AI Models**: Llama 3.3 70B (Orchestrator), Llama 3.1 8B (Experts).
- **Infrastructure**: Groq (for low-latency inference) or AWS Bedrock.

## 4. Key Implementation Details

### 4.1 The Reasoning Loop
The system implements a ReAct-style loop:
1. **Classify**: Determine if the query is about Policy or Loans.
2. **Decompose**: Break the query into sequential steps.
3. **Execute**: Dispatch tasks to the relevant expert agents.
4. **Synthesize**: Combine findings into a human-readable "Final Output."

### 4.2 Agent Thought Graph
A unique UI component that renders the backend `audit_trail` as a horizontal timeline. 
- **Adaptive Spacing**: Boxes resize based on output length.
- **Transparency**: Every thought, finding, and tool call is visible to the officer.

## 5. Deployment Guide

### 5.1 Local Setup
1. Install dependencies: `pip install -r requirements.txt`
2. Configure `.env` with Groq API keys.
3. Run the backend: `python banking_agents/main.py`
4. Open `index.html` in a browser.

### 5.2 AWS Cloud Deployment
- **API**: Deploy the FastAPI app to **AWS Lambda** via API Gateway.
- **AI**: Migrate inference to **Amazon Bedrock**.
- **Data**: Upload policy documents to **Amazon S3**.


