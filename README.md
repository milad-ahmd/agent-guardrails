> [!NOTE]
> **This skill lives in the main collection: [milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills/tree/main/skills/agent-guardrails)**. Please ⭐ star it there; that's where updates land first.
> Docs: **https://milad-ahmd.github.io/agent-skills/skills/agent-guardrails/** · Claude Code: `/plugin install all-skills --marketplace milad-ahmd/agent-skills`

<div align="center">

# 🚧 agent-guardrails

**A tested hook that stops your agent force pushing main, rm -rf outside the project, reading .env or curl | bash. An Agent Skill for Claude Code, Cline, Cursor, Codex and other AI coding agents.**

[![License: MIT](https://img.shields.io/github/license/milad-ahmd/agent-guardrails)](LICENSE)
[![Stars](https://img.shields.io/github/stars/milad-ahmd/agent-guardrails?style=social)](https://github.com/milad-ahmd/agent-guardrails)
![Category](https://img.shields.io/badge/category-Security%20&%20Maintenance-blue)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cline%20%7C%20Cursor%20%7C%20Codex-8A2BE2)

[Install](#-install) · [Usage](#-usage) · [How it works](skills/agent-guardrails/SKILL.md) · [All skills](https://github.com/milad-ahmd/agent-skills)

</div>

> Part of **[agent-skills](https://github.com/milad-ahmd/agent-skills)**, a growing collection of practical skills for AI coding agents.

## 📦 Install

**One command (installs the whole collection):**

```bash
curl -fsSL https://raw.githubusercontent.com/milad-ahmd/agent-skills/main/install.sh | bash -s -- agent-guardrails
```

**Manually (Claude Code):**

```bash
git clone https://github.com/milad-ahmd/agent-guardrails /tmp/agent-guardrails
mkdir -p ~/.claude/skills && cp -r /tmp/agent-guardrails/skills/agent-guardrails ~/.claude/skills/
```

**Per project:** copy `skills/agent-guardrails` into `<project>/.claude/skills/`.
**Any other agent:** paste [`SKILL.md`](skills/agent-guardrails/SKILL.md) into your rules or system prompt.

## 💬 Usage

Just ask your agent:

```text
Stop Claude Code from force pushing to main
Add guardrails so the agent can't rm -rf or cat my .env
```

The full workflow, rules and output format are in [`SKILL.md`](skills/agent-guardrails/SKILL.md).

## 🔎 Sample output

`guardrails.py` is plain Python 3 with no dependencies. The same code runs as the Claude Code hook. Real output from its checker and its built-in self-test:

```text
$ python3 guardrails.py check "git push --force origin main"
DENY
  deny  force-push-protected force push to protected branch main
(exit 4)

$ python3 guardrails.py check "rm -rf ./build"
ALLOW

$ python3 guardrails.py test | head -14
ok   allow git push origin feature
ok   allow git push -u origin HEAD
ok   deny  git push --force origin main
ok   deny  git push -f origin master
ok   deny  git push --force-with-lease origin main
ok   deny  git push origin --delete main
ok   ask   git push --force origin feature
ok   ask   git push origin +feature
ok   ask   git push origin main
ok   ask   git push [on main]
ok   ask   git commit -m 'wip' [on main]
ok   allow git commit -m 'wip'
ok   allow git commit -m "Remove .env from docs; drop table notes"
ok   ask   git commit --no-verify -m wip
```

`install` merges one PreToolUse entry into `.claude/settings.json` with a backup, and `uninstall` puts the file back as it was. It reads command text only, so it is a seatbelt, not a sandbox: the SKILL.md lists what it can't see.

## 🧩 More skills

See the full collection: **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 🤝 Contributing

This repo is a read-only mirror. Please open issues and PRs in **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 📄 License

[MIT](LICENSE) © Milad Ahmadi

<div align="center">

**If this skill saved you time, a ⭐ helps others find it.**

</div>
