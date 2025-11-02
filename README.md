# Brag Document System

A personal accomplishment tracking system built with Claude Code that helps you document and preserve your achievements over time.

For a detailed discussion of the genesis, development, and value of this system, see: [Building a Brag Document AI Agent with Claude Code](https://michaelmarcal.com/building-a-brag-document-ai-agent-with-claude-code/)

## What is a Brag Document?

A Brag Document is a living record of your accomplishments that:

- Summarizes achievements concisely
- Provides background context for understanding the impact
- Focuses on measurable outcomes and results
- Serves as a reference for performance reviews, resumes, and self-reflection
- Helps you remember your wins without sifting through old notes

## Features

This system provides an interactive workflow for creating brag document entries:

1. **Guided Interview Process** - Prompts you with specific questions to capture the full context of your accomplishment
2. **Automated Drafting** - Uses a specialized AI agent to transform your responses into a well-structured entry
3. **Automated Review & Feedback** - A reviewer agent analyzes your draft for spelling, grammar, impact metrics, and overall quality
4. **Iterative Refinement** - System prompts for additional metrics if needed and creates improved versions based on feedback
5. **Organized Storage** - Automatically saves entries with date-stamped filenames for easy retrieval

## Getting Started

### Prerequisites

- [Claude Code](https://claude.com/claude-code) installed and configured

### Usage

To create a new brag document entry, run:

```
/brag-draft
```

The system will guide you through three questions:

1. Explain the accomplishment you feel excited about
2. What area of your life does this affect? (career, personal, etc.)
3. What were the outcomes? Be as specific as possible

After you provide your responses, the system will:
- Save your raw input to [draft/input/](draft/input/)
- Generate a polished 1-2 paragraph summary
- Save the initial draft to [draft/](draft/) with the filename format `YYYY-MM-DD-[descriptive-title].md`
- Automatically review the draft and save feedback to [draft/feedback/](draft/feedback/)
- Prompt you for additional metrics or impact data if the review identifies gaps
- Generate an improved version (if additional data provided) saved as `YYYY-MM-DD-[descriptive-title]_v2.md`

## Project Structure

```
brag/
├── .claude/
│   ├── commands/
│   │   └── brag-draft.md          # Main slash command workflow
│   └── subagents/
│       ├── brag-draft-writer.md    # AI agent for drafting entries
│       └── brag-reviewer.md        # AI agent for reviewing and providing feedback
├── draft/
│   ├── input/                      # Raw user responses
│   ├── feedback/                   # Review feedback for each draft
│   └── *.md                        # Completed brag document entries
└── README.md
```

## How the Review Process Works

After generating your initial draft, the system automatically:

1. **Reviews the draft** using the brag-reviewer agent which evaluates:
   - Spelling and grammar
   - Language clarity and word choice
   - Impact metrics and quantifiable outcomes
   - Structure and conciseness

2. **Saves feedback** to the `draft/feedback/` directory with detailed suggestions

3. **Identifies gaps** in metrics or impact data that would strengthen your entry

4. **Prompts for more information** if specific metrics are missing (e.g., engagement numbers, timeline, quantifiable results)

5. **Generates an improved version** incorporating your additional data and the reviewer's feedback

This iterative process ensures your brag documents are polished, specific, and impactful.

## Example Entries

- [draft/2025-10-12-mikeos-personal-ai-assistant.md](draft/2025-10-12-mikeos-personal-ai-assistant.md) - Example of a completed brag document entry
- [draft/2025-11-01-blog-post-brag-agent_v2.md](draft/2025-11-01-blog-post-brag-agent_v2.md) - Example showing the revision process with improved metrics
- [draft/feedback/2025-11-01-blog-post-brag-agent_feedback.md](draft/feedback/2025-11-01-blog-post-brag-agent_feedback.md) - Example of reviewer feedback

## Why Use This?

- **Performance Reviews**: Have concrete examples ready when review season comes
- **Resume Updates**: Easily pull accomplishments with quantified impact
- **Job Interviews**: Reference specific achievements and their outcomes
- **Self-Reflection**: Track your growth and progress over time
- **Career Planning**: Identify patterns in what you excel at

## Customization

You can customize the workflow by editing:

- [.claude/commands/brag-draft.md](.claude/commands/brag-draft.md) - Modify the questions or process flow
- [.claude/subagents/brag-draft-writer.md](.claude/subagents/brag-draft-writer.md) - Adjust the writing style or structure
- [.claude/subagents/brag-reviewer.md](.claude/subagents/brag-reviewer.md) - Customize the review criteria and feedback style

## Tips for Better Entries

- **Be specific**: Include numbers, percentages, timelines
- **Show impact**: Focus on outcomes, not just activities
- **Provide context**: Explain why this matters
- **Capture it fresh**: Document accomplishments while details are still clear

## License

Personal project - use and modify as you see fit.
