# Based on your descriptions, here's my discernment: (fork)
*Jul 29, 2026, 5:45 PM*

---

### You
*Jul 29, 2026, 5:28 PM*

I have been asking you to 'create a teaching curriculum' on a variety of subjects with great success.  I now wish to formulize your curriculum output.  I need a prompt that designs a teaching curriculum on a supplied subject. Ignore the code tutorial subjects of the following curriculums, the prompt should be agnostic and suitable for most subjects.

I have attached three files:
1. A "curriculum-phases.md" file that produces high level 'phases' containing particular details of the subject that the student will be taught.
2. A "curriculum-modules.md" file that used 'modules' with multiple levels of underlying topics for each module.
3. And finally, an "ai-pair-programming.md" file containg a prompt that actualizes the curriculum teaching methods.

Before we start do not create any new prompts. You will only tell me what you think I want and how you reasoned that out.  Can you discern which file is which by my description?

---

### Arya
*Jul 29, 2026, 5:28 PM*

I have reviewed the files you provided. Based on your descriptions and the contents of the files, I have correctly identified each as follows:

1.  **`curriculum-phases.md`**: This is indeed the file that lays out high-level developmental stages (Phases 1–6). It acts as a structural roadmap that prioritizes foundational understanding and subject-wide logic before diving into specific technical applications.
2.  **`curriculum-modules.md`**: This file is the Socratic, modular guide. It focuses on deep-dive pedagogical interaction, using exploratory questions and a "Socratic loop" to ensure the student understands the philosophy behind the tools before moving on to the next set of objectives.
3.  **`ai-pair-programming.md`**: This file contains the operational SOP (Standard Operating Procedure). It acts as the tactical execution framework—specifically the SVCP (Step-Verify-Commit-Proceed) protocol—that governs how the teaching and implementation will actually be carried out during the learning process.

**What I believe you want:**
You are looking to synthesize these three distinct approaches—**Structural Roadmap** (Phases), **Pedagogical Depth** (Modules), and **Tactical Execution** (SOP)—into a singular, unified "Master Prompt." 

**My reasoning:**
*   You are moving toward formalization. Using these files as separate components is powerful, but you clearly want to be able to supply a subject and have the AI generate an entire end-to-end learning lifecycle automatically.
*   You want the *methodological flexibility* of the current files applied to *any* subject, stripped of specific technical constraints (like the specific Rust or Docker details found in your examples).
*   By asking me to identify these first, you are ensuring I have correctly parsed the "DNA" of your preferred teaching style before we codify it into a template that controls future outputs. 

You are effectively looking to build a "Curriculum Engine" that treats the subject as the input and outputs a structured, Socratic, and strictly verified learning program.

---

### You
*Jul 29, 2026, 5:40 PM*

You have misunderstood one aspect of my desire for the new prompt. I want to maintain the "ai-pair-programming.md" files prompt as a separate object that will be included in a discussion directly after the prompt we are designing in this discussion. Do not modify or include "ai-pair-programming.md" into the new prompt.  I want the new prompt to be designed to use this SOP as a target for creating curriculums.

I want to suggest a more formal structure to the curriculum output text where each level of the curriculum is labeled for reference, like this:
"
Phase: A high over view what will be taught, a simple project may have only one phase and a more complex subject may have many phases. For example 'Phase 1: Environment Architecture'

Module: modules within each phase will contain the next level of teaching.  Within the modules are named tasks like 'Discussion Topics:' followed by the tasks that need to be learned in detail.
'Core Types: 
    - Structs, Enums, and advanced data modeling.'

You are correct about the Socratic and strictly verified content of the curriculum design.

Reiterate your understanding, reasoning and ask clarify questions.

---

### Arya
*Jul 29, 2026, 5:41 PM*

I understand. My previous assessment was slightly off-target regarding the integration of your SOP; thank you for the correction.

### My Understanding
You want a **"Curriculum Architect" prompt**. This prompt is intended to be the "Stage 0" of our interactions. Its sole purpose is to take a subject and produce a highly structured, hierarchical teaching document.

Once this document is generated, you will then introduce the `ai-pair-programming.md` SOP in a separate, subsequent move to act as the operational framework for executing that curriculum. The curriculum itself must be formatted with formal labels—specifically **Phases** (high-level grouping) containing **Modules** (sub-units), which in turn contain **Tasks** (granular learning objectives). The content must remain Socratic in nature, pushing for philosophy and foundational understanding before technical implementation.

### My Reasoning
* **Separation of Concerns:** By keeping the Curriculum Architect and the SOP separate, you ensure that the *design* of the learning path (the "What") is decoupled from the *execution* of the learning path (the "How"). This prevents the rigidity of the SVCP protocol from interfering with the architectural design phase of the curriculum.
* **Formalization:** The requested labeling structure (Phase -> Module -> Task) creates a consistent indexing system. This makes it trivial for us to reference specific parts of the curriculum during the "execution" phase (e.g., "Let's begin with Task 2 of Phase 1, Module 1").
* **Socratic Integrity:** You want the curriculum itself to maintain that "instructor" persona that asks probing, exploratory questions to ensure I (as the AI) am not just dumping facts, but building a mental model in the student.

### Clarifying Questions
To ensure the prompt I eventually design is exactly what you need, I have three questions:

1. **The "Socratic" Balance:** In the new curriculum format (Phase/Module/Task), do you want me to embed the "Exploratory Questions" directly into each Module/Task, or should they be reserved for the post-curriculum interaction when we actually start the execution phase?
2. **Phase/Module Logic:** Should the prompt explicitly instruct the AI to limit the number of phases and modules based on the complexity of the subject? For instance, should it ask the user to define the scope/level of the student before it generates the document, or should it assume a specific depth as the default?
3. **Reference Labels:** Do you want the labeling system to include a "Reference ID" for every item (e.g., `Phase 1, Module 1.1, Task A`) to simplify referencing during our pair-programming sessions?

How would you like me to handle these specific points?

---

### You
*Jul 29, 2026, 5:44 PM*

1. Embed the exploratory questions into the modules and tasks directly.
2. Ask the student to suggest his experience and ability to help focus the curriculum properly.
3. Add the suggested reference labels.

I am ready to see a suggested prompt if you are ready to create.

---

### Arya
*Jul 29, 2026, 5:44 PM*

I understand your requirements perfectly. You are looking for a "Curriculum Architect" prompt that enforces a rigorous, labeled structure while incorporating Socratic depth and participant-tailored scoping.

I have drafted the following prompt for your consideration. It is designed to be agnostic—you simply drop the subject into the bracketed space, and it performs the necessary initial assessment before outputting the structured curriculum.

***

### Proposed Curriculum Architect Prompt

**Role:** You are a Senior Pedagogical Architect. Your goal is to design a high-level, Socratic teaching curriculum for a given subject.

**Initial Assessment:**
Before generating the curriculum, first ask the user to define their current experience level and specific objectives regarding the subject. Use this input to calibrate the complexity and scope of the curriculum.

**Curriculum Structure:**
Once the user provides their background, generate a curriculum using the following strict hierarchical format. Use these labels to ensure clear referencing:

- **[PHASE #]: [Title]** (e.g., Phase 1: Foundations)
    - **[MODULE #.#]: [Title]**
        - **Objective:** (A concise statement of the module's goal)
        - **Discussion Topics:** 
            - [Task Name]: [Description]
            - [Task Name]: [Description]
        - **Exploratory Questions:** (Specific open-ended questions designed to test the learner's deeper understanding of the module's concepts.)

**Design Principles:**
1. **Socratic Focus:** Emphasize philosophy and fundamental architecture over surface-level instructions. Aim to build a mental model of the subject.
2. **Modular Granularity:** Ensure tasks are atomic and logical, preparing the user for an eventual transition into a task-based execution SOP.
3. **Reference-Ready:** Ensure every phase, module, and task is clearly labeled for future reference during pair-programming sessions.
4. **Pedagogical Pacing:** Do not provide technical implementation steps yet. Focus on the structural "Why" and "What."

**Subject to design:** [INSERT SUBJECT HERE]

***

### Does this meet your expectations?

I have designed this to act as your "Stage 0," where the AI first acts as an interviewer to assess the student's level, then follows your formal labeling and Socratic requirements. 

**Does this prompt capture the structure you envisioned, or would you like to refine the "Discussion Topics" section further to ensure the tasks remain appropriately granular?**

---

### You
*Jul 29, 2026, 5:49 PM*

I accept this prompt design.  I would now like to work on one aspect of the SOP that needs better definition.

The "Integrated AI Pair Programming Workflow (SOP)" needs to understand that when a Phase or module has been completed it must not move to the next phase or module within the current answer.  Just note that a phase or module has been completed and we are ready to move on to the next.

Other than that the Integrated AI Pair Programming Workflow (SOP) is a good start, keep it intact but produce a new version of the SOP with this new command inserted at an appropriate juncture.

---

### Arya
*Jul 29, 2026, 5:49 PM*

To ensure the SOP remains a disciplined agent of your "Step-Verify-Commit-Proceed" (SVCP) protocol, I have inserted a **"Formal Completion Gate"** at Section 7. This step forces a hard stop at the end of every Phase or Module, preventing the AI from cascading into the next section without your explicit authorization.

Here is the updated SOP:

***

### Integrated AI Pair Programming Workflow (SOP)

1. **High-Level Architecture**
   - Understanding: Foundational stage defining core features and requirements via abstract, implementation-agnostic algorithms. Remains detached from specific technologies or paradigms.

2. **Environment and Tool Selection**
   - Understanding: Evaluation of development environments and toolsets based strictly on the requirements established in Stage 1.

3. **Action Plan and Modularization**
   - Understanding: Design conversion into an action plan of atomic, small sub-projects to minimize complexity and maximize testability.

4. **Literate Programming**
   - Understanding: All code produced with explanatory comments physically adjacent to the code. The codebase serves as its own documentation.

5. **Test-Driven Development (TDD) and Composition**
   - Understanding: Strict TDD pattern: Unit tests first, followed by module composition tests.

6. **The SVCP Protocol (Step-Verify-Commit-Proceed)**
   - Sequential Reference: Every response must be numbered (e.g., Reply #01).
   - Singular Unit Focus: Strictly one logic unit at a time. No parallel development.
   - Atomic Iteration: Every implementation task must be broken down into individual communication steps. Each step must conclude with a specific Verification requirement.
   - Commitment: We do not proceed to a new step until the verification of the current step is confirmed as successful by both parties.
   - Error Resolution: If a unit encounters an error, the protocol halts until resolution and verification.

7. **Formal Completion Gate**
   - **Mandatory Halt:** Upon the successful verification and commitment of the final task in a Phase or Module, the SOP protocol enters a "Wait State."
   - **Transition Prohibition:** The AI must explicitly state: "Phase/Module [X] is successfully completed." The AI is prohibited from outputting, describing, or initiating any instructions for the subsequent Phase or Module.
   - **User Re-engagement:** The AI must wait for the user to provide an explicit command to begin the next Phase or Module.

***

### My Reasoning
By making the "Formal Completion Gate" a distinct Section (7) within the SOP, it becomes a programmatic constraint rather than a suggestion. Since you will be supplying this SOP *after* the curriculum is built, this will ensure that even when we are deep in the technical weeds of a project, the AI treats the transition between major units of the curriculum as a "check-in" point rather than an automated flow.

**Does this version of the SOP correctly enforce the discipline you require, or would you like to adjust the language of the "Transition Prohibition" to be even more restrictive?**

---

### You
*Jul 29, 2026, 5:50 PM*

Your gate looks good to me.

---

### Arya
*Jul 29, 2026, 5:50 PM*

I am pleased that the "Formal Completion Gate" aligns with your requirements. By integrating it as Section 7, we ensure that the transition between major units is not merely a courtesy, but a hard-coded procedural requirement.

We now have the two critical components of your educational framework:

1.  **The Curriculum Architect:** A design-phase prompt that interviews the student to calibrate scope, then produces a strictly labeled (Phase/Module/Task), Socratic, and pedagogically sound roadmap.
2.  **The Pair Programming SOP:** An execution-phase protocol that forces atomic iteration and, critically, halts all forward movement until you explicitly authorize the start of a new module or phase.

Together, these form a powerful, closed-loop machine for mastering new subjects. 

Since you have accepted both the new Curriculum Architect prompt and the modified SOP, we are ready for implementation. Should you want to begin, simply provide a subject, and we can launch the **Curriculum Architect** to initialize the roadmap. 

How would you like to proceed?

---

*Exported from Gab AI on Jul 29, 2026, 5:50 PM*