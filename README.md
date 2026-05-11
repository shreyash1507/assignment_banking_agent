# Agentic Banking Platform: Policy Bot Navigator

A sophisticated multi-agent AI system designed for the banking industry. This platform leverages autonomous reasoning agents to navigate complex policies, assess loan eligibility, and provide transparent, explainable "Agent Thought Graphs" to bank officers and customers.

---

## Key Features

- **Multi-Agent Orchestration**: A Hub-and-Spoke model where a central Orchestrator plans and dispatches tasks to domain experts.
- **Agent Thought Graph**: A real-time, horizontal timeline visualization of the AI's internal reasoning loop.
- **Constraint Handling**: Built-in guardrails for compliance, PII detection, and operational limits.
- **Explainable AI**: Every step of the reasoning process is captured in an audit trail and presented in the UI.
- **Enterprise Ready**: Designed for seamless deployment on **AWS Bedrock** and **AWS Lambda**.

---

## Core Implementation Highlights

- **Working prototype of a multi-agent system**: Functional Hub-and-Spoke architecture where a central Orchestrator plans and delegates tasks to domain experts.
  - *Pointer*: [orchestrator.py](Backend/banking_agents/agents/reusable/orchestrator.py) initializes the system and loads dynamic domain tools.
- **Automated constraint handling**: Configurable limits for agent reasoning loops and task decomposition to ensure system stability and predictable latency.
  - *Pointer*: [orchestrator.py](Backend/banking_agents/agents/reusable/orchestrator.py#L234) (`max_iterations` guardrail) and [guardrails.yaml](Backend/banking_agents/config/guardrails.yaml).
- **Built-in validation/guardrails**: Multi-stage validation covering input sanitization (injection prevention) and output compliance (legal disclaimers).
  - *Pointer*: [input_validator.py](Backend/banking_agents/guardrails/input_validator.py) and [output_validator.py](Backend/banking_agents/guardrails/output_validator.py) integrated in [main.py](Backend/banking_agents/main.py#L75).
- **Explainability & structured output**: Transparent reasoning through a step-by-step audit trail that maps internal LLM thoughts to UI components.
  - *Pointer*: [orchestrator.py](Backend/banking_agents/agents/reusable/orchestrator.py#L239) (`audit_trail` construction) and returned in the `ChatResponse`.
- **Dynamic Agent Extensibility**: Decoupled, configuration-driven architecture allowing domain experts to be registered via YAML without changing core logic.
  - *Pointer*: `_build_dynamic_tools` in [orchestrator.py](Backend/banking_agents/agents/reusable/orchestrator.py) and [orchestrator.yaml](Backend/banking_agents/config/orchestrator.yaml).
- **Regulatory-First Reasoning Protocol**: Implements a strict 4-stage hierarchy (Scenario Match → Rule Scan → Formula Extraction → Calculation) for compliant loan assessments.
  - *Pointer*: The `system_prompt` reasoning protocol in [loan_eligibility_rag_agent.py](Backend/banking_agents/agents/domain/loan_eligibility_rag_agent.py#L104).
- **Hallucination Shield (RAG Guardrails)**: Integrated confidence thresholds that detect and block responses when retrieved document quality is insufficient.
  - *Pointer*: [rag_guard.py](Backend/banking_agents/guardrails/rag_guard.py) and its usage in the domain agents.

---

## Project Architecture

The platform is organized into four functional layers:
1. **Presentation**: A high-performance Vanilla JS frontend.
2. **Orchestration**: A FastAPI-based reasoning hub.
3. **Expert Agents**: Specialized units for Policy RAG and Loan Eligibility.
4. **Knowledge Layer**: Secure storage for policy documentation and decision matrices.

For a detailed breakdown, see [Documentation/architecture_flow.md](Documentation/architecture_flow.md).

---

## Project Structure

```text
.
├── Backend/
│   ├── banking_agents/        # Core agentic logic (Orchestrator, Experts)
│   │   ├── agents/            # Domain-specific agent implementations
│   │   ├── config/            # YAML-based agent configurations
│   │   └── main.py            # API entry point
│   ├── requirements.txt       # Python dependencies
│   └── .env                   # Environment variables (API Keys)
├── Frontend/
│   └── index.html             # Main UI and Agent Thought Graph renderer
├── Documentation/             # Architecture diagrams and implementation guides
└── README.md                  # Project overview (this file)
```

---

## Getting Started

### Prerequisites
- Python 3.10+
- An API Key (Groq or AWS Bedrock credentials)

### Local Execution
1. **Navigate to the Backend**:
   ```bash
   cd Backend
   ```
2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Configure Environment**:
   Update the `.env` file with your API keys.
4. **Run the API**:
   ```bash
   python -m banking_agents.main
   ```
5. **Launch UI**:
   Open `Frontend/index.html` in any modern web browser.

---

## Cloud Deployment (AWS)

The platform is optimized for **AWS Bedrock**. For detailed instructions on deploying via AWS Lambda, S3, and Bedrock Agents, refer to the [Documentation/aws_architecture_flow.md](Documentation/aws_architecture_flow.md).

---

## Documentation

- [Project Implementation Guide](Documentation/project_implementation_guide.md)
- [System Architecture & Flow](Documentation/architecture_flow.md)
- [AWS Cloud Architecture](Documentation/aws_architecture_flow.md)


