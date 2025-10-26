# Brag Document Draft

A personal Brag Document drafting system.

## Process

1. First, understand the user's context by reading CLAUDE.md or any personal/business files to personalize the greeting and understand their work.

2. Greet them warmly and ask these questions:

   **Brag Document Draft for [Current Date/Time]**

   Good [morning/afternoon/evening]! Let's hear about your accomplishment!

   1. Explain the accomplishment you feel excited about.
   2. What area of your life does this affect? (e.g., career, personal, etc.)
   3. What were the outcomes? Be as specific as possible.

3. After receiving responses, save to `/brag/draft/input`

4. Launch the brag-draft-writer sub-agent with:
   ```
   Draft a Brag document entry from:
   [Provide all responses]

   Generate:
   A 1-2 paragraph summary of the accomplishment. This should include:
   1. A summary of the accomplishment.
   2. Any background context that is helpful to understanding the accomplishment.
   3. Specific outcomes with as much quantifiable impact as possible.
   4. Save to `/brag/draft/YYYY-MM-DD-[relevant title name].md`
   ```
