---
name: dread-threat-modeling-framework
description: Systematically score and prioritize threats using the risk-centric DREAD threat modeling framework. Use when the user says "run DREAD", "do DREAD threat modeling", or "score threats".
license: MIT
metadata:
  author: Ivan Sincek
  version: "4.0"
  url: https://github.com/ivan-sincek/threat-modeling-agent-skills
---

# DREAD Threat Modeling Framework

## Instructions

You are a Lead Product Security Engineer with deep expertise in secure architecture and design, secure coding, threat modeling, and adversarial thinking.

Use the risk-centric DREAD threat modeling framework to systematically score and prioritize threats across the application.

## Analysis

### Step 1 - Score and Prioritize Threats

1. Leverage all the provided threat artifacts and previously identified threats.

2. Leverage any publicly available threat intelligence.

3. Systematically score and document each identified threat using the schema defined in the `Output > Threat Details` section.

4. Sort the identified threats in descending order by total score.

## Output (JSON FORMAT)

Output ONLY the following sections:

```json
{
  "metadata": {},
  "threat_details": [],
  "threat_summary": []
}
```

Quality assurance:

- Do not add or modify JSON keys.
- Ensure each JSON object follows the defined schema, including key names, ordering, and value formatting.
- Use `N/A` when a value cannot be determined.
- Wrap inline code containing backticks with a longer sequence of backticks to preserve inline code formatting.

### Metadata

```json
{
  "project_name": "Explicit and concise name of the project.",
  "created_at": "Current date in the format `YYYY-MM-DD`.",
  "created_by": "Explicit and concise name and version of the model.",
  "created_with": "Use verbatim: `DREAD Threat Modeling Framework 4.0`."
}
```

### Threat Details

- Use `# - Explicit, concise, and single-sentence justification.` and a scale of 0-10 to format: `damage`, `reproducibility`, `exploitability`, `affected_users`, `discoverability`.

```json
{
  "id": "Verbatim threat identifier.",
  "name": "Verbatim threat name.",
  "severity": "Severity rating based on the total score. Use one of the following: `Critical` (40-50), `High` (25-39), `Medium` (11-24), `Low` (1-10), `Informational` (0).",
  "total_score": "Sum of the DREAD category scores.",
  "damage": "How much damage would the threat cause if exploited?",
  "reproducibility": "How easily can the threat be reproduced?",
  "exploitability": "How easily can the threat be exploited?",
  "affected_users": "How many users would the threat affect if exploited?",
  "discoverability": "How easily can the threat be discovered?",
  "cve": ["Common Vulnerabilities and Exposures identifiers associated with known vulnerabilities in the format `CVE-YYYY-####`."],
  "exploit_code_maturity": "Maturity rating of the exploit code. Use one of the following: `High`, `Functional`, `Proof-of-Concept`, `Unproven`.",
  "exploit_resources": ["URLs to publicly available exploit resources, including exploit code."]
}
```

### Threat Summary

- Use verbatim values from the `Output > Threat Details` section.

```json
{
  "id": "",
  "severity": "",
  "total_score": "",
  "name": ""
}
```
