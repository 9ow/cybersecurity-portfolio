# Threat behavior frameworks and AI-assisted analysis

## Adversary technique modeling

MITRE ATT&CK organizes documented adversary behavior by **tactic** (the objective/why), **technique** (general method/how) and **procedure** (how a particular actor conducted it in a specific event). A single command is not enough to attribute an attack to a group. TTP mapping supports detection engineering, control coverage, purple-team planning and evidence-driven threat modeling. State what was directly observed and why the mapping is relevant.

MITRE ATLAS emphasizes threats to AI/ML systems and adjacent data/model pipelines, while ATT&CK covers broader enterprise/cloud/mobile/industrial adversary behaviors. AI concerns include **data poisoning** (training/evaluation contamination), **adversarial inputs** (crafted samples that evade models), **model theft/extraction**, **prompt injection** (untrusted content attempting to override instructions) and **deepfake-enabled social engineering**. These differ from ordinary web injection and require separate controls such as data provenance, prompt/data separation, output evaluation and access monitoring.

## Local model workflows and their limitations

The material introduces Ollama as an approach to running a model locally, reducing the need to send all prompts to a cloud service. Example setup concepts include pulling a local model (`ollama pull mistral`) and invoking `ollama run mistral`; any installer script should be reviewed before executing. An AI-generated Nmap command must be manually checked for target scope, scanning flags, potentially intrusive scripts and traffic caps. Never blindly execute generated shell.

For large `snmpwalk`, `ldapsearch` or Nmap output, a model may extract candidate services or summarize anomalies, but it cannot reliably invent missing packet captures, distinguish redacted fields or independently confirm a vulnerability. Preserve verified source observations privately; only provide redacted data to permitted services. The source also identifies cloud-based assistants and newer automated enumeration products, without establishing measured accuracy or personal operation.

## Output review checklist

1. Was the suggested target within authorized scope?
2. Is every flag/script understood, including unexpected side effects?
3. Does the observation exist in the actual sanitized tool output?
4. Is the inferred OS/product/vulnerability uncertain or corroborated?
5. Does the report avoid credentials, identifying addresses and network diagrams?
6. Are conclusions accurately labeled as confirmed, suspected or unknown?

Useful references: https://attack.mitre.org/ and https://atlas.mitre.org/.