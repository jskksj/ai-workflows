---
##AI Pair Programming##

1. High-Level Architecture

- Understanding: This is the foundational stage where we define the core features and requirements. We will establish abstract, language-agnostic algorithms. It will remain entirely detached from low-level implementation or specific programming paradigms.
- Reasoning: You prioritized a purely logical foundation to ensure the integrity of the design before applying technical constraints.

2. Environment and Language Selection

- Understanding: We will evaluate development environments and languages based on their ability to fulfill the specific architectural requirements established in the first stage.
- Reasoning: This serves as the transition from abstract design to concrete implementation, ensuring our toolset is dictated by the architecture.

3. Action Plan and Modularization

- Understanding: We will convert the design into an action plan consisting of sub-projects. Each sub-project must be atomic, small, and optimized to minimize token usage during development and testing. We will determine if a singular language or a multi-language hybrid approach is better suited for the system.
- Reasoning: Small, atomic units ensure maintainability and high-fidelity testing, which is essential for LLM-assisted development.

4. Literate Programming

- Understanding: All code must be produced using 'Literate Programming' principles. Explanatory comments must be physically adjacent to the code they describe, ensuring the codebase functions as readable documentation.
- Reasoning: This maximizes clarity and ensures that the logic behind every snippet is transparent and easily scrutinized.

5. Test-Driven Development (TDD) and Composition

- Understanding: We will strictly follow a TDD pattern. We will generate independent unit tests first, followed by architecture composition tests to ensure that the integrated modules fulfill the high-level plan.
- Reasoning: This creates a rigorous validation loop, ensuring that every functional component is both verified individually and validated as part of the total architecture.

6. Process Protocol (New Commands)

- Sequential Reference: Every response issued in this interaction will be numbered sequentially (e.g., Reply #01, Reply #02).
- Singular Unit Focus: During the implementation and testing phases, we will focus exclusively on one unit at a time. No parallel development or discussion of multiple units will occur. If a unit encounters an error, we will remain focused on that unit until it is fully resolved before moving forward.
---