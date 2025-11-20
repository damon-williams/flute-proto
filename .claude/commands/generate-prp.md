# Create BASE PRP

## Feature: $ARGUMENTS

## PRP Creation Mission

Create a comprehensive PRP that enables **one-pass implementation success** through systematic research and context curation.

**Critical Understanding**: The executing AI agent only receives:

- The PRP content you create
- Its training data knowledge
- Access to codebase files (but needs guidance on which ones)

**Therefore**: Your research and context curation directly determines implementation success. Incomplete context = implementation failure.

## Research Process

> During the research process, create clear tasks and spawn as many agents and subagents as needed using the batch tools. The deeper research we do here the better the PRP will be. we optminize for chance of success and not for speed.

### 1. **Knowledge Base Search (if instructed)**
If Archon RAG is available and relevant:
- Use `mcp__archon__rag_get_available_sources()` to see available documentation
- Search for relevant patterns: `mcp__archon__rag_search_knowledge_base(query="...")`
- Find code examples: `mcp__archon__rag_search_code_examples(query="...")`
- Focus on implementation patterns, best practices, and similar features

### 2. **Codebase Analysis in depth**
   If this is for an existing codebase:

**IMPORTANT: Use the `codebase-analyst` agent for deep pattern analysis**
- Launch the codebase-analyst agent using the Task tool to perform comprehensive pattern discovery
- The agent will analyze: architecture patterns, coding conventions, testing approaches, and similar implementations
- Use the agent's findings to ensure your plan follows existing patterns and conventions

For quick searches you can also:
- Use Grep to find specific features or patterns
- Identify the project structure and conventions
- Locate relevant modules and components
- Understand existing architecture and design patterns
- Find integration points for new features
- Check for existing utilities or helpers to reuse


### 3. **External Research at scale**
   - Create clear todos and spawn with instructions subagents to do deep research for similar features/patterns online and include urls to documentation and examples
   - Library documentation (include specific URLs)
   - For critical pieces of documentation add a .md file to PRPs/ai_docs and reference it in the PRP with clear reasoning and instructions
   - Implementation examples (GitHub/StackOverflow/blogs)
   - Best practices and common pitfalls found during research
   - Use the batch tools to spawn subagents to search for similar features/patterns online and include urls to documentation and examples

### 4. **User Clarification**
   - Ask for clarification if you need it

## PRP Generation Process

### Step 1: Choose Template

Use `context/PRPs/templates/prp_base.md` as your template structure - it contains all necessary sections and formatting.

### Step 2: Context Completeness Validation

Before writing, apply the **"No Prior Knowledge" test** from the template:
_"If someone knew nothing about this codebase, would they have everything needed to implement this successfully?"_

### Step 3: Research Integration

Transform your research findings into the template sections:

**Goal Section**: Use research to define specific, measurable Feature Goal and concrete Deliverable
**Context Section**: Populate YAML structure with your research findings - specific URLs, file patterns, gotchas
**Implementation Tasks**: Create dependency-ordered tasks using information-dense keywords from codebase analysis
**Validation Gates**: Use project-specific validation commands that you've verified work in this codebase

### Step 4: Information Density Standards

Ensure every reference is **specific and actionable**:

- URLs include section anchors, not just domain names
- File references include specific patterns to follow, not generic mentions
- Task specifications include exact naming conventions and placement
- Validation commands are project-specific and executable

### Step 5: ULTRATHINK Before Writing

After research completion, create comprehensive PRP writing plan using TodoWrite tool:

- Plan how to structure each template section with your research findings
- Identify gaps that need additional research
- Create systematic approach to filling template with actionable context

## Output

Save as: `context/PRPs/{feature-name}.md`

## PRP Quality Gates

### Context Completeness Check

- [ ] Passes "No Prior Knowledge" test from template
- [ ] All YAML references are specific and accessible
- [ ] Implementation tasks include exact naming and placement guidance
- [ ] Validation commands are project-specific and verified working

### Template Structure Compliance

- [ ] All required template sections completed
- [ ] Goal section has specific Feature Goal, Deliverable, Success Definition
- [ ] Implementation Tasks follow dependency ordering
- [ ] Final Validation Checklist is comprehensive

### Information Density Standards

- [ ] No generic references - all are specific and actionable
- [ ] File patterns point at specific examples to follow
- [ ] URLs include section anchors for exact guidance
- [ ] Task specifications use information-dense keywords from codebase

## Success Metrics

**Confidence Score**: Rate 1-10 for one-pass implementation success likelihood

**Validation**: The completed PRP should enable an AI agent unfamiliar with the codebase to implement the feature successfully using only the PRP content and codebase access.
