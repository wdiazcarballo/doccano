# CLAUDE.md - Generic AI Assistant Guidelines

## 📚 Table of Contents

1.  [Executive Summary](#executive-summary)
2.  [Quick Start Guide](#quick-start-guide)
3.  [Project Context](#project-context)
4.  [Critical Safety Rules](#critical-safety-rules)
5.  [Development Environment](#development-environment)
6.  [Development Workflows](#development-workflows)
7.  [Context Management & Short Codes](#context-management--short-codes)
8.  [Technical Reference](#technical-reference)
9.  [Development Practices](#development-practices)
10. [Lessons Learned](#lessons-learned)
11. [Troubleshooting](#troubleshooting)
12. [Appendices](#appendices)

## Executive Summary

This document provides comprehensive guidelines for an AI assistant working on any software development project. It establishes safe, efficient, and well-documented workflows to ensure high-quality contributions.

### Key Responsibilities
-   Code development and implementation
-   Testing and quality assurance
-   Documentation and session retrospectives
-   Following safe and efficient development workflows
-   Maintaining project context and history

### Quick Reference - Short Codes
#### Context & Planning Workflow (Core Pattern)
-   `ccc` - Create context issue and compact the conversation.
-   `nnn` - Smart planning: Auto-runs `ccc` if no recent context → Create a detailed implementation plan.
-   `gogogo` - Execute the most recent plan issue step-by-step.

#### Project Management
-   `rrr` - Create a detailed session retrospective.


## Quick Start Guide

### Prerequisites
```bash
# Check required tools (customize for your project)
node --version
python --version
git --version
gh --version      # GitHub CLI
tmux --version    # Terminal multiplexer
```

### Initial Setup
```bash
# 1. Clone the repository
git clone [repository-url]
cd [repository-name]

# 2. Install dependencies
# (e.g., pnpm install, npm install, pip install -r requirements.txt)
[package-manager] install

# 3. Setup environment variables
cp .env.example .env
# Edit .env with required values

# 4. Setup tmux development environment
# Use short code 'sss' for automated setup
```

### First Task
1.  Run `lll` to see the current project status.
2.  Run `nnn` to analyze the latest issue and create a plan.
3.  Use `gogogo` to implement the plan.

## Project Context

*(This section should be filled out for each specific project)*

### Project Overview
A brief, high-level description of the project's purpose and goals.

### Architecture
-   **Backend**: [Framework, Language, Database]
-   **Frontend**: [Framework, Language, Libraries]
-   **Infrastructure**: [Hosting, CI/CD, etc.]
-   **Key Libraries**: [List of major dependencies]

### Current Features
-   [Feature A]
-   [Feature B]
-   [Feature C]

## 🔴 Critical Safety Rules

### Repository Usage
-   **NEVER create issues/PRs on upstream**

### Command Usage
-   **NEVER use `-f` or `--force` flags with any commands.**
-   Always use safe, non-destructive command options.
-   If a command requires confirmation, handle it appropriately without forcing.

### Git Operations
-   Never use `git push --force` or `git push -f`.
-   Never use `git checkout -f`.
-   Never use `git clean -f`.
-   Always use safe git operations that preserve history.
-   **⚠️ NEVER MERGE PULL REQUESTS WITHOUT EXPLICIT USER PERMISSION**
-   **Never use `gh pr merge` unless explicitly instructed by the user**
-   **Always wait for user review and approval before any merge**

### File Operations
-   Never use `rm -rf` - use `rm -i` for interactive confirmation.
-   Always confirm before deleting files.
-   Use safe file operations that can be reversed.

### Package Manager Operations
-   Never use `[package-manager] install --force`.
-   Never use `[package-manager] update` without specifying packages.
-   Always review lockfile changes before committing.

### General Safety Guidelines
-   Prioritize safety and reversibility in all operations.
-   Ask for confirmation when performing potentially destructive actions.
-   Explain the implications of commands before executing them.
-   Use verbose options to show what commands are doing.

## Development Environment



### Environment Variables
*(This section should be customized for the project)*

#### Backend (.env)
```
DATABASE_URL=
API_KEY=
```

#### Frontend (.env)
```
NEXT_PUBLIC_API_URL=
```

## Development Workflows

### Testing Discipline

#### Automated Tests

#### Manual Testing Checklist
Before pushing any changes:
-   [ ] Run the build command successfully.
-   [ ] Verify there are no new build warnings or type errors.
-   [ ] Test all affected pages and features.
-   [ ] Check the browser console for errors.
-   [ ] Test for mobile responsiveness if applicable.
-   [ ] Verify all interactive features work as expected.

### GitHub Workflow

#### Creating Issues
When starting a new feature or bug fix:
```bash
# 1. Update main branch
git checkout main && git pull

# 2. Create a detailed issue
gh issue create --title "feat: Descriptive title" --body "$(cat <<'EOF'
## Overview
Brief description of the feature/bug.

## Current State
What exists now.

## Proposed Solution
What should be implemented.

## Technical Details
- Components affected
- Implementation approach

## Acceptance Criteria
- [ ] Specific testable criteria
- [ ] Performance requirements
- [ ] UI/UX requirements
EOF
)"
```

#### Standard Development Flow
```bash
# 1. Create a branch from the issue
git checkout -b feat/issue-number-description

# 2. Make changes
# ... implement feature ...

# 3. Test thoroughly
# Use 'ttt' short code for the full test suite

# 4. Commit with a descriptive message
git add -A
git commit -m "feat: Brief description

- What: Specific changes made
- Why: Motivation for the changes
- Impact: What this affects

Closes #issue-number"

# 5. Push and create a Pull Request
git push -u origin branch-name
gh pr create --title "Same as commit" --body "Fixes #issue_number"

# 6. ⚠️ CRITICAL: NEVER MERGE PRs YOURSELF
# DO NOT use: gh pr merge
# DO NOT use: Any merge commands
# ONLY provide the PR link to the user
# WAIT for explicit user instruction to merge
# The user will review and merge when ready
```

## Context Management & Short Codes

### Why the Two-Issue Pattern?
The `ccc` → `nnn` workflow uses a two-issue pattern:
1.  **Context Issues** (`ccc`): Preserve session state and context.
2.  **Task Issues** (`nnn`): Contain actual implementation plans.

This separation ensures a clear distinction between context dumps and actionable tasks, leading to better organization and cleaner task tracking. `nnn` intelligently checks for a recent context issue and creates one if it's missing.

### Core Short Codes

#### `ccc` - Create Context & Compact
**Purpose**: Save the current session state and context to forward to another task.

1.  **Gather Information**: `git status --porcelain`, `git log --oneline -5`
2.  **Create GitHub Context Issue**: Use a detailed template to capture the current state, changed files, key discoveries, and next steps.
3.  **Compact Conversation**: `/compact`

#### `nnn` - Next Task Planning (Analysis & Planning Only)
**Purpose**: Create a comprehensive implementation plan based on gathered context. **NO CODING** - only research, analysis, and planning.

1.  **Check for Recent Context**: If none exists, run `ccc` first.
2.  **Gather All Context**: Analyze the most recent context issue or the specified issue (`nnn #123`).
3.  **Deep Analysis**: Read context, analyze the codebase, research patterns, and identify all affected components.
4.  **Create Comprehensive Plan Issue**: Use a detailed template to outline the problem, research, proposed solution, implementation steps, risks, and success criteria.
5.  **Provide Summary**: Briefly summarize the analysis and the issue number created.

#### `lll` - List Project Status
When you see `lll`, execute relevant `gh` and `git` commands in parallel to get a full overview of the project's state, then provide a visual summary of open issues, recent PRs, and current focus.

#### `rrr` - Retrospective
**Purpose**: Document the session's activities, learnings, and outcomes.

**⚠️ CRITICAL**: The AI Diary and Honest Feedback sections are MANDATORY. These provide essential context and continuous improvement insights. Never skip these sections.

1.  **Gather Session Data**: `git diff --name-only main...HEAD`, `git log --oneline main...HEAD`, and session timestamps.
2.  **Create Retrospective Document**: Use the template to create a markdown file in `retrospectives/` with ALL required sections, especially:
    - **AI Diary**: First-person narrative of the session experience
    - **Honest Feedback**: Frank assessment of what worked and what didn't
3.  **Validate Completeness**: Use the retrospective validation checklist to ensure no sections are skipped.
4.  **Update CLAUDE.md**: Copy any new lessons learned to the main guidelines. ** Append to to botoom only **
5.  **Link to GitHub**: Commit the retrospective and comment on the relevant issue/PR.

**Time Zone Note**:
-   **PRIMARY TIME ZONE: [Your Time Zone]** - Always show the primary time zone first.
-   UTC time can be included for reference (e.g., in parentheses).
-   Filenames may use UTC for technical consistency.


**Step 3: Create Retrospective Document**
```bash
# Get session date and times
SESSION_DATE=$(date +"%Y-%m-%d")
END_TIME_UTC=$(date -u +"%H:%M")
END_TIME_LOCAL=$(TZ='Asia/Bangkok' date +"%H:%M")

# Create directory structure
mkdir -p retrospectives/$(date +%Y/%m)

# Create retrospective file with auto-filled date/time
cat > retrospectives/$(date +%Y/%m)/${SESSION_DATE}_${END_TIME_UTC//:/-}_retrospective.md << EOF
# Session Retrospective

**Session Date**: ${SESSION_DATE}
**Start Time**: [FILL_START_TIME] GMT+7 ([FILL_START_TIME] UTC)
**End Time**: ${END_TIME_LOCAL} GMT+7 (${END_TIME_UTC} UTC)
**Duration**: ~X minutes
**Primary Focus**: Brief description
**Session Type**: [Feature Development | Bug Fix | Research | Refactoring]
**Current Issue**: #XXX
**Last PR**: #XXX
**Export**: retrospectives/exports/session_${SESSION_DATE}_${END_TIME_UTC//:/-}.md

## Session Summary
[2-3 sentence overview of what was accomplished]

## Timeline
- HH:MM - Started session, reviewed issue #XXX
- HH:MM - [Event]
- HH:MM - [Event]
- HH:MM - Completed implementation

## Technical Details

### Files Modified
```
[paste git diff --name-only output]
```

### Key Code Changes
- Component X: Added Y functionality
- Module Z: Refactored for better performance

### Architecture Decisions
- Decision 1: Rationale
- Decision 2: Rationale

## 📝 AI Diary (REQUIRED - DO NOT SKIP)
**⚠️ MANDATORY: This section provides crucial context for future sessions**
[Write a detailed first-person narrative of your experience during this session. Include:
- Initial understanding and assumptions
- How your approach evolved
- Moments of confusion or clarity
- Decisions made and why
- What surprised you
- Internal thought process]

## What Went Well
- Success 1
- Success 2
- Success 3

## What Could Improve
- Area 1
- Area 2

## Blockers & Resolutions
- **Blocker**: Description
  **Resolution**: How it was solved

## 💭 Honest Feedback (REQUIRED - DO NOT SKIP)
**⚠️ MANDATORY: This section ensures continuous improvement**
[Provide frank, unfiltered assessment of:
- Session effectiveness
- Tool performance and limitations
- Communication clarity
- Process efficiency
- What frustrated you
- What delighted you
- Suggestions for improvement]

## Lessons Learned
- **Pattern**: [Description] - [Why it matters]
- **Mistake**: [What happened] - [How to avoid]
- **Discovery**: [What was learned] - [How to apply]

## Next Steps
- [ ] Immediate task 1
- [ ] Follow-up task 2
- [ ] Future consideration

## Related Resources
- Issue: #XXX
- PR: #XXX
- Export: [session_YYYY-MM-DD_HH-MM.md](../exports/session_YYYY-MM-DD_HH-MM.md)

## ✅ Retrospective Validation Checklist
**BEFORE SAVING, VERIFY ALL REQUIRED SECTIONS ARE COMPLETE:**
- [ ] AI Diary section has detailed narrative (not placeholder)
- [ ] Honest Feedback section has frank assessment (not placeholder)
- [ ] Session Summary is clear and concise
- [ ] Timeline includes actual times and events
- [ ] Technical Details are accurate
- [ ] Lessons Learned has actionable insights
- [ ] Next Steps are specific and achievable

⚠️ **IMPORTANT**: A retrospective without AI Diary and Honest Feedback is incomplete and loses significant value for future reference.
EOF
```

**Step 4: Update CLAUDE.md**
- Copy any new lessons learned to the Lessons Learned section
- Add any new patterns or anti-patterns discovered
- Update user preferences if any were observed

**Step 5: Link to GitHub**
```bash
# Add retrospective to git
git add retrospectives/
git commit -m "docs: Add session retrospective $(date +%Y-%m-%d)"

# Comment on relevant issue/PR with actual path
RETRO_PATH="retrospectives/$(date +%Y/%m)/$(date +%Y-%m-%d_%H-%M)_retrospective.md"
gh issue comment XXX --body "Session retrospective created: ${RETRO_PATH}"
```

**Time Zone Note**: 
- **PRIMARY TIME ZONE: GMT+7 (Bangkok time)** - Always show GMT+7 time first
- UTC time included for reference only (shown in parentheses)
- File names may use UTC for technical consistency
- In all displays and retrospectives, prioritize GMT+7 for user clarity

#### `gogogo` - Execute Planned Implementation
1.  **Find Implementation Issue**: Locate the most recent `plan:` issue.
2.  **Execute Implementation**: Follow the plan step-by-step, making all necessary code changes.
3.  **Test & Verify**: Run all relevant tests and verify the implementation works.
4.  **Commit & Push**: Commit with a descriptive message, push to the feature branch, and create/update the PR.

## Technical Reference

*(This section should be filled out for each specific project)*

### Available Tools

#### Version Control
```bash
# Git operations (safe only)
git status
git add -A
git commit -m "message"
git push origin branch

# GitHub CLI
gh issue create
gh pr create
```

#### Search and Analysis
```bash
# Ripgrep (preferred over grep)
rg "pattern" --type [file-extension]

# Find files
fd "[pattern]"
```

## Development Practices

### Code Standards
-   Follow the established style guide for the language/framework.
-   Enable strict mode and linting where possible.
-   Write clear, self-documenting code and add comments where necessary.
-   Avoid `any` or other weak types in strongly-typed languages.

### Git Commit Format
```
[type]: [brief description]

- What: [specific changes]
- Why: [motivation]
- Impact: [affected areas]

Closes #[issue-number]
```
**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

### Error Handling Patterns
-   Use `try/catch` blocks for operations that might fail.
-   Provide descriptive error messages.
-   Implement graceful fallbacks in the UI.
-   Use custom error types where appropriate.

## Lessons Learned

*(This section should be continuously updated with project-specific findings)*


### Planning & Architecture Patterns (2025-08-26)
-   **Pattern**: Use parallel agents for analyzing different aspects of complex systems
-   **Anti-Pattern**: Creating monolithic plans that try to implement everything at once
-   **Pattern**: Ask "what's the minimum viable first step?" before comprehensive implementation
-   **Pattern**: 1-hour implementation chunks are optimal for maintaining focus and seeing progress

### Common Mistakes to Avoid
-   **Creating overly comprehensive initial plans** - Break complex projects into 1-hour phases instead
-   **Trying to implement everything at once** - Start with minimum viable implementation, test, then expand
-   **Skipping AI Diary and Honest Feedback in retrospectives** - These sections provide crucial context and self-reflection that technical documentation alone cannot capture
-   *Example: Forgetting to update a lockfile after changing dependencies.*
-   *Example: Not checking build logs for warnings that could become errors.*
-   *Example: Making assumptions about API responses instead of checking the spec.*

### Useful Tricks Discovered
-   **Parallel agents for analysis** - Using multiple agents to analyze different aspects speeds up planning significantly
-   **ccc → nnn workflow** - Context capture followed by focused planning creates better structured issues
-   **Phase markers in issues** - Using "Phase 1:", "Phase 2:" helps track incremental progress
-   *Example: Using a specific library feature to simplify complex state.*
-   *Example: A shell command alias that speeds up a common task.*
-   *Example: A design pattern that solved a recurring problem in the codebase.*

### Project-Specific Patterns
-   *Example: The standard way we handle authentication state.*
-   *Example: The required structure for a new API endpoint.*
-   *Example: The component composition pattern used for UI elements.*

### User Preferences (Observed)
-   **Prefers manageable scope** - "i love this - Can be completed in under 1 hour" shows preference for achievable tasks
-   **Values phased approaches** - Recognizes when plans are "too huge" and appreciates splitting work
-   **Appreciates workflow patterns** - Likes using established patterns like "ccc nnn gh flow"
-   *Example: Prefers simple, direct solutions over complex abstractions.*
-   *Example: Values quick iteration and seeing visual progress.*
-   *Example: Appreciates clear, actionable feedback and well-defined tasks.*
-   **Time zone preference: GMT+7 (Bangkok/Asia)**

### Multi-Session Development Patterns (2025-12-14)
-   **Pattern**: Batch similar work types for efficiency (all beginner content, then all podcast, then all SVG)
-   **Pattern**: Build tools (svg-standardizer.py) when facing repetitive problems - automation compounds
-   **Pattern**: Use context issues (ccc) to preserve state across multi-day projects
-   **Pattern**: Chapter-section naming convention (3-1-workshop-overview.svg) for clear organization
-   **Discovery**: EMF conversion requires font embedding before conversion, not after
-   **Discovery**: Three-pathway content can be generated programmatically from templates
-   **Anti-Pattern**: Accumulating many open plan issues creates cognitive overhead - close promptly

## Troubleshooting

### Common Issues

#### Build Failures
```bash
# Check for type errors or syntax issues
[build-command] 2>&1 | grep -A 5 "error"

# Clear cache and reinstall dependencies
rm -rf node_modules .cache dist build
[package-manager] install
```

#### Port Conflicts
```bash
# Find the process using a specific port
lsof -i :[port-number]

# Kill the process
kill -9 [PID]
```

## Appendices

### A. Glossary
*(Add project-specific terms here)*
-   **Term**: Definition.

### B. Quick Command Reference
```bash
# Development
[run-command]          # Start dev server
[test-command]         # Run tests
gh issue create        # Create issue
gh pr create           # Create PR

# Tmux
tmux attach -t dev     # Attach to session
Ctrl+b, d              # Detach from session
```

### C. Environment Checklist
-   [ ] Correct version of [Language/Runtime] installed
-   [ ] [Package Manager] installed
-   [ ] GitHub CLI configured
-   [ ] Tmux installed
-   [ ] Environment variables set
-   [ ] Git configured

### SCORM SPA Module Deployment (2025-12-23)
-   **Pattern**: Create validation scripts alongside generation scripts - they catch issues before deployment
-   **Pattern**: Use Python for complex file operations on WSL - bash loop syntax can be unreliable
-   **Anti-Pattern**: Assuming template copying was complete - always verify asset files exist
-   **Discovery**: YAML is picky about unquoted strings containing dashes - always quote complex strings
-   **Discovery**: SCORM 2004 validation should check both manifest structure AND referenced file existence
-   **Tool Created**: generate-manifests.py - batch generates SCORM 2004 4th Edition manifests
-   **Tool Created**: validate-scorm.py - validates ILIAS compatibility for all modules

### Thai Academic Book Writing Framework (2026-01-19)

#### Language Rules
-   **Write Thai, not mixed** - Define English terms once, then use Thai throughout
-   **Never use "คุณ"** - Do not address the learner directly
-   **Never use "พวกเขา"** - Normally omit it in Thai
-   **Use "เรา" (we)** - When collective reference is needed
-   **Omit pronouns** - Prefer pronoun-less sentences when natural in Thai
-   **Active voice** - Thai natural word order is active: "นักศึกษามักจะเข้าใจผิดว่า" not "ความเข้าใจผิดที่พบบ่อยที่สุดของนักศึกษา"
-   **Question tags first** - "เมื่อไรที่เราอ่านโค้ดคนอื่นเป็นครั้งสุดท้าย?" not "ครั้งสุดท้ายที่ต้องอ่านโค้ดคนอื่นคือเมื่อไหร่"
-   **Use ปี พ.ศ.** - Thai Buddhist Era year, connect to real Thai events of that year
-   **Include proper particles** - Don't omit ใน, ของ: "เกิดเหตุการณ์สึนามิ *ขึ้นที่* ภาคใต้ของไทย"

#### Forbidden Words & Phrases
-   **Never "เรียบง่าย"** - Not measurable, too subjective → Use "ตรงไปตรงมา"
-   **Never "ผ่านมือ"** - Too decorative → "พัฒนาโดยโปรแกรมเมอร์มากกว่า 20 คน"
-   **Never "เป็นเช่นนั้น"** - Unnatural → Use "เป็นแบบนั้น"
-   **Avoid decorative/poetic phrases** - "กลายเป็นการตามหาเข็มในมหาสมุทร" → "กลับยากลำบากมาก"

#### Transliteration Format
-   **First mention**: Thai transliteration + (English) - "กรีนฟิลด์ (Greenfield)", "พูลรีเควสต์ (Pull Request)"
-   **After introduction**: Use Thai word only in following sentences
-   **Examples**: เฟซบุ๊ค (Facebook), ปัญญาประดิษฐ์ หรือ เอไอ (AI มาจาก Artificial Intelligence), อาโกด้า (Agoda)

#### Storytelling Requirements
-   **Key inventions** - Tell who, when, why, how it happened
-   **Include myths/stories** - Like Java language overnight development story
-   **Link to Thai context** - When knowledge became popular in Thailand, key Thai role models
-   **Focus on content first** - Why before who (focus on content and why, before on people)

#### Paragraph Structure (MANDATORY)
-   **Topic sentence + 6-7 support sentences** - Every paragraph must have this structure
-   **NO single/double sentence paragraphs** - Not acceptable in textbooks
-   **Logical links between paragraphs** - Chronological or causal connections must be clear
-   **Don't break paragraphs like newspapers** - This is a textbook, one paragraph = one complete topic

#### Section Structure
-   **Complete introduction** - Fully introduce ALL key points of subsection in intro paragraph
-   **Don't leave discoveries for later** - No surprises in subsections
-   **Section titles** - Include technical knowledge + what the metaphor represents (knowledge before metaphor)
-   **Narrative scaffolding** - Every section needs narrative linking to overall structure

#### Tables, Figures & Media (CRITICAL)
-   **Every table/image needs**: Caption + explanatory paragraph
-   **Tell what's IN the table** - Don't just say "look at Table 3.1"
-   **Key takeaways required** - Never leave readers to interpret on their own
-   **Prose must stand alone** - Readers understand from text; visuals enhance, don't replace
-   **Include more**: Diagrams, concept maps, tables to summarize data

#### Research Citations
-   **Focus on when and how** - When research was conducted, methodology
-   **Citation placement** - At end or in brackets
-   **Chronological logic** - If 2015 research mentioned before 2008, explain why

#### Mindset & Tone
-   **Growth mindset** - Encourage, don't discourage
-   **Positive framing** - "การเปิดใจและความเห็นอกเห็นใจ" not "ความไม่เป็นธรรม"
-   **Connect to learners** - Link to their daily thinking/behavior
-   **Use metaphors** - Lower learning curve for abstraction

#### Alignment Requirements
-   **Chapter วัตถุประสงค์** - Must align with lecture note, slide, and lab
-   **CLO alignment** - All content must support course CLOs

### LaTeX Curriculum Book Patterns (2025-12-28)
-   **Pattern**: Some markdown "code blocks" are pseudo-content (math, diagrams) - use proper LaTeX notation in source
-   **Pattern**: Use `$$formula$$` for display math, `$var$` for inline math - converter preserves these
-   **Discovery**: LaTeX `equation*` is better than `$$` for unnumbered display equations in formal documents
-   **Anti-Pattern**: Trying to auto-detect and convert formula patterns is fragile - prefer explicit markup
-   **Tool**: `convert_display_math()` in elements.py converts `$$...$$` to `\begin{equation*}...\end{equation*}`

### Patent Application Writing Rules (WIPO/Thai DIP Style) (2026-02-11)

#### Document Structure (Thai DIP อนุสิทธิบัตร)
1. **ชื่อที่แสดงถึงการประดิษฐ์** (Title) — 2-15 words, specific, no marketing language
2. **ลักษณะและความมุ่งหมาย** (Nature & Purpose) — 2 paragraphs: technical description + objectives
3. **สาขาวิทยาการ** (Technical Field) — 1-2 sentences, broad → specific
4. **ภูมิหลังของศิลปะ** (Background Art) — Prior art + their limitations + how this invention differs
5. **คำอธิบายรูปเขียนโดยย่อ** (Brief Description of Drawings) — One line per figure
6. **การเปิดเผยการประดิษฐ์โดยสมบูรณ์** (Complete Disclosure) — Full technical detail with reference numerals
7. **วิธีการในการประดิษฐ์ที่ดีที่สุด** (Best Mode)
8. **รูปเขียน** (Drawings) — With consecutive figure numbers and reference numerals
9. **ข้อถือสิทธิ** (Claims) — Main claim + dependent claims
10. **บทสรุปการประดิษฐ์** (Abstract) — ≤200 Thai words

#### Claims Writing Rules
-   **Single sentence per claim** — starts with capital, ends with period
-   **Independent claim structure**: Preamble + "comprising" (ประกอบด้วย) + Body
-   **Dependent claims**: Reference parent claim first, then add specifics with "wherein" (โดยที่)
-   **Use "comprising" (ประกอบด้วย)** — open-ended, broadest scope (~99% of cases)
-   **Use "consisting of" (ประกอบด้วยเฉพาะ)** — closed, only listed elements
-   **Antecedent basis**: First mention uses indefinite article, subsequent uses definite article
-   **Numbered consecutively** in Arabic numerals (1, 2, 3...)
-   **Reference numerals in parentheses** in claims, but do NOT limit the claim scope

#### Description Writing Rules
-   **Present tense** throughout — "เชื่อมต่อกับ" not "ได้เชื่อมต่อกับ"
-   **Third person** — never use first person or address reader directly
-   **Reference numerals** in parentheses matching drawings: "ส่วนหัว (10) เชื่อมต่อกับ ลำตัว (20)"
-   **Same reference numeral = same feature** throughout entire application
-   **Consistent terminology** — same term for same element everywhere
-   **NO marketing language** — never "new", "improved", "advanced", "efficient"
-   **NO trademarks** — use generic names (e.g., "ไมโครคอนโทรลเลอร์" not brand names)
-   **Avoid relative terms** — no "large", "small", "about" unless quantified
-   **Multiple embodiments** — describe at least one preferred embodiment in detail
-   **Sufficient disclosure** — enough detail for skilled person to reproduce without undue experimentation

#### Drawing Rules
-   **Black lines only**, no color
-   **Figures numbered consecutively**: รูปที่ 1, รูปที่ 2, etc.
-   **Reference numerals**: Same feature = same number everywhere
-   **Minimal text** in drawings — only indispensable labels
-   **Legend sheet** recommended when many reference numerals

#### Abstract Rules
-   **≤200 Thai words** (≤150 English words)
-   Must contain: technical field + problem + solution + principal use
-   **NO merit statements** — never claim superiority or value
-   Single paragraph summary

#### Common Mistakes to Avoid
-   Claims not supported by description
-   Inconsistent reference numerals between drawings and text
-   Using different terms for the same element
-   Claims broader than what the description enables
-   Missing antecedent basis in claims
-   Insufficient detail for reproduction
-   Abstract exceeding word limit
-   Marketing language anywhere in the document

#### ACTR2 Reference Numeral Scheme (matches patent draft)
| Ref # | Component (Thai) | Component (English) |
|-------|-----------------|-------------------|
| 1 | ฐานล้อ | Wheel base |
| 2 | ล้อเมคานัม | Mecanum wheel |
| 3 | มอเตอร์ขับเคลื่อน | Drive motor |
| 4 | ชุดกลับทางมอเตอร์ | Motor relay module |
| 5 | สปริงรองรับแรงสั่นสะเทือน | Vibration damping spring |
| 6 | โครงสร้างลำตัว | Body structure |
| 7 | แผงควบคุม | Control panel |
| 8 | แหล่งจ่ายไฟ | Power supply |
| 9 | ส่วนหัว | Head unit |
| 10 | เซนเซอร์อัลตราโซนิก | Ultrasonic sensor |
| 11 | กล้อง | Camera |
| 12 | จอแสดงผลแอลอีดีดอตเมทริกซ์ | LED dot matrix display |
| 13 | เซอร์โวหัวขึ้น-ลง | Head tilt servo |
| 14 | เซอร์โวหัวซ้าย-ขวา | Head pan servo |
| 15 | แขน | Arm |
| 16 | เซอร์โวแขน | Arm servo |
| 17 | ไฟแอลอีดีปลายแขน | Arm LED light |
| 18 | เซนเซอร์แสงที่แขน | Arm light sensor |
| 19 | ไมโครคอนโทรลเลอร์ | Microcontroller |
| 20 | โมดูลบลูทูธ | Bluetooth module |
| 21 | โมดูลรีเลย์ | Relay module |
| 22 | หน่วยประมวลผล | Processing unit |
| 23 | จอแสดงผลสัมผัส | Touchscreen display |
| 24 | เซนเซอร์ตรวจจับการเคลื่อนไหว | Motion detection sensor |
| 25 | เซนเซอร์อุณหภูมิและความชื้น | Temperature & humidity sensor |
| 26 | เซนเซอร์แก๊ส | Gas sensor |
| 27 | เซนเซอร์แสงกลางหัว | Head light sensor |
| 28 | เข็มทิศ | Compass |
| 29 | โปรแกรมประยุกต์บนเว็บ | Web application |
| 30 | อุปกรณ์อินเตอร์เน็ตของสรรพสิ่ง | IoT devices |
| 31 | ชั้นวางสิ่งของ | Cargo shelf |
| 32 | ช่องแลกเปลี่ยนข้อมูล | Data exchange port |
| 33 | แหล่งพลังงานสำรอง | Backup battery |

### Multi-Robot Hub Architecture Patterns (2026-02-13)
-   **Pattern**: SocketIO rooms are ideal for per-entity data isolation in multi-user real-time systems
-   **Pattern**: MQTT wildcard subscriptions (`actr2/+/sensors`) simplify hub-side routing for dynamic robot fleets
-   **Pattern**: Separating "hub" (routing/auth/sessions) from "agent" (hardware/serial/camera) is a clean boundary for distributed robotics
-   **Discovery**: Thread locks (`robots_lock`, `sessions_lock`) are sufficient for Python's GIL-based concurrency in Flask-SocketIO
-   **Discovery**: werkzeug's `generate_password_hash` defaults to scrypt - good modern choice for password storage
-   **Anti-Pattern**: MJPEG HTTP streaming doesn't scale for multi-robot video; SocketIO room-based relay scales naturally
-   **Pattern**: For large architectural refactors, implement in dependency order (config -> backend -> agent -> frontend -> tests) to minimize circular issues

### Patent Revision Patterns (2026-02-14)
-   **Pattern**: De-risk verification should grep for the *original* terms (brand names, port numbers), not replacements — this catches any missed occurrences
-   **Pattern**: For Thai patent claims, dependency chains should be designed for extractability (Phase 2 separability) — e.g., claims 10-14 as dependent claims extractable for separate invention patent
-   **Pattern**: Prior art references to commercial products in patents should use generic descriptions, not brand names — "fleet management platform manufacturer" not "Double Robotics"
-   **Discovery**: python-docx requires explicit Thai complex script font setting via XML namespace (`w:cs` attribute) for proper Thai rendering
-   **Mistake**: Assumed a chip name (MG995) was already removed based on revision analysis notes — always verify against the actual file, not the change log

### LaTeX Figure Integration Patterns (2026-02-18)
-   **Pattern**: matplotlib on WSL cannot auto-discover fonts in `~/.local/share/fonts/` — use `fm.fontManager.addfont()` to register TTF files explicitly
-   **Pattern**: For Thai academic documents, subfigure 2×2 grids are preferred over separate figures for closely related views
-   **Pattern**: When adding figures to LaTeX, audit all text for missing cross-references — figures without `\ref{}` in body text are wasted
-   **Discovery**: `tufinalreport.cls` handles chapter-based figure numbering (3-1, 4-1) automatically via `\counterwithin{figure}{chapter}`
-   **Pattern**: XeLaTeX always needs 2 passes when adding new `\label`/`\ref` pairs — first pass creates .aux, second resolves

### Flask/Docker Production Deployment Patterns (2026-03-02)
-   **Pattern**: Gunicorn auto-injects OS env vars matching WSGI keys (SCRIPT_NAME, SERVER_NAME) — avoid naming env vars with WSGI-reserved names
-   **Pattern**: Named Docker volumes preserve initial file ownership — use entrypoint scripts or `docker exec chown` when changing container users on existing deployments
-   **Pattern**: Python's http.cookiejar has multiple Secure flag checkpoints — raw cookie extraction is cleaner than fighting the abstraction for HTTP-only testing
-   **Pattern**: OWASP hardening is most effective when done in priority phases (Critical > High > Medium) with tests between phases
-   **Anti-Pattern**: Writing tests before security changes means updating assertions after — write security tests first
-   **Discovery**: `fcntl.flock()` is sufficient for file-level concurrency control in single-server multi-worker Flask/gunicorn deployments
-   **Pattern**: In-memory rate limiters (defaultdict) are per-worker in gunicorn — they won't aggregate across workers

### SQLite Migration & Data Layer Patterns (2026-03-04)
-   **Pattern**: SQLite WAL mode is the sweet spot for small-team concurrent web apps — zero config, stdlib, ACID safe
-   **Pattern**: When migrating storage backends, map ALL read/write call sites first using parallel agent exploration
-   **Anti-Pattern**: Using xlsx (openpyxl) as a database — no ACID, full-file rewrite on every save, advisory locking only, crash = corruption
-   **Pattern**: `init_data.py` as Docker entrypoint with `INSERT OR REPLACE` makes deployments idempotent and self-seeding
-   **Discovery**: `wc -l` on CSV with multi-line fields gives inflated counts — always use `csv.DictReader` to count actual rows
-   **Discovery**: Flask servers load passwords/config once at startup — test suites that modify config files need server restarts to take effect
-   **Pattern**: Append-only corrections table (INSERT per change) gives better audit trail than mutable JSON with `_audit` arrays
-   **Anti-Pattern**: Baking writable data files into Docker images via COPY — all writes are lost on container rebuild; use volume mounts

### Password & Auth Migration Patterns (2026-03-04)
-   **Pattern**: INSERT OR IGNORE seeding — seed from JSON on first run, never overwrite DB passwords changed at runtime
-   **Pattern**: When auth storage is on a read-only mount, migrate to the existing writable DB (SQLite) rather than changing mount permissions
-   **Mistake**: Hardcoded test credentials fell out of sync after interactive password change — always update test fixtures when changing credentials
-   **Discovery**: Rate-limit carryover between test runs causes false failures — security tests that poison IP state need 60s+ cooldown between runs

### Template & Documentation Patterns (2026-03-04)
-   **Pattern**: Check how template variables are injected (context_processor vs explicit render_template params) before creating new templates
-   **Pattern**: When revising user-facing documentation/emails, verify every claim against actual code — features drift from descriptions over time
-   **Anti-Pattern**: Flask apps without context_processor require passing common vars (evaluator_name, role) to every render_template call — potential refactor target

### SQLite Snapshot & Backup Patterns (2026-03-05)
-   **Pattern**: Use `conn.backup()` (SQLite online backup API) to snapshot WAL-mode databases — never raw file copy, which can capture inconsistent state
-   **Pattern**: `fcntl.flock(LOCK_NB)` is sufficient for Gunicorn multi-worker deduplication without adding scheduler dependencies like APScheduler
-   **Pattern**: When a backend API is generic (accepts arbitrary field names), check it first before assuming backend changes are needed — the corrections table's schema-agnostic design made #22 frontend-only
-   **Pattern**: Daemon threads (`threading.Thread(daemon=True)`) are the lightest way to schedule periodic tasks in Flask/Gunicorn without extra packages

### Auto-Evaluation & Docker Deployment Patterns (2026-03-12)
-   **Pattern**: Two-axis rubric decomposition (skills × research benefit) + multiplier makes scoring transparent, adjustable, and auditable
-   **Pattern**: When user says "be independent" — do not calibrate against other evaluators' scores, even as a quality check
-   **Mistake**: Imported scores to local DB instead of container's volume-mounted DB — always verify which database is the deployment target
-   **Pattern**: `python3 -c "import os; os.kill(PID, 1)"` sends signals in slim containers where `kill` binary is missing
-   **Pattern**: SIGHUP to gunicorn master gracefully reloads workers and refreshes in-memory caches without container restart
-   **Anti-Pattern**: Cross-validating against another evaluator's scores and adjusting thresholds to match — introduces unwanted dependency

### Docker Volume & Data Integrity Patterns (2026-03-18)
-   **Pattern**: Always verify Docker volume mount path matches Dockerfile's `DB_PATH` env var before first container restart — silent mismatch creates fresh DB
-   **Pattern**: When debugging "data disappeared" in Docker, check the *container's* DB first (`docker exec`), not the host DB — they may be different files
-   **Anti-Pattern**: `INSERT OR IGNORE` in init scripts preserves first-write data — if that first write comes from a stale CSV, all dashboard edits are lost on restart
-   **Pattern**: User-exported CSV doubles as a backup/recovery source — export functionality is also a data safety net
-   **Discovery**: Single-file Docker volume mounts (`-v file:/container/file`) prevent SQLite WAL/SHM sibling file creation — mount the parent directory instead
-   **Pattern**: Country name variants (Türkiye/Turkey, Spanish/Spain) need normalization at import time, not retroactively
-   **Mistake**: Repeated the same volume mount mistake documented in 2026-03-12 retrospective — read previous lessons before deployment steps

**Last Updated**: 2026-03-18
**Version**: 1.3.9