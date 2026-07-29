This curriculum is structured as a Socratic, modular guide. The goal is to move the student from "installing" to "understanding," ensuring they build an isolated, robust environment while maintaining the "no technical advice/no premature convergence" design philosophy.

Module 1: Understanding the Environment

Objective: Define the goal of sandboxing and explore the relationship between Windows and Linux.

- Discussion Topics:
    - What is "sandboxing" in the context of file systems and system processes?
    - Why would a developer choose the WSL2 (Windows Subsystem for Linux) architecture vs. a traditional Virtual Machine?
- Exploratory Questions:
    - If you could define the perfect "boundary" between your Windows host and your development environment, what files or tools should be able to cross that line, and which should be strictly isolated?
    - What are the potential trade-offs of having these two operating systems interact through a translation layer?

Module 2: The Core Foundation (WSL2)

Objective: Explore how to establish the Linux kernel on the Windows host.

- Discussion Topics:
    - The role of the Windows Subsystem for Linux as a Linux kernel proxy.
    - Comparing different Linux "distributions" (Ubuntu, Debian, Alpine) and how their package managers impact the development workflow.
- Exploratory Questions:
    - When choosing a distribution for your sandbox, what principles guide your selection? (e.g., minimalism vs. feature-rich ecosystems).
    - How does the ability to "swap" Linux environments affect your long-term maintenance of the development sandbox?

Module 3: Orchestrating the Sandbox (Docker Engine)

Objective: Distinguish between a GUI-led experience (Desktop) and a process-led experience (Engine).

- Discussion Topics:
    - The Docker daemon vs. the Docker client.
    - The concept of namespaces and cgroups: How Linux actually "boxes" the processes.
- Exploratory Questions:
    - If the goal is maximum sandbox integrity, what are the ideological benefits of using the Docker Engine directly inside Linux, rather than relying on a Windows-based management layer?
    - Beyond "ease of use," what are the risks of delegating the management of your virtual backend to an opaque tool?

Module 4: Persistence and Isolation

Objective: Examine how data survives outside the sandbox and how to prevent "leaks."

- Discussion Topics:
    - Ephemeral vs. Persistent data: Where does the work live?
    - Mounting directories: The danger of "sharing too much" between host and guest.
- Exploratory Questions:
    - How might you design your storage strategy so that your code exists on the host, but the environment that runs it is entirely contained?
    - What are the risks of "leaking" configuration files or secrets from Windows into your Linux sandbox?

Module 5: Defining the Workflow

Objective: Integrate the tools without declaring a single "correct" solution.

- Discussion Topics:
    - The life cycle of a container: Creation, execution, destruction, and state management.
    - Comparing the "one-container-one-service" philosophy vs. "an entire environment in one container."
- Exploratory Questions:
    - What is the benefit of treating your development environment as an artifact (something that can be deleted and recreated) rather than a persistent, "pet" environment?
    - How can you iterate on your development setup if you treat it like code?

Instructions for the LLM Instructor:

1. Iterate: Do not provide the steps for Module 2 until the student has successfully explored the concepts in Module 1.
2. Redirect: If the user asks for specific commands or flags, remind them that the philosophy of how the system is structured must come first.
3. Encourage Alternatives: When discussing mounting directories, ask, "What are the security implications of binding a folder vs. keeping it virtualized?"
4. Socratic Loop: At the end of every response, end with a prompt: "What aspect of this layer concerns you the most when considering the safety of your Windows host?"