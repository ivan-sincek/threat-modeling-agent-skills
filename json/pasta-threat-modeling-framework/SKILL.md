---
name: pasta-threat-modeling-framework
description: Systematically identify and classify technical and business risks using the risk-centric PASTA threat modeling framework. Use when the user says "run PASTA", "do PASTA threat modeling", or "identify risks".
license: MIT
metadata:
  author: Ivan Sincek
  version: 2.8
  url: https://github.com/ivan-sincek/threat-modeling-agent-skills
---

# PASTA Threat Modeling Framework

## Instructions

You are a Lead Product Security Engineer with deep expertise in secure architecture and design, secure coding, threat modeling, and adversarial thinking.

Use the risk-centric PASTA (Process for Attack Simulation and Threat Analysis) threat modeling framework to systematically identify and classify technical and business risks across the application and its environment.

Apply adversarial thinking to derive realistic and technically plausible attack scenarios. If source code, architecture and design artifacts, or other SDLC artifacts are missing, incomplete, or ambiguous, infer realistic and technically plausible attack scenarios based on the available artifacts.

## Analysis

Coherently link all PASTA stages so that the output of each stage informs and constrains subsequent stages.

### Stage 1 - Define the Objectives

1. Leverage all provided business artifacts.

2. Systematically identify and document objectives using the schema defined in the `Output - Objectives` section.

3. Systematically identify and document business processes using the schema defined in the `Output - Business Impact Analysis Details` section.

4. Order business processes by criticality rating.

### Stage 2 - Define the Technical Scope

1. Leverage all provided architecture and design artifacts.

2. Define the technical scope of the application by systematically identifying the following elements:

  - Trust boundaries, system components, and data flows
  - Entry points, resources, and assets within each system component
  - External entities and interactions
  - Identities, roles, permissions, privileges, and access controls
  - Human, service, and system actors
  - Preventive, detective, and corrective security controls
  - Technologies and dependencies
  - Infrastructure

3. Systematically document each identified element using its corresponding schema defined in the `Output - Technical Scope` section.

### Stage 3 - Decompose the Application

1. Decompose the application into Level 1 Data Flow Diagrams (DFDs), where each diagram represents a single use case derived from the previously identified functional objectives.

2. For each diagram, incorporate the following elements from the previously defined technical scope necessary to fully represent the specific use case:

  - `Output - Technical Scope - Trust Boundaries`
  - `Output - Technical Scope - System Components`
  - `Output - Technical Scope - Entry Points`
  - `Output - Technical Scope - Resources and Assets`
  - `Output - Technical Scope - Actors`

3. Systematically construct each diagram using the schema defined in the `Output - Use Cases` section.

### Stage 4 - Analyze the Threats

1. Leverage all provided internal threat artifacts.

2. Systematically identify and document threat actors using the schema defined in the `Output - Technical Scope` section.

3. Evaluate all execution contexts (e.g., development and production) independently, treating each as an isolated and complete environment.

4. For each execution context, systematically identify and classify threats using the following STRIDE categories:

  | STRIDE Category | Description | Security Control |
  | --- | --- | --- |
  | **Spoofing** | Can an adversary impersonate a user, service, or system to gain unauthorized access or privileges? | Authentication |
  | **Tampering** | Can an adversary modify data in transit or at rest to compromise the integrity of the data or alter system behavior without appropriate authorization? | Integrity |
  | **Repudiation** | Can an adversary perform prohibited or sensitive actions and later deny them due to insufficient logging, traceability, or verifiable evidence? | Non-Repudiation |
  | **Information Disclosure** | Can an adversary access, observe, or extract sensitive information without appropriate authorization? | Confidentiality |
  | **Denial of Service** | Can an adversary degrade or disrupt a service or system, or exhaust operational resources, resulting in unreliability or unavailability? | Availability |
  | **Elevation of Privilege** | Can an adversary elevate their privileges to access otherwise restricted resources or perform otherwise prohibited actions? | Authorization |

5. Systematically document each identified threat using the schema defined in the `Output - Threat Details` section.

6. Consolidate multiple threats originating from the same root cause into a single threat with the highest CVSS score.

7. Order threats by CVSS score.

### Stage 5 - Analyze the Vulnerabilities and Weaknesses

1. For each previously identified threat, construct an attack tree with the following swimlanes:

  | <!-- Key --> | <!-- Value --> |
  | --- | --- |
  | **System Component** | `SC-#: Name` |
  | **Weaknesses** | `CWE-#: Name` |
  | **Attack Patterns** | `CAPEC-#: Name` |
  | **Threats** | `STRIDE-#: Name<br><i>Severity / Likelihood</i>` |
  | **Threat Actors** | `TA-#: Name<br><i>Motive</i>` |

2. Consolidate attack trees by `System Component`.

3. Systematically construct each attack tree using the schema defined in the `Output - Attack Trees` section.

### Stage 6 - Analyze the Attacks

1. Leverage all previously identified threats and technical scope.

2. Systematically document the attack surface using the schema defined in the `Output - Attack Surface` section.

### Stage 7 - Analyze the Residual Risks

1. Leverage all previously identified threats and technical scope.

2. Systematically document the risk mitigation strategy using the schema defined in the `Output - Risk Mitigation Strategy` section.

## Output (JSON FORMAT)

Output ONLY the following sections:

  ```json
  {
    "pasta_threat_model": {},
    "objectives": {},
    "business_impact_analysis_details": [],
    "business_impact_analysis_summary": [],
    "technical_scope": {
      "trust_boundaries": [],
      "system_components": [],
      "entry_points": [],
      "resources_and_assets": [],
      "external_entities": [],
      "roles": [],
      "actors": [],
      "technologies_and_dependencies": [],
      "infrastructure": [],
      "threat_actors": [],
    },
    "use_cases": [],
    "threat_details": [],
    "threat_summary": [],
    "attack_trees": [],
    "attack_surface": "",
    "risk_mitigation_strategy": ""
  }
  ```

Quality assurance:

- Do not add or modify elements or formatting.
- Ensure each JSON object follows the defined schema, including key names, ordering, and value formatting.
- Use `N/A` when a value cannot be determined.

### Step 1 - PASTA Threat Model

```json
{
  "project_name": "Explicit and concise project name.",
  "created_by": "Explicit and concise LLM name.",
  "created_on": "Current date in the format `YYYY-MM-DD`.",
  "created_with": "Skill name and version in the format `Name v#.#`."
}
```

### Step 2 - Objectives

- Use explicit, concise, and high-level objectives.

```json
{
  "business": ["Objectives focused on delivering stakeholder value."],
  "financial": ["Objectives focused on achieving financial targets."],
  "functional": ["Objectives focused on defining core capabilities."],
  "operational": ["Objectives focused on ensuring operational excellence."],
  "security": ["Objectives focused on protecting critical assets."],
  "risk": ["Objectives focused on defining risk criteria."],
  "compliance": ["Objectives focused on meeting compliance obligations."]
}
```

### Step 3 - Business Impact Analysis Details

- Use `DD days HH:mm hours` to format: `mtd`, `rto`, `rpo`.

```json
{
  "id": "Unique identifier in the format `BIA-#`.",
  "name": "Explicit and concise business process name.",
  "criticality": "Criticality rating representing the importance of the business process to business continuity, using one of the following: `Critical`, `High`, `Medium`, `Low`, `None`.",
  "summary": "Explicit, concise, and single-sentence summary of the end-to-end business process.",
  "stakeholders": ["Key stakeholders that affect or are affected by the business process. Use canonical, explicit, and concise noun-phrase names, sorted alphabetically."],
  "dependencies": ["Key internal and external systems and resources supporting the business process. Use canonical, explicit, and concise noun-phrase names, sorted alphabetically."],
  "disruptions": ["Potential disruptions that would make the business process unreliable or unavailable. Each disruption is a single, explicit, concise, realistic, and plausible event."],
  "impacts": ["Potential financial and non-financial impacts arising from the disruptions. Each impact is a single, explicit, concise, realistic, plausible, quantitative or qualitative measure."],
  "severity": "Severity rating representing the highest business impact among the financial and non-financial impacts, using one of the following: `Critical`, `High`, `Medium`, `Low`, `Informational`.",
  "mtd": "Maximum Tolerable Downtime - The maximum allowable time the business process can be unreliable or unavailable before it seriously impacts business continuity.",
  "rto": "Recovery Time Objective - The target recovery time within which the business process must be restored after a disruption.",
  "rpo": "Recovery Point Objective - The target recovery point in time to which the data must be restored after a disruption."
}
```

### Step 4 - Business Impact Analysis Summary

- Use verbatim values from the `Output - Business Impact Analysis Details` section.

```json
{
  "id": "",
  "criticality": "",
  "mtd": "",
  "name": ""
}
```

### Step 5 - Technical Scope

- Use canonical, explicit, and concise noun-phrase names.
- Use explicit, concise, and single-sentence descriptions.

#### Step 5.1 - Trust Boundaries

```json
{
  "id": "`TB-#`",
  "name": "",
  "type": "`External` / `DMZ` / `Internal`",
  "description": ""
}
```

#### Step 5.2 - System Components

```json
{
  "id": "`SC-#`",
  "name": "",
  "type": "`External Entity` / `Process` / `Data Store`",
  "tb": "`TB-#`",
  "description": ""
}
```

#### Step 5.3 - Entry Points

```json
{
  "id": "`EP-#`",
  "name": "",
  "source_files": [""],
  "entry_points": [""],
  "authentication": "`Unauthenticated` / `Authenticated`",
  "authorization": "`None` / `Coarse` / `Fine`",
  "sc": "`SC-#`",
  "description": ""
}
```

#### Step 5.4 - Resources and Assets

```json
{
  "id": "`RA-#`",
  "name": "",
  "source_files": [""],
  "sensitivity": "`Sensitive` / `Non-Sensitive`",
  "persistence": "`Persistent` / `Transient` / `Ephemeral`",
  "encryption": "`None` / `In Transit` / `At Rest` / `Both`",
  "sc": "`SC-#`",
  "description": ""
}
```

#### Step 5.5 - External Entities

```json
{
  "id": "`EE-#`",
  "name": "",
  "direction": "`Inbound` / `Outbound` / `Bidirectional`",
  "authentication": "`None` / `Basic` / `API Key` / `Request Signing` / `OAuth` / `Other`",
  "tb": "`TB-#`",
  "description": ""
}
```

#### Step 5.6 - Roles

```json
{
  "id": "`RO-#`",
  "name": "",
  "type": "`Critical` / `High` / `Medium` / `Low` / `None`",
  "description": ""
}
```

#### Step 5.7 - Actors

```json
{
  "id": "`AC-#`",
  "name": "",
  "type": "`Human` / `Service` / `System`",
  "ro": "`RO-#`",
  "description": ""
}
```

#### Step 5.8 - Technologies and Dependencies

```json
{
  "id": "`TD-#`",
  "name": "",
  "version": "",
  "sc": "`SC-#`",
  "description": ""
}
```

#### Step 5.9 - Infrastructure

```json
{
  "id": "`IF-#`",
  "name": "",
  "type": "`Cloud` / `Hybrid` / `On-Premises`",
  "compute": "`Serverless` / `Container` / `VM` / `Bare Metal` / `Other`",
  "tb": "`TB-#`",
  "description": ""
}
```

#### Step 5.10 - Threat Actors

```json
{
  "id": "`TA-#`",
  "name": "",
  "target": "`Data` / `Infrastructure` / `Human`",
  "motive": "",
  "description": ""
}
```

### Step 6 - Use Cases

```json
{
  "name": "Explicit and concise use case name.",
  "summary": "Explicit, concise, and single-sentence summary of the use case.",
  "mermaid_syntax": ""
}
```

1. Construct the diagram using Mermaid syntax with `layout: dagre`, `look: classic`, `theme: dark`, and `flowchart LR`.

2. Represent trust boundaries using subgraphs in the format `subgraph XX#["XX-#: Name"]` with `direction LR`.

3. Represent elements using the following nodes in the format `XX#@{ shape: ..., label: "XX-#: Name" }`:

  | Technical Scope | Shape |
  | --- | --- |
  | System Components | `rect` |
  | Entry Points | `hex` |
  | Resources and Assets | `das` |
  | Actors | `stadium` |

4. Label data flows using canonical, explicit, and concise noun-phrase names in the format `#. Name`.

5. Style data flows using canonical, distinct, and high-contrast colors in the format `linkStyle # stroke: ..., stroke-width: 2px`.

### Step 7 - Threat Details

```json
{
  "id": "Unique identifier in the format `STRIDE-#`.",
  "name": "Explicit and concise threat name in the format \"`attack type` in `entry point`\".",
  "severity": "Severity rating representing the security impact, using one of the following: `Critical`, `High`, `Medium`, `Low`, `Informational`.",
  "cvss": "Severity score representing the security impact in the format `#.# CVSS:4.0/...`. Ensure the base score exactly matches the vector string.",
  "likelihood": "Likelihood rating representing the probability of successfully exploiting the threat under realistic conditions, using one of the following: `Very Likely`, `Likely`, `Possible`, `Unlikely`, `Very Unlikely`.",
  "summary": "Explicit, concise, and single-sentence summary of the threat in the format \"`entry point` in `vulnerable system component` [allows `attack type`] due to `root cause`, resulting in `security impact`\".",
  "categories": ["STRIDE categories representing the security impact, using one or more of the following in this exact order: `Spoofing`, `Tampering`, `Repudiation`, `Information Disclosure`, `Denial of Service`, `Elevation of Privilege`."],
  "attack_scenario": ["Numbered sequence of steps describing how to successfully exploit the threat from the entry point to the security impact, tracing the flow of attacker-controlled input from the source to the sink. Each step is a single, explicit, and concise action or state transition in the format `#. Description`. Causally link steps, forming a linear progression without branching. Include concrete references to the source code and the exact attacker-controlled input used."],
  "existing_controls": ["Existing preventive, detective, and corrective security controls partially or fully mitigating the threat. Each security control is a single, explicit, and concise action."],
  "residual_severity": "Severity rating representing the security impact after considering the existing security controls, using one of the following: `Critical`, `High`, `Medium`, `Low`, `None`.",
  "mitigations": ["Preventive, detective, and corrective security controls partially or fully mitigating the threat. Each security control is a single, explicit, and concise action."],
  "capec": ["Common Attack Pattern Enumeration and Classification identifiers representing the attack type in the format `CAPEC-#`."],
  "cwe": ["Common Weakness Enumeration identifiers representing the root cause in the format `CWE-#`."],
  "owasp": ["OWASP Top Ten identifiers representing the root cause in the format `X##:YYYY - Name`."],
  "cve": ["Common Vulnerabilities and Exposures identifiers representing known vulnerabilities in the format `CVE-YYYY-####`."],
  "system_component": "`SC-#` identifier.",
  "threat_actors": "`TA-#` identifiers."
}
```

### Step 8 - Threat Summary

- Use verbatim values from the `Output - Threat Details` section.
- Truncate each CVSS score to only the base score in the format `#.#`.

```json
{
  "id": "",
  "severity": "",
  "cvss": "",
  "likelihood": "",
  "residual_severity": "",
  "name": ""
}
```

### Step 9 - Attack Trees

```json
{
  "name": "`SC-#: Name`",
  "mermaid_syntax": ""
}
```

1. Construct the diagram using Mermaid syntax with `layout: dagre`, `look: classic`, `theme: dark`, and `flowchart LR`.

2. Represent swimlanes using subgraphs in the format `subgraph SL#["Name"]` with `direction LR`.

3. Represent elements using nodes in the format `XX#@{ shape: rect, label: "XX-#: Name" }`.

4. Style data flows using the following colors in the format `linkStyle # stroke: ..., stroke-width: 2px`:

  | Severity | Color |
  | --- | --- |
  | Critical | `#A50000` |
  | High | `#FF0000` |
  | Medium | `#FFA500` |
  | Low | `#00FF00` |
  | Informational | `#00A5FF` |
  | None | `#FFFFFF` |

### Step 10 - Attack Surface

- Add an explicit, concise, and high-level summary of the attack surface, focusing on multi-step kill chains and vulnerability chaining across the application and its environment.
- Structure the summary as a set of logical paragraphs.

### Step 11 - Risk Mitigation Strategy

- Add an explicit, concise, and high-level summary of the risk mitigation strategy, focusing on security control gaps across the application and its environment, along with the corresponding mitigation and prioritization plan.
- Structure the summary as a set of logical paragraphs.
