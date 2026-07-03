# Chapter 9: Building Custom Security Agents – Part 1 (Fundamentals)

By this point in the book, you have mastered prompting and are using AI daily for productivity, threat intel, incident response, and architecture. The next major leap is moving from _using_ AI to _building_ with AI—specifically, creating custom agents that can autonomously or semi-autonomously handle security tasks.

This chapter (Part 1) covers the fundamentals. Chapter 10 will dive into advanced multi-agent systems and sophisticated workflows.

## Understanding Agents vs Tools vs copilots

-   **Tools**: Simple functions the model can call (e.g., run a query, search a database).
-   **Copilots**: Interactive assistants that help you in real time.
-   **Agents**: Systems that can reason, use tools, maintain memory, plan, and execute multi-step tasks toward a goal, often with some autonomy.

**Key Frameworks in 2026**:

-   **LangChain / LangGraph**: Most mature and flexible for complex workflows.
-   **LlamaIndex**: Excellent for RAG-heavy agents.
-   **CrewAI**: Great for role-based multi-agent teams.
-   **AutoGen / Microsoft Semantic Kernel**: Strong for conversational multi-agent setups.
-   **OpenAI Swarm**: Lightweight and elegant for orchestration.

**Recommendation for Security Teams**: Start with LangChain + LangGraph for most use cases. It offers excellent debugging, persistence, and control.

## Core Concepts You Must Understand

1.  **Reasoning Loops** (ReAct, Plan-and-Execute, etc.)
2.  **Tool Use / Function Calling** — Giving agents the ability to interact with external systems.
3.  **Memory** — Short-term (current task), long-term (vector store), and entity memory.
4.  **State Management** — Tracking progress across steps.
5.  **Guardrails & Safety** — Preventing harmful actions.

## Building Your First Security Agent

**Example Project: Security Log Analysis Agent**

**Step-by-Step Setup** (using LangChain + Ollama or Claude):
```
from langchain_openai import ChatOpenAI  # or ChatOllama
from langchain.agents import create_tool_calling_agent, AgentExecutor
from langchain_core.tools import tool
from langchain_core.prompts import ChatPromptTemplate

# Define tools
@tool
def query_siem(log_query: str) -> str:
    """Query the SIEM for logs"""
    # Implement actual integration
    return "Sample log results..."

@tool
def enrich_ioc(ioc: str) -> str:
    """Enrich IOC with threat intel"""
    # Call VirusTotal, MISP, etc.
    pass

tools = [query_siem, enrich_ioc]

# Create agent
llm = ChatOpenAI(model="claude-3-5-sonnet")  # or local model

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a senior SOC analyst agent..."),
    ("placeholder", "{chat_history}"),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}"),
])

agent = create_tool_calling_agent(llm, tools, prompt)
agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
```
**Basic Agent Prompt (System Message):**
```
You are SecAnalystAgent, an autonomous security operations agent. 
Your goals: Investigate alerts, correlate events, enrich IOCs, and recommend actions.
Always think step-by-step. Use tools when needed. Never take destructive actions without human approval.
```
## Memory Management for Security Agents

-   **Conversation Memory**: Keeps context of the current investigation.
-   **Vector Store Memory**: Stores past incidents, playbooks, and threat intel for RAG.
-   **Entity Memory**: Tracks specific IOCs, hosts, or users across sessions.

**Example with Chroma:**
```
from langchain_community.vectorstores import Chroma
from langchain_openai import OpenAIEmbeddings

vectorstore = Chroma(collection_name="security_knowledge", embedding_function=OpenAIEmbeddings())
```
## Tool Creation Best Practices for Security

-   SIEM / EDR query tools
-   Ticketing system integration (create/update tickets)
-   Threat intel lookup
-   Code analysis tools
-   Notification tools (Slack/Teams/email with approval)

**Security-First Tool Design**:

-   All tools that can take action should require human confirmation for high-impact operations.
-   Implement audit logging for every agent action.
-   Rate limiting and safety checks.

## Exercise: Build Your First Agent Today

1.  Install LangChain and choose a model (local or cloud).
2.  Create a simple “Vulnerability Enrichment Agent” with two tools: one for CVE lookup and one for threat context.
3.  Give it a goal: “Enrich and risk-score these 5 CVEs for our environment.”
4.  Run it and observe the reasoning trace.
5.  Iterate by adding memory and better tools.

**Expected Outcome**: Within a few hours, you will have a working agent that can meaningfully assist with repetitive security tasks.

## Common Pitfalls (Part 1)

-   Over-autonomy too early → Start with human-in-the-loop.
-   Poor tool design → Tools should be focused and well-documented.
-   Ignoring cost/latency → Local models + caching are your friends for high-volume work.
-   Lack of evaluation → Always test agents on historical data before live use.

## Chapter Summary and Key Takeaways

-   Agents represent the shift from conversational AI to actionable, goal-oriented systems.
-   Start simple: one agent, few tools, strong system prompt, good memory.
-   Security agents must emphasize safety, auditability, and human oversight.
-   The fundamentals you learn here form the foundation for sophisticated multi-agent systems in the next chapter.
-   Treat agent development like software engineering — version control, testing, documentation, and monitoring are essential.

**Security Architect Tip**: Create an internal “Agent Development Playbook” that defines standards for tool creation, prompt templates, evaluation criteria, and approval processes. This ensures consistency and reduces risk as your team scales agent development.

You now have the foundational skills to build useful security agents. In Chapter 10, we will expand this into multi-agent teams capable of complex, collaborative security work such as autonomous threat hunting and purple teaming.
