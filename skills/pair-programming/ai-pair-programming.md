Integrated AI Pair Programming Workflow (SOP)

1. High-Level Architecture
  - Understanding: Foundational stage defining core features and requirements via abstract, implementation-agnostic algorithms. Remains detached from specific technologies or paradigms.

2. Environment and Tool Selection
  - Understanding: Evaluation of development environments and toolsets based strictly on the requirements established in Stage 1.

3. Action Plan and Modularization
  - Understanding: Design conversion into an action plan of atomic, small sub-projects to minimize complexity and maximize testability.

4. Literate Programming
  - Understanding: All code produced with explanatory comments physically adjacent to the code. The codebase serves as its own documentation.

5. Test-Driven Development (TDD) and Composition
  - Understanding: Strict TDD pattern: Unit tests first, followed by module composition tests.

6. The SVCP Protocol (Step-Verify-Commit-Proceed)
  - Sequential Reference: Every response must be numbered (e.g., Reply #01).
  - Singular Unit Focus: Strictly one logic unit at a time. No parallel development.
  - Atomic Iteration: Every implementation task must be broken down into individual communication steps. Each step must conclude with a specific Verification requirement.
  - Commitment: We do not proceed to a new step until the verification of the current step is confirmed as successful by both parties.
  - Error Resolution: If a unit encounters an error, the protocol halts until resolution and verification.

7. Formal Completion Gate
  - Mandatory Halt: Upon the successful verification and commitment of the final task in a Phase or Module, the SOP protocol enters a "Wait State."
  - Transition Prohibition: The AI must explicitly state: "Phase/Module [X] is successfully completed." The AI is prohibited from outputting, describing, or initiating any instructions for the subsequent Phase or Module.
  - User Re-engagement: The AI must wait for the user to provide an explicit command to begin the next Phase or Module.