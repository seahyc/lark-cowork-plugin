# lark-cowork-plugin

A [Claude Cowork](https://claude.ai/cowork) plugin that gives Claude access to your Lark/Feishu workspace — calendar, messages, documents, sheets, bitable, tasks, email, and meeting minutes.

## What it does

Once installed, Claude can:

| Capability | What you can ask |
|------------|-----------------|
| **Calendar** | "What meetings do I have this week?", "Schedule a 1:1 with Alice tomorrow at 3pm", "Find a free slot for the team" |
| **Messages** | "What was discussed in the #engineering channel today?", "Send a message to Bob", "React to that last message with 👍" |
| **Documents** | "Summarise this Lark doc", "Find all docs about the Q4 plan", "Search the wiki for onboarding guides" |
| **Sheets** | "Read the data in this spreadsheet", "Write these results to column B", "Create a new sheet with these headers" |
| **Bitable** | "List all records in the Projects table", "What fields does the Tasks bitable have?" |
| **Tasks** | "What tasks am I assigned?", "Show me overdue tasks" |
| **Email** | "Search my inbox for emails from Alice", "Show me unread emails about the budget" |
| **Minutes** | "Get the transcript from yesterday's all-hands", "Summarise the meeting recording" |

## Requirements

This plugin requires the **lark-cli** tool to be installed and authenticated.

### 1. Install lark-cli

```bash
# From source
git clone https://github.com/seahyc/lark-cli
cd lark-cli && make install
```

### 2. Create a Lark app

1. Go to [open.larksuite.com](https://open.larksuite.com) and create a custom app
2. Enable the permissions you need (see table below)
3. Add redirect URI: `http://localhost:9999/callback`
4. Enable "Refresh user_access_token" in Security Settings

<details>
<summary>Full permissions list</summary>

| Scope group | Permissions |
|-------------|-------------|
| `calendar` | `calendar:calendar` |
| `contacts` | `contact:contact.base:readonly`, `contact:department.base:readonly` |
| `documents` | `docx:document:readonly`, `docs:document.content:read`, `wiki:wiki:readonly`, `space:document:retrieve` |
| `messages` | `im:message:readonly`, `im:message`, `im:message.reactions:read`, `im:message.reactions:write_only` |
| `mail` | IMAP credentials (configured separately via `lark mail setup`) |
| `bitable` | `bitable:app:readonly` |
| `tasks` | `task:task:read` |
| `minutes` | `minutes:media:read`, `minutes:transcript:read` |

</details>

### 3. Configure and authenticate

```bash
# Create config
cp config.example.yaml .lark/config.yaml
# Edit .lark/config.yaml with your App ID

# Set app secret
export LARK_APP_SECRET="your_app_secret"

# Login (opens browser)
lark auth login
```

## Install the plugin

### In Claude Cowork

```
/plugin install lark@seahyc
```

Or add this repo as a marketplace first:
```
/plugin marketplace add seahyc/lark-cowork-plugin
/plugin install lark
```

### For local development

```bash
git clone https://github.com/seahyc/lark-cowork-plugin
claude --plugin-dir ./lark-cowork-plugin
```

## Slash commands

| Command | Description |
|---------|-------------|
| `/lark:lark-setup` | Set up or troubleshoot lark-cli |

## Skills

Skills are auto-invoked when Claude detects a relevant request:

- `lark:lark-calendar` — Calendar management
- `lark:lark-messages` — Chat messages and reactions
- `lark:lark-docs` — Documents, Drive, and Wiki
- `lark:lark-sheets` — Spreadsheets
- `lark:lark-bitable` — Bitable databases
- `lark:lark-tasks` — Tasks
- `lark:lark-email` — Email via IMAP
- `lark:lark-minutes` — Meeting recordings and transcripts
- `lark:lark-contacts` — Company directory

## Related

- [seahyc/lark-cli](https://github.com/seahyc/lark-cli) — lark-cli
