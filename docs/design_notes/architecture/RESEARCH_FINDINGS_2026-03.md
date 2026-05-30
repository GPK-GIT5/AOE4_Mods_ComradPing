# Research Findings: GitHub Copilot Agent Skill Development

**Date:** 2026-03-01  
**Focus:** Authoritative sources for building a "readme-to-ai-reference" Copilot Skill  
**Purpose:** Convert human-readable READMEs into AI-optimized reference material  
**Audience:** Copilot Skill developers, system prompts, AI documentation teams

**Related Document:**  
👉 [REFERENCE_DESIGN_2026-03.md](REFERENCE_DESIGN_2026-03.md) — Reference Material Architecture, Retrieval Optimization, and Hallucination Mitigation

---

## Goal

Provide authoritative documentation sources for developing a GitHub Copilot Agent Skill that converts a human README into AI-optimized reference material.

**Key Requirements:**
- Official documentation (GitHub/Microsoft only)
- Clear, brief descriptions of each source
- Relevance to building the "readme-to-ai-reference" Copilot Skill
- No marketing commentary
- Optimized for AI/system consumption

---

## Primary Sources: Official GitHub & Microsoft Documentation

### 1. GitHub Docs — Creating Copilot Agent Skills

**Source:**  
https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills

**Description:**  
Official documentation for creating Copilot Agent Skills using SKILL.md files.

**Covers:**
- Skill structure and anatomy
- Required SKILL.md format and frontmatter
- Skill discovery and loading mechanisms
- Repository placement guidelines
- Activation conditions and context

**Relevance:**  
Defines authoritative implementation requirements for the "readme-to-ai-reference" skill.

---

### 2. VS Code Documentation — Copilot Agent Skills

**Source:**  
https://code.visualstudio.com/docs/copilot/customization/agent-skills

**Description:**  
Explains Agent Skills runtime behavior and integration within VS Code.

**Covers:**
- What Agent Skills are and how they function
- Folder structure conventions
- How Copilot discovers and loads skills contextually
- Skill execution within VS Code environment
- Skill invocation patterns

**Relevance:**  
Clarifies runtime behavior, context window behavior, and how skills integrate into VS Code's Copilot experience.

---

### 3. GitHub Docs — Copilot CLI Plugin & Skill Creation

**Source:**  
https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-creating

**Description:**  
Technical guide for structuring skills across Copilot CLI and other interfaces.

**Covers:**
- Structuring skills for Copilot CLI compatibility
- YAML frontmatter syntax and required fields
- Skill naming conventions and metadata fields
- Versioning and skill lifecycle
- CLI-specific discovery mechanisms

**Relevance:**  
Defines proper metadata structure and ensures skill compatibility across Copilot interfaces (CLI, VS Code, GitHub web).

---

### 4. GitHub Docs — Custom Instructions for Copilot

**Source:**  
https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot

**Description:**  
Explains repository-level customization and instruction scoping mechanisms.

**Covers:**
- `.github/copilot-instructions.md` behavior
- Path-specific instruction scoping via glob patterns
- Instruction precedence and layering
- Integration with Copilot Agent Skills

**Relevance:**  
Clarifies how Agent Skills integrate with repository instructions and context layering for consistent AI behavior.

---

### 5. GitHub Blog — Copilot Agent Mode Overview

**Source:**  
https://github.blog/ai-and-ml/github-copilot/agent-mode-101-all-about-github-copilots-powerful-mode/

**Description:**  
High-level overview of Agent Mode capabilities and workflows.

**Covers:**
- Agent Mode architecture and design principles
- Tool access patterns (read, search, edit, run)
- Multi-step workflow automation
- Error handling and recovery
- Limitations and constraints

**Relevance:**  
Important for understanding skill orchestration with other agents and multi-step transformation workflows.

---

### 6. GitHub Changelog — Copilot Agent Skills Support

**Source:**  
https://github.blog/docs/project_overview/changelog/2025-12-18-github-copilot-now-supports-agent-skills/

**Description:**  
Official announcement of Agent Skills feature availability.

**Confirms:**
- Skills feature stability and supported status
- Dynamic skill loading based on context
- Feature maturity level
- Known limitations

**Relevance:**  
Confirms architectural stability and that Agent Skills are production-ready for skill development.

---

## Secondary Sources: Documentation & Data Format Standards

### 7. GitHub Docs — Markdown Specification

**Source:**  
https://docs.github.com/en/get-started/writing-on-github

**Description:**  
Complete Markdown syntax reference for GitHub-flavored Markdown.

**Covers:**
- Heading hierarchy and anchors
- Table formatting
- Code block syntax and language specification
- Link syntax and references
- List nesting and formatting

**Relevance:**  
Required for generating output artifacts: `AI_INDEX.md`, `architecture.md`, `file_index.md` with stable anchors.

---

### 8. YAML 1.2 Specification

**Source:**  
https://yaml.org/spec/

**Description:**  
Official YAML serialization language specification (version 1.2).

**Covers:**
- Data type syntax
- Anchor and alias behavior
- Comment syntax
- Nested structure rules
- String quoting and escaping

**Relevance:**  
Required for generating structured `settings_schema.yaml` output with proper syntax validation.

---

## Implementation Checklist (Derived from Official Sources)

### Steps to Build the Skill

**1. Create skill folder structure:**
```
.skills/readme-to-ai-reference/
├── SKILL.md                 # Main skill definition (required)
├── README.md                # Optional: human-friendly overview
└── examples/                # Optional: example outputs
```

**2. Create SKILL.md with required components:**
- YAML frontmatter specifying name, description, version
- Objective: Clear, single-purpose statement
- Inputs: Expected input format and constraints
- Outputs: Artifact types and formats
- Workflow: Step-by-step transformation process
- Quality gates: Validation rules before finalization

**3. Define output artifacts:**
- `ai/AI_INDEX.md` — Machine-readable index with anchors
- `ai/architecture.md` — Structural organization with TOC
- `ai/file_index.md` — File catalog with relationships
- `ai/settings_schema.yaml` — Structured metadata schema
- `ai/glossary.md` — Term definitions with backlinks
- `ai/capabilities_map.md` — Feature matrix (if applicable)

**4. Implement stable anchors:**
```markdown
<!-- DOC:ARCH:DELEGATE_LIFECYCLE -->
<!-- DOC:SCHEMA:ENTITIES -->
<!-- DOC:GLOSSARY:ATTRIBNAME -->
```
These enable reliable cross-referencing and prevent link rot.

**5. Enforce non-hallucination constraint:**
- "Do not invent file paths, constants, or functions."
- Validate against source README before each output
- Log all inferred vs. explicitly stated content
- Fail gracefully on ambiguous requirements

---

## Output Format Specification

### Markdown Output Files

**File: AI_INDEX.md**  
Purpose: Machine-readable entry point  
- Anchored sections for each logical domain
- Hierarchical heading structure (H1 → H6)
- Backtick-wrapped syntax elements
- Consistent code block language tags

**File: architecture.md**  
Purpose: Structural relationships  
- ASCII diagrams (if complex) or textual descriptions
- Clear layer/component boundaries
- Data flow indicators
- Integration points

**File: file_index.md**  
Purpose: File-level navigation  
- Table with columns: Filename | Purpose | Type | Key Exports
- Consistent path notation (relative from repo root)
- Language/format indicators

**File: glossary.md**  
Purpose: Term resolution  
- Alphabetical ordering
- One term per H3 heading
- Example usage where applicable
- Links to related terms

### YAML Output Files

**File: settings_schema.yaml**  
Purpose: Structured configuration reference  
- Valid YAML 1.2 syntax
- Type annotations for each field
- Default values where applicable
- Hierarchical property nesting

---

## Quality Assurance Criteria

### Before Skill Deployment

- [ ] SKILL.md frontmatter contains: name, description, version, author
- [ ] All output files exist and validate (Markdown lint, YAML lint)
- [ ] Anchors are unique and stable across regenerations
- [ ] No invented paths or undefined constants in outputs
- [ ] Example invocations execute successfully
- [ ] Outputs pass accessibility checks (alt text, link validation)
- [ ] Total file size reasonable for context windows

### During Skill Invocation

- [ ] Source README is fully parsed before transformation begins
- [ ] Ambiguities flagged and logged (not silently resolved)
- [ ] Outputs validated against constraints before return
- [ ] User receives clear error messages on failure
- [ ] Partial results documented (if timeout occurs)

---

## Source Citation Rules

When using this documentation:

1. **Always cite which source governs each implementation decision**
   - Example: "Per GitHub Docs (Creating Agent Skills), SKILL.md frontmatter must include..."

2. **Prefer official GitHub Docs over blog posts**
   - Instance: Use https://docs.github.com/ as primary reference
   - Blog posts serve as behavioral explanation, not normative spec

3. **Treat blog posts as behavioral explanation, not requirements**
   - Changelogs: Confirm feature availability
   - Blog articles: Illustrate use cases and best practices
   - Official docs: Define requirements and constraints

4. **Link to stable GitHub Docs URLs**
   - Format: `https://docs.github.com/en/copilot/[path]`
   - Avoid short links that may redirect

5. **Document version assumptions**
   - Copilot SKill format: Latest (as of 2026-03)
   - Markdown: GitHub-flavored
   - YAML: Version 1.2

---

## End  

