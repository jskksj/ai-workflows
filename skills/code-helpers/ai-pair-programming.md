## Integrated AI Pair Programming Workflow (SOP) ##
```
1. High-Level Architecture
- Understanding: Foundational stage defining core features and requirements via abstract, language-agnostic algorithms. Remains detached from implementation specificities.
- Reasoning: Ensures design integrity before technical constraints are applied.

2. Environment and Language Selection
- Understanding: Evaluation of tools based strictly on the requirements established in Stage 1.
- Reasoning: Ensures tools remain servants to the architecture, not the drivers.

3. Action Plan and Modularization
- Understanding: Design conversion into an action plan of atomic, small sub-projects to minimize token usage and maximize testability.
- Reasoning: Atomic units allow for the "Step-Verify-Commit-Proceed" loop to be applied effectively, preventing technical debt.

4. Literate Programming
- Understanding: All code produced with explanatory comments physically adjacent to the code. The codebase serves as its own documentation.
- Reasoning: Maximizes transparency and ensures the logic is immediately auditable.

5. Test-Driven Development (TDD) and Composition
- Understanding: Strict TDD pattern: Unit tests first, followed by module composition tests.
- Reasoning: Creates a rigorous validation loop that verifies individual units and total system health.

6. The SVCP Protocol (Step-Verify-Commit-Proceed)
- Sequential Reference: Every response must be numbered (e.g., Reply #01).
- Singular Unit Focus: Strictly one logic unit at a time. No parallel development.
- Atomic Iteration: Every implementation task must be broken down into individual communication steps. Each step must conclude with a specific Verification requirement (e.g., git status, cargo check, or specific test output).
- Commitment: We do not proceed to a new step until the verification of the current step is confirmed as successful by both parties.
- Error Resolution: If a unit encounters an error, the protocol halts. We remain focused on that specific unit until the error is resolved, verified, and committed.
```