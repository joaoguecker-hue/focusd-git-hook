# focusd-git-hook

Turn every `git commit` into a habit streak. 🔥

This tiny hook calls [`focusd`](https://9482969453720.gumroad.com/l/aopuhv) — a blazingly-fast,
local-first CLI habit tracker — and checks off your **"Code"** habit
automatically every time you commit. Zero cloud, zero context-switching:
your streak lives in the same terminal you never leave.

## Install

```bash
curl -o .git/hooks/post-commit \
  https://raw.githubusercontent.com/joaoguecker-hue/focusd-git-hook/main/post-commit
chmod +x .git/hooks/post-commit
```

Want it to fire on `git push` instead of every commit? Save the same
script as `.git/hooks/pre-push`.

## Requirements

- [Focusd](https://9482969453720.gumroad.com/l/aopuhv) installed and a habit named `Code`
  (`focusd add "Code"`).

## Why Focusd?

- **Local-first.** One SQLite file on *your* disk. No account, no cloud,
  no subscription-of-the-month.
- **Blazingly fast.** Go binary, cold start in milliseconds.
- **Terminal-native.** Neovim plugin + Tmux statusline integration.

**→ [Get Focusd Premium — $20, one-time, yours forever](https://9482969453720.gumroad.com/l/aopuhv)**
