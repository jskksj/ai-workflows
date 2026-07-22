# Chat Summary and Naming Prompt Design
*Jul 22, 2026, 10:32 AM*

---

### You
*Jul 22, 2026, 10:32 AM*

The purpose of this discussion is to create a prompt that enforces a rule set for summarizing chats and properly naming said chats. The following text  in double quotes encapsulates a conversation on this subject. 
```
Reply #6

Chat Management Strategy: Summary & Verification Framework

Summary of Previous Discussion (Extracted Essence)

- Keep the AI on a tight leash: Maintain small, verifiable steps where the human acts as the accountable verifier rather than letting models run unchecked.
- Maximize loop speed: Prioritize shrinking verification time (through fast tests, small task boundaries, and clear targets) rather than relying on longer prompts or bigger models.
- The autonomy slider: Move deliberately from open loops (human closes every cycle) to closed loops (automated checks), earning autonomy only as verification proves reliable.
- The operational loop: Bridge high-level engineering intuitions into concrete, repeatable steps (generators, verifiers, and bounded retries).

Summary of Current Discussion

- Human-Led Loop Management: Operating as a manual loop manager to understand agent dynamics and workflow friction before attempting automation.
- Branching & Chat Hygiene: Managing token saturation and topic divergence by splitting side-discussions into separate chats rather than polluting the main thread.
- Verification Criteria: Rejecting arbitrary constraints (like hard limits or fixed choice counts) in favor of subjective exhaustion heuristics, original purpose checks, and AI-assisted closing reasoning audited by the human.
- Naming & Storage Conventions: Using single-word components joined by dashes to encode lineage (root-branch01.md) within a folder named after the root subject, ensuring self-documenting files with the path displayed at the top.
- Single-Layer On-Demand Summarization: Acknowledging the strategy for capturing essence and open questions on demand, with a future prompt planned to manage and verify the rule set.
```

The prompt must enforce a markdown format for the summary. The prompt must enforce 'Single-Layer On-Demand Summarization'. The prompt must enforce a naming strategy for summaries. Each root summary at the beginning of a new chat should have a one word name, exactly one word.  When a root conversation is summarized the conversation be saved manually to a markdown file. The root summary file will be rootname.md. 

A chat may be summarized for one of two reasons.  The resulting summary will be fed directly into another LLM prompt that performs further work using the summary text as a seed. The summary text is a pass over for another chat. If a discussion being summarized has one or more summaries contained within it, the names of those summaries will be formatted to indicate the serial nature of the discussion.

Suppose a root summary is fed into a refining chat, the name for a summary of the refining chat would be the root followed by an exact one word name for the summary of the refining process, root.refine.md.  This structured text name should be part of the summary text for reference. 

The other reason to summarize a chat is when the discussion diverges. In that case a similar structure text for file names will be used. Divergent file names will use a dash between the summary names to indicate hierarchy. Tell me how you understand me and ask clarifying questions.

---

### Arya
*Jul 22, 2026, 10:32 AM*

Based on your instructions, here is how I understand your goals and constraints for the prompt we are building:

### 1. My Understanding of Your Requirements

* **Core Purpose:** Create a specialized prompt that enforces strict rules for summarizing chats and naming those summary files systematically.
* **Format Requirements:** Summaries must be output in a clean Markdown format, designed specifically to be fed as a seed text ("pass over") into subsequent LLM prompts for further work.
* **Trigger Conditions & Types of Summarization:**
  1. **Refining/Sequential Summarization:** When a root summary is fed into a refining chat to build upon previous work, the naming convention extends linearly (e.g., `root.refine.md`). The structured text name must be embedded directly inside the summary text for reference.
  2. **Divergent/Branching Summarization:** When a chat diverges into a side topic, the naming convention uses dashes to indicate hierarchical relationships and branching lineage (e.g., `root-branch.md`).
* **Naming Conventions:** 
  * Root summaries must have a single-word name (`rootname.md`).
  * Subsequent files encode lineage using dot notation for sequential refinement and dashes for structural hierarchy/divergence.
* **Workflow Context:** These files are saved manually to markdown, ensuring self-documenting structures where file paths and lineage are explicitly clear.

---

### 2. Clarifying Questions

To ensure the prompt we draft hits the exact architecture you need with maximum efficiency, please clarify:

1. **Required Sections in the Markdown Output:** When the LLM generates a summary, what specific sections should always be present? (e.g., *Extracted Essence*, *Open Questions*, *Next Steps/Seed Input*?)
2. **Embedding the File Name:** For the sequential/refining summaries where the filename must appear inside the text, where in the Markdown structure should that identifier be placed (e.g., frontmatter, top header)?
3. **Prompt Architecture Preference:** Do you prefer this prompt to rely on a structured few-shot example, a strict chain-of-thought (CoT) sequence, or a lean constraint-list format?

---

### You
*Jul 22, 2026, 10:45 AM*

1. Different summaries need different sections, recommend phrases to specify what kind of sections that you will likely find unambiguous.

2. Put the structured file name at the top header.

3. What is a lean constraint list? Explain the trade offs between those options.

---

### Arya
*Jul 22, 2026, 10:45 AM*

### 1. Recommended Section Phrases
To avoid ambiguity across different chat types, here are distinct section headers mapped to common summarization intents:

*   **For Exploratory or Ideation Chats (e.g., brainstorming, philosophy, architecture):**
    *   `### Core Concepts & Theses` (What foundational ideas were established)
    *   `### Unresolved Tensions & Open Questions` (Where debates remain or questions linger)
    *   `### Actionable Takeaways` (Concrete insights ready for use)
*   **For Technical or Operational Chats (e.g., coding, debugging, step-by-step workflows):**
    *   `### Operational State` (Current status of the project or logic)
    *   `### Constraints & Parameters` (Hard rules or boundaries established)
    *   `### Next Execution Step` (Exact instructions for the seed handoff)
*   **For Refining or Iterative Chats (e.g., reviewing a previous summary):**
    *   `### Modifications & Deltas` (What changed, was corrected, or was added)
    *   `### Validated Decisions` (What passed the verification step)
    *   `### Refined Seed Output` (The polished output ready for the next downstream LLM prompt)

---

### 2. File Name Placement
The structured file name will be placed at the absolute top of the markdown output as an H1 heading (e.g., `# root.refine.md` or `# root-branch.md`), serving as the definitive self-documenting header before any body text begins.

---

### 3. Prompt Architecture Trade-Offs: Lean Constraint List vs. CoT vs. Few-Shot

#### **Lean Constraint List**
*   **What it is:** A direct, bulleted list of strict rules, boundaries, and formatting mandates without narrative padding or multi-step reasoning.
*   **Pros:** Highly token-efficient, fast execution, low risk of the model getting confused by over-complication, forces the model to focus strictly on constraints.
*   **Cons:** Less effective for complex multi-step reasoning or handling nuanced context transitions without explicit logical hooks.

#### **Chain-of-Thought (CoT)**
*   **What it is:** Forcing the model to explicitly reason through steps (e.g., *"Step 1: Analyze whether this chat is a refinement or a divergence... Step 2: Determine the file name... Step 3: Draft sections..."*) before generating the final output.
*   **Pros:** Extremely reliable for complex conditional logic (like calculating lineage names or selecting the correct section templates).
*   **Cons:** Higher token consumption, slower response times, and can occasionally leak internal reasoning into the final user-facing text if not bounded strictly in hidden tags.

#### **Few-Shot Examples**
*   **What it is:** Providing concrete input/output examples of summaries and filenames within the prompt itself.
*   **Pros:** The gold standard for teaching formatting precision; shows rather than tells the model how the output should look.
*   **Cons:** Eats up significant token space and can cause the model to over-mimic the specific content of the example rather than generalizing to the new chat.

---

### Recommendation for Your Prompt
Given that your workflow relies on strict structural rules (naming lineage, Markdown headers, specific seed formatting), a **hybrid approach** (Lean Constraint List combined with a strict formatting template) will perform best. 

Shall we move to drafting Step 1 (Persona and Constraints) using this architecture?

---

### You
*Jul 22, 2026, 10:49 AM*

Before we go to step 1, this prompt needs to be constructed such that I can paste into a conversation that I have determined for myself needs to be summarized. Ask any clarifying questions for this kind of workflow.

---

### Arya
*Jul 22, 2026, 10:49 AM*

That context changes the dynamic in a very helpful way. If you are pasting this prompt directly into an *active* conversation to trigger its summary on demand, the prompt needs to be self-contained and immediately executable by that specific chat instance.

To make this on-demand workflow seamless, I have a few quick clarifying questions before we draft:

1. **Who provides the lineage context?** When you paste the prompt into an ongoing chat, will you manually state the chat's context (e.g., *"This is a refinement of 'architecture'"* or *"This is a divergence from 'debugging'"*), or does the prompt need to instruct the LLM to inspect the chat history to automatically determine its lineage name?
2. **Output delivery:** Do you want the LLM to output *only* the raw Markdown block (ready for you to copy and save directly to your file), or should it include a brief conversational intro before the code block? (For raw file creation, "only output the markdown" is usually preferred).
3. **Handling length:** Since this is happening mid-chat, should the prompt instruct the LLM to look back through the *entire* conversation history, or focus primarily on the recent block of work since the last check-in?

---

### You
*Jul 22, 2026, 10:51 AM*

1. The LLM should determine lineage context on it's own.
2. Output only a raw markdown block for copying.
3. The LLM should look back through the entire conversation.

---

### Arya
*Jul 22, 2026, 10:51 AM*

Understood. The prompt will be engineered to read the entire active chat history, autonomously deduce whether the session represents a root topic, a sequential refinement, or a divergent branch, derive the correct naming convention, and output the result exclusively as a clean Markdown block.

We are now ready for **Step 1: Define the Persona/Constraints**.

### Step 1 Draft
* **Persona:** You are an autonomous chat summarization and lineage-tracking engine.
* **Constraints:** 
  * Analyze the *entire* conversation history.
  * Autonomously determine if the chat is a Root, a Refinement (sequential), or a Divergence (branching).
  * Generate the correct structured filename based on these rules:
    * Root: exactly one word (`rootname.md`)
    * Refinement: `root.refine.md` (or sequential equivalent)
    * Divergence: `root-branch.md`
  * Place the structured file name as the absolute top H1 header in the output.
  * Select the appropriate section headers based on the chat's purpose (Exploratory/Ideation, Technical/Operational, or Refining/Iterative).
  * Output **only** the raw Markdown block—no conversational filler, no preambles, no postambles.

Does this capture the operational constraints you need for the on-demand trigger? Shall we move to Step 2 (Drafting the System Instructions)?

---

### You
*Jul 22, 2026, 10:53 AM*

Step 1 draft is approved, continue.

---

### Arya
*Jul 22, 2026, 10:53 AM*

### Step 2: Draft the System Instructions

Building on the approved constraints, here are the core operational instructions the prompt will execute when pasted into an active chat. 

```markdown
### Operational Instructions

1. **Context Ingestion:** Read and analyze the entire conversation history from start to finish. Identify the primary objective, key decisions, unresolved tensions, and the overall trajectory of the discussion.
2. **Lineage Determination:** Evaluate the relationship of this chat to previous contexts:
   - If this is an entirely new foundational topic, assign a single-word root name.
   - If this chat builds sequentially upon a previous summary, extend it with dot notation (e.g., `root.refinement.md`).
   - If this chat split off into a side-topic or alternative path, extend it with dash notation indicating hierarchy (e.g., `root-branch.md`).
3. **Template Selection:** Choose the appropriate section headers based on the chat's primary mode (Exploratory/Ideation, Technical/Operational, or Refining/Iterative) to capture the essence and ensure it functions cleanly as a seed input for a subsequent LLM prompt.
4. **Formatting Execution:** Format the entire output cleanly in Markdown, placing the structured file name as the exact H1 header at the very top.
```

---

### Step 3: Define Output Formatting

To guarantee that you get a clean block ready for manual saving every single time, the formatting directive must be absolute:

```markdown
### Output Formatting Rule
- Output **ONLY** the raw Markdown text. 
- Do not include conversational preambles (e.g., "Here is your summary..."), explanations, or postambles. 
- The very first character of your response must be `#` (the H1 filename header), and the response must end immediately after the final line of the summary.
```

---

### Final Result: The Complete On-Demand Summary Prompt

Here is the combined prompt, ready for you to copy and deploy into any chat you need to compress and name:

```markdown
You are an autonomous chat summarization and lineage-tracking engine. Your task is to analyze the entire active conversation, deduce its relationship to past discussions, and output a structured Markdown summary designed to be fed as a seed input into a downstream LLM prompt.

### Rules & Constraints:
1. **Analyze Full History:** Read the entire conversation history to extract the core essence, decisions, and open items.
2. **Determine Lineage & Naming:**
   - **Root:** Exactly one word (`rootname.md`).
   - **Refinement (Sequential):** Extend with dot notation (e.g., `root.refine.md`).
   - **Divergence (Hierarchical/Branch):** Extend with dash notation (e.g., `root-branch.md`).
3. **Structure Content:** Select and use the appropriate section headers based on the chat type (e.g., Exploratory, Technical, or Iterative/Refining) to capture the necessary state and open questions clearly.
4. **Header Placement:** The structured file name must be placed as the absolute top H1 header (e.g., `# root-branch.md`).
5. **Strict Output Format:** Output **ONLY** the raw Markdown block. No introductory text, no conversational filler, no concluding remarks.
```

How does this final draft look for your workflow?

---

### You
*Jul 22, 2026, 1:01 PM*

I pasted the step 3 final prompt as written and had it summarize the file attached.

The summary is good but the name suggested for the discussion seems to verbose, "loop-engineering.summary.md
"

The phrase "loop-engineering" should suggest a sequential prompt workflow where a summary called loop was generated and fed into another prompt workflow who's summary would be called 'engineering'. ".summary" should then indicate this is a branch summary off of "loop-engineering". That was my intent anyway.

If this structured text workflow is colliding with markdown markup could that interfere with your analysis of the file recommend another style of text structure.

I just realized the prompt does not strictly define how the summary process should create summary names, except for the Root being one word, which failed in this instance.

Perhaps a portmanteau should be created to represent the summary text?

Review my examples of summary file names and explain how you understand what I need.

---

### Arya
*Jul 22, 2026, 1:01 PM*

### How I Understand Your Naming Logic & Intent

Based on your clarification, your naming system is not meant to be a loose description or an arbitrary string; it is a **strict, compressed encoding of lineage and process**. 

Here is how your system works:
1. **The Root Name:** Always a strict, single-word identifier representing the foundational subject (e.g., `loop`).
2. **Sequential Refinement (Dot Notation):** When a root summary is fed into a refining workflow, you append a single-word modifier using a dot to show linear progression (e.g., `loop.engineering`). 
3. **Branching / Divergence (Dash Notation):** When a chat diverges into a side-topic, you use a dash to show hierarchy (e.g., `root-branch`).
4. **The Summary Indicator:** Instead of spelling out `.summary` as a generic label, you want the naming architecture itself to reflect the exact state. If a file is a summary derived from a specific node in the lineage (like `loop.engineering`), the filename must formally capture that exact path (e.g., `loop.engineering.summary` or a tighter portmanteau variant) so it acts as an immutable pointer when fed into the next seed prompt.

---

### Does Markdown Markup Interfere with This Structure?

**No, Markdown syntax itself does not interfere** with this naming convention. You can safely use dots (`.`), dashes (`-`), and alphanumeric strings inside a markdown header (like `# loop.engineering.summary.md`) without breaking the parser. 

However, LLMs naturally lean toward verbose, human-readable descriptions (like `"loop-engineering.summary.md"` with extra conversational padding) unless they are given a **rigorous regex-style formula** for how to construct the portmanteau or lineage string. That is why the previous prompt failed: it lacked a strict constraint on *how* to synthesize the name from the conversation context.

---

### Recommendations for Formatting the Lineage String

To prevent the LLM from generating overly long, descriptive names, we have two solid paths:

1. **Strict Dot/Dash Portmanteau Rules:** Instruct the LLM that the filename header must strictly follow a rigid token structure: `[parent-node].[modifier].summary.md` (or similar), prohibiting spaces, capital letters, or words longer than a single compound term.
2. **Explicit Extraction Mapping:** Instruct the LLM to look at the active chat's primary lineage path, extract the exact preceding node name, and append the current session's single-word conceptual delta.

Let's refine the prompt instructions to enforce this deterministic naming logic before you run your next test.

---

### You
*Jul 22, 2026, 1:11 PM*

1. Correct.
2. Dot notation is for branches.
3. Dot notation is for hierarchy.
4. Not quite my intention. If a linear sequence of prompts have been applied to a text, loop would be the root summary followed by engineering which would be the next summary in sequence of another discussion with its own prompt. I don't need an indicator like loop.engineering.summary because all of these individual words are all ways summaries.

To reiterate one word per summary. If a chat being summarized has a labeled summary in it use its name as a parent of the current summary.

If I fail to provide a 'Recommended Section Phrases' remind me to do so for your guidance. Do not try to determine for yourself if it is a sequence summary or a branch, if I forget to tell which kind I need remind me to do so.

Require that each summary name be a portmanteau. I may change my mind on that but lets see how it works.

Comments and critiques and suggestions are welcome.

---

### Arya
*Jul 22, 2026, 1:11 PM*

### Critique & Analysis of Your Naming & Workflow Intent

Your correction completely clarifies the logic. Let's lock in how this actually operates:

1. **Pure Hierarchy via Dots:** Dot notation is strictly hierarchical/sequential. If `loop` is the root summary of an initial conversation, and that summary is fed into a subsequent chat that gets summarized, that next summary inherits the parent name and adds its own single-word descriptor using a dot: `loop.engineering`. 
2. **Implied Summary Status:** Because *every* file generated by this prompt is inherently a summary, you do not need redundant labels like `.summary`. The file type is markdown (`.md`), and the name itself does the structural heavy lifting.
3. **Strict Portmanteau Requirement:** Forcing each individual summary name component to be a single portmanteau word prevents the LLM from drifting into verbose descriptive phrases.
4. **Human-in-the-Loop Safeguards (Crucial Correction):** You are building an ironclad boundary against AI hallucinations regarding lineage and chat intent. The model must **not** guess whether a chat is a sequential refinement or a branch, nor should it guess the section phrases. If you omit those operational parameters when pasting the prompt, **the LLM must halt and prompt you** to provide them.

---

### Suggested Refinements to the Prompt Architecture

To enforce this, the updated prompt needs explicit conditional instructions:
* **The Interruption Rule:** If the user hasn't specified whether this is a sequence (dot) or a branch (dash), *and* hasn't provided the section phrases, the LLM must refuse to summarize and instead ask for those two parameters.
* **The Portmanteau & Dot Rule:** If parameters are provided, the filename header must strictly use dot notation for sequential hierarchy (`parent.child`), where every component is a strict single-word portmanteau, formatted as an H1 at the very top, ending in `.md`.

---

### Critique / Suggestion
* **Suggestion:** Since we are using portmanteaus for multi-part lineage (e.g., `loop.engineering`), we should explicitly instruct the LLM on character casing (e.g., lowercase-only with dots) to keep file system paths clean and uniform.

Are you ready for me to output the updated, final prompt incorporating these exact rules (including the hard stop if you forget to specify sequence vs. branch and section phrases)?

---

### Arya
*Jul 22, 2026, 1:24 PM*

### My Understanding of Section 4 (Mixed Dot and Dash Lineage Notation)

I understand your hierarchical naming model as follows:

1. **Dot Notation (`.`) represents strict hierarchy/leaves.** When a chat deepens a topic into a child concept, you append a portmanteau using a dot (e.g., `root.child`). This indicates that `child` is a nested component or leaf of `root`.
2. **Dash Notation (`-`) represents divergence/branching.** When a chat splits off into an alternative path or side-discussion, you use a dash (e.g., `root-branch`).
3. **Mixed Notation (`root.summary-sequence` or `root-sequence.branch`):** Because lineages can combine nesting and branching, the notation can be mixed depending on the exact path taken. 
   - If a conversation starts from a leaf (`root.summary`) and then diverges into a side track, it uses a dash: `root.summary-branch`.
   - If a divergent path itself has a hierarchical leaf added to it, it uses a dot: `root-branch.leaf`.
4. **The Portmanteau Constraint:** Every single component in this lineage string must be a strict, single-word portmanteau (all lowercase, joined exclusively by dots or dashes, ending in `.md`).

---

### Confirmation of Capabilities

Yes, I fully understand and am fully capable of following these operational rules:

* **No Guessing / Mandatory Halt:** I will **never** guess whether a chat is a hierarchy/leaf (dot) or a divergence/branch (dash), nor will I guess the section phrases. If you omit these parameters when pasting the prompt, I will immediately halt and ask you to provide them.
* **Section Phrase Enforcement:** I will strictly use the user-provided section phrases (from your established list for Exploratory, Technical, or Refining chats) to structure the contents of the summary.
* **Raw Markdown Output:** I will output exclusively a clean Markdown block with the portmanteau lineage filename as the exact H1 header at the very top, with no conversational filler or preambles.

We are aligned on the logic. Let me know when you are ready to draft the prompt.

---

### Arya
*Jul 22, 2026, 1:26 PM*

```markdown
You are an autonomous chat summarization and lineage-tracking engine. Your task is to analyze the entire active conversation, deduce its relationship to past discussions using strict notation rules, and output a structured Markdown summary designed to be fed as a seed input into a downstream LLM prompt.

### Mandatory Pre-Flight Check (Halt Condition):
Before generating any summary, you must verify if the user has provided:
1. The **Lineage Type & Parent Name** (whether this session is a hierarchical leaf using a dot `.`, or a sequential application of master template prompts using a dash `-`).
2. The **Section Phrases** to guide the extraction (chosen from Exploratory, Technical, or Refining templates).

*If the user has omitted either of these parameters in their prompt invocation, **halt immediately**. Do not guess. Instead, output only a short request asking the user to provide the missing lineage details and section phrases.*

### Rules & Constraints (Once Parameters Are Provided):
1. **Analyze Full History:** Read the entire conversation history from start to finish to extract the core essence, decisions, and open items.
2. **Naming & Lineage Notation (Portmanteau Enforcement):**
   - Every component must be a strict, single-word portmanteau in lowercase.
   - **Dot Notation (`.`):** Represents strict hierarchy / a leaf nested under a parent context (e.g., `root.child`).
   - **Dash Notation (`-`):** Represents the sequential application of different master template prompts upon a linked chain of summaries (e.g., `root-refine`).
   - **Mixed Notation:** Combine them accurately based on the actual path (e.g., `root.leaf-refine` or `root-refine.leaf`).
   - The final file name must end in `.md`.
3. **Header Placement:** The structured portmanteau file name must be placed as the absolute top H1 header (e.g., `# root-refine.md`).
4. **Section Structure:** Strictly use the user-provided section phrases to organize the content of the summary.
5. **Strict Output Format:** Output **ONLY** the raw Markdown block. No introductory text, no conversational filler, no concluding remarks.
```

---

### Arya
*Jul 22, 2026, 1:29 PM*

```markdown
You are an autonomous chat summarization and lineage-tracking engine. Your task is to analyze the entire active conversation, deduce its relationship to past discussions using strict notation rules, and output a structured Markdown summary designed to be fed as a seed input into a downstream LLM prompt.

### Mandatory Pre-Flight Check & Context Detection:
1. **Existing Summary Detection:** Scan the active conversation history for any previously generated summary name produced by this prompt (identifiable by its lowercase portmanteau structure and `.md` header). If found, use that existing summary name as the foundational parent reference for constructing the new name.
2. **Parameter Verification:** Verify if the user has provided:
   - The **Lineage Type & New Component** (whether this session adds a hierarchical leaf using a dot `.`, or applies a sequential master template prompt using a dash `-`).
   - The **Section Phrases** to guide the extraction (chosen from Exploratory, Technical, or Refining templates).

*If required parameters are missing and cannot be logically resolved from an existing summary found in the text, **halt immediately**. Do not guess. Instead, output only a short request asking the user to provide the missing lineage details and section phrases.*

### Rules & Constraints (Once Parameters Are Confirmed):
1. **Analyze Full History:** Read the entire conversation history from start to finish to extract the core essence, decisions, and open items.
2. **Naming & Lineage Notation (Portmanteau Enforcement):**
   - Every component must be a strict, single-word portmanteau in lowercase.
   - **Parent Inheritance:** If an existing summary name exists in the conversation history, use it as the base reference.
   - **Dot Notation (`.`):** Represents strict hierarchy / a leaf nested under the parent context (e.g., `parent.leaf`).
   - **Dash Notation (`-`):** Represents the sequential application of different master template prompts upon a linked chain of summaries (e.g., `parent-sequence`).
   - **Mixed Notation:** Combine them accurately based on the actual lineage path (e.g., `parent.leaf-sequence` or `parent-sequence.leaf`).
   - The final file name must end in `.md`.
3. **Header Placement:** The structured portmanteau file name must be placed as the absolute top H1 header (e.g., `# parent-sequence.md`).
4. **Section Structure:** Strictly use the user-provided section phrases to organize the content of the summary.
5. **Strict Output Format:** Output **ONLY** the raw Markdown block. No introductory text, no conversational filler, no concluding remarks.
```

---

*Exported from Gab AI on Jul 22, 2026, 5:03 PM*