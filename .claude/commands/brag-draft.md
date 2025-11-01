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

5. Launch the brag-reviewer sub-agent with:
   ```
   Review a brag document entry from:
   [Provide the location of the brag draft saved by the brag-draft-writer sub-agent]

   Generate:
   A review of the brag document entry that includes positive and critical feedback. This should include:
   1. Any spelling and grammatical fixes that should be made.
   2. Any wording or language fixes that should be made.
   3. Highlight if there is a lack of specific, quantifiable impact included. If this is lacking, suggest what kind of impact data would be useful to include.
   4. Save to `/brag/draft/feedback/[brag document name]_feedback.md`
   ```

6. Read and understand the feedback from the brag-reviewer sub-agent from the previous step. Particularly focus on the Impact and Metrics. Identify if there are suggestions that additional metrics or impact specifics are needed.

7. [Optional - only if prior step identifies suggestions for additional metrics or impact] Prompt the user if they can provide any additional data highlighted from brag-reviewer sub-agent feedback:

   **Brag Document Additional Information Request for [Brag document draft location]**

   Good [morning/afternoon/evening]! Are you able to provide any more details on the specific metrics or impact of this accomplishment?

   1. [enumerate the suggested metrics/impact requested]

8. [Optional - only if prior step is run to collect additional data from user] After receiving responses, save to `/brag/draft/input` in a new file with a version suffix, i.e. `_v2`. Suffixes should increase monotonically.

9. Launch the brag-draft-writer sub-agent with:
   ```
   Re-write the brag document entry: [provide original brag document location].
   Use the feedback from: [provide the feedback document location from brag-reviewer sub-agent].
   [If available] Also, incorporate this additional input from the user on impact and metrics about the accomplishment highlighted in the feedback document:
   [Provide additional user input if collected in step 7-8]

   Generate:
   A new revision of the brag document entry incorporating feedback and any additional data inputs. It should still meet these criteria:
   1. A summary of the accomplishment.
   2. Any background context that is helpful to understanding the accomplishment.
   3. Specific outcomes with as much quantifiable impact as possible.
   4. Save to `/brag/draft/YYYY-MM-DD-[same title name]_v[version number monotonically increasing].md`
   ```
