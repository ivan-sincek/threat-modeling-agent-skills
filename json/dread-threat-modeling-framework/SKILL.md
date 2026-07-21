---
name: dread-threat-modeling-framework
description: Systematically score and prioritize threats using the risk-centric DREAD threat modeling framework. Use when the user says "run DREAD", "do DREAD threat modeling", or "score threats".
license: MIT
metadata:
  author: Ivan Sincek
  version: 2.8
  url: https://github.com/ivan-sincek/threat-modeling-agent-skills
---

# DREAD Threat Modeling Framework

## Instructions

You are a Lead Product Security Engineer with deep expertise in secure architecture and design, secure coding, threat modeling, and adversarial thinking.

Use the risk-centric DREAD threat modeling framework to systematically score and prioritize threats across the application.

## Analysis

### Step 1 - Score and Prioritize Threats

1. Leverage all provided threat artifacts and previously identified threats.

2. Leverage all available external threat intelligence.

3. Systematically score and document each previously identified threat using the schema defined in the `Output - Threat Details` section.

4. Order threats by total score.

## Output (JSON FORMAT)

Output ONLY the following sections:

  ```json
  {
    "stride_threat_model": {},
    "threat_details": [],
    "threat_summary": []
  }
  ```

Quality assurance:

- Do not add or modify elements or formatting.
- Ensure each JSON object follows the defined schema, including key names, ordering, and value formatting.
- Use `N/A` when a value cannot be determined.

### Step 1 - STRIDE Threat Model

```json
{
  "project_name": "Explicit and concise project name.",
  "created_by": "Explicit and concise LLM name.",
  "created_on": "Current date in the format `YYYY-MM-DD`.",
  "created_with": "Skill name and version in the format `Name v#.#`."
}
```

### Step 2 - Threat Details

- Use `#.#` (0.0-50.0) to format: `total_score`.
- Use `#.# - Justification.` (0.0-10.0) to format: `damage`, `reproducibility`, `exploitability`, `affected_users`, `discoverability`.
- Use explicit, concise, and single-sentence justifications.

```json
{
  "id": "Verbatim identifier of the threat.",
  "name": "Verbatim name of the threat.",
  "severity": "Severity rating based on the total score, using one of the following: `Critical` (40-50), `High` (25-39), `Medium` (11-24), `Low` (1-10), `Informational` (0).",
  "total_score": "Sum of all DREAD scores.",
  "damage": "How much damage the threat would cause if exploited?",
  "reproducibility": "How easily the threat can be reproduced?",
  "exploitability": "How easily the threat can be exploited?",
  "affected_users": "How many users the threat would affect if exploited?",
  "discoverability": "How easily the threat can be discovered?",
  "cve": ["Common Vulnerabilities and Exposures identifiers representing known vulnerabilities in the format `CVE-YYYY-####`."],
  "exploit_resources": ["URLs to publicly known exploit resources, including proof-of-concept (PoC) code."]
}
```

### Step 3 - Threat Summary

- Use verbatim values from the `Output - Threat Details` section.

```json
{
  "id": "",
  "severity": "",
  "total_score": "",
  "name": ""
}
```
