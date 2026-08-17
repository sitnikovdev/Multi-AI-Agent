# Multi AI Agent

A production-oriented **Multi AI Agent** application built with **LangGraph, LangChain, Grok/Llama, Tavily, FastAPI, Streamlit, Docker, Jenkins, SonarQube, and AWS**.

The project demonstrates how to build an AI application that can route user requests to specialized agents, use external web search for up-to-date information, expose the AI workflow through an API, and deploy the application using a CI/CD pipeline.

## 🚀 Project Overview

The application allows users to:

* Select an agent type, such as:

  * Financial Agent
  * Medical Agent
  * Study Agent
  * Other specialized agents
* Enter a natural-language question.
* Let the appropriate agent process the request.
* Search the web when current information is required.
* Generate a final response using an LLM.

The project also demonstrates a complete deployment workflow:

```text
User
  ↓
Streamlit
  ↓
FastAPI
  ↓
LangGraph
  ↓
LangChain
  ↓
LLM + Tavily
  ↓
Response
```

The application is containerized with Docker and deployed to AWS through a Jenkins CI/CD pipeline:

```text
GitHub
  ↓
Jenkins
  ↓
SonarQube
  ↓
Docker Build
  ↓
AWS ECR
  ↓
AWS ECS Fargate
  ↓
Application
```

---

## 🏗️ Architecture

```text
                         ┌──────────────┐
                         │     User     │
                         └──────┬───────┘
                                │
                                ▼
                         ┌──────────────┐
                         │  Streamlit   │
                         │   Frontend   │
                         └──────┬───────┘
                                │ HTTP
                                ▼
                         ┌──────────────┐
                         │   FastAPI    │
                         │   Backend    │
                         └──────┬───────┘
                                │
                                ▼
                         ┌──────────────┐
                         │  LangGraph   │
                         │ Agent Engine │
                         └──────┬───────┘
                                │
                   ┌────────────┴────────────┐
                   ▼                         ▼
            ┌──────────────┐         ┌──────────────┐
            │  LangChain   │         │    Tavily    │
            │ LLM / Tools  │         │ Web Search   │
            └──────┬───────┘         └──────┬───────┘
                   │                         │
                   └────────────┬────────────┘
                                ▼
                         ┌──────────────┐
                         │  Grok/Llama  │
                         │     LLM      │
                         └──────────────┘
```

### CI/CD Architecture

```text
┌──────────┐
│  GitHub  │
└────┬─────┘
     │
     ▼
┌──────────┐
│ Jenkins  │
└────┬─────┘
     │
     ▼
┌────────────┐
│ SonarQube  │
└────┬───────┘
     │
     ▼
┌────────────┐
│   Docker   │
│    Build   │
└────┬───────┘
     │
     ▼
┌────────────┐
│   AWS ECR  │
└────┬───────┘
     │
     ▼
┌────────────────┐
│ ECS + Fargate  │
└───────┬────────┘
        │
        ▼
┌────────────────┐
│      ALB       │
└────────────────┘
```

---

## 🛠️ Tech Stack

| Technology          | Purpose                                        |
| ------------------- | ---------------------------------------------- |
| **Python**          | Main programming language                      |
| **Grok / Llama**    | Large Language Model                           |
| **LangChain**       | LLM and tool integration                       |
| **LangGraph**       | Agent workflow orchestration                   |
| **Tavily**          | Web search and external information retrieval  |
| **FastAPI**         | Backend REST API                               |
| **Streamlit**       | Frontend UI                                    |
| **Docker**          | Application containerization                   |
| **GitHub**          | Source code management                         |
| **SonarQube**       | Static code quality analysis                   |
| **Jenkins**         | CI/CD automation                               |
| **AWS ECR**         | Docker image registry                          |
| **AWS ECS Fargate** | Container deployment                           |
| **AWS ALB**         | Load balancing and stable application endpoint |

---

## ✨ Key Features

### Multi-Agent Architecture

The application can support multiple specialized agents.

For example:

```text
                   User Query
                       │
                       ▼
                  Agent Router
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Financial      Medical      Study
       Agent          Agent        Agent
          │            │            │
          └────────────┼────────────┘
                       ▼
                    Response
```

Each agent can have its own instructions, tools, and workflow.

### 🌐 Web Search

The application can use Tavily to retrieve current information from the internet.

This is useful for questions involving:

* Current news
* Financial markets
* Recent events
* Current technologies
* Other time-sensitive information

The general workflow is:

```text
User Question
      ↓
Agent
      ↓
Does the question require current information?
      │
   ┌──┴──┐
  Yes    No
   │      │
   ▼      │
Tavily    │
   │      │
   └──┬───┘
      ▼
     LLM
      ↓
   Response
```

### 🔗 FastAPI Backend

FastAPI handles:

* User requests
* Agent selection
* AI workflow execution
* API responses
* Communication between frontend and AI logic

### 🖥️ Streamlit Frontend

Streamlit provides a simple web interface where users can:

1. Select an agent.
2. Enter a question.
3. Submit the request.
4. View the generated response.

### 🐳 Docker

The application is packaged into a Docker image to provide a consistent runtime environment.

```text
Application
     ↓
 Dockerfile
     ↓
Docker Image
     ↓
Docker Container
```

### 🔍 SonarQube

SonarQube is used to analyze source code quality.

The analysis can identify:

* Bugs
* Code smells
* Code duplication
* Security-related issues
* Maintainability problems

### 🔄 Jenkins CI/CD

Jenkins automates the deployment pipeline.

The pipeline performs:

```text
Checkout
   ↓
Code Quality Analysis
   ↓
Docker Build
   ↓
Push Image
   ↓
Deploy
```

### ☁️ AWS Deployment

Docker images are stored in **Amazon ECR** and deployed using **Amazon ECS with Fargate**.

An **Application Load Balancer (ALB)** can be placed in front of the ECS service to provide a stable endpoint and distribute traffic between running tasks.

---

## 📁 Project Structure

A typical project structure can look like this:

```text
multi-ai-agent/
│
├── app/
│   ├── agents/
│   │   ├── financial_agent.py
│   │   ├── medical_agent.py
│   │   └── study_agent.py
│   │
│   ├── graph/
│   │   └── agent_graph.py
│   │
│   ├── tools/
│   │   └── web_search.py
│   │
│   ├── api/
│   │   └── routes.py
│   │
│   ├── config/
│   │   └── settings.py
│   │
│   └── main.py
│
├── frontend/
│   └── streamlit_app.py
│
├── tests/
│
├── Dockerfile
├── Jenkinsfile
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

> The exact structure may vary depending on the implementation.

---

## ⚙️ Configuration

Create a `.env` file based on `.env.example`.

Example:

```env
GROK_API_KEY=your_grok_api_key
TAVILY_API_KEY=your_tavily_api_key

LLM_MODEL=your_model_name
```

Never commit your `.env` file or API keys to GitHub.

Add the following to `.gitignore`:

```gitignore
.env
__pycache__/
*.pyc
.venv/
```

---

## 🔑 API Keys

The application requires API credentials for the external services used by the project.

### LLM Provider

Create an API key for the selected LLM provider and add it to:

```env
GROK_API_KEY=...
```

### Tavily

Create a Tavily API key and add:

```env
TAVILY_API_KEY=...
```

The application loads these values through its configuration layer rather than hardcoding credentials in the source code.

---

## 💻 Local Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd multi-ai-agent
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

On Windows:

```powershell
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

```bash
cp .env.example .env
```

Update `.env` with your API keys and model configuration.

### 5. Run the FastAPI backend

```bash
uvicorn app.main:app --reload
```

The API will be available locally at:

```text
http://localhost:8000
```

FastAPI documentation:

```text
http://localhost:8000/docs
```

### 6. Run Streamlit

In another terminal:

```bash
streamlit run frontend/streamlit_app.py
```

The Streamlit interface will then be available locally.

---

## 🐳 Running with Docker

Build the Docker image:

```bash
docker build -t multi-ai-agent .
```

Run the container:

```bash
docker run --env-file .env -p 8000:8000 multi-ai-agent
```

Check the application:

```text
http://localhost:8000
```

---

## 🔄 CI/CD Pipeline

The Jenkins pipeline follows this workflow:

### Stage 1 — Jenkins Setup

Jenkins is installed and configured to execute the pipeline.

### Stage 2 — GitHub Integration

Jenkins retrieves the latest source code from the GitHub repository.

```text
GitHub
   ↓
Jenkins Workspace
```

### Stage 3 — SonarQube Analysis

The source code is analyzed for quality issues.

```text
Jenkins Workspace
       ↓
   SonarQube
       ↓
Quality Report
```

### Stage 4 — Docker Build

The application is packaged into a Docker image.

```bash
docker build -t multi-ai-agent .
```

### Stage 5 — Push to AWS ECR

The Docker image is pushed to an Amazon ECR repository.

```text
Docker Image
     ↓
   AWS ECR
```

### Stage 6 — Deploy to ECS Fargate

ECS Fargate pulls the image from ECR and runs the application as a container.

```text
ECR
 ↓
ECS Service
 ↓
Fargate Task
 ↓
Application
```

### Stage 7 — Application Load Balancer

An ALB can be configured to route incoming requests to the ECS service.

```text
Client
  ↓
ALB
  ↓
ECS Service
  ↓
Fargate Tasks
```

---

## 🧪 Code Quality

SonarQube is integrated into the CI/CD process so that code quality can be checked before the application is packaged and deployed.

The pipeline can be configured to fail when the project does not meet the required quality gate.

This helps prevent problematic code from reaching production.

---

## 🔐 Security Considerations

Do not store secrets directly in the source code.

Avoid:

```python
GROK_API_KEY = "my-secret-key"
```

Use environment variables or a dedicated secrets-management solution instead.

Recommended approach:

```text
Environment / Secrets Manager
            ↓
       Configuration
            ↓
        Application
```

For production AWS deployments, credentials and secrets should preferably be managed through appropriate AWS IAM and secrets-management mechanisms rather than committed to the repository.

---

## 📈 Future Improvements

Possible improvements include:

* Add more specialized agents.
* Implement a supervisor/router agent.
* Add persistent conversation memory.
* Add authentication and authorization.
* Add automated unit and integration tests.
* Add monitoring and logging.
* Add AWS CloudWatch integration.
* Add automated rollback.
* Add GitHub webhook-triggered Jenkins builds.
* Add streaming responses.
* Add conversation history.
* Add RAG with a vector database.
* Add evaluation of agent responses.
* Add tracing and observability.
* Use AWS Secrets Manager for production secrets.

---

## 🎯 Learning Goals

This project demonstrates several important concepts for an AI Engineer:

* LLM application development
* Agentic AI
* Multi-agent architecture
* Tool calling
* Web search integration
* LangChain
* LangGraph
* REST API development
* Frontend/backend separation
* Docker containerization
* Git and GitHub
* Static code analysis
* CI/CD
* Docker image registries
* AWS ECS
* AWS Fargate
* Application Load Balancing
* Production deployment of AI applications

---

## 📌 Project Workflow

The complete development workflow is:

```text
1. Project Setup
       ↓
2. Environment Configuration
       ↓
3. API Configuration
       ↓
4. LangChain Integration
       ↓
5. LangGraph Agent Workflow
       ↓
6. FastAPI Backend
       ↓
7. Streamlit Frontend
       ↓
8. Frontend + Backend Integration
       ↓
9. GitHub Version Control
       ↓
10. Dockerfile
       ↓
11. Jenkins Setup
       ↓
12. GitHub + Jenkins Integration
       ↓
13. SonarQube Integration
       ↓
14. Docker Build
       ↓
15. Push to AWS ECR
       ↓
16. Deploy to ECS Fargate
       ↓
17. Configure ALB
       ↓
18. Production Application
```

---

## 📄 License

This project is intended for educational and demonstration purposes.

Add an appropriate license before using the project in production.

---

If you found this project useful, consider giving the repository a ⭐.

