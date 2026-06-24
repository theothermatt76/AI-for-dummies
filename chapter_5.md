# Chapter 5: Threat Intelligence & Hunting with AI

Threat intelligence and proactive hunting are where AI moves from productivity assistant to genuine force multiplier. Modern security teams face an overwhelming volume of threat data—new CVEs, malware reports, dark web chatter, and adversary TTPs. AI excels at ingesting, correlating, enriching, and surfacing actionable insights from this flood.

In this chapter, you will learn how to use AI to accelerate OSINT, analyze indicators, map behaviors to frameworks like MITRE ATT&CK, and begin building lightweight custom threat intelligence tools.

## OSINT Automation and Enrichment

AI dramatically speeds up open-source intelligence collection and contextualization.

**Core Workflow Prompt:**
```
You are an elite threat intelligence analyst with expertise in OSINT, dark web monitoring, and nation-state actor tracking.

Research the following indicator or topic: [e.g., "new ransomware group 'ShadowCrypt' " or IP 203.0.113.42]

Provide:
1. Summary of known associations (threat actors, campaigns, malware)
2. Recent activity (last 30–90 days)
3. Technical IOCs and TTPs
4. Victim verticals and geography
5. Recommended defensive controls
6. Confidence level and sources (cite where possible)

Cross-reference with known frameworks and look for emerging patterns.
```
**Enrichment Template for IOCs:**
```
Enrich this set of indicators:

[IP, domain, hash, email, etc.]

For each:
- Reputation (VirusTotal-like signals)
- Historical sightings
- Associated malware or campaigns
- Risk scoring (low/medium/high) with justification
- Suggested Sigma or YARA detection ideas
```
**Pro Tip:** Use Perplexity or models with browsing capabilities for the most current information, then validate with local models for sensitive correlation.

## Analyzing Malware Reports, IOCs, and TTPs

Turn lengthy vendor reports into actionable intelligence quickly.

**Malware Analysis Prompt:**
```
You are a senior malware reverse engineer and detection engineer.

Analyze this malware report:

[PASTE REPORT TEXT OR KEY SECTIONS]

Extract and structure:
- Malware family and variants
- Infection vector and persistence mechanisms
- C2 infrastructure patterns
- Full MITRE ATT&CK mapping (tactics, techniques, sub-techniques)
- Key IOCs (hashes, domains, registry keys, etc.)
- Evasion techniques used
- High-fidelity detection opportunities (network, endpoint, behavioral)
```
For large reports, first ask the model to create a concise executive summary, then drill down into specific sections.

## Natural Language Querying of Threat Data

Move beyond rigid SIEM queries to conversational exploration of your threat data.

**Example Queries:**

-   “Show me all activity related to living-off-the-land techniques in the last 7 days across our EDR and network logs.”
-   “Compare the TTPs of the latest APT41 campaign with our current detection coverage.”
-   “What emerging threats should we prioritize for our healthcare customer base?”

**Building a Simple Threat Intel Copilot:** Use tools like Continue.dev, Claude Projects, or AnythingLLM with uploaded threat reports, ATT&CK matrices, and your internal intel. This creates a private knowledge base you can query naturally.

## Mapping and Gap Analysis with MITRE ATT&CK

AI is exceptionally good at framework translation and coverage analysis.

**ATT&CK Mapping Prompt:**
```
Map the following adversary behavior description to the MITRE ATT&CK Enterprise matrix (2026 version).

Behavior: [detailed description]

For each relevant technique:
- Technique ID and name
- Detection opportunities (existing vs missing)
- Data sources required
- Confidence of mapping

Then provide an overall coverage gap analysis and prioritized detection recommendations.
```
**Defensive Gap Analysis:**
```
We currently have strong coverage in Initial Access and Credential Access but weaker in Lateral Movement and Defense Evasion. 

Given this new campaign description [paste], identify our highest risk gaps and suggest specific controls or detections to close them.
```
## Building Custom Threat Intel Copilots

At this stage, you can create persistent assistants:

1.  **Claude Projects or Custom GPT**: Upload your top 20 recent threat reports, your organization’s ATT&CK Navigator layer, and playbooks.
2.  **Local RAG Setup** (Ollama + AnythingLLM or PrivateGPT): Feed in MISP exports, STIX bundles, and internal incident data (redacted).
3.  **Daily Briefing Agent**: Create a recurring prompt that pulls recent news and correlates against your environment.

**Daily Threat Hunt Starter Prompt:**
```
Conduct a proactive threat hunt for our environment.

Focus areas: [e.g., cloud identity attacks, supply chain compromises]

Steps:
1. Review latest relevant threat intelligence
2. Identify applicable TTPs
3. Suggest specific hunt queries for our stack (EDR: CrowdStrike, Cloud: AWS/Azure, SIEM: Sentinel)
4. Prioritize based on our attack surface
```
## Exercise: Build Your First Threat Intel Workflow

1.  Pick a recent public threat report or campaign (e.g., a new ransomware variant or APT activity).
2.  Use AI to fully enrich it and map to ATT&CK.
3.  Generate 3–5 detection ideas or hunt queries.
4.  Validate at least one idea against your real (or test) environment.
5.  Save the entire workflow and best prompts to your AI Playbook.

Bonus: Compare results from Claude 4, Grok, and your local 70B+ model. Note differences in depth and conservatism.

## Chapter Summary and Key Takeaways

-   AI turns threat intelligence from a firehose into a targeted stream of actionable insights.
-   Strong prompting + RAG/context = dramatically better analysis than manual methods.
-   Always cross-verify critical intelligence with multiple sources and human judgment.
-   Focus on mapping to frameworks (ATT&CK) and generating detections/hunts—the highest leverage activities.
-   Start building small personal copilots now; they become foundational for the agent systems in later chapters.

**Security Architect Tip:** Maintain a “Threat Intel AI Ledger” — for every campaign you analyze with AI, record time saved, new detections created, and any hallucinations caught. This data will prove invaluable when justifying investment in multi-agent threat hunting systems (Chapter 10).

You are now equipped to hunt more proactively and intelligently. In Chapter 6, we apply these same capabilities to the high-pressure world of Incident Response and Forensics, where speed and accuracy matter most.

Continue when you’re ready to level up your reactive capabilities.
