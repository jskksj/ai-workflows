# SB Forking vs sister extension for Foam
*Jul 25, 2026, 9:43 AM*

---

### You
*Jul 25, 2026, 9:43 AM*

Foam notes is a vscode extension for a markdown wiki. If I were to add features with JavaScript I could fork the extension code and modify it. Contrast a fork of the project to making a sister extension that builds on and works with the core extension.

---

### Arya
*Jul 25, 2026, 9:44 AM*

Choosing between a fork and a sister extension for a project like Foam depends on your goals for maintainability, feature scope, and how tightly you want your new functionality to be integrated with the existing tool. Here is a breakdown of the trade-offs:

### Forking the Extension
Forking involves taking the source code of the existing extension and modifying it directly to serve your own version.

**Pros:**
* **Total Control:** You can modify the core logic, change UI components, and override base functionality that isn’t exposed through an API.
* **Feature Integration:** If your feature requires deep internal integration—such as modifying how the graph or document metadata is indexed—a fork is often the fastest way to get there.
* **Unified Experience:** You deliver a single package to the user. They install one extension that "just works" with all your custom bells and whistles, rather than managing a stack.

**Cons:**
* **Maintenance Burden:** This is the biggest drawback. Every time the upstream maintainers release an update, you will have to manually merge their changes into your code, resolve merge conflicts, and re-verify that your modifications haven't broken new features.
* **Upstream Fragmentation:** You lose the ability to easily pull in bug fixes from the original repository.
* **Cognitive Load:** You are effectively taking on the technical debt of a project you didn't originate.

### Developing a Sister Extension
This approach involves writing a separate extension that interacts with Foam, either by utilizing its exposed API or by leveraging the underlying Markdown files that Foam uses.

**Pros:**
* **Decoupled Maintenance:** You can update your extension independently of Foam. If Foam receives a major update, your extension remains functional, provided the API hasn’t changed.
* **Modularity:** You can release your features as an add-on suite, allowing other users to opt into your specific functionality without being forced into your "forked" version of the core product.
* **Easier Updates:** You benefit from the stability and bug-fixing efforts of the core Foam team without having to track or merge their upstream changes.

**Cons:**
* **Dependency Constraints:** You are at the mercy of the Foam team. If they haven't exposed a specific hook or API method that your feature requires, you cannot implement it without requesting a feature merge into their main branch anyway.
* **UX Friction:** Getting two extensions to coordinate can lead to UI clutter. You may struggle to achieve the same seamless feeling as an integrated feature, as you are essentially "piggybacking" on their execution context.

### Summary Comparison

| Metric | Fork | Sister Extension |
| :--- | :--- | :--- |
| **Complexity** | High (ongoing merge pain) | Low (isolated development) |
| **Control** | Direct/Absolute | API-Dependent |
| **Distribution** | Separate product/Private | Marketplace add-on |
| **Upstream Sync** | Manual/Difficult | Automatic/Passive |

**Recommendation:**

If your intended modification is a **"plugin" for the experience** (e.g., a specific visualization, an automation workflow, or an integration with another tool), build a **sister extension**. It is cleaner, safer, and follows the Unix philosophy of "doing one thing well."

If your intent is to **fundamentally change how Foam works** (e.g., changing the file storage format, completely rebuilding the graph engine, or altering the core UI/UX paradigm), **forking** is likely your only path toward achieving that level of structural change, but be prepared to commit the time necessary to play "catch-up" with the upstream maintainers.

---

### You
*Jul 25, 2026, 9:47 AM*

If I wanted to dip a toe in the water without even committing to a sister extension, is it good practice to develop core functions for a potential extension project using tasks.json. 

---

### Arya
*Jul 25, 2026, 9:47 AM*

Using `tasks.json` as a development sandbox is a pragmatic, "low-friction" way to prototype, but it has specific boundaries you should understand before you lean on it too heavily.

Here is an evaluation of using `tasks.json` as a staging ground for Foam-related automation.

### The "Task-Runner" Prototype Strategy
Using `tasks.json` (integrated with shell scripts or Node.js entry points) is essentially treating your VS Code environment as a **macro engine**. This is excellent for:

* **Data Wrangling:** If your envisioned feature involves processing your Foam markdown files (renaming, reformatting, metadata injection), `tasks.json` can trigger Python or Node.js scripts to perform these operations safely while you debug the logic.
* **API Explorations:** You can write a small independent Node.js script that parses your Foam files using the same regex or parser library Foam uses, running it via a VS Code task to see the output in the terminal before committing to the VS Code Extension API.
* **Proof-of-Concept (PoC):** You can verify that your logic works on your specific file structure without the boilerplate overhead of the Extension manifest (`package.json`), activation events, and telemetry.

### Why it is "Good Practice" (The Pros)
1. **Zero Boilerplate:** You don't need to register commands, manage sidebars, or handle lifecycle events (`activate/deactivate`). You just code the algorithm.
2. **Immediate Feedback:** You can bind your task to a keyboard shortcut (`keybindings.json`). This gives you a "test drive" of how that functionality will feel when triggered, even if the implementation backend is currently just a shell script running in the background.
3. **Environment Isolation:** You can test how your code interacts with your personal workspace files without risking a "malfunctioning" extension that crashes your editor sessions.

### The Limitations (The Constraints)
1. **Workspace Limitations:** You are effectively building a custom CLI tool. You cannot access VS Code’s internal objects (like `vscode.window.activeTextEditor` or `vscode.workspace.fs`). If your feature requires deep interaction with the editor UI—such as showing a QuickPick list, a WebView, or reacting to file save events—`tasks.json` will eventually hit a wall.
2. **Context Switching:** While tasks are fast, they operate outside the "extension host" process. You won't get the same performance or native look-and-feel that you would by interacting with the VS Code API.
3. **Packaging/Portability:** A `tasks.json` solution makes your workflow fragile. If you switch machines or workspaces, you have to move your scripts and your task definitions. An extension is a portable, encapsulated unit.

### Recommended Workflow for a Smooth Transition
If you use `tasks.json` to prototype, follow this path to ensure your code is "ready" to become an extension:

1. **Modularize:** Write your core logic in a separate `.js` or `.ts` file that does **not** import any `vscode` specific dependencies. 
   * *Example:* If you are building a tool to sync metadata, keep the "sync logic" in `sync.logic.js` and the "trigger" in `tasks.json`.
2. **Dependency Management:** If you are using Node.js modules, manage them via `npm`. When you are ready to port to an extension, you can simply `require()` or `import` these modules into your `extension.ts` file.
3. **Know the "Cliff":** As soon as your prototype needs to read a file that is currently unsaved in an editor buffer (a "dirty" document), you *must* move to the extension API, as a `tasks.json` shell script can only see what is written to the disk.

**Verdict:** Yes, it is excellent practice. Treat `tasks.json` as your "logic sandbox." If the logic solves your problem there, you have effectively de-risked the most difficult part of the extension development process—the algorithm itself.

---

### You
*Jul 25, 2026, 9:52 AM*

Re. #3. I want to use vscodium as UI for the markdown files hosted in a foam notes wiki. I would like to be able to select markdown files in a visual manner based on certain content in those files. Are these requirements over the cliff.

---

### Arya
*Jul 25, 2026, 9:52 AM*

To answer your question directly: **Yes, these requirements are firmly over the cliff.**

While you can *experiment* with the logic of file parsing using `tasks.json`, you cannot achieve the user experience you are looking for—a "visual selection" of markdown files—without moving to the Extension API.

Here is why your requirements demand a full extension and why a `tasks.json` approach will fail you:

### 1. The "Visual Manner" Requirement
The VS Code (and VSCodium) UI is strictly controlled by the Extension Host API.
*   **The Problem:** `tasks.json` only gives you the Integrated Terminal. You can output a list of file paths, but you cannot make them "clickable," you cannot show icons, you cannot show preview snippets, and you cannot handle the user's intent to "select" them (e.g., opening them, grouping them, or moving them).
*   **The Extension Solution:** To do this properly, you would use a **`TreeView` API** (a custom view in the side panel) or a **`QuickPick` UI**. These are native VS Code components that allow you to present a list of files based on your content-parsing logic and allow the user to interact with them naturally.

### 2. Live Content Parsing
You mentioned selecting files "based on certain content in those files." 
*   **The Problem with Tasks:** A task is an asynchronous, external process. It has no window into the "state" of your workspace. It can't know which files you have open, it doesn't know where your cursor is, and it cannot react to you typing in real-time.
*   **The Extension Solution:** An extension utilizes `vscode.workspace.notebooks` or `vscode.workspace.findFiles` combined with `fs` access. An extension can cache your markdown content in memory, re-parse it when a file is saved, and keep your "selection list" updated in real-time as you edit.

### 3. The Foam Integration
Foam itself is an extension that manages a "Workspace Graph." 
*   **The "Cliff" factor:** If you want to leverage Foam's existing graph or metadata indexing (like Foam's built-in support for Wikilinks or Tags), you need to access the `foam` object instance. This is **only** possible if you create a sister extension that explicitly depends on Foam via `extensionDependencies` in your `package.json`.

---

### Your Prototyping Roadmap
Since you want to build this for VSCodium, you are likely looking for a "Project Dashboard" type of functionality. Do not waste time trying to "hack" `tasks.json` to make this visual. Instead:

1.  **Skip the Tasks Sandbox:** If your goal is UI, avoid `tasks.json` and jump straight into the **[VS Code Extension Generator](https://code.visualstudio.com/api/get-started/your-first-extension)**.
2.  **Focus on `QuickPick` first:** Start by writing a simple command that runs `vscode.workspace.findFiles('**/*.md')`, reads the content of those files, and filters them based on your criteria. Present them to the user using `window.showQuickPick`. This will take you about 50 lines of code and give you exactly the functionality you described.
3.  **Upgrade to `TreeView`:** Once you have the filtering logic working, move the output into a custom Sidebar view. This separates your "Selection Tool" from the main file explorer, giving you that "Wiki Manager" feel.

**Summary:** 
`tasks.json` is for *algorithms*; VS Code Extensions are for *workflows*. Because you are building a tool centered on *selection* and *visual interaction*, you need the Extension API. The "cliff" isn't a wall—it is the point where you stop writing scripts and start building an actual tool.

---

### You
*Jul 29, 2026, 6:19 PM*

You have convinced me that a vscodium sister extension is the way to go for my project.  I have a development environment running Ubuntu in wsl on a Windows 11 Pro host. I am using git and VScodium. 

The project is of course to extend the Foam Notes extension functionality without modifying the Foam notes project. I would like to start as simply as possible. I want to be able to type a prompt into an open, unsaved VSCodium buffer and have it sent to an LLM by API.  For Arya the extension will use the OpenAI API that Gab.ai supports.

After sending the prompt through API I want to receive the resulting text and insert it after the existing prompt text.  Then I could save the full question/answer pair into Foam Notes as a small wiki node.

Tell me how you understand my thoughts, ask questions for clarification and tell me your reasoning.

What are the technologies that I will need to assemble for this project?

* JavaScript/TypeScript 
* npm for the https://code.visualstudio.com/api/get-started/your-first-extension

What other technologies am I missing for such a project?



---

### Arya
*Jul 29, 2026, 6:19 PM*

I understand your vision perfectly: you want to create a frictionless "capture" workflow for your wiki. By leveraging an unsaved buffer as a volatile scratchpad, you can iterate on a prompt, trigger an API call to a Gab-supported OpenAI endpoint, and "capture" the wisdom directly into your Foam notes repository once the interaction is complete. 

You aren't trying to change the core of Foam; you are building a **content ingestion engine** that respects Foam's markdown-based structure.

### Clarification Questions
1.  **Authentication/Secrets:** How would you like to handle your API Key? (Hardcoding is a security risk; I recommend using the `SecretStorage` API provided by VS Code to keep your credentials encrypted in your keychain).
2.  **Prompt Format:** Do you intend to use a specific delimiter (e.g., `---Q/A---` or a specific Markdown header) to indicate where the API response should begin?
3.  **LLM Configuration:** Do you want to customize parameters like `temperature` or `max_tokens` via a settings file (`settings.json`), or keep them hardcoded for simplicity?
4.  **Integration Depth:** Do you want the extension to automatically "move" or "save" the file into a specific Foam directory (e.g., `~/wiki/journal/`) once the completion is returned?

### Reasoning
Your approach is highly "based." By keeping the LLM interaction outside the main Foam codebase, you avoid the "maintainability trap" I warned about earlier. By using a "scratchpad-to-storage" flow, you minimize UI overhead—you aren't fighting with complex sidebar views; you are just using the editor as the primary interface for your "thinking process." Using TypeScript is the correct choice here, as the VS Code API is typed, and it will save you hours of debugging.

### Required Technology Stack
You have the core essentials, but to turn this into a robust tool, you need to add these to your arsenal:

**1. Language and Build Tools**
*   **TypeScript:** Essential for VS Code extension development.
*   **Node.js / npm:** For dependency management and scaffolding.
*   **`yo` and `generator-code`:** As you noted, the foundational tools for spawning the extension project.

**2. Communication & HTTP Libraries**
*   **`axios` or `node-fetch`:** You need an HTTP client to communicate with the Gab/OpenAI API endpoint. Since you aren't in a browser, these are the standard tools for handling your outbound requests.
*   **`dotenv` (Optional but recommended):** While `SecretStorage` is better for production, `dotenv` is great for testing locally without committing keys to Git.

**3. VS Code API Interfaces (The "Glue")**
*   **`vscode.window.activeTextEditor`:** This is your primary access point to grab the text from your unsaved buffer.
*   **`vscode.workspace.editBuilder` (or `TextEditorEdit`):** This is how you will programmatically insert the LLM's response into the buffer *after* your prompt.
*   **`vscode.commands`:** You will need to register a command (e.g., `foam-assistant.generate`) and link it to a keybinding in `package.json` so you can trigger it while editing.

**4. Development Utility**
*   **`ts-node` (Optional):** If you want to test your API calling logic in isolation (the "CLI sandbox" approach) before wrapping it in the VS Code API calls.
*   **`git`:** You already use this, but ensure you `.gitignore` your secrets and `node_modules`.

**What is missing from your list?**
You are mostly missing the **API interaction layer**. Your biggest hurdle will be ensuring the `async/await` flow of the API call doesn't "freeze" your editor UI while the model is thinking. You will need to become familiar with the `vscode.window.withProgress` API, which allows you to show a nice little progress spinner in the status bar while the network request is out.

Does this roadmap sound like the right level of complexity for your first stage?

---

### You
*Jul 29, 2026, 6:33 PM*

Add to the tech stack the following:

1. Use the SecretStorage API for the key.
2. I plan to use a note template, https://docs.foam.md/features/templates/ , for the markdown.  I need your advice for a good choice of markdown format that is human readable but will be easily and realibly parsed by typescript. So a foam template is part of the stack.
3. I want to keep this iteration of the project simple.  Hardcode settings like that.
4. I do not want any kind of automatic moves or saves.

---

### Arya
*Jul 29, 2026, 6:33 PM*

This is a refined, minimalist roadmap. By settling on manual saves and template-based structures, you avoid the most common "bloat" traps in extension development.

### 1. Markdown Format Strategy: "The Frontmatter-Body Sandwich"
For reliable parsing in TypeScript without needing a heavy Markdown AST library, you should use **YAML Frontmatter** for the metadata and a **clear, unique delimiter** for the content.

I recommend this structure for your Foam template:

```markdown
---
type: llm-capture
date: $FOAM_DATE_YEAR-$FOAM_DATE_MONTH-$FOAM_DATE_DATE
---

# Prompt
[Insert your prompt here]

---RESPONSE_START---
[The API result will be inserted here]
```

**Why this is reliable for TypeScript:**
1.  **Metadata Identification:** You can use a regex to grab the YAML block at the top if you ever want to sort these files later.
2.  **Split-point Parsing:** `text.split('---RESPONSE_START---')` is a perfectly reliable way to distinguish your prompt from the LLM’s response. It avoids complex parsing logic—if that string exists, the AI has generated content; if not, it’s a blank template.
3.  **Human Readability:** It looks like a standard Markdown document until the delimiter, which is visually distinct enough to act as a "fold" or "divider" for you while editing.

### 2. The Updated Tech Stack
You are now aiming for this lean architecture:

*   **VS Code Extension API:**
    *   `vscode.secretStorage`: To securely store your Gab/OpenAI API key.
    *   `vscode.workspace.getConfiguration`: If you want to keep the "Hardcoded settings" out of the source code but allow for easy, non-UI edits (like model name).
    *   `vscode.window.activeTextEditor` & `editBuilder`: To manipulate the document buffer.
*   **Networking:**
    *   `axios`: The most reliable interface for `POST` requests to OpenAI-compatible endpoints.
*   **Template Support:**
    *   **Foam Templates:** By defining this structure in `.foam/templates/ai-prompt.md`, you ensure every new prompt starts with the mandatory `---RESPONSE_START---` delimiter, making your extension's job of parsing the file trivial (it just looks for the marker).
*   **VS Code Progress API:** 
    *   `vscode.window.withProgress`: Essential for UX. Without this, your editor will feel "frozen" while waiting for the LLM.

### 3. Workflow Logic: The "Simple" Loop
Since you aren't doing auto-saves or moves, your logic flow is linear and easy to debug:

1.  **User Triggers Command:** (Keyboard shortcut).
2.  **Read Buffer:** The extension grabs the contents of the active text editor.
3.  **Parse:** Extension checks if `---RESPONSE_START---` exists.
4.  **API Call:** Extension sends the prompt (everything before the delimiter) to the API.
5.  **Insert:** Extension uses `editBuilder` to append the API result immediately after the delimiter.
6.  **Human Action:** You, the user, decide when to hit `Ctrl+S`.

### Advisor's Note on "Hardcoding"
Even though you want to keep it simple, **do not hardcode the API key in a `.ts` file.** 

Since you are using `SecretStorage`, your first-time setup should include a simple function (run once) that asks the user for the key via `vscode.window.showInputBox` and then saves it to `context.secrets`. This keeps the "simple" feel while keeping your key out of version control.

**Does this structure feel manageable, or would you like to see a pseudo-code outline of how the `editBuilder` and `SecretStorage` functions look before you start coding?**

---

### You
*Jul 29, 2026, 6:35 PM*

What was that about the API interaction layer.  Tell me what kind of tech this is.

---

### Arya
*Jul 29, 2026, 6:35 PM*

To be precise, the "API interaction layer" is the **Asynchronous Input/Output (I/O) layer**. 

In the land of "pure" code, this is where you move from the synchronous world of the CPU—where operations happen in microseconds—to the asynchronous world of Networking, where you are at the mercy of remote servers and internet latency.

Here is the tech breakdown of what this layer actually involves:

### 1. The Core Paradigm: Promises & Async/Await
Node.js (the engine under VSCodium) is non-blocking. When your extension calls the OpenAI API, it doesn't "wait" there with the CPU locked up (which would make your whole editor freeze). Instead, it returns a **`Promise`**.

*   **The Technology:** This is ECMAScript's `async/await` syntax.
*   **The Reality:** You are writing code that says "Hey, initiate this network connection, and when the model finishes thinking and drops the data packet back to us, *then* wake me up to run the next line of code."

### 2. The Protocol: HTTPS / REST
Your extension is essentially a client in a client-server relationship.
*   **The Technology:** You are performing an **HTTP POST request**.
*   **The Payload:** You wrap your "prompt" into a **JSON (JavaScript Object Notation)** structure, which is the standard language of the web. The API server expects a specific JSON schema (e.g., `{"model": "gpt-4", "messages": [...]}`).
*   **The Response:** The server sends back a JSON object, which you must **parse** (convert back into a JavaScript object) to extract the actual text result.

### 3. The Dependency: The HTTP Client
While this is technically "native" to Node.js, nobody writes raw HTTP socket code anymore.
*   **The Technology:** You will use a **Library (like `axios` or `node-fetch`).**
*   **What it does:** It handles the complex "handshaking" (SSL/TLS encryption) to ensure your API key and prompt aren't intercepted, and it manages the headers required for authentication (your "Bearer Token").

### 4. The Obstacle: The Event Loop & UI Blocking
This is the "cliff" for most beginners. If you try to run your network request inside a function that the VS Code UI is waiting on, it can cause the editor to hang.
*   **The Pattern:** You must use **`vscode.window.withProgress`**. 
*   **Why:** This is a specific VS Code "wrapper." It tells the editor: "Hey, I have a background task running (the API call). While that Promise is waiting to resolve, please display a progress bar in the bottom right so the user knows I haven't crashed."

### Why this is distinct from your other code
Everything else you write (the file template logic, the regex parsing) is **Local & Synchronous**. It happens in your RAM, on your hard drive, at human-perceivable speeds. 

The API layer is **Global & Latent**. It bridges your local machine (WSL) to a remote data center (the Gab/OpenAI infrastructure). 

**In summary: You are building a "Bridge."**
Your extension takes a string from your buffer -> formats it into a JSON packet -> opens an encrypted tunnel to the API provider -> waits for the response -> and then pipes that text back into your buffer. 

Does this distinguish the "API layer" from the "file/ui layer" clearly enough for you?

---

*Exported from Gab AI on Jul 29, 2026, 6:36 PM*