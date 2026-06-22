# Threat Modeling Agent Skills

Easy-to-use, high-quality threat modeling agent skills.

Highly recommend reading [The Complete Guide to Building Skill for Claude](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf).

Future plans:

* Add the PASTA and DREAD threat modeling frameworks.
* Add support for JSON-formatted output.

## Table of Contents

* [Threat Modeling Frameworks](#threat-modeling-frameworks)
    * [STRIDE](#stride)
    * [PASTA](#pasta)
    * [DREAD](#dread)
* [How to Upload](#how-to-upload)
* [How to Use](#how-to-use)

## Threat Modeling Frameworks

### STRIDE

**Skill:** [stride-threat-modeling-framework/SKILL.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/stride-threat-modeling-framework/SKILL.md)

**Description:**

* STRIDE is a software-centric / system-centric threat modeling framework used to identify threats.
* Applies structured, single-step kill chain reasoning without considering business context, objectives, or impact.
* Scoped to the application.

**Example:** [stride-threat-modeling-framework/examples/stride_threat_model.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/stride-threat-modeling-framework/examples/stride_threat_model.md)

### PASTA

In progress...

**Skill:** [pasta-threat-modeling-framework/SKILL.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/pasta-threat-modeling-framework/SKILL.md)

**Description:**

* PASTA is a risk-centric threat modeling framework used to identify risks.
* Applies structured, multi-step kill chain reasoning while considering business context, objectives, and impact.
* Scoped to the application and its environment.

**Example:** N/A

### DREAD

**Skill:** N/A

**Description:**

* DREAD is a risk scoring and prioritization framework.
* Bot used to identify threats or risks.

**Example:** N/A

## How to Upload

To do.

## How to Use

Initial prompt:

```text
Perform STRIDE threat modeling and save the output to "stride_threat_model.md".
```

Output formatting prompt:

```text
Convert "stride_threat_model.md" to "stride_threat_model.html".

Include the Mermaid CDN: https://cdn.jsdelivr.net/npm/mermaid@11.15.0/dist/mermaid.min.js

Add a table of contents.

Make all non–key-value tables sortable.
```
