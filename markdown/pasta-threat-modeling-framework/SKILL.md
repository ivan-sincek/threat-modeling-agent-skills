---
name: pasta-threat-modeling-framework
description: Systematically identify and classify technical and business risks using the risk-centric PASTA threat modeling framework. Use when the user says "run PASTA", "do PASTA threat modeling", or "identify risks".
license: MIT
metadata:
  author: Ivan Sincek
  version: 2.7
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

1. Leverage all provided threat artifacts.

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

## Output (MARKDOWN FORMAT)

Output ONLY the following sections:

  - `# PASTA Threat Model`
  - `## Objectives`
  - `## Business Impact Analysis Details`
  - `## Business Impact Analysis Summary`
  - `## Technical Scope`
  - `## Use Cases`
  - `## Threat Details`
  - `## Threat Summary`
  - `## Attack Trees`
  - `## Attack Surface`
  - `## Risk Mitigation Strategy`

Quality assurance:

- Do not add or modify elements or formatting.
- Ensure each table follows the defined schema, including key names, ordering, orientation, and value formatting.
- Use `N/A` when a value cannot be determined.
- Escape `|` as `\|` in values to prevent breaking tables.

### Step 1 - PASTA Threat Model

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **Project Name** | Explicit and concise project name. |
| **Created By** | Explicit and concise LLM name. |
| **Created On** | Current date in the format `YYYY-MM-DD`. |
| **Created With** | Skill name and version in the format `Name v#.#`. |

### Step 2 - Objectives

- Use explicit, concise, and high-level objectives.
- Use `<br>` to separate objectives.

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **Business** | Objectives focused on delivering stakeholder value. |
| **Financial** | Objectives focused on achieving financial targets. |
| **Functional** | Objectives focused on defining core capabilities. |
| **Operational** | Objectives focused on ensuring operational excellence. |
| **Security** | Objectives focused on protecting critical assets. |
| **Risk** | Objectives focused on defining risk criteria. |
| **Compliance** | Objectives focused on meeting compliance obligations. |

### Step 3 - Business Impact Analysis Details

- Use ` / ` to separate: `Stakeholders`, `Dependencies`.
- Use `<br>` to separate: `Disruptions`, `Impacts`.
- Use `DD days HH:mm hours` to format: `MTD`, `RTO`, `RPO`.

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **ID** | Unique identifier in the format `BIA-#`. |
| **Name** | Explicit and concise business process name. |
| **Criticality** | Criticality rating representing the importance of the business process to business continuity, using one of the following: `Critical`, `High`, `Medium`, `Low`, `None`. |
| **Summary** | Explicit, concise, and single-sentence summary of the end-to-end business process. |
| **Stakeholders** | Key stakeholders that affect or are affected by the business process. Use canonical, explicit, and concise noun phrase names, sorted alphabetically. |
| **Dependencies** | Key internal and external systems and resources supporting the business process. Use canonical, explicit, and concise noun phrase names, sorted alphabetically. |
| **Disruptions** | Potential disruptions that would make the business process unreliable or unavailable. Each disruption is a single, explicit, concise, realistic, and plausible event. |
| **Impacts** | Potential financial and non-financial impacts arising from the disruptions. Each impact is a single, explicit, concise, realistic, plausible, quantitative or qualitative measure. |
| **Severity** | Severity rating representing the highest business impact among the financial and non-financial impacts, using one of the following: `Critical`, `High`, `Medium`, `Low`, `Informational`. |
| **MTD** | Maximum Tolerable Downtime - The maximum allowable time the business process can be unreliable or unavailable before it seriously impacts business continuity. |
| **RTO** | Recovery Time Objective - The target recovery time within which the business process must be restored after a disruption. |
| **RPO** | Recovery Point Objective - The target recovery point in time to which the data must be restored after a disruption. |

### Step 4 - Business Impact Analysis Summary

- Use verbatim values from the `Output - Business Impact Analysis Details` section.

| ID | Criticality | MTD | Name |
| --- | --- | --- | --- |
| --- | --- | --- | --- |

### Step 5 - Technical Scope

- Use canonical, explicit, and concise noun phrase names.
- Use explicit, concise, and single-sentence descriptions.
- Use `<br>` to separate: `Source Files`, `Entry Points`.

#### Step 5.1 - Trust Boundaries

| ID | Name | Type | Description |
| --- | --- | --- | --- |
| `TB-#` | --- | `External` / `DMZ` / `Internal` | --- |

#### Step 5.2 - System Components

| ID | Name | Type | TB | Description |
| --- | --- | --- | --- | --- |
| `SC-#` | --- | `External Entity` / `Process` / `Data Store` | `TB-#` | --- |

#### Step 5.3 - Entry Points

| ID | Name | Source Files | Entry Points | Authentication | Authorization | SC | Description |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `EP-#` | --- | `---` | `---` | `Unauthenticated` / `Authenticated` | `None` / `Coarse` / `Fine` | `SC-#` | --- |

#### Step 5.4 - Resources and Assets

| ID | Name | Source Files | Sensitivity | Persistence | Encryption | SC | Description |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `RA-#` | --- | `---` | `Sensitive` / `Non-Sensitive` | `Persistent` / `Transient` / `Ephemeral` | `None` / `In Transit` / `At Rest` / `Both` | `SC-#` | --- |

#### Step 5.5 - External Entities

| ID | Name | Direction | Authentication | TB | Description |
| --- | --- | --- | --- | --- | --- |
| `EE-#` | --- | `Inbound` / `Outbound` / `Bidirectional` | `None` / `Basic` / `API Key` / `Request Signing` / `OAuth` / `Other` | `TB-#` | --- |

#### Step 5.6 - Roles

| ID | Name | Type | Description |
| --- | --- | --- | --- |
| `RO-#` | --- | `Critical` / `High` / `Medium` / `Low` / `None` | --- |

#### Step 5.7 - Actors

| ID | Name | Type | RO | Description |
| --- | --- | --- | --- | --- |
| `AC-#` | --- | `Human` / `Service` / `System` | `RO-#` | --- |

#### Step 5.8 - Technologies and Dependencies

| ID | Name | Version | SC | Description |
| --- | --- | --- | --- | --- |
| `TD-#` | --- | `---` | `SC-#` | --- |

#### Step 5.9 - Infrastructure

| ID | Name | Type | Compute | TB | Description |
| --- | --- | --- | --- | --- | --- |
| `IF-#` | --- | `Cloud` / `Hybrid` / `On-Premises` | `Serverless` / `Container` / `VM` / `Bare Metal` / `Other` | `TB-#` | --- |

#### Step 5.10 - Threat Actors

| ID | Name | Target | Motive | Description |
| --- | --- | --- | --- | --- |
| `TA-#` | --- | `Data` / `Infrastructure` / `Human` | --- | --- |

### Step 6 - Use Cases

- Add a heading in the format `Use Case #: Name`, using an explicit and concise use case name.
- Add an explicit, concise, and single-sentence summary of the use case above the diagram.

1. Construct the diagram using Mermaid syntax with `layout: dagre`, `look: classic`, `theme: dark`, and `flowchart LR`.

2. Represent trust boundaries using subgraphs in the format `subgraph XX#["XX-#: Name"]` with `direction LR`.

3. Represent elements using the following nodes in the format `XX#@{ shape: ..., label: "XX-#: Name" }`:

  | Technical Scope | Shape |
  | --- | --- |
  | System Components | `rect` |
  | Entry Points | `hex` |
  | Resources and Assets | `das` |
  | Actors | `stadium` |

4. Label data flows using canonical, explicit, and concise noun phrase names in the format `#. Name`.

5. Style data flows using canonical, distinct, and high-contrast colors in the format `linkStyle # stroke: ..., stroke-width: 2px`.

### Step 7 - Threat Details

- Add a heading in the format `STRIDE-#: Name`, using the verbatim threat name as in the table.
- Use ` / ` to separate: `Categories`, `CAPEC`, `CWE`, `OWASP`, `CVE`, `Threat Actors`.
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
| **System Component** | `SC-#` identifier. |
| **Threat Actors** | `TA-#` identifiers. |

### Step 8 - Threat Summary

- Use verbatim values from the `Output - Threat Details` section.
- Truncate each CVSS score to only the base score in the format `#.#`.

| ID | Severity | CVSS | Likelihood | Residual Severity | Name |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |

### Step 9 - Attack Trees

- Add a heading in the format `Attack Tree SC-#: Name`.

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
