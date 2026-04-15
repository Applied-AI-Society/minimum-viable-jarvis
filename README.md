# Minimum Viable Jarvis

Your personal AI-operated business OS. Spin up your own private copy from this template, open it, and start talking. By the end of your first session, you will have an AI system that knows who you are and a plan for the thing that matters most to you right now.

## What This Is

A structured workspace of plain markdown files that gives you AI-augmented recall, strategic clarity, and compounding context. Your AI agent (Claude Code, Hermes, Codex, or any harness) reads these files and operates from them. Every conversation makes the system smarter.

This is not a chatbot. This is a persistent memory system that compounds over time. Think Iron Man's Jarvis: it knows your goals, your relationships, your projects, your decisions. And it gets better every day you use it.

## Quick Start

1. Install the prerequisites: [Node.js](https://nodejs.org), [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (`npm install -g @anthropic-ai/claude-code`), [VS Code](https://code.visualstudio.com) (then open it and run "Shell Command: Install 'code' command in PATH" from the command palette so the `code` CLI works), and [GitHub CLI](https://cli.github.com) (`brew install gh` on Mac). The GitHub CLI is required for the built-in sync script.
   - **If `claude --version` fails after install:** Claude Code is installed but not on your PATH. Add it to your shell config (Mac / Linux):
     ```bash
     echo 'export PATH="$HOME/.claude/local:$PATH"' >> ~/.zshrc
     source ~/.zshrc
     ```
     (Use `~/.bashrc` instead of `~/.zshrc` if you are on bash.) Open a new terminal and `claude --version` should work.
2. Sign in to GitHub from the CLI: `gh auth login`. Follow the prompts (choose HTTPS and authenticate via browser for the smoothest path).
3. Create a `github-repos` folder in your home directory to keep all your repos in one predictable place: `mkdir -p ~/github-repos && cd ~/github-repos`
4. Get your own private copy. This repo is a **GitHub template**, so creating yours is one click:
   - Visit [github.com/Applied-AI-Society/minimum-viable-jarvis](https://github.com/Applied-AI-Society/minimum-viable-jarvis)
   - Click **"Use this template"** → **"Create a new repository"**
   - Name it `minimum-viable-jarvis` (or whatever you prefer), set visibility to **Private**, click Create
   - Clone your new private repo locally:
     ```bash
     cd ~/github-repos
     gh repo clone YOUR-USERNAME/minimum-viable-jarvis
     cd minimum-viable-jarvis
     ```
5. Open in VS Code: `cd ~/github-repos && code minimum-viable-jarvis`
6. Open the terminal (Terminal > New Terminal) and run: `claude`
7. Your Jarvis will walk you through the rest. On your first session, it runs the **onboard** skill automatically: imports your existing AI history, builds your profile, and interviews you about your most important blocker.
8. Turn on hourly auto-sync so your work is backed up to GitHub: `bash scripts/install-sync-cron.sh`

> **Pulling future updates from the template:** The MVJ template gets better over time (new skills, updated scripts). When you want the latest, just say to your Jarvis: *"sync with upstream"*. It will pull the new goodies from `Applied-AI-Society/minimum-viable-jarvis` without touching your personal files. See the [sync-with-upstream](skills/sync-with-upstream/SKILL.md) skill for details. You cannot accidentally push to the upstream template: you are not a collaborator on that repo, and the skill configures your local remote with a disabled push URL as a second safety net.

## Folder Structure

```
minimum-viable-jarvis/
├── CLAUDE.md                    # Points to AGENTS.md (Claude Code reads this first)
├── AGENTS.md                    # Full operating instructions for any AI agent
├── README.md                    # You are here
├── user/                        # Everything about you
│   └── USER.md                  # Your profile (created on first session)
├── people/                      # One file per person in your life
├── artifacts/                   # Strategic documents, plans, decisions
├── meeting-transcripts/         # Processed transcripts from meetings
├── scripts/                     # Workspace automation
│   ├── sync.sh                  # Commit local changes, pull + push to GitHub
│   └── install-sync-cron.sh     # Register hourly sync as a cron job
└── skills/                      # Skill files that define repeatable workflows
    ├── onboard/                 # First-session onboarding flow
    ├── create-user-profile/     # Build or update your user profile
    ├── think-through-it/        # Interview on your most important blocker
    ├── process-braindump/       # Route unstructured input to the right files
    ├── prep-for-meeting/        # Generate meeting prep briefs
    ├── process-transcript/      # Extract insights from meeting transcripts
    ├── create-skill/            # Create new skills through interview
    └── sync-with-upstream/      # Pull updates from the MVJ template
```

### user/

Everything your Jarvis needs to know about you. The core file is `USER.md`, which captures your identity, values, decision-making style, current situation, and goals. Created automatically on your first session.

You can add anything here: a `voice-profile.md` for your writing style, exported ChatGPT/Claude conversation history, strategic documents, anything. The more your Jarvis knows about you, the more useful it is.

### people/

One markdown file per person. Name, role, how you met, what you are working on together, interaction history, personal details. Your Jarvis uses these to brief you before meetings, remember commitments, and maintain relationship context you would otherwise forget.

### artifacts/

Your strategic documents. Plans, decision records, principles, status updates, proposals. Date-prefixed: `YYYY-MM-DD-descriptive-slug.md`. These are the outputs of your strategic thinking sessions.

### meeting-transcripts/

Processed meeting notes. Drop a raw transcript (from Granola, Otter, voice memo, or manual notes) and your Jarvis extracts attendees, decisions, action items, and updates the relevant people files.

### skills/

Skill files are plain-English SOPs for your AI agent. Each one describes a repeatable workflow step by step. Your Jarvis reads them and follows them. You build new skills over time as you discover patterns in your work.

## Built-In Skills

| Skill | What It Does | How to Trigger |
|-------|-------------|----------------|
| **onboard** | Full first-session setup: import AI history, build profile, strategic interview | Runs automatically if no USER.md exists |
| **create-user-profile** | Interview to build or update your profile | "Create my profile" or "Update my profile" |
| **think-through-it** | Strategic interview on whatever you are most stuck on | "Help me think through something" or "I'm stuck" |
| **process-braindump** | Route a brain dump to the correct files | Paste any unstructured text or voice transcript |
| **prep-for-meeting** | Meeting prep brief from your relationship files | "Prep me for my meeting with Sarah" |
| **process-transcript** | Extract everything from a meeting transcript | "Process this transcript" or paste a transcript |
| **create-skill** | Interview you to create a new skill file | "Create a skill for X" or "I want a workflow for X" |
| **sync-with-upstream** | Pull the latest template updates (new skills, scripts, README) without touching your personal files | "Sync with upstream" or "Pull template updates" |

## How It Works

**First session:** Your Jarvis runs the onboard skill. It asks you to import any existing AI conversation history (ChatGPT, Claude exports, docs about yourself), synthesizes a profile, then interviews you about the thing that matters most right now. You walk away with `user/USER.md` and an actionable plan in `artifacts/`.

**Every session after:** Open your workspace. Talk to your Jarvis. Brain dump what is on your mind (use voice-to-text for speed). Your Jarvis routes the information to the right files. Over time, your `people/` folder fills with relationship context, your `artifacts/` folder fills with strategic documents, and your Jarvis gets smarter about you and your operation.

**The compound effect:** At 30 days, your Jarvis knows your top 20 relationships, your strategic priorities, and your decision-making patterns. At 90 days, it can brief you before any meeting, draft in your voice, and catch things you would miss. The system does not plateau. It compounds.

## The Philosophy

**The truth in your head is not the truth.** Not operationally. Not for AI. Not for your team. If it only lives in your head, it might as well not exist. It is unsearchable, unshared, and inaccessible to your AI.

**You are the bottleneck.** Not the tools, not the models. Your strategic thinking, your clarity of communication, and your willingness to document what you know. This system helps you get what is inside your head into files that compound.

**Sovereignty matters.** Everything in this system is plain markdown files on your computer. No vendor lock-in. No subscription required to access your own data. If a better AI tool comes out tomorrow, point it at the same folder and keep going.

## Keeping Your Workspace Synced

Once you push your workspace to GitHub, you want it to stay synced automatically so nothing is ever lost and so any machine (or collaborator you invite) is up to date. The starter repo ships with a small sync script and a one-liner to install it as an hourly cron:

```bash
# one-time
bash scripts/install-sync-cron.sh
```

That registers a cron entry that runs `scripts/sync.sh` every hour. The script commits anything new, rebases against the remote, and pushes. Output is appended to `.jarvis-sync.log` (ignored by git).

Prerequisites: `gh auth login` must be complete (so pushes work without prompting). Remove the cron later with:

```bash
crontab -l | grep -v scripts/sync.sh | crontab -
```

## Harness Compatibility

This workspace works with any AI harness that can read files:

- **Claude Code** (reads `CLAUDE.md` automatically)
- **Hermes** (reads `AGENTS.md`)
- **Codex** (reads `AGENTS.md`)
- **Cursor, OpenCode, Aider** (point them at the workspace)

The `CLAUDE.md` file points to `AGENTS.md`, which contains the full operating instructions. Any harness that reads either file gets the same behavior.

## Full Tutorial

For the complete walkthrough with installation help, conceptual framing, and exercises:

**[The Supersuit Up Workshop](https://docs.appliedaisociety.org/docs/workshops/supersuit-up)**

## Community

- **[Applied AI Society](https://appliedaisociety.org)**: The community behind this project
- **[Discord](https://discord.gg/K7uWJBMFaN)**: Ask questions, share what you built, get help
- **[Public Docs](https://docs.appliedaisociety.org)**: Concepts, playbooks, and frameworks for the applied AI economy

## Contributing

This is an open-source starter repo. If you build a skill that others could use, submit a PR. If you find a bug or have a suggestion, open an issue. The system gets better when people share what they learn.

## License

MIT
