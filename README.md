<div align="center">

# ⚡ Focusd

### Habit tracking at terminal velocity.

**Blazingly fast** · **Local-first** · **Zero cloud** · **Built in Go + SQLite**

### 🔥 [**Get Focusd — $20, one-time, yours forever →**](https://9482969453720.gumroad.com/l/aopuhv)

</div>

```bash
╭────────────────────────────────────────────────────╮
│  ⚡ F O C U S D                    ● daemon: online │
├────────────────────────────────────────────────────┤
│                                                    │
│   Code        [████████░░]   Streak: 15 dias 🔥    │
│   Deep Work   [██████░░░░]   Streak:  9 dias       │
│   Read        [███░░░░░░░]   Streak:  4 dias       │
│                                                    │
├────────────────────────────────────────────────────┤
│   git hooks · recent                               │
│   ✔ 14:32  post-commit   feat: parser rewrite      │
│   ✔ 11:05  post-commit   fix: off-by-one in CTE    │
│   ✔ 09:47  post-commit   chore: bump deps          │
╰────────────────────────────────────────────────────╯
```

<div align="center">

*Your habits live where your code lives: in the terminal.*

</div>

---

## 🧠 The problem: context-switching is a streak killer

You're deep in a refactor. Flow state. Then you remember you have to log
your habits... in an Electron app. Or worse — on your *phone*. By the
time you're back in the editor, the flow is gone and the app ate 800 MB
of RAM to show you a checkbox.

Every cloud habit tracker wants an account, a subscription, and your
data on someone else's server. **Focusd wants none of that.** It's a
single Go binary, your data is one SQLite file on *your* disk, and it
cold-starts in single-digit milliseconds — faster than you can blink,
let alone switch contexts.

## 🧩 Neovim & Tmux: first-class citizens, not afterthoughts

A status bar that stutters is worse than no status bar. Focusd's editor
integrations are built around one rule: **the UI thread never waits.**

The Neovim component polls the local daemon *asynchronously* (libuv) and
your statusline reads from an in-memory cache — a **sub-millisecond**
lookup. No blocking, no stuttering, no dropped keystrokes. Ever.

```lua
-- init.lua — start/stop focus sessions without leaving the editor
local focusd = require("focus_tracker")
focusd.setup()
vim.keymap.set("n", "<leader>fs", "<cmd>FocusStart 1<cr>")
vim.keymap.set("n", "<leader>fq", "<cmd>FocusStop<cr>")
-- lualine: add the cached (sub-ms, non-blocking) component
-- sections = {{ lualine_x = {{ focusd.lualine }} }}
```

Your focus timer, always visible in the tmux statusline — with a 400ms
hard timeout so the bar *never* hangs, even if the daemon is down:

```tmux
# .tmux.conf
set -g status-interval 1
set -g status-right '#(focus_status.sh) | %H:%M'
```

## 🪝 What's in this repo?

A tiny git hook that turns every commit into progress on your **"Code"**
habit. Commit code → streak goes up. Zero effort, maximum dopamine.

Per-repo install:

```bash
curl -o .git/hooks/post-commit \
  https://raw.githubusercontent.com/joaoguecker-hue/focusd-git-hook/main/post-commit
chmod +x .git/hooks/post-commit
```

> Requires [Focusd](https://9482969453720.gumroad.com/l/aopuhv) running locally
> (`focusd start`) and a habit to credit.

## 🎯 Global install (the silver bullet)

Copying a hook into every repo you touch is busywork — and busywork is
exactly what Focusd exists to kill. Install it **once, globally**, and
every commit in every repo on your machine feeds the streak:

```bash
mkdir -p ~/.focusd-hooks
curl -o ~/.focusd-hooks/post-commit \
  https://raw.githubusercontent.com/joaoguecker-hue/focusd-git-hook/main/post-commit
chmod +x ~/.focusd-hooks/post-commit
git config --global core.hooksPath ~/.focusd-hooks
```

Done. New clones, old repos, that side project from 2023 — all of them
count from now on. To undo: `git config --global --unset core.hooksPath`.

> **Heads up:** `core.hooksPath` *replaces* per-repo `.git/hooks`. If a
> project uses its own hooks (husky, pre-commit), drop copies of them
> into `~/.focusd-hooks` or skip the global route for that machine.

## 🚀 Why Focusd?

| | |
|---|---|
| ⚡ **Blazingly fast** | Native Go binary. Cold start in ~5 ms. No runtime, no daemon babysitting, no waiting. |
| 🔒 **Local-first** | One SQLite file you own. No account. No cloud. No telemetry. `scp` it, `rsync` it, back it up your way. |
| 🖥️ **Terminal-native** | Neovim, tmux, git hooks. Check habits and watch streaks without ever leaving your shell. |
| 💸 **One-time $20** | Not a subscription. Buy it once, it's yours forever. |

## 📦 Get Focusd Premium

Stop renting your habit data from the cloud. Own it.

<div align="center">

### 🔥 [**Get Focusd — $20, one-time, yours forever →**](https://9482969453720.gumroad.com/l/aopuhv)

*Built by a developer who lives in the terminal, for developers who
never want to leave it.*

</div>
