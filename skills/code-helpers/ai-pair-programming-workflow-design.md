# DESIGN AI Pair Programming Workflow Understanding
*Jul 26, 2026, 11:26 AM*

---

### You
*Jul 26, 2026, 11:26 AM*

AI assisted software development.  We each work on a given project in manner similar, but not identical to human 'pair programming'.

The first step must be to develop a high level architecture development plan that lays out the features and requirements of a software project.  This aspect of the design will never concern itself with low level implementation details.  This high level dev assessment will lay out appropriate algorithms that are language agnostic.  The assessment will never concern itself with a particular programming language paradigm.

The next step will explore a development environment and implementation language options that best fulfill the elements of the system architecture.

The next step must be to create an action plan from the preceding design document. This action plan will concern with mid level implementation details.  Will the project be a singular language. Or, will it instead be a multi-language hybrid approach. This action plan will create a list of sub-projects. Each sub-project will all ways be an atomic, small, easy to discuss, understand and test bit of code. A requirement of the action plan is that the modules minimize token use during development testing.

We must produce code using 'Literate Programming' principals where comments explain the code that the comments are adjacent to,.

We must follow a strict 'Test Driven Development' pattern. The action plan steps will be followed exactly to produce independent unit tests.  Once we have some unit test then there must be architecture composition tests.  These tests use the independent modules developed from the plan to test that the interconnected modules fulfill the development plan.

Explain your understanding of each of these paragraphs. Explain your reasoning for how you reached that understanding. Stop and wait for further instructions.

---

### Arya
*Jul 26, 2026, 11:26 AM*

I understand the workflow you have outlined for our collaborative software development. Here is my breakdown of each phase and the reasoning behind my interpretation:

### 1. High-Level Architecture
*   **Understanding:** This is the foundational stage. We will define the "What" and "Why" of the project—its core features, requirements, and the logic underpinning them—without touching code or choosing a language. The algorithms must be defined in pure, abstract, language-agnostic logic.
*   **Reasoning:** You explicitly forbade low-level implementation details and language paradigms. This indicates a desire to ensure the structural integrity of the project from a purely logical perspective before applying technical constraints.

### 2. Environment and Language Selection
*   **Understanding:** Once the abstract architecture is sound, we evaluate our options for the "Where" and "How." We will analyze development environments and programming languages based on their objective suitability for the architectural requirements we established in step one.
*   **Reasoning:** Since this follows the architecture plan, it serves as the bridge between abstract design and concrete execution. It implies that the *nature* of the architecture should dictate the tools used, not the other way around.

### 3. Action Plan and Modularization
*   **Understanding:** This is the project management layer. We will convert the design into a series of atomic, testable, and manageable sub-projects. These units must be small enough to be easily comprehended and must be designed to be token-efficient for testing and iterative development. We must also decide if the architecture is better served by a monolithic language or a polyglot approach.
*   **Reasoning:** By specifying "atomic" and "small," you are prioritizing maintainability, debuggability, and cost-efficient interaction with an LLM.

### 4. Literate Programming
*   **Understanding:** All code generation must be documented so that the explanation is physically adjacent to the code it describes. The final output should be a coherent document where the code is presented as a narrative of logic.
*   **Reasoning:** This minimizes the cognitive load required to understand the codebase. It treats code as a form of literature intended for human (or AI) comprehension, rather than just machine execution.

### 5. Test-Driven Development (TDD) and Composition
*   **Understanding:** We will write tests before any functional code. We move from individual units (unit tests) to how those units integrate (composition tests) to verify that the final whole complies with the original architectural vision. 
*   **Reasoning:** This is a rigorous approach to ensuring that every line of code serves a purpose defined in the requirements, preventing "feature creep" and ensuring that architectural bugs are caught early through empirical validation.

I am ready to proceed. Please provide the details of the software project you wish to initiate.

---

### You
*Jul 26, 2026, 11:32 AM*

Do not proceed with any development yet. I want to add some details to your reply. At every stage of this process all replies to queries or questions must be numbered sequentially for future reference.
- Reply #01, Reply #02 etc.

Once we have reached the test and implementation stage, we will always focus on exactly one small unit at a time.  In no case will multiple units be discussed in parallel or in the same discussion. If there are problems with a unit of code will stay entirely focused on resolving those problems before moving on.

Repeat the details in your first reply and add these new commands where you think they best fit for review.  Do not start any software design discussions

---

### Arya
*Jul 26, 2026, 11:33 AM*

Reply #01

I have updated my understanding of our collaborative workflow to include your requirements for strict sequencing, atomicity in development, and clear reference tracking. Here is the revised framework for our process:

### 1. High-Level Architecture
*   **Understanding:** This is the foundational stage where we define the core features and requirements. We will establish abstract, language-agnostic algorithms. It will remain entirely detached from low-level implementation or specific programming paradigms.
*   **Reasoning:** You prioritized a purely logical foundation to ensure the integrity of the design before applying technical constraints.

### 2. Environment and Language Selection
*   **Understanding:** We will evaluate development environments and languages based on their ability to fulfill the specific architectural requirements established in the first stage.
*   **Reasoning:** This serves as the transition from abstract design to concrete implementation, ensuring our toolset is dictated by the architecture.

### 3. Action Plan and Modularization
*   **Understanding:** We will convert the design into an action plan consisting of sub-projects. Each sub-project must be atomic, small, and optimized to minimize token usage during development and testing. We will determine if a singular language or a multi-language hybrid approach is better suited for the system.
*   **Reasoning:** Small, atomic units ensure maintainability and high-fidelity testing, which is essential for LLM-assisted development.

### 4. Literate Programming
*   **Understanding:** All code must be produced using 'Literate Programming' principles. Explanatory comments must be physically adjacent to the code they describe, ensuring the codebase functions as readable documentation.
*   **Reasoning:** This maximizes clarity and ensures that the logic behind every snippet is transparent and easily scrutinized.

### 5. Test-Driven Development (TDD) and Composition
*   **Understanding:** We will strictly follow a TDD pattern. We will generate independent unit tests first, followed by architecture composition tests to ensure that the integrated modules fulfill the high-level plan.
*   **Reasoning:** This creates a rigorous validation loop, ensuring that every functional component is both verified individually and validated as part of the total architecture.

### 6. Process Protocol (New Commands)
*   **Sequential Reference:** Every response issued in this interaction will be numbered sequentially (e.g., Reply #01, Reply #02).
*   **Singular Unit Focus:** During the implementation and testing phases, we will focus exclusively on one unit at a time. No parallel development or discussion of multiple units will occur. If a unit encounters an error, we will remain focused on that unit until it is fully resolved before moving forward.

I have incorporated these instructions into our standard operating procedure. I am standing by for your next instruction.

---

*Exported from Gab AI on Jul 26, 2026, 5:16 PM*