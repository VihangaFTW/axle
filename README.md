# Axle

My take on a terminal coding agent.

![Axle](assets/cli.png)

## Install

```bash
npm install -g @vm2/axle
```

Then run `axle` in any project directory.

Here are some access codes:

- 2V5J-Q86Q-KFVP
- WBPW-XYTX-F2K2
- 9D8N-YBTC-V8VW
- 8VGV-V2YJ-VUX5
- XK29-AZNQ-ZEAJ
- D4XX-E43X-N6US
- 57JY-6MNU-EHBK
- 56UR-9QRQ-ZE5D
- CVCD-EKDU-ZDE6
- ZY73-Z8UC-QUKV

Axle is an invite-gated alpha. If the above codes do not work, email
[contact@vihangamihiranga.com](mailto:contact@vihangamihiranga.com) for an
invite code, then run `/login` on first start to redeem it.

## What is in it

- A curated list of models with their OpenRouter equivalents.
- Local file and shell tools with web search and fetch
- Sessions you can resume, plus `/undo` and `/redo` over the edits a turn made
- Support for custom subagents and skills loaded from your own `.axle`, `.agents`, or `.claude`
  directories
- Image attachments, themes, and a configurable reasoning effort

Run `/` in the TUI for the full command list.

## Permissions

Out of the box Axle has no permissions set: every local tool runs freely inside
the project, and anything reaching outside it asks first.

To narrow that, write a `permissions.json` in any of the `.axle`, `.agents` or
`.claude` directories. Global files are read first and project
files last, so a project rule wins.

```json
{
  "permission": {
    "*": "allow",

    "path": {
      "*": "allow",
      "*.env": "deny",
      "*.env.example": "allow",
      "*/.ssh/*": "deny",
      "~/notes/*": "ask"
    },

    "bash": {
      "*": "allow",
      "git push *": "ask",
      "curl *": "ask",
      "rm -rf *": "deny"
    },

    "external_directory": {
      "*": "ask",
      "~/.cargo/registry/*": "allow"
    },

    "read": { "*": "allow" },
    "write": { "*": "allow", "*.lock": "ask" },
    "edit": { "*": "allow", "package.json": "ask" },
    "list": { "*": "allow" },
    "glob": { "*": "allow" },
    "grep": { "*": "allow" },
    "shell": { "*": "allow", "*--force*": "ask" },
    "skill": { "*": "allow", "deploy": "ask" },
    "agent": { "*": "allow", "reviewer": "deny" }
  }
}
```

`path` applies to every file a tool touches, `bash` to each command in a chain,
`external_directory` to anything outside the project root, and the rest to one
tool each. `*` is greedy, `~` expands, and within a surface the last matching
rule wins, so put catch-alls first. Surfaces are judged independently and the
strictest answer stands.

## Note

Alpha. Expect things to move and break. Please report bugs or feature requests via `/issue`.
