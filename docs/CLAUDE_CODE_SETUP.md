# Quickstart: Claude Code — the fastest way to try peekdocs with an AI assistant

This is the **Claude Code** walkthrough. For the full MCP reference — how it works, other hosts, the available tools, and how to change which folders the assistant can search — see [User Guide → MCP server](USER_GUIDE.md#mcp-server-search-from-an-ai-assistant). For the **fully-local, fully-private** route (a downloadable model, nothing leaves your machine), see the [Local AI Assistant beginner's guide](LOCAL_AI_SETUP.md).

If you use **Claude Code** (Anthropic's terminal CLI), it is already an MCP host — so you can try peekdocs in a couple of minutes with no separate model or app to install. *(No Claude Code? Install it first, then come back.)*

> **This is the cloud path — it breaks peekdocs's fully-local privacy posture.** Claude Code (like ChatGPT, Claude Desktop, or any cloud assistant) runs the AI model on the vendor's servers, so the file snippets peekdocs returns are sent off your machine for the model to read. peekdocs itself still makes no network calls — but your **document content leaves your computer** the moment a cloud assistant reads it. That's fine for folders you don't consider sensitive, and it's the fastest way to try MCP; for anything sensitive, use the [fully-local setup](USER_GUIDE.md#fully-local-and-private-pairing-with-a-downloadable-model) instead, where nothing leaves your machine.

1. **Install the server** (once):

   ```bash
   pipx install "peekdocs[mcp] @ git+https://github.com/exbuf/peekdocs.git"
   ```

   *(Already have peekdocs? A plain `pipx install` is a no-op — see [Installing and running](USER_GUIDE.md#installing-and-running) for the `--force` reinstall that adds the `[mcp]` extra.)*

2. **Register it, fenced to one folder:**

   ```bash
   claude mcp add peekdocs -- peekdocs-mcp --root ~/Documents
   ```

   Point `--root` at the folder you want the assistant to be able to search — it can see *only* inside that folder. You'll get `Added stdio MCP server peekdocs …`.

   > **Don't run `peekdocs-mcp --root …` directly to "test" it.** It's a server, so it just sits there silently waiting for a client — that's normal, not a hang. Press Ctrl-C and let Claude Code start it for you.

3. **Open a *new* Claude Code session** — exit and run `claude` again, or open a new terminal window (MCP tools load when a session starts). Then confirm it connected:

   ```
   /mcp
   ```

   You should see **peekdocs** listed as connected.

4. **Just ask, in plain language:**

   > "Use peekdocs to search my Documents for the word *contract* and tell me which files it's in."

   Claude runs the search and answers with file names and line numbers.

**Good to know**

- **Scope:** it searches your `--root` folder and its subfolders — *not* the directory you launched Claude Code from. Ask "what folder did you search?" and it will tell you.
- **Point it elsewhere:** re-register with a different `--root` (run `claude mcp remove peekdocs` first if it says it already exists). More detail: [Changing which folders the assistant can search](USER_GUIDE.md#changing-which-folders-the-assistant-can-search).
- **Remove it:** `claude mcp remove peekdocs`.
- **Privacy:** as the note at the top of this page says, the cloud path sends your file snippets off your machine (details: [Does it keep everything on your machine?](USER_GUIDE.md#does-it-keep-everything-on-your-machine)). To keep everything local, pair peekdocs with a downloadable model instead — see [Fully local and private](USER_GUIDE.md#fully-local-and-private-pairing-with-a-downloadable-model).
