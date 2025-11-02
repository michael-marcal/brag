# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a brag document system built entirely with Claude Code agents. It uses a multi-agent architecture where a main slash command orchestrates two specialized subagents (writer and reviewer) to create, review, and refine personal accomplishment entries.

## Architecture

The system follows a **file-driven, agent-orchestrated workflow**:

1. **Main Command** (`/brag-draft`): Orchestrates the entire workflow, manages user interaction, and coordinates subagents
2. **Writer Subagent** (`brag-draft-writer`): Transforms raw user input into polished 1-2 paragraph entries
3. **Reviewer Subagent** (`brag-reviewer`): Provides critical feedback on spelling, grammar, language, impact metrics, and structure
4. **File System**: Serves as the state machine - files track workflow progress and history

### Workflow Phases

**Phase 1: Input Collection**
- Main command asks three questions (accomplishment, area of life, outcomes)
- Saves raw responses to `draft/input/YYYY-MM-DD-[title].md`

**Phase 2: Draft Generation**
- Launches writer subagent with user responses
- Writer creates 1-2 paragraph entry saved to `draft/YYYY-MM-DD-[title].md`

**Phase 3: Automated Review**
- Launches reviewer subagent with draft location
- Reviewer saves structured feedback to `draft/feedback/[title]_feedback.md`

**Phase 4: Optional Refinement**
- Main command reads feedback and identifies gaps in metrics/impact
- If needed, prompts user for additional data
- Saves to `draft/input/[title]_v2.md` and re-launches writer
- Writer creates improved version as `draft/YYYY-MM-DD-[title]_v2.md`

## Key Conventions

### File Naming

- **Input files**: `YYYY-MM-DD-[descriptive-title].md`
- **Draft files**: `YYYY-MM-DD-[descriptive-title].md` (matches input)
- **Feedback files**: `[draft-filename]_feedback.md` (in feedback/ directory)
- **Versions**: Append `_v2`, `_v3`, etc. (monotonically increasing)

### Brag Document Criteria

Every entry must:
1. Be exactly 1-2 paragraphs long
2. Include: accomplishment summary, background context, quantifiable outcomes
3. Use active voice and clear language
4. Focus on outcomes over activities
5. Lead with most impactful information

### File Structure

```
draft/
├── input/                           # Raw user responses
│   ├── YYYY-MM-DD-title.md         # Initial input
│   └── YYYY-MM-DD-title_v2.md      # Revised input with more metrics
├── feedback/                        # Review feedback
│   └── YYYY-MM-DD-title_feedback.md
├── YYYY-MM-DD-title.md             # Initial draft
└── YYYY-MM-DD-title_v2.md          # Revised draft
```

## Modifying the System

### To Change Interview Questions
Edit `.claude/commands/brag-draft.md` step 2 - modify the three questions while maintaining the structure

### To Adjust Writing Style
Edit `.claude/subagents/brag-draft-writer.md` - modify tone, structure requirements, or length constraints

### To Change Review Criteria
Edit `.claude/subagents/brag-reviewer.md` - adjust evaluation criteria or feedback categories

### To Add New Workflow Steps
Edit `.claude/commands/brag-draft.md` - the main command controls the entire orchestration sequence

## Important Implementation Details

### Subagent Communication
- Subagents receive **all context in a single prompt** - they don't read files independently
- Main command must provide file locations AND relevant content when launching subagents
- Subagents are stateless - they only return results via file writes

### Versioning Logic
- New versions triggered when reviewer identifies missing metrics AND user can provide them
- Version numbers increment monotonically (`_v2`, `_v3`, not `_final` or `_revised`)
- Both input and draft files use same version suffix

### Date Handling
- Use actual dates from user responses or system date
- Format: `YYYY-MM-DD` (ISO 8601)
- Include in both filename and content when relevant (e.g., publication dates)

### Tone and Interaction
- Main command reads CLAUDE.md or personal files for context before greeting
- Greetings personalized with time of day (morning/afternoon/evening)
- Feedback requests are conversational, not robotic
- Reviewer is "polite but honest"

## Common Operations

**Running the workflow:**
```
/brag-draft
```

**Typical file flow for a single entry:**
```
1. draft/input/2025-11-01-example.md           (user responses)
2. draft/2025-11-01-example.md                 (initial draft)
3. draft/feedback/2025-11-01-example_feedback.md (review)
4. draft/input/2025-11-01-example_v2.md        (additional metrics)
5. draft/2025-11-01-example_v2.md              (refined draft)
```

## Design Philosophy

This system demonstrates:
- **File-driven state**: No database needed; git tracks all history
- **Agent specialization**: Different AI personas for different roles
- **Iterative refinement**: Natural support for multiple feedback rounds
- **Quantification focus**: Explicit emphasis on measurable outcomes
- **Human-centered orchestration**: Main command manages complexity, not the user
