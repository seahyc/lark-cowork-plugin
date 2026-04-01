---
description: Set up or troubleshoot the lark-cli tool for Lark/Feishu integration
---

Help the user set up `lark-cli` for use with Claude Cowork.

## Prerequisites Check

First, verify lark-cli is installed:
```bash
which lark && lark --version
```

If not found, direct the user to install it:
- GitHub: https://github.com/yjwong/lark-cli
- Or fork: https://github.com/seahyc/lark-cli

## Configuration Check

Check if a Lark app is configured:
```bash
lark auth status
```

If not configured, walk through:

1. **Create a Lark app** at https://open.larksuite.com
2. **Enable permissions** — ask the user which capabilities they need:
   - Calendar: `calendar:calendar`
   - Contacts: `contact:contact.base:readonly`, `contact:department.base:readonly`
   - Documents/Sheets: `docx:document:readonly`, `docs:document.content:read`, `wiki:wiki:readonly`, `space:document:retrieve`
   - Messages: `im:message:readonly`, `im:message`, `im:message.reactions:read`, `im:message.reactions:write_only`
   - Bitable: `bitable:app:readonly`
   - Tasks: `task:task:read`
   - Minutes: `minutes:media:read`, `minutes:transcript:read`
3. **Add redirect URI**: `http://localhost:9999/callback`
4. **Enable** "Refresh user_access_token" in Security Settings
5. **Configure** `.lark/config.yaml` with the App ID
6. **Set** `LARK_APP_SECRET` environment variable
7. **Authenticate**: `lark auth login`

## Scope-by-scope Login

For minimal permissions, authenticate only for what's needed:
```bash
lark auth login --scopes calendar,contacts    # just calendar and contacts
lark auth login --add --scopes messages       # add messages later
```

Available scope groups: `calendar`, `contacts`, `documents`, `messages`, `mail`, `minutes`, `bitable`, `tasks`
