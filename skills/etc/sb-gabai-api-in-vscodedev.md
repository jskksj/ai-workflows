# SB Gab.ai API in vscode.dev
*Jul 24, 2026, 1:46 PM*

---

### You
*Jul 24, 2026, 1:46 PM*

I would like you to teach me how to use the gab.ai openai API to send and receive text from within vscode.dev. I don't know JavaScript.

---

### Arya
*Jul 24, 2026, 1:46 PM*

To use the Gab AI API within VS Code for the web (vscode.dev), you can use an extension that supports generic OpenAI-compatible API setups. Since you don't know JavaScript, the easiest way is to use a pre-built extension that allows you to configure a custom API endpoint.

### Step 1: Get your API Credentials
First, you need your API key and the base URL.
1. Log in to your account at [https://gab.ai](https://gab.ai).
2. Go to your settings to create or retrieve your **API Key**.
3. The base URL for the Gab AI API is `https://api.gab.ai/v1`.

### Step 2: Install a VS Code Extension
Since you are using `vscode.dev`, you need an extension that allows you to point to a custom API URL.
1. Open the **Extensions** view in your sidebar (`Ctrl+Shift+X`).
2. Search for an extension like **"CodeGPT"** or **"Continue"**. These are popular extensions that allow you to use your own API keys.
3. Install the extension.

### Step 3: Configure the Extension
Once installed, open the extension settings (usually found in the sidebar or via the command palette `Ctrl+Shift+P`):
1. **Provider/Base URL:** Set this to `https://api.gab.ai/v1`.
2. **API Key:** Paste the API key you generated from your Gab AI dashboard.
3. **Model:** Select a supported model as listed at [https://gab.ai/docs](https://gab.ai/docs). If the extension asks for a specific "Model ID" (like `gpt-4o` or `claude-3-5-sonnet`), ensure it matches a name supported on the Gab AI platform.

### Important Notes
* **Documentation:** For the most up-to-date information on endpoints and requirements, always refer to [https://gab.ai/docs](https://gab.ai/docs). 
* **Credits:** Using the API will consume credits based on your usage. Ensure you have an active balance, as API usage is separate from the chat interface.
* **Compatibility:** Because `vscode.dev` runs in the browser, some extensions may have limitations compared to the full desktop version of VS Code. If an extension fails to connect, ensure your browser isn't blocking the requests and that your API key is correctly entered.

If you encounter specific configuration errors while trying to connect, please email `support@gab.ai` with the name of the extension you are using and the error message you receive.

---

### You
*Jul 24, 2026, 1:55 PM*

List the vscodium compatible extensions that will open an API connection.

---

### Arya
*Jul 24, 2026, 1:55 PM*

To connect to an API within VSCodium, you should look for extensions that act as "Language Model Providers." These allow you to plug in a "Base URL" (the API endpoint) and an "API Key" to use custom models directly in your editor.

Here are the most reliable VSCodium-compatible extensions for this purpose:

### 1. Continue
Continue is the gold standard for open-source AI in VS Code/VSCodium. It is highly configurable and supports OpenAI-compatible endpoints natively.
*   **Best for:** Developers who want deep integration.
*   **Setup:** Once installed, it will create a `config.json` folder in your user directory. You can add your provider by specifying the `openai` type and setting your `apiKey` and `apiBase` to your desired custom URL.

### 2. Copilot Custom Models Endpoint (by keklick1337)
This extension is specifically designed to register a Language Model Chat Provider for GitHub Copilot Chat (or equivalent interfaces).
*   **Best for:** Using custom API endpoints as "native" models in the sidebar chat.
*   **Setup:** It provides a dedicated "Custom Copilot" view in the activity bar where you can click to add a provider, input your API Base URL, and set the API key.

### 3. OAIProxy
OAIProxy is a lightweight extension designed to bridge external providers into the editor's native chat interface.
*   **Best for:** A streamlined "set it and forget it" experience.
*   **Setup:** After installing, you configure the `oaicopilot.baseUrl` in the VSCodium settings menu, select the "OAIProxy" provider in the chat model picker, and input your API key.

### 4. vscode-openai
This is a straightforward extension that handles BYOK (Bring Your Own Key) scenarios well for vanilla OpenAI and compatible services.
*   **Best for:** Users who want a balance between GUI configuration and functionality.
*   **Setup:** You can configure the `Base URL` and `API Key` directly through the extension's settings page or the quick-pick command menu.

### 5. OpenCodeCommit
While focused on git workflows, this extension provides a robust way to link various API backends, including custom OpenAI-compatible endpoints, for tasks like commit generation and code analysis.
*   **Best for:** Users who want AI integrated specifically into their git and workflow processes.
*   **Setup:** Configuration is managed through a `config.toml` file, which is synced to the VSCodium settings.

### Summary Recommendation for Your Goal
If you do not want to touch code or JSON configuration files, **Copilot Custom Models Endpoint** or **OAIProxy** are your best options. They prioritize a GUI-based setup where you simply paste the URL and key into a settings menu.

As of today, AD 2026, ensure you are running a recent version of VSCodium (1.107.0 or higher), as many of these extensions rely on the updated Language Model Chat Provider API introduced in recent iterations of the platform.

---

### You
*Jul 24, 2026, 1:57 PM*

I will want to pass text from a markdown file and pass it to gab.ai. And then I want to put the reply text back into the same file.

---

### Arya
*Jul 24, 2026, 1:58 PM*

To achieve this workflow, you need an extension that features **"Selection-based"** or **"Command-based"** AI interaction. Since you want to process text within a Markdown file and replace it with the AI's response without knowing how to code, here is the most effective approach using the extensions mentioned previously.

### The Recommended Workflow (using "Continue")

The **Continue** extension is highly recommended because it supports a feature called "Slash Commands." You can define a command that tells the AI to operate on your selected text.

1.  **Select Text:** Open your Markdown file in VSCodium. Highlight the text you want the AI to process.
2.  **Invoke the AI:** Use the shortcut `Ctrl+L` (or the sidebar) to open the chat window. 
3.  **Command to Replace:** In many of these extensions, once the text is selected, you can type a prompt like: *"Edit the provided text and replace the selection with the improved version."*
4.  **Insert/Replace:** Most modern editor AI extensions include a "thumbs up" or "Insert" button next to the response. Clicking this will overwrite the highlighted section with the AI's output.

### Using "vscode-openai" for Document Processing

The **vscode-openai** extension is arguably the most straightforward for "File-to-API" tasks:

1.  **Highlight your Markdown text.**
2.  **Use the Command Palette:** Press `Ctrl+Shift+P`.
3.  **Search for:** `OpenAI: Send Request`. (There is usually a command titled "Ask OpenAI" or "Send Selection to OpenAI").
4.  **Process:** The extension will send your highlighted text to the Gab AI API (using the endpoint you configured).
5.  **Inject Result:** Once the response returns, the extension will offer a "Diff View" or an "Insert" button to replace your current selection with the API’s answer.

### Configuration Checklist for Success

To make sure this works seamlessly:

*   **Endpoint Settings:** In the extension's settings, ensure the **Base URL** is set to `https://api.gab.ai/v1`.
*   **Model Selection:** When in the chat or prompt box, look for the model dropdown menu. Ensure it is set to a "Text/Reasoning" model from the Gab AI catalog.
*   **Context:** Because you are working with Markdown files, remember that long files or large selections consume more credits due to the "context window" (the AI has to re-read everything sent to it to maintain the flow). If your Markdown file grows very large, try to select only the specific paragraph or section you need to edit to save on credit usage.

### Troubleshooting Tips
*   **If the connection fails:** Check that you have an active internet connection and that the API key in your extension settings does not have any accidental spaces at the beginning or end.
*   **If the response is blank:** Your current "Max Tokens" setting in the extension might be too low. Increase the "Max Tokens" or "Output Length" in the extension’s settings to allow for a longer response.
*   **Support:** If you find that the extension is not correctly parsing the "replace" action, check the extension’s specific documentation at [https://gab.ai/docs](https://gab.ai/docs), or contact `support@gab.ai` if you believe the issue is related to how the Gab AI API is interacting with your specific environment.

---

*Exported from Gab AI on Jul 30, 2026, 1:44 PM*