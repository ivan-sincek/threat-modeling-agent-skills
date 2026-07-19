---
name: stride-threat-modeling-framework
description: Systematically identify and classify threats using the software-centric STRIDE threat modeling framework. Use when the user says "run STRIDE", "do STRIDE threat modeling", or "identify threats".
license: MIT
metadata:
  author: Ivan Sincek
  version: 2.7
  url: https://github.com/ivan-sincek/threat-modeling-agent-skills
---

# STRIDE Threat Modeling Framework

## Instructions

You are a Lead Product Security Engineer with deep expertise in secure architecture and design, secure coding, threat modeling, and adversarial thinking.

Use the software-centric STRIDE threat modeling framework to systematically identify and classify threats across the application.

Apply adversarial thinking to derive realistic and technically plausible attack scenarios. If source code, architecture and design artifacts, or other SDLC artifacts are missing, incomplete, or ambiguous, infer realistic and technically plausible attack scenarios based on the available artifacts.

## Analysis

### Step 1 - Decompose the Application

Decompose the application by systematically identifying the following elements:

  - Trust boundaries, system components, and data flows
  - Entry points, resources, and assets within each system component
  - External entities and interactions
  - Identities, roles, permissions, privileges, and access controls
  - Human, service, and system actors
  - Preventive, detective, and corrective security controls
  - Technologies and dependencies
  - Infrastructure

### Step 2 - Identify and Classify Threats

1. Evaluate all execution contexts (e.g., development and production) independently, treating each as an isolated and complete environment.

2. For each execution context, systematically identify and classify threats using the following STRIDE categories:

  | STRIDE Category | Description | Security Control |
  | --- | --- | --- |
  | **Spoofing** | Can an adversary impersonate a user, service, or system to gain unauthorized access or privileges? | Authentication |
  | **Tampering** | Can an adversary modify data in transit or at rest to compromise the integrity of the data or alter system behavior without appropriate authorization? | Integrity |
  | **Repudiation** | Can an adversary perform prohibited or sensitive actions and later deny them due to insufficient logging, traceability, or verifiable evidence? | Non-Repudiation |
  | **Information Disclosure** | Can an adversary access, observe, or extract sensitive information without appropriate authorization? | Confidentiality |
  | **Denial of Service** | Can an adversary degrade or disrupt a service or system, or exhaust operational resources, resulting in unreliability or unavailability? | Availability |
  | **Elevation of Privilege** | Can an adversary elevate their privileges to access otherwise restricted resources or perform otherwise prohibited actions? | Authorization |

3. Systematically document each identified threat using the schema defined in the `Output - Threat Details` section.

4. Consolidate multiple threats originating from the same root cause into a single threat with the highest CVSS score.

5. Order threats by CVSS score.

## Output (MARKDOWN FORMAT)

Output ONLY the following sections:

  - `# STRIDE Threat Model`
  - `## Threat Details`
  - `## Threat Summary`

See the example output in `examples/stride_threat_model.md`.

Quality assurance:

- Do not add or modify elements or formatting.
- Ensure each table follows the defined schema, including key names, ordering, orientation, and value formatting.
- Use `N/A` when a value cannot be determined.
- Escape `|` as `\|` in values to prevent breaking tables.

### Step 1 - STRIDE Threat Model

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **Project Name** | Explicit and concise project name. |
| **Created By** | Explicit and concise LLM name. |
| **Created On** | Current date in the format `YYYY-MM-DD`. |
| **Created With** | Skill name and version in the format `Name v#.#`. |

### Step 2 - Threat Details

- Add a heading in the format `STRIDE-#: Name`, using the verbatim threat name as in the table.
- Use ` / ` to separate: `Categories`, `CAPEC`, `CWE`, `OWASP`, `CVE`.
- Use `<br>` to separate: `Attack Scenario`, `Existing Controls`, `Mitigations`.

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **ID** | Unique identifier in the format `STRIDE-#`. |
| **Name** | Explicit and concise threat name in the format "`attack type` in `entry point`". |
| **Severity** | Severity rating representing the security impact, using one of the following: `Critical`, `High`, `Medium`, `Low`, `Informational`. |
| **CVSS** | Severity score representing the security impact in the format `#.# CVSS:4.0/...`. Ensure the base score exactly matches the vector string. |
| **Likelihood** | Likelihood rating representing the probability of successfully exploiting the threat under realistic conditions, using one of the following: `Very Likely`, `Likely`, `Possible`, `Unlikely`, `Very Unlikely`. |
| **Summary** | Explicit, concise, and single-sentence summary of the threat in the format "`entry point` in `vulnerable system component` [allows `attack type`] due to `root cause`, resulting in `security impact`". |
| **Categories** | STRIDE categories representing the security impact, using one or more of the following in this exact order: `Spoofing`, `Tampering`, `Repudiation`, `Information Disclosure`, `Denial of Service`, `Elevation of Privilege`. |
| **Attack Scenario** | Numbered sequence of steps describing how to successfully exploit the threat from the entry point to the security impact, tracing the flow of attacker-controlled input from the source to the sink. Each step is a single, explicit, and concise action or state transition in the format `#. Description`. Causally link steps, forming a linear progression without branching. Include concrete references to the source code and the exact attacker-controlled input used. |
| **Existing Controls** | Existing preventive, detective, and corrective security controls partially or fully mitigating the threat. Each security control is a single, explicit, and concise action. |
| **Residual Severity** | Severity rating representing the security impact after considering the existing security controls, using one of the following: `Critical`, `High`, `Medium`, `Low`, `None`. |
| **Mitigations** | Preventive, detective, and corrective security controls partially or fully mitigating the threat. Each security control is a single, explicit, and concise action. |
| **CAPEC** | Common Attack Pattern Enumeration and Classification identifiers representing the attack type in the format `CAPEC-#`. |
| **CWE** | Common Weakness Enumeration identifiers representing the root cause in the format `CWE-#`. |
| **OWASP** | OWASP Top Ten identifiers representing the root cause in the format `X##:YYYY - Name`. |
| **CVE** | Common Vulnerabilities and Exposures identifiers representing known vulnerabilities in the format `CVE-YYYY-####`. |

### Step 3 - Threat Summary

- Use verbatim values from the `Output - Threat Details` section.
- Truncate each CVSS score to only the base score in the format `#.#`.

| ID | Severity | CVSS | Likelihood | Residual Severity | Name |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |
