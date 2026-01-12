---
layout: post
subtitle: An npm package to instantly install AI agents and prompts into your development projects
title: "Introducing prompt-library CLI: Making AI Assistants More Accessible"
date: 2026-01-12 08:00:00 -0400
categories: [Artificial Intelligence, Software Engineering, Developer Tools]
tags: [Artificial Intelligence, Prompt Engineering, Developer Tools, npm, Node.js, CLI Tools, Productivity]
comments: true
social-share: true
thumbnail-img: /assets/img/prompt-library-introduction.png
thumbnail-dimensions: "width: 600px; max-width: 100%; height: auto;"
---

![prompt-library CLI introduction](/assets/img/prompt-library-introduction.png)

## Introduction

A few months ago, I shared my [personal prompt library](https://shawnewallace.com/2025-11-19-building-a-personal-prompt-library/) - a curated collection of AI assistant prompts, agents, and configurations organized by development scenario. While the library solved the problem of prompt reuse and organization, I quickly discovered a new friction point: the manual setup process. Developers had to navigate GitHub, copy files, and manually configure their projects to use the agents and prompts. Today, I'm releasing **prompt-library CLI** - an npm package that makes installing and managing AI assistants as simple as `npm install`.

## The Problem: Installation Friction

The original prompt library required several manual steps:

1. Navigate to the GitHub repository
2. Browse through folders to find relevant agents or prompts
3. Copy file contents
4. Determine the correct installation location (`.claude/` vs `.github/`)
5. Paste and save files
6. Repeat for each item you wanted to install

For a single agent, this might take 2-3 minutes. For a full scenario with multiple agents and prompts, it could easily consume 10-15 minutes. More importantly, this manual process created barriers:

- **Team onboarding**: Getting new team members set up with the same AI assistants was time-consuming
- **Multi-project consistency**: Installing the same set of agents across multiple projects was tedious
- **Updates**: Keeping agents up-to-date required manually checking for changes
- **Discovery**: Finding which agents existed required browsing through repository folders

## The Solution: A Simple CLI

The `prompt-library` CLI transforms the installation experience from a multi-step manual process into a simple command:

```bash
npm install -g @shawnwallace/prompt-library
prompt-library init
```

The interactive wizard handles setup. Your project has AI agents ready in seconds.

### Key Features

#### Quick Setup
The interactive `init` wizard walks you through:
- Selecting your AI tool (Claude Code, GitHub Copilot, or both)
- Choosing a scenario template or custom selection
- Picking specific agents and prompts
- Automatic installation to the correct directories

#### Fuzzy Search
Find items by partial name matching:

```bash
prompt-library add clarity    # Finds "clarity-editor" agent
prompt-library add arch       # Finds "archy" architect agent
```

#### Scenario Bundles
Install pre-configured sets for specific workflows:

```bash
prompt-library add dotnet-clean-architecture
```

This installs Sharp (.NET expert), Archy (architect), and the ADR prompt - everything you need for a .NET Clean Architecture project.

#### Multi-Tool Support
Works seamlessly with both Claude Code and GitHub Copilot, automatically installing to the correct directory structure:

- **Claude Code**: `.claude/agents/` and `.claude/prompts/`
- **GitHub Copilot**: `.github/agents/` and `.github/prompts/`

#### Installation Tracking
Creates a `.prompt-library.json` file in your project to track what's installed, including versions and file hashes for future update detection.

#### Smart Defaults
The CLI auto-detects your setup and provides sensible defaults, making the experience smooth even for first-time users.

## Quick Start

### Installation

**Option 1: Global Installation (Recommended)**

```bash
npm install -g @shawnwallace/prompt-library
prompt-library --version
```

**Option 2: Use with npx (No Installation)**

```bash
npx @shawnwallace/prompt-library init
```

### Basic Usage

**Interactive Setup:**

```bash
cd /path/to/your/project
prompt-library init
```

**List Available Items:**

```bash
prompt-library list              # Show all
prompt-library list --agents     # Agents only
prompt-library list --scenarios  # Scenarios only
prompt-library list --installed  # What's installed
```

**Add Specific Items:**

```bash
prompt-library add hemingway           # Writing clarity editor
prompt-library add archy               # Architecture planner
prompt-library add dotnet-clean-architecture  # .NET scenario
```

**Preview Before Installing:**

```bash
prompt-library add hemingway --dry-run
prompt-library init --dry-run
```

## Available Content

### Agents

The CLI provides access to specialized AI agents:

| Agent | Description |
|-------|-------------|
| **Hemingway** | Writing clarity editor using Orwell principles |
| **Archy** | Architect and strategic planning assistant |
| **Chester** | Code reviewer for standards and best practices |
| **Sharp** | Expert .NET software engineer |
| **Percy** | Strategic planning and architecture assistant |
| **Apex** | API architect specialized in resilience patterns |

### Prompts

Ready-to-use prompt templates:

| Prompt | Description |
|--------|-------------|
| **Writing Clarity Review** | Review text using Orwell's six rules |
| **Architectural Decision Record** | Create structured ADR documents |
| **README Generator** | Create comprehensive README files |
| **Client Discovery** | Extract details from meeting notes |

### Scenario Bundles

Pre-configured sets for specific workflows:

| Scenario | Description | Includes |
|----------|-------------|----------|
| **dotnet-clean-architecture** | .NET with Clean Architecture & DDD | Sharp, Archy, ADR prompt |
| **python-data-science** | Data science and ML projects | Percy, README prompt |
| **typescript-frontend** | React/Vue/Angular TypeScript apps | Archy, Chester, README |
| **devops-infrastructure** | IaC and CI/CD | Archy |

## Technical Implementation

I built the CLI with Node.js and these key technologies:

- **Commander.js**: Command-line interface framework
- **Inquirer.js**: Interactive prompts and wizards
- **Axios**: Fetching agent files from GitHub
- **Chalk & Ora**: Beautiful terminal output with spinners
- **fs-extra**: Enhanced file system operations

### Architecture Highlights

The tool follows a clean architecture:

```
cli/
├── bin/               # Executable entry point
├── src/
│   ├── commands/      # Command implementations (init, list, add)
│   ├── core/          # Core utilities (fetcher, installer, registry)
│   ├── utils/         # Helper utilities (logger)
│   └── constants.js   # Configuration
└── .prompt-library/
    └── registry.json  # Item catalog
```

**Key Design Decisions:**

1. **Project-Local Installation**: Agents install to your project directory, not globally, ensuring team consistency
2. **Git-Friendly**: All installed files are plain markdown, easy to version control
3. **Atomic Operations**: Installation tracking prevents partial installations
4. **Dry-Run Mode**: Preview changes before committing
5. **Fuzzy Matching**: Forgiving search to find items quickly

## Lessons Learned

Building the CLI reinforced several important principles:

### 1. Reduce Friction to Drive Adoption

Even a well-designed library won't be used if the setup process is painful. The CLI reduced the barrier to entry from "I'll set this up later" to "Let me try this now."

### 2. Interactive Beats Declarative for Initial Setup

While declarative configuration (like a config file) works well for experienced users, an interactive wizard is more approachable for first-time setup. The CLI uses `inquirer.js` to create a conversational experience.

### 3. Preview Mode Builds Trust

The `--dry-run` flag was a late addition but has become essential. Being able to preview what will happen before it happens builds user confidence.

### 4. Fuzzy Matching Saves Time

Users rarely remember exact names. Fuzzy matching means "hemingway", "clarity", or "writing" all find the Hemingway agent.

### 5. Good Defaults Matter

The majority of users take the default options. Choosing good defaults based on common use cases makes the experience smooth.

## Updating Agents

The CLI keeps your agents up-to-date:

```bash
# Check what's installed
prompt-library list --installed

# Reinstall to get latest version
prompt-library add hemingway
# When prompted, select "Reinstall (overwrite)"
```

For a clean slate:

```bash
# Remove existing installation
rm -rf .claude/agents .claude/prompts
rm .prompt-library.json

# Reinstall
prompt-library init
```

## Future Enhancements

While the current version is fully functional, I'm planning several enhancements:

### Automatic Updates

```bash
prompt-library check    # Check for updates
prompt-library update   # Update all installed items
```

### Custom Registries

Allow teams to maintain their own agent registries:

```bash
prompt-library add my-agent --registry=https://my-company.com/agents
```

### Agent Templates

Scaffold new agents from templates:

```bash
prompt-library create my-agent --template=code-reviewer
```

### Community Ratings and Reviews

Help users discover the most effective agents:

```bash
prompt-library list --popular    # Show most downloaded agents
prompt-library info hemingway    # View details and ratings
```

### VS Code Extension

Deep integration with VS Code for even smoother installation and management.

## Contributing Your Own Agents

One of the most powerful aspects of the prompt library is that it's designed to be a community resource. If you've crafted an effective AI agent or prompt template, you can contribute it back to the library for others to use.

### How to Contribute

Contributing is straightforward:

1. **Fork the Repository**: Start by forking [shawnewallace/prompt-library](https://github.com/shawnewallace/prompt-library)

2. **Create Your Agent**: Add your agent or prompt to the appropriate location:
   - Scenario-specific agents: `scenarios/{scenario}/agents/`
   - Shared agents: `shared/agents/`
   - Prompts: `shared/prompts/` or `scenarios/{scenario}/prompts/`

3. **Follow the Format**: Agents use frontmatter metadata:

```markdown
---
name: Your Agent Name
description: Brief description of what the agent does
tools: ['search', 'extensions', 'todos']
---

# Your Agent Instructions

Your detailed agent instructions here...
```

4. **Update the Registry**: Add your agent to `cli/.prompt-library/registry.json`:

```json
{
  "id": "your-agent-id",
  "name": "Your Agent Name",
  "type": "agent",
  "description": "Brief description",
  "sourcePath": "shared/agents/your-agent.agent.md",
  "tags": ["relevant", "tags"]
}
```

5. **Submit a Pull Request**: Include details about what your agent does and why it's useful

### What Makes a Good Contribution?

The best contributions share these characteristics:

- **Focused Purpose**: Each agent should do one thing well
- **Clear Instructions**: Write clear, specific instructions the AI can follow
- **Tested**: Test your agent with real scenarios before contributing
- **Well-Documented**: Include a description and usage examples
- **Reusable**: Design for general use, not hyper-specific cases

### Types of Contributions Welcomed

Beyond agents, the library benefits from various types of contributions:

**Agents**: Specialized AI assistants for specific tasks (code review, testing, documentation, architecture, etc.)

**Prompts**: Reusable prompt templates for common scenarios

**Scenarios**: Complete workflow bundles combining multiple agents and prompts

**Documentation**: Examples, tutorials, best practices

**Improvements**: Enhancements to existing agents based on real-world usage

### Building a Community Resource

The vision for the prompt library is to become a community-driven collection of battle-tested AI agents and prompts. Every developer has crafted effective prompts for their specific needs - contributing them helps the entire community. Whether you've created an agent for API testing, database migrations, security reviews, or any other specialized task, your contribution can save other developers time and help them work more effectively with AI assistants.

## Real-World Examples

### Example 1: .NET Developer

```bash
cd ~/projects/my-dotnet-app
prompt-library init
# Select: Claude Code → dotnet-clean-architecture
```

Files installed to:
- `~/projects/my-dotnet-app/.claude/agents/sharp.md`
- `~/projects/my-dotnet-app/.claude/agents/archy.md`
- `~/projects/my-dotnet-app/.claude/prompts/adr.md`

Now in Claude Code: "Use Sharp to help me implement this feature following Clean Architecture"

### Example 2: Content Creator

```bash
prompt-library add hemingway
prompt-library add writing-clarity
```

Use in Claude Code: "Use Hemingway to review this blog post"

### Example 3: Team Setup

```bash
# Team lead sets up the project
cd ~/projects/team-react-app
prompt-library init
# Select: GitHub Copilot → typescript-frontend

# Commit the installed agents
git add .github/
git commit -m "feat: add AI agents for code review and architecture"

# Team members clone and have immediate access
# Restart VS Code and the agents are available
```

## Try It Today

The prompt-library CLI is available now on npm:

```bash
npm install -g @shawnwallace/prompt-library
prompt-library init
```

**Resources:**
- 📦 [npm package](https://www.npmjs.com/package/@shawnwallace/prompt-library)
- 💻 [GitHub repository](https://github.com/shawnewallace/prompt-library)
- 📚 [CLI documentation](https://github.com/shawnewallace/prompt-library/tree/main/cli)
- 📝 [Original library post](https://shawnewallace.com/2025-11-19-building-a-personal-prompt-library/)

## Finally

The prompt-library CLI transforms a manual, 15-minute process into a one-command installation. This removes friction and helps developers use AI assistants in their daily work. Whether you're setting up a new project, onboarding team members, or standardizing AI interactions across your organization, the CLI provides a fast, consistent, and reliable solution.

AI assistants are now standard tools in modern software development. The prompt-library CLI ensures that configuring these assistants is no longer a barrier to adoption. Install it today and see how quickly you can have AI agents working in your projects.

What agents will you try first? I'd love to hear about your experience in the comments below or through [GitHub discussions](https://github.com/shawnewallace/prompt-library/discussions).

---

*This post was written with assistance from Claude Code, naturally using agents from the prompt library.*
