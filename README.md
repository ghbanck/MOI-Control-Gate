<h1 align="center">MOI Control Gate</h1>

<p align="center">
  <strong>Public architecture notes for evidence boundaries, LLM output review, and workflow reliability</strong>
</p>

<p align="center">
  A public-facing architecture repository for documenting how LLM-assisted workflows can separate claims, evidence, verification, approval, and release boundaries.
</p>

<p align="center">
  <em>A fluent answer is not verification.</em>
</p>

---

## Overview

MOI Control Gate is a public architecture repository for documenting the broader direction behind MOI: a control-gate approach for making LLM-assisted workflows easier to review, constrain, and audit.

The project focuses on one practical workflow problem: LLM output can look complete before it is verified.

A model can generate fluent text. A workflow can appear finished. A claim can sound confident. A reference can look like evidence. A person can approve an action.

Those are different states.

MOI Control Gate exists to describe a public-safe architecture for separating those states:

```text
declared != evidenced != verified != approved
```

This repository is not a production runtime, security product, verifier, or complete implementation. It is a public architecture layer intended to explain the problem, the boundaries, the design direction, and the safe public vocabulary around the project.

---

## At a Glance

| Area                  | Description                                                                                       |
| --------------------- | ------------------------------------------------------------------------------------------------- |
| Repository type       | Public architecture documentation                                                                 |
| Main purpose          | Evidence boundaries and LLM output review for technical workflows                                 |
| Primary users         | Technical artists, pipeline builders, workflow designers, AI-assisted production users, reviewers |
| Main value            | Clearer separation between claims, evidence, verification, approval, and release language         |
| Current status        | Initial public README                                                                             |
| Implementation status | Not included in this repository yet                                                               |
| Runtime status        | Not included in this repository                                                                   |
| Related public demo   | [`MOI-Lite-Demo`](https://github.com/ghbanck/MOI-Lite-Demo)                                       |
| Future direction      | Public-safe control-gate architecture and possible MCP/API-facing design notes                    |
| License               | MIT                                                                                               |

---

## Current Status

This repository currently contains documentation only.

It is safe for this repo to begin small. The goal is not to publish a private runtime or expose internal control logic. The goal is to define the public-facing architecture direction clearly and safely.

| Area                       | Status                                                              |
| -------------------------- | ------------------------------------------------------------------- |
| Public architecture README | In progress                                                         |
| Public-safe vocabulary     | In progress                                                         |
| Private implementation     | Not included                                                        |
| Runtime code               | Not included                                                        |
| Demo code                  | Kept in [`MOI-Lite-Demo`](https://github.com/ghbanck/MOI-Lite-Demo) |
| MCP/API implementation     | Future direction                                                    |
| Production readiness       | Not claimed                                                         |

This repository should not be read as proof that a production system has been deployed, audited, certified, or completed.

---

## Relationship to MOI Lite Demo

`MOI-Lite-Demo` is the lightweight public demo layer.

It demonstrates a small public-facing slice of the idea: evidence-gated responses and the basic distinction between declared, verified, and approved states.

Repository:

```text
https://github.com/ghbanck/MOI-Lite-Demo
```

`MOI-Control-Gate` is different.

This repository is intended to carry the broader public architecture narrative:

```text
MOI-Lite-Demo
= public demo / façade / presentation layer

MOI-Control-Gate
= public architecture direction for workflow reliability, LLM output review, and evidence boundaries
```

MOI Lite Demo should remain small, safe, and intentionally limited.

MOI Control Gate is where the broader architecture, concepts, design principles, public safety boundaries, and future roadmap can be documented without exposing private implementation details.

---

## Why It Exists

LLM-assisted workflows often fail in ways that are not obvious at first glance.

The problem is not only hallucination.

The deeper production problem is workflow contamination: a model can introduce confidence, completion, authority, or inferred progress where the workflow still needs evidence, verification, human decision, or operational review.

This can make a response look useful while hiding unresolved state.

Examples of workflow-degrading behavior patterns:

* unsupported certainty;
* false completion;
* overclaiming;
* unclear evidence boundaries;
* approval being implied without approval;
* references being treated as proof without verification;
* assumptions stacking across multiple responses;
* generated text sounding more complete than the workflow actually is;
* release or deployment language appearing without operational evidence;
* human decision points being blurred or skipped.

MOI Control Gate does not claim to eliminate those problems.

It aims to define a safer public architecture for making those states easier to expose, classify, constrain, and discuss.

---

## Core Principle

MOI Control Gate treats LLM output as something that must pass through explicit boundaries before it can be trusted in a workflow.

```text
A claim is not proof.
Evidence is not approval.
A fluent response is not verification.
A completed-looking workflow is not necessarily complete.
A model is not the source of truth.
```

The architecture should help separate:

* what was declared;
* what was evidenced;
* what was verified;
* what was contradicted;
* what was inferred;
* what remains unknown;
* what requires human decision.

The purpose is not to make the LLM “truthful” by itself.

The purpose is to avoid treating the LLM as the final authority.

---

## Public Architecture Direction

The public architecture direction can be summarized as:

```text
Input or candidate output
-> segmentation
-> claim extraction
-> claim classification
-> evidence boundary check
-> support / contradiction assessment
-> release decision
-> public-safe response
```

A control-gate layer should provide structure around the model:

```text
LLM formulates text.
Backend controls state.
Evidence must be checked.
Human approval remains separate.
Public output must respect the release boundary.
```

This repository may eventually document public-safe versions of those layers.

It will not publish private prompts, proprietary heuristics, private routing instructions, sensitive enforcement logic, or operational internals.

---

## Main Concepts

### Declared

Something was stated.

A statement can be useful, but it is not automatically verified.

Example:

```text
"The deployment was validated."
```

At this stage, the system should not assume validation happened.

### Evidenced

A statement has a reference, file, log, source, or supporting material.

Evidence may exist, but it still needs to be checked. A source existing somewhere does not automatically prove the claim.

### Verified

The available evidence has been checked within the system’s defined verification boundary.

Verification should be explicit, scoped, and traceable.

### Contradicted

The available evidence conflicts with the claim.

Contradiction should override unsupported confidence.

### Approved

A human or authorized process has approved an action.

Approval does not make an unsupported claim true. Approval and truth are different workflow states.

---

## Why This Matters for Technical Workflows

Technical workflows depend on clear state.

When an LLM collapses claim, evidence, verification, and approval into one fluent answer, the result can damage real work:

* a handoff may be treated as ready too early;
* a deployment may be described as verified without logs;
* a file may be described as updated without a diff;
* a test may be described as passing without execution;
* a document may be described as approved without human decision;
* a missing evidence boundary may become invisible.

MOI Control Gate is designed around the opposite behavior:

```text
make uncertainty visible;
preserve decision boundaries;
keep evidence separate from approval;
avoid unsupported release language;
make verification status explicit.
```

---

## Design Principles

* **Claims before confidence.**
* **Evidence before verification.**
* **Verification before release language.**
* **Human decision remains separate.**
* **A model is not the source of truth.**
* **Uncertainty should stay visible.**
* **Public output should not imply unavailable proof.**
* **When evidence is missing, the system should not invent closure.**

---

## Intended Scope

MOI Control Gate is intended to explore and document:

* evidence-gated LLM output review;
* workflow reliability patterns;
* public-safe release boundaries;
* claim-level annotation concepts;
* human decision separation;
* source-of-truth separation;
* epistemic status mapping;
* backend-owned response release patterns;
* future MCP/API transport concepts;
* public-safe architecture diagrams and examples.

This repository may later include safe example code, sanitized schemas, diagrams, and documentation.

For now, it begins with documentation only.

---

## Out of Scope

This repository does not currently include:

* the private MOI Lite runtime;
* production deployment code;
* internal audit prompts;
* repair prompts;
* private rule matrices;
* private routing instructions;
* non-sanitized vocabulary lists;
* proprietary gate heuristics;
* diagnostic traces;
* production trace packets;
* private logs;
* secrets or API keys;
* model-provider integration code;
* final MCP implementation;
* production enforcement internals.

The repository is public-facing by design.

Sensitive implementation details belong outside this repo.

---

## Safety Boundary

This project should not be described as:

```text
production-ready
deployment-verified
security-certified
externally audited
MCP-complete
a truth guarantee
a hallucination eliminator
a replacement for human approval
```

Use safer language:

```text
public architecture direction
workflow-control research
evidence-boundary design
LLM output review architecture
human decision separation
public-safe control-gate documentation
```

---

## Relationship to Private Implementation

Private implementations may contain operational details that are intentionally not represented here.

This public repository does not mirror private implementation work.

Instead, it documents the safe conceptual layer:

```text
what problem the system addresses;
what boundaries matter;
what public concepts are safe to explain;
what must remain private;
what future architecture direction is being explored.
```

The absence of private code in this repository is intentional.

---

## Planned Documentation Areas

Future public documentation may include:

```text
docs/
  architecture/
    control-gate-overview.md
    declared-evidenced-verified-approved.md
    evidence-boundaries.md
    output-review-flow.md

  concepts/
    false-completion.md
    unsupported-certainty.md
    approval-boundaries.md
    source-of-truth-separation.md

  examples/
    public-response-examples.md
    safe-claim-review-examples.md
```

These files are not required for the initial commit.

The initial repository can start with this README only.

---

## Possible Future Implementation Areas

If public code is added later, it should remain sanitized and demonstrative.

Possible future additions:

* public-safe schemas;
* minimal example response contracts;
* toy claim-review examples;
* non-production demo endpoints;
* static examples of release-boundary behavior;
* documentation-only diagrams;
* test fixtures with fake data.

Public implementation should not include:

* private runtime logic;
* private prompts;
* sensitive heuristics;
* real deployment routes;
* production credentials;
* private trace formats;
* operational internals.

---

## Example: Safe Response Boundary

A user says:

```text
"The handoff is ready for deploy."
```

A control-gate style response should avoid accepting the claim as fact without evidence.

Public-safe response style:

```text
Not verified here. Evidence not provided. Approval not demonstrated.
```

This does not prove the handoff is false.

It only preserves the correct boundary:

```text
the claim was declared;
evidence was not shown;
approval was not demonstrated;
therefore release confidence should not be implied.
```

---

## Example: Output Review Direction

A generated answer may contain several claims:

```text
"The file was updated. The tests passed. The deployment is ready."
```

A control gate should be able to separate them:

```text
"The file was updated." -> requires diff or file evidence.
"The tests passed." -> requires test output.
"The deployment is ready." -> requires deployment checks and approval.
```

This is the broader direction behind MOI Control Gate: response-level and claim-level clarity for LLM-assisted workflows.

---

## Current Repository Role

This repository is the public starting point for MOI Control Gate.

```text
Purpose: public architecture documentation
Current contents: README only
Implementation: not included yet
Private runtime: not included
Public demo reference: MOI-Lite-Demo
```

It is safe for this repo to begin small.

The goal is not to publish a private system.

The goal is to explain the architecture direction clearly and safely.

---

## Links

* MOI Lite Demo: https://github.com/ghbanck/MOI-Lite-Demo
* GitHub: https://github.com/ghbanck

---

## License

MIT License. See `LICENSE` when available.
