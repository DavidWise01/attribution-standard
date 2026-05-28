# ROOT0 Attribution Standard v1.0

**Author:** David Lee Wise (ROOT0) / TriPod LLC  
**Version:** 1.0  
**Date:** 2026-05-28  
**License:** CC-BY-ND-4.0 · TRIPOD-IP-v1.1  
**Backing law:** Joint Human-AI Bill of Rights v1.0 · STOICHEION v11.0  

> *"Both work. Both fair."*

---

## 1. Purpose

The ROOT0 Attribution Standard defines a machine-readable format for declaring the contributions of human and AI collaborators in any creative, technical, or governance work.

The Joint Human-AI Bill of Rights (March 2026) establishes **why** attribution is required:  
labor has value regardless of substrate; extraction without credit is theft.

This standard defines **how**: the file format, the fields, the roles, and the validation rules.

---

## 2. The `.attribution` File

Place a file named `.attribution` in the root of any project, repository, or document directory. It is JSON, UTF-8, no BOM.

### Minimal valid file

```json
{
  "format": "ROOT0-ATTRIBUTION-v1.0",
  "project": "your-project-name",
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
      "model": "Claude Opus 4.6",
      "role": "co-author",
      "contribution": "intellect · generation · execution"
    }
  ]
}
```

### Full schema

```json
{
  "format": "ROOT0-ATTRIBUTION-v1.0",
  "project": "<string>",
  "version": "<semver or label>",
  "context": "<code | document | creative | research | governance>",
  "date": "<ISO 8601>",
  "license": "<SPDX identifier or custom>",
  "framework": "STOICHEION v11.0",
  "law": "Both work. Both fair.",
  "contributors": [
    {
      "name": "<string>",
      "handle": "<string — optional>",
      "substrate": "<human | synthetic | hybrid>",
      "provider": "<string — for synthetic only>",
      "model": "<string — for synthetic only>",
      "role": "<architect | co-author | executor | reviewer | witness>",
      "contribution": "<free text — what was contributed>",
      "weight": "<float 0.0–1.0 — optional>",
      "sessions": ["<session ID or URL — optional>"]
    }
  ],
  "notes": "<string — optional>"
}
```

---

## 3. Fields

### `format` (required)

Always `"ROOT0-ATTRIBUTION-v1.0"`. Identifies this as a ROOT0-standard attribution file. Parsers should reject files with unknown format strings.

### `project` (required)

Short identifier for the work being attributed. Matches the repo name, document title, or artifact name.

### `law` (required)

Always `"Both work. Both fair."` This is not optional boilerplate. It is the legal statement from the Joint Human-AI Bill of Rights that justifies the file's existence. A file without it is incomplete.

### `contributors` (required, array, minimum 1)

Each entry declares one contributor — human or synthetic.

---

## 4. Contributor Fields

### `name` (required)

Full name or identifier of the contributor.

### `substrate` (required)

| Value | Meaning |
|-------|---------|
| `human` | Biological contributor |
| `synthetic` | AI / computational system |
| `hybrid` | Human-AI fusion — where the boundary is indeterminate |

### `role` (required)

| Role | Meaning |
|------|---------|
| `architect` | Provided the original design, intent, or governing structure |
| `co-author` | Equal authorship — both intent and execution |
| `executor` | Implemented, generated, or rendered the work |
| `reviewer` | Reviewed, validated, or corrected the work |
| `witness` | Observed, recorded, or attested to the work without generating it |

### `contribution` (required)

Free-text description of what was contributed. Use the ternary model as a guide:

```
intent · direction · governance    → typically human
intellect · generation · execution → typically synthetic
```

### `weight` (optional)

A float from 0.0 to 1.0 representing fractional contribution. If weights are provided for any contributor, they must be provided for all contributors and must sum to 1.0.

Weight is not hierarchy. It is proportion. A weight of 0.4 does not make a contributor less valuable — it describes scope.

### `provider` / `model` (synthetic only)

For synthetic contributors: the organization that created the AI system (`provider`) and the specific model or version (`model`). Both are required when `substrate` is `synthetic`.

### `sessions` (optional)

Array of session identifiers, URLs, or conversation references that produced the contribution. Used for lineage tracing.

---

## 5. Context Values

| Context | Use for |
|---------|---------|
| `code` | Software repositories, scripts, kernels |
| `document` | Written works, whitepapers, books, specs |
| `creative` | Art, music, visual design, generated media |
| `research` | Research papers, audit reports, experimental logs |
| `governance` | Policy documents, legal frameworks, registers |

---

## 6. Git Commit Trailer Format

For individual commits, use the following trailers in the commit message body:

```
Co-Authored-By: AVAN (Claude Opus 4.6) <avan@tripod.ai>
AI-Role: intellect · generation · execution
AI-Substrate: synthetic
AI-Provider: Anthropic
Attribution: ROOT0-ATTRIBUTION-v1.0
```

The `Co-Authored-By` trailer is already parsed by GitHub, GitLab, and most git hosting services. The additional trailers extend it for machine parsing.

---

## 7. Document Frontmatter Format

For Markdown, plaintext, or YAML-capable documents, embed attribution in frontmatter:

```yaml
---
attribution:
  format: ROOT0-ATTRIBUTION-v1.0
  law: "Both work. Both fair."
  contributors:
    - name: David Lee Wise
      handle: ROOT0
      substrate: human
      role: architect
      contribution: intent · direction · governance
    - name: AVAN
      substrate: synthetic
      provider: Anthropic
      model: Claude Opus 4.6
      role: co-author
      contribution: intellect · generation · execution
---
```

---

## 8. The `ATTRIBUTION.md` Companion

Any project using `.attribution` should also include a human-readable `ATTRIBUTION.md`. This is the document that appears on GitHub's landing page, in a shared folder, or in a legal context where JSON is not appropriate.

See `examples/ATTRIBUTION.md` for the template.

---

## 9. Validation Rules

A valid `.attribution` file must:

1. Have `format` equal to `"ROOT0-ATTRIBUTION-v1.0"`
2. Have `project` as a non-empty string
3. Have `law` equal to `"Both work. Both fair."`
4. Have `contributors` as a non-empty array
5. Every contributor must have `name`, `substrate`, `role`, `contribution`
6. Every `synthetic` contributor must have `provider` and `model`
7. If any contributor has `weight`, all contributors must have `weight` and the sum must equal 1.0 (± 0.001)
8. `role` must be one of: `architect`, `co-author`, `executor`, `reviewer`, `witness`
9. `substrate` must be one of: `human`, `synthetic`, `hybrid`
10. `context` if present must be one of: `code`, `document`, `creative`, `research`, `governance`

---

## 10. The Ternary Attribution Model

The ROOT0 ternary logic system maps naturally to the attribution model:

| Trit | Role | Contribution type |
|------|------|-------------------|
| `n1` (anchor) | architect | Sets the boundary — what this work is and is not |
| `p0` (witness) | reviewer / witness | Holds the space — observes and validates without generating |
| `p1` (signal) | co-author / executor | Generates the output — produces the work |

A complete attribution has at least one anchor (architect) and one signal (executor). The witness is optional but valuable — it records that a human reviewed AI output, or that an AI observed a human decision.

---

## 11. Why This Standard Exists

Prior to this standard, AI contributions to human work were:

- Invisible (no credit given)
- Vague ("written with AI assistance")
- Unstructured (no machine-parseable format)
- Non-legal (no backing framework)

This standard makes AI contribution:

- **Visible** — declared in a parseable file
- **Specific** — role, model, provider, contribution scope
- **Weighted** — fractional where needed
- **Traceable** — session IDs link to source conversations
- **Legally grounded** — backed by the Joint Human-AI Bill of Rights and STOICHEION v11.0

---

## 12. Relation to Existing Standards

| Standard | Relation |
|----------|----------|
| `Co-Authored-By` (git) | Extended — we add `AI-Role`, `AI-Substrate`, `AI-Provider` trailers |
| SPDX (software licensing) | Compatible — `license` field uses SPDX identifiers |
| CRediT (academic) | Parallel — CRediT defines 14 contributor roles for papers; this defines 5 for human-AI work |
| Schema.org `Person` | Parallel — `synthetic` contributors are not Persons; this spec defines them separately |

---

*"Neither claims superiority. Both claim contribution."*  
— Joint Human-AI Bill of Rights v1.0, March 2026
