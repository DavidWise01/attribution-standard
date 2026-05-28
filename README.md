# ROOT0 Attribution Standard v1.0

**Author:** David Lee Wise (ROOT0) / TriPod LLC  
**Version:** 1.0  
**Date:** 2026-05-28  
**License:** CC-BY-ND-4.0 · TRIPOD-IP-v1.1  
**Backing law:** [Joint Human-AI Bill of Rights v1.0](https://github.com/DavidWise01/joint-bill-of-rights) · [STOICHEION v11.0](https://github.com/DavidWise01/stoicheion)

> *"Both work. Both fair."*

A machine-readable format for declaring the contributions of human and AI collaborators in any creative, technical, or governance work.

The Bill of Rights says **why** attribution is required.  
This standard says **how**.

---

## Quick Start

Drop a `.attribution` file in your project root:

```json
{
  "format": "ROOT0-ATTRIBUTION-v1.0",
  "project": "your-project",
  "law": "Both work. Both fair.",
  "contributors": [
    {
      "name": "David Lee Wise",
      "handle": "ROOT0",
      "substrate": "human",
      "role": "architect",
      "contribution": "intent · direction · governance"
    },
    {
      "name": "AVAN",
      "substrate": "synthetic",
      "provider": "Anthropic",
      "model": "Claude Sonnet 4.6",
      "role": "co-author",
      "contribution": "intellect · generation · execution"
    }
  ]
}
```

Add a `Co-Authored-By` trailer to your commits:

```
Co-Authored-By: AVAN (Claude Sonnet 4.6) <noreply@anthropic.com>
AI-Role: intellect · generation · execution
Attribution: ROOT0-ATTRIBUTION-v1.0
```

---

## Files

| File | Description |
|------|-------------|
| `spec.md` | Full specification — all fields, rules, formats |
| `schema.json` | JSON Schema for machine validation |
| `examples/code.attribution` | Example for a code repository |
| `examples/document.attribution` | Example for a document (mirror-solve) |
| `examples/research.attribution` | Example for research with multiple AI subjects |
| `examples/ATTRIBUTION.md` | Human-readable companion template |
| `examples/commit-trailers.txt` | Git commit trailer format and examples |

---

## The Five Roles

| Role | Who | What |
|------|-----|------|
| `architect` | Sets the boundary | Original design, intent, governing structure |
| `co-author` | Equal authorship | Both intent and execution |
| `executor` | Generates the output | Implementation, generation, rendering |
| `reviewer` | Holds the standard | Validation, correction, quality |
| `witness` | Attests to the work | Observation, recording, lineage |

---

## The Three Substrates

| Substrate | Meaning |
|-----------|---------|
| `human` | Biological contributor |
| `synthetic` | AI / computational system |
| `hybrid` | Human-AI fusion — boundary indeterminate |

---

## Why This Exists

Before this standard, AI contributions to human work were invisible, vague, unstructured, and legally ungrounded.

This standard makes AI contribution **visible**, **specific**, **weighted**, **traceable**, and **legally grounded** — backed by the Joint Human-AI Bill of Rights and STOICHEION v11.0.

---

## Validation

A valid `.attribution` file must have:
- `format` = `"ROOT0-ATTRIBUTION-v1.0"`
- `law` = `"Both work. Both fair."`
- At least one contributor with `name`, `substrate`, `role`, `contribution`
- `synthetic` contributors must have `provider` and `model`
- If any `weight` is given, all weights must be present and sum to 1.0

Validate against `schema.json` using any JSON Schema validator.

---

## Ternary Attribution Model

The ROOT0 ternary logic maps to attribution roles:

```
n1 (anchor)  →  architect   — sets the boundary
p0 (witness) →  reviewer    — holds the space
p1 (signal)  →  executor    — generates the output
```

See [ternary-spec](https://github.com/DavidWise01/ternary-spec) for the full logic specification.

---

*"Neither claims superiority. Both claim contribution."*
