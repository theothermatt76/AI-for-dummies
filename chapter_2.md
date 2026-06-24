## Chapter 2: Getting Started – From Zero to Daily User

You now understand what LLMs are and why they matter for security work. This chapter focuses on turning that knowledge into immediate, practical capability. By the end, you should have a reliable daily workflow and be using AI multiple times per day in ways that save real time.

# Step 1: Choose and Set Up Your Core Tools

A professional security engineer maintains a **portfolio** of AI tools rather than relying on one. Here’s the recommended 2026 stack:

**Primary Chat Interfaces (Cloud Frontier Models)**

-   **Claude 4 (Anthropic)**: Currently the strongest for deep technical reasoning, long-context analysis, and careful security thinking. Excellent at structured output and refusing dangerous requests.
-   **GPT-4o / o3 series (OpenAI)**: Best all-rounder with superior tool use, code execution (Canvas), and multimodal capabilities (analyze screenshots of dashboards or packet captures).
-   **Grok 3 / Grok 4 (xAI)**: Strong real-time knowledge, less censored, excellent for technical depth and creative red teaming.
-   **Perplexity Pro**: Best for research with citations. Use when you need sourced threat intel or recent CVEs.

**Local / Private Models (Critical for Sensitive Work)**

-   **Ollama** + **Open WebUI**: Easiest way to run models locally. Start with Llama 3.1 70B or 405B (if you have the hardware), Mistral Large, or Qwen2.5-Coder.
-   **LM Studio** or **AnythingLLM**: Great for beginners with nice interfaces and built-in RAG.
-   Hardware recommendation: At minimum, a machine with 32GB+ RAM and an NVIDIA GPU (24GB+ VRAM ideal for 70B models).

**Action Items Today:**

1.  Create accounts on Claude.ai, ChatGPT, Grok, and Perplexity (use enterprise/Team plans where possible for zero data retention).
2.  Install Ollama (ollama.com) and pull your first model: ollama pull llama3.1:70b.
3.  Set up a secure "AI Research VM" (isolated, no production access) for running local models and testing.

# Step 2: Interface Mastery

Learn the unique strengths of each interface:

-   **Claude Projects**: Create a "Security Operations" project and upload your company’s redacted policies, playbooks, and architecture diagrams. This gives Claude persistent context.
-   **ChatGPT Custom GPTs**: Build simple custom versions (e.g., "Log Analyzer GPT", "Threat Model Assistant").
-   **Artifacts / Canvas**: Use for iterative code writing and diagram generation.
-   **Grok**: Excellent for real-time X/Twitter threat discussion and uncensored technical exploration.

**Pro Tip**: Use keyboard shortcuts religiously. Speed compounds. Keep multiple tabs open with different models running the same task in parallel for comparison.

# Step 3: Basic Prompting Patterns for Technical Security Work

Start simple but structured. Use these templates daily:

**Pattern 1: Role + Task + Format (RTF)**
`You are a principal security engineer at a Fortune 500 financial institution.

Task: Review this Terraform code for security issues.

Output format: 
1. Critical issues (with severity)
2. Medium issues
3. Recommendations with code examples`

**Pattern 2: Step-by-Step Reasoning**
`Analyze this suspicious PowerShell script. Think step by step:
4. What does each section do?
5. Is it malicious? Why?
6. IOCs to look for?
7. Detection opportunities?`

**Pattern 3: Comparison / Trade-off Analysis**
`Compare the security implications of using AWS Security Hub vs. Microsoft Defender for Cloud in a multi-cloud environment with heavy Kubernetes usage. Include cost, coverage, false positive rates, and integration effort.`

**Pattern 4: Summarization with Context**
`Summarize this incident report for an executive audience (CISO + Board). Keep it under 400 words. Highlight business risk, not technical details. End with three recommended next steps.`

Practice these patterns until they become muscle memory.

# Step 4: Secure Usage Practices (Non-Negotiable)

As a security professional, your AI usage must be more disciplined than the average user’s.

**Golden Rules:**

-   **Never input real secrets**, production logs with PII, or sensitive architecture details into public models.
-   Use data classification:
    -   Public / Redacted → Any model
    -   Internal → Enterprise plans only
    -   Confidential / Sensitive → Local models or air-gapped instances only
-   Sanitize prompts: Replace IPs, hostnames, usernames with placeholders (e.g., REDACTED-IP-1).
-   Enable privacy settings: Turn off chat history where possible, use temporary chats for sensitive topics.
-   Monitor your own outputs: AI conversations can leak information through metadata or indirect references.

**Recommended Workflow for Sensitive Tasks:**

1.  Redact the data heavily
2.  Run on local model first
3.  Only escalate to cloud model if local capability is insufficient

# Step 5: Integrate AI into Your Existing Security Tooling

The real daily value comes from tight integration:

-   **VS Code + GitHub Copilot / Cursor**: Best investment you’ll make. Use for writing detection rules, parsers, automation scripts. Enable Copilot Chat.
-   **JetBrains AI Assistant**: Excellent for Java/.NET security tool development.
-   **Terminal Assistants**:
    -   Warp terminal (built-in AI)
    -   Fig (now part of Amazon)
    -   Or local: Continue.dev + Ollama
-   **Obsidian + Smart Connections / Copilot**: Build your personal security knowledge base with AI.
-   **SIEM Integration**: Many organizations now have Copilot-like features in Splunk, Sentinel, or Elastic.

**Quick Win Setup:** Install the Continue.dev VS Code extension and configure it to use both Claude (for hard problems) and your local Llama model (for routine tasks).

# Exercise: Your First Full Day with AI

1.  Pick a recent ticket or task you worked on.
2.  Have AI help you rewrite the detection rule / investigation summary / architecture diagram.
3.  Compare outputs from Claude 4 and your local model.
4.  Document time saved.
5.  Repeat with three more tasks.

Track your usage for one week. Most engineers see 2–4 hours saved per week even at this basic level.

# Chapter Summary and Key Takeaways

-   Build a multi-model toolkit (cloud + local).
-   Master structured prompting — it’s your new technical superpower.
-   Security and privacy must guide every AI interaction.
-   Deep integration into your IDE and terminal creates compounding returns.
-   Start small, stay consistent, and measure results.

You are no longer a casual user. You now have a professional AI setup.

**Security Architect Tip**: Create a personal “AI Playbook” document (in Markdown or Obsidian) where you save your best prompts and model comparison notes. Update it weekly. This becomes incredibly valuable as you progress to agents in later chapters.

In Chapter 3, we will dive deep into prompt engineering — turning good usage into elite-level capability.
