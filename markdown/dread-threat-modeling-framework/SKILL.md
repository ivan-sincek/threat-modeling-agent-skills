---
name: dread-threat-modeling-framework
description: Systematically score and prioritize threats using the risk-centric DREAD threat modeling framework. Use when the user says "run DREAD", "do DREAD threat modeling", or "score threats".
license: MIT
metadata:
  author: Ivan Sincek
  version: 2.7
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

## Output (MARKDOWN FORMAT)

Output ONLY the following sections:

  - `# DREAD Threat Model`
  - `## Threat Details`
  - `## Threat Summary`

Quality assurance:

- Do not add or modify elements or formatting.
- Ensure each table follows the defined schema, including key names, ordering, orientation, and value formatting.
- Use `N/A` when a value cannot be determined.
- Escape `|` as `\|` in values to prevent breaking tables.

### Step 1 - DREAD Threat Model

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **Project Name** | Explicit and concise project name. |
| **Created By** | Explicit and concise LLM name. |
| **Created On** | Current date in the format `YYYY-MM-DD`. |
| **Created With** | Skill name and version in the format `Name v#.#`. |

### Step 2 - Threat Details

- Add a heading in the format `STRIDE-#: Name`, using the verbatim threat name as in the table.
- Use `#.#` to format: `Total Score`.
- Use `#.# - Justification.` (0.0-10.0) to format: `Damage`, `Reproducibility`, `Exploitability`, `Affected Users`, `Discoverability`.
- Use explicit, concise, and single-sentence justifications.
- Use ` / ` to separate: `CVE`.
- Use `<br>` to separate: `Exploit Resources`.

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **ID** | Verbatim identifier of the threat. |
| **Name** | Verbatim name of the threat. |
| **Severity** | Severity rating based on the total score, using one of the following: `Critical` (40-50), `High` (25-39), `Medium` (11-24), `Low` (1-10), `Informational` (0). |
| **Total Score** | Sum of all DREAD scores. |
| **Damage** | How much damage the threat would cause if exploited. |
| **Reproducibility** | How easily the threat can be reproduced. |
| **Exploitability** | How easily the threat can be exploited. |
| **Affected Users** | How many users the threat would affect if exploited. |
| **Discoverability** | How easily the threat can be discovered. |
| **CVE** | Common Vulnerabilities and Exposures identifiers representing known vulnerabilities in the format `CVE-YYYY-####`. |
| **Exploit Resources** | Plaintext URLs to publicly known exploit resources, including proof-of-concept (PoC) code. |

### Step 3 - Threat Summary

- Use verbatim values from the `Output - Threat Details` section.

| ID | Severity | Total Score | Name |
| --- | --- | --- | --- |
| --- | --- | --- | --- |
