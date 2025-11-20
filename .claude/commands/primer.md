# Project Primer

Get up to speed on this project quickly by reading key documentation files and understanding the current state.

## Execution Strategy

**IMPORTANT**: Use parallel tool calls whenever possible to maximize efficiency. Read multiple documentation files in a single message.

## Context Loading Process

### 1. **Discover & Read Core Documentation** (Run in parallel)

   Use the Read tool to load these files simultaneously from the /context folder:
   - `ARCHITECTURE.md` - Technical decisions and patterns (PRIORITY 1)
   - `INITIAL.md` - High level overview of the project
   - `TASK.md` - Historical context and past work
   - `README.md` - Project documentation

   **If a file doesn't exist**, note it and continue - don't let missing files block you.

   **What to understand:**
   - What problem does this solve?
   - What's the tech stack?
   - What patterns must be followed?
   - What's been built already?
   - What lessons were learned?

### 2. **Current Git State** (Run in parallel with step 1)

   Execute these bash commands:
   - `git log --oneline -10` - Recent commit history
   - `ls -la` - Root directory contents

   **What to understand:**
   - Current branch (shown in initial context)
   - Recent changes and commits
   - Files in root directory

### 3. **Discover Project Structure** (After reading docs)

   Use Glob tool to discover file patterns (run in parallel):
   - `Glob: *.md` - Find all markdown documentation
   - `Glob: requirements.txt` - Python dependencies
   - `Glob: package.json` - Node dependencies
   - `Glob: src/**/*.py` - All Python source files
   - `Glob: features/*.md` - Feature specifications
   - `Glob: PRPs/*.md` - Product Requirement Prompts

   Use find for directory structure (portable, works everywhere):
   ```bash
   find . -maxdepth 2 -type d | grep -v ".git" | grep -v "__pycache__" | grep -v ".pytest" | sort
   ```

   **What to understand:**
   - How code is organized
   - Main directories (src/, tests/, features/, PRPs/)
   - Available documentation
   - Dependencies and tech stack

### 4. **Identify Active Work** (After structure discovery)

   Look for:
   - `features/` directory - Feature specifications for planned work
   - `PRPs/` directory - Generated implementation blueprints
   - TASK.md "In Progress" section - Current work
   - Feature branches in git log

   **What to understand:**
   - What's the next priority feature?
   - What's currently in development?
   - What's blocked or pending?

## Output Summary

After gathering all context, provide a concise but comprehensive summary:

```markdown
## Project Primer Summary

### What it is
[1-2 sentence description of project purpose and target users]

### Tech Stack
- **Language & Framework**: [Primary language, version, framework]
- **Database**: [Database type, ORM, caching]
- **Security**: [Auth methods, encryption approaches]
- **Testing**: [Test frameworks and tools]
- **Dev Tools**: [Linters, formatters, pre-commit hooks]

### Key Patterns & Architecture

**Database Patterns:**
[ID strategy, timestamp handling, key architectural patterns from ARCHITECTURE.md]

**API Patterns:**
[API design, authentication, rate limiting, error handling patterns]

**Security Philosophy:**
[Compliance requirements, encryption strategy, audit logging]

**Code Organization:**
[File size limits, module patterns, documentation requirements]

### Recent Work (Last 3-5 Completed Features)

**1. FEATURE-XX: [Name] ([Date])**
- [Key accomplishments]
- [Files created/modified]
- [Performance metrics if relevant]

[Continue for 2-3 more recent features...]

### Current State

**Branch**: [Current branch name]
**Untracked/Modified files**: [What's changed]
**Recent commits**: [Last 3 commits with hashes]

**Current Development Priority**: [Next feature to build]
- Status: [Not started / In Progress / Blocked]
- Scope: [Brief description]
- Key requirements: [Bullet list of main technical requirements]

### Important Notes

**Testing Requirements:**
[Testing patterns, coverage requirements, test structure]

**Documentation Discipline:**
[Which docs to read first, when to update what]

**Performance Targets:**
[API latency, throughput, resource limits]

**Gotchas from Past Work:**
[Specific lessons learned from TASK.md that prevent common mistakes]

### Ready to work on

**Immediate next feature**: [Feature name and number]
- [Where the spec is located]
- [Prerequisites that are complete]
- [Dependencies already in place]

**Suggested workflow**:
1. [Specific next steps with commands if applicable]
2. [Alternative approaches]

**Questions to clarify**:
- [What the user might want to decide]
- [Areas that need clarification]
```

## Adaptive Approach

- **If files don't exist**, note what's missing but continue gathering what IS available
- **Adapt to project structure** - not all projects follow the same patterns
- **Use parallel tool calls** - read multiple files simultaneously for speed
- **Prioritize understanding** over completeness - it's okay to note gaps
- **Be specific** - include file paths, line numbers, and concrete examples where helpful
- **Focus on actionable insights** - what should the developer do next?
