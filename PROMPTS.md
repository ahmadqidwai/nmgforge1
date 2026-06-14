# PROMPTS.md - my key prompts log

Keep the handful of prompts that actually moved the build. Not every message - the ones that
mattered: the system/sub-agent prompts, the ones you iterated on, the "this finally worked"
moment. Paste them here MANUALLY as you go.

Why manual? Some free Ollama cloud models do not save a local session log, so an auto audit
log may be empty. That is fine and expected (see the brief's Model Fairness section). What
guarantees your process is judged fairly is: the working plugin + reproducible report.json,
incremental git commits, this PROMPTS.md, and a short DECISIONS.md. Keep these up to date.

Format per entry:
- **Prompt** (paste it)
- **For:** what you were trying to do
- **Revised?** did you have to change it, and why

---

## Example (replace with your own)

- **Prompt:** "Extend linkintel/analyzer.py over_optimized_anchors: flag a destination where
  one non-generic anchor is >= 60% of all internal anchors pointing at it AND count >= 10.
  Run python linkintel/analyzer.py and show the counts."
- **For:** completing the over-optimized exact-match anchor rule
- **Revised?** Yes - first version flagged tiny destinations; added the count >= 10 floor.

---

## My prompts

1. **Prompt:** Analyze the entire repository before writing any code. Read rulebook.md, report.schema.json, linkintel/analyzer.py, mcp/server.py, run.py, agents, and dashboard files. Compare the current implementation against the challenge requirements, identify bugs, accuracy gaps, weak algorithms, and missing features, rank all improvements by score impact versus implementation effort, and create a detailed implementation roadmap. Explain which files and functions should be modified first and recommend the best execution order for maximizing competition performance. Do not generate code yet.

   **For:** Understanding the codebase, identifying scoring opportunities, and creating an implementation plan before starting development.

   **Revised?** No.




2. * **Prompt:**
  Inspect the over_linked_page implementation in analyzer.py. Explain what the current logic does, why the [:0] slice exists, whether it matches the rulebook definition of "top 5% by Unique Inlinks", what edge cases could produce incorrect results, and what the safest deterministic implementation would be. Do not modify code yet.

* **For:**
  Verifying the correctness of over-linked page detection before making changes to a scoring-critical part of the analyzer.

* **Revised?**
  No. Used to understand the existing implementation and validate the fix before modifying code.
  4. **Prompt:** Open analyzer.py and locate the over-linked page implementation. Show the current code, the exact number of over-linked pages returned on the sample dataset, the number that would be returned using a strict top-5%-of-population approach, the URLs that differ between the two approaches, and whether the difference is significant on the provided sample dataset. Do not modify code yet.

   **For:** Comparing the existing implementation against a strict top-5% interpretation and determining whether a code change was justified.

   **Revised?** No.
   8. **Prompt:** Review analyzer.py and focus only on the link_candidates() function. The system currently identifies related pages but returns suggested_anchor=None for every recommendation. Design and implement a deterministic anchor generation system using the target page's H1, Title, and keywords. Generate descriptive SEO-friendly anchors, avoid generic anchors, keep the implementation deterministic and reproducible, explain the design before modifying code, and show before/after examples from the sample dataset. Do not modify any other part of the analyzer.

   **For:** Improving recommendation quality by generating meaningful suggested anchors instead of returning null values.

   **Revised?** No.

   9. **Prompt:** Review analyzer.py and focus only on the link_candidates() function. Design a deterministic anchor generation system that uses H1 tags, page titles, shared topics, and URL slugs to generate descriptive suggested anchors. Avoid generic anchors, keep the implementation reproducible, explain the design before coding, and show example outputs from the sample dataset.

   **For:** Improving recommendation quality by replacing null suggested anchors with meaningful SEO-friendly anchor suggestions.

   **Revised?** No.






