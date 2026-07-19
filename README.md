# Threat Modeling Agent Skills

Easy-to-use, high-quality threat modeling agent skills.

Future plans:

* Add the DREAD threat modeling framework.

## Table of Contents

* [Threat Modeling Frameworks](#threat-modeling-frameworks)
    * [STRIDE](#stride)
    * [PASTA](#pasta)
    * [DREAD](#dread)
* [How to Use](#how-to-use)

## Threat Modeling Frameworks

### STRIDE

* STRIDE is a software-centric / system-centric threat modeling framework used to identify threats.
* Applies structured, single-step kill chain reasoning without considering business context, objectives, or impact.
* Scoped to the application.
* Works well with both lower-end and higher-end LLMs.

**Skill:** [stride-threat-modeling-framework/SKILL.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/stride-threat-modeling-framework/SKILL.md)

**Example:** [stride-threat-modeling-framework/examples/stride_threat_model.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/stride-threat-modeling-framework/examples/stride_threat_model.md)

### PASTA

* PASTA is a risk-centric threat modeling framework used to identify risks.
* Applies structured, multi-step kill chain reasoning while considering business context, objectives, and impact.
* Scoped to the application and its environment.
* Works better with higher-end LLMs.

**Skill:** [pasta-threat-modeling-framework/SKILL.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/pasta-threat-modeling-framework/SKILL.md)

### DREAD

* DREAD is a risk scoring and prioritization framework.
* Not used to identify threats or risks.
* Used to complement the STRIDE and PASTA threat modeling frameworks.

**Skill:** [dread-threat-modeling-framework/SKILL.md](https://github.com/ivan-sincek/threat-modeling-agent-skills/blob/main/markdown/dread-threat-modeling-framework/SKILL.md)

## How to Use

- Copy the contents of the [markdown](https://github.com/ivan-sincek/threat-modeling-agent-skills/tree/main/markdown) directory into your project's `.claude/skills/` directory.
- Alternatively, upload each `SKILL.md` file manually under `Customize -> Skills` to your Claude app.

Basic prompt:

```text
Perform STRIDE threat modeling and save the output to "stride_threat_model.md".
```

Advanced prompt:

```text
- Perform STRIDE threat modeling and save the output to "stride_threat_model.md".
- Convert "stride_threat_model.md" to "stride_threat_model.html".
- Add the Mermaid CDN: https://cdn.jsdelivr.net/npm/mermaid@11.15.0/dist/mermaid.min.js
- Ensure the `body` CSS rule includes `width: 100%; max-width: 100%;`.
- Ensure the `td` CSS rule includes `word-break: keep-all;`.
- Add a table of contents.
- Make all non-key-value tables sortable.
```
