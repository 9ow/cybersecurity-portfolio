# Adversary frameworks and AI testing implications

Source: Unit 1 slides 29–35, Unit 3 slides 37–40 and Unit 5 slides 42–45.

**MITRE ATT&CK** catalogs observed adversary behavior: a *tactic* is the objective (why), a *technique* the general method (how), and a *procedure* a specific execution in context. Matching an Nmap tool invocation does not prove a threat actor identity or full ATT&CK technique. Framework mapping should cite observations and uncertainty; defenders can use it for coverage assessments and detection planning.

**MITRE ATLAS** focuses on attacks against AI/ML systems: training-data poisoning, adversarial inputs, model extraction, prompt injection and deepfake social engineering. ATT&CK covers broader enterprise adversary behavior; ATLAS covers AI-specific surfaces. They overlap and neither substitutes for vulnerability verification or risk scoring.

Unit 3 presents Ollama local models and ShellGPT/cloud models for drafting scan commands; Unit 5 describes summarizing enumeration outputs. LLMs may hallucinate flags, targets, vulnerabilities or implications. Review target scope, script side effects, command options and output before running or reporting. Local operation reduces some external data transfer but does not guarantee secure handling. Do not submit raw infrastructure output or personal data to a third-party AI service without permission. No LLM setup or personal scan was verified.

Sources cited by lecture: https://attack.mitre.org/ and https://atlas.mitre.org/.