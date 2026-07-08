# Appendices

## Appendix A: Comprehensive Prompt Library

This appendix contains the best, battle-tested prompts from the book, organized by category. Copy, adapt, and expand them as needed.

**1. General Security Analysis**
```
You are a principal security architect with 20 years of experience. Analyze [topic/system] using [framework, e.g., STRIDE]. Be thorough, conservative in risk assessment, and provide actionable recommendations.
```
**2. Threat Intelligence Enrichment**
```
You are an elite threat intelligence analyst. Enrich this indicator [IOC] with context, associated actors, campaigns, TTPs, and defensive recommendations. Include confidence levels.
```
**3. Incident Response Timeline**
```
Construct a clear chronological timeline from the provided logs and alerts. Map events to MITRE ATT&CK and highlight potential attack paths.
```
**4. Vulnerability Prioritization** 
```
Contextualize this vulnerability [details] for our environment [context]. Provide realistic exploitability, business impact, and recommended timeline.
```
**5. Detection Rule Generation**
```
Create a high-fidelity [Sigma/KQL/YARA] detection rule for this behavior [description]. Include test cases and false positive considerations.
```
**6. Architecture Review**
```
Perform a Zero Trust-aligned security review of this architecture. Identify gaps and provide specific, prioritized recommendations.
```
**7. Self-Critique Addition (use with any prompt):**
```
After your response, critique it for hallucinations, missed edge cases, and overly optimistic assumptions. Then provide an improved version.
```

## Appendix B: Agent Code Templates

**Basic LangChain Agent Template**
```
from langchain_core.tools import tool
from langchain.agents import create_tool_calling_agent, AgentExecutor
from langchain_core.prompts import ChatPromptTemplate
from langchain_openai import ChatOpenAI  # or ChatOllama

# Define tools here...

llm = ChatOpenAI(model="claude-3-5-sonnet-20240620", temperature=0)

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a senior security operations agent..."),
    ("placeholder", "{chat_history}"),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}"),
])

agent = create_tool_calling_agent(llm, tools, prompt)
agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True, max_iterations=15)
```
**CrewAI Multi-Agent Template** (see Chapter 10 for full example)

**LangGraph Stateful Workflow** – Recommended for complex agents with human-in-the-loop.

## Appendix C: Tool & Model Comparison Matrix (2026)

| Category              | Best Options                          | Strengths                              | Best For Security Use Cases                  | Privacy / Control Level |
|-----------------------|---------------------------------------|----------------------------------------|----------------------------------------------|-------------------------|
| Frontier Cloud Models | Claude 4, GPT-o3 series, Grok 4      | Superior reasoning, tool use, vision, structured output | Complex analysis, architecture reviews, incident response, threat modeling | Low                     |
| Strong Local / Open Models | Llama 4 405B, Mixtral Large, Qwen2.5-Coder | Full data control, no usage costs, customizable | Sensitive data processing, high-volume tasks, air-gapped environments | High                    |
| Research & OSINT      | Perplexity Pro, Grok                 | Real-time knowledge, citations, web browsing | Threat intelligence gathering, OSINT enrichment | Medium                  |
| Coding & Agent Development | Cursor + Claude 4, Continue.dev + local models | Excellent code generation, IDE integration, debugging | Detection engineering, agent building, script creation | Varies                  |
| Enterprise / Secure   | Claude Team/Enterprise, Azure OpenAI, custom VPC deployments | Zero data retention, compliance features, audit logs | Production agents handling sensitive data | High                    |

**Key Recommendations (2026):**

- **Hybrid Strategy** — Use frontier cloud models for high-complexity reasoning and local/open models for sensitive or high-volume work.
- **Privacy-First** — Default to local models (70B+) for any prompt containing sensitive, customer, or internal architecture data.
- **Cost vs Capability** — Frontier models for strategic/architecture work; local models for daily operations and agents.
- **Evaluation** — Always test the same prompt across 2–3 different models and compare outputs.

**Update Note**: This matrix will evolve quickly. Check the book's companion GitHub repository for the latest version.

## Appendix D: Glossary

-   **Agent** — Autonomous or semi-autonomous system that can reason, use tools, and pursue goals.
-   **RAG (Retrieval-Augmented Generation)** — Technique that grounds LLM responses in external knowledge.
-   **ReAct** — Reasoning + Acting prompt pattern.
-   **LoRA** — Low-Rank Adaptation for efficient fine-tuning.
-   **Prompt Injection** — Attack where malicious instructions are inserted into prompts.
-   **Zero Trust** — Security model based on "never trust, always verify."
-   **MITRE ATT&CK** — Framework for describing adversary behaviors.

## Appendix E: Further Reading and Resources

**Books:**

-   _The Coming Wave_ – Mustafa Suleyman
-   _Co-Intelligence_ – Ethan Mollick
-   _Hands-On Large Language Models_ – Jay Alammar & Maarten Grootendorst

**Online Resources:**

-   OWASP Top 10 for LLM Applications
-   MITRE ATLAS
-   LangChain / LangGraph Documentation
-   CrewAI Documentation
-   Security-specific AI communities (invite-only Discords, private Slack groups)

**Stay Updated:**

-   Follow key researchers and practitioners on X (formerly Twitter).
-   Monitor arXiv for new security + AI papers.
-   Participate in AI Red Teaming exercises.
