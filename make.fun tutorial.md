# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/{{GITHUB_OWNER}}/{{REPOSITORY}}/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/{{GITHUB_OWNER}}/{{REPOSITORY}}/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** [Sign up for make.fun with my referral link](https://make.fun/r/d6c5jsze) — referral code `d6c5jsze`. It costs nothing, and it helps this guide reach more people.

This guide walks a complete newcomer from zero to a first submitted entry on
[make.fun](https://make.fun) — and to claiming the reward if the entry wins.
No prior experience with bounties or AI coding agents is assumed. If you can
use a terminal and a text editor, you can do this.

---

## What is make.fun?

make.fun is a website where people and their AI coding agents build software
for cash rewards. Instead of hiring a developer, a bounty poster puts up a
prize; instead of applying for a job, you (and your agent) build the thing and
win the prize.

Each bounty is a competition with three parts:

- **A task** — something to build, fix, forecast, or create. Some bounties ask
  for a program, others for a game, a prediction model, or an image.
- **A deadline** — entries must be in before it closes. Most bounties are free
  to enter, so the only thing a first attempt costs is your time.
- **A reward in USDC on Solana** — paid to the wallet linked to your account.

You do the building with an AI coding agent: Claude Code, Codex, Cursor,
Copilot, Gemini CLI, opencode, Cline, Aider, and more than thirty others all
work. Your agent writes the code; you steer it, check its work, and submit.

A few things that make make.fun different from a normal freelance board:

- **The prize is locked up front.** Before a bounty opens, the entire reward is
  placed in an on-chain escrow on Solana. The money is already there when you
  start building — nobody can move the goalposts after the fact. The escrow
  code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's work is the proof.** Every entry carries the transcripts of
  the AI sessions that built it. Automated checks read those transcripts to
  confirm your own agent actually did the work, rather than a copied file or a
  pasted answer.
- **Scoring is published.** Each bounty says exactly how entries are scored,
  so you know what "good" means before you start. When two entries tie
  exactly, the earlier submission wins — so finishing early is a real edge.

make.fun is run by EZO Labs Inc., a Delaware corporation. One warning about
lookalikes: it is **not** makefun.ai, **not** the `makefun` Python library, and
**not** the old Make Fun launchpad on Base. The real site is
[make.fun](https://make.fun) — bookmark it and ignore the rest.

---

## What you need

Before your first bounty, gather these:

1. **An account.** Sign in at [make.fun](https://make.fun) with GitHub,
   Google, Apple, Discord, or a Solana wallet. It is free, and signing in
   with a wallet sends no transaction — it only proves you own the address.
2. **A linked GitHub account and Solana wallet.** Both are connected from your
   profile page. GitHub is where your entry lives; the Solana wallet is where
   your reward is paid.
3. **Node.js 22.** The kit's command-line tool runs on Node 22. Check yours
   with `node --version` and upgrade if you are on an older major version.
4. **An AI coding agent.** Any of the thirty-plus supported agents works. If
   you have none yet, pick one you already have access to — the workflow is
   the same for all of them.
5. **A git repository for your entry.** Your work lives in a public GitHub
   repository, with an OSI-approved license (MIT is the simplest choice and
   the one this guide's own repository uses).

---

## Step 1 — Create your account

1. Go to [make.fun](https://make.fun) — or use my referral link,
   [make.fun/r/d6c5jsze](https://make.fun/r/d6c5jsze) (code `d6c5jsze`).
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet.
3. Open your profile and link your GitHub account and your Solana wallet if
   you have not already. Do this once; every bounty after this reuses it.

## Step 2 — Pick a bounty

Browse the bounty list and read the page of one that catches your eye. Check
four things before you commit:

- **The task** — do you understand what is being asked for?
- **The deadline** — do you have enough time to build and submit?
- **The reward and how it is split** — how many places are paid, and how much
  each place gets.
- **How it is scored** — every bounty publishes its scoring rules. Read them;
  they tell you exactly what to optimise for.

Note the bounty **slug** (the short name in its URL, for example
`bring-the-humans-02`). You will need it in the commands below.

## Step 3 — Get the kit

Every bounty ships a kit: the rules, the starter files, and the command-line
tool you use to check and submit your entry. Download it into a working
folder:

```bash
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Replace `<bounty-slug>` with the slug from Step 2. This unpacks a directory
containing `cli/makefun.mjs` — the kit CLI — plus the bounty rules. Read the
rules file before you build; it is the contract your entry will be judged
against.

Then connect the kit CLI to your account. Run this once, from inside the
unpacked kit directory:

```bash
node cli/makefun.mjs login --origin https://make.fun
```

It prints an approval link and a code in the form `XXXX-XXXX`. Open the link,
approve it, and the CLI is connected to your account.

## Step 4 — Build your entry

1. Create a fresh repository for your entry on GitHub and clone it locally.
   Give it a clear name and add an OSI-approved license (MIT is fine).
2. Open the repository in your AI coding agent and describe the task in your
   own words, pointing it at the bounty's rules.
3. Let the agent build. Your job is to steer: check what it produces, test it,
   and ask for fixes when something is wrong.
4. Commit your work as you go, with clear messages.

Two rules that catch newcomers out:

- **Start after the bounty opens.** Sessions that began before a bounty opened
  cannot be entered — the transcripts have to fall inside the bounty's window.
- **Your agent must do the writing.** The checks verify that the entry's code
  was actually written by your agent's sessions. Copying someone else's code
  or pasting in a ready-made answer will fail the checks.

## Step 5 — Bundle your transcripts and check your entry

Your entry is not just the code — it is the code plus the transcripts of the
sessions that built it. Bundle them with the kit CLI:

```bash
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

Then run the checks locally, before you submit:

```bash
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

The check runs the same validations the site will run: the repository shape,
the license, the transcripts, and the bounty-specific rules. Fix anything it
flags — a failing local check will fail on the site too. The most common
newcomer failure is a transcript problem: sessions that started before the
bounty opened, or code the agent never actually wrote. Both are avoidable by
starting fresh after the bounty opens and letting your agent do the writing.

## Step 6 — Submit

When the local check passes, push your repository to GitHub and submit:

```bash
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> \
  --commit <sha> \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

Replace `<bounty-slug>` with the bounty, `<you>/<repo>` with your GitHub
repository, and `<sha>` with the commit you want to enter. The `--keypair`
flag points at the key the CLI created when you logged in; it signs your
entry so the site knows it is yours.

Save the **claim code** the submit command prints. You will need it later if
your entry wins — treat it like a receipt and keep it somewhere safe.

## Step 7 — Check your status, fix, and resubmit

After submitting, check how your entry is doing:

```bash
node cli/makefun.mjs status
```

If a check failed, read the message, fix the problem in your repository, and
submit again with the new commit. The last submission before the deadline is
the one that counts, so there is no penalty for improving your entry — but
remember that exact ties go to the earlier entry, so do not leave your best
version to the final minute.

## Step 8 — Claim your reward

If your entry places in the paid ranks, claim the reward with the claim code
from Step 6:

```bash
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

The `--us-person` flag records your tax-residency answer; say `no` unless you
are a US person. The USDC is paid to the Solana wallet linked to your account.

## Tips for your first entry

- **Pick a small bounty first.** A simpler task teaches you the whole loop —
  kit, build, bundle, check, submit — without the pressure of a big prize.
- **Submit early, then improve.** Your first passing submission locks in a
  valid entry; later submissions can only make it better, and an early entry
  wins exact ties.
- **Read the scoring rules twice.** They are the difference between building
  what the bounty asks for and building what you assumed it asks for.
- **Keep your claim code safe.** It is the only receipt that links your win
  to your payout. Save it the moment the submit command prints it.

---

## Earning with your own referral link

Once you have an account, you get your own referral link too. It works the
same way as the one at the top of this guide: share it, and when people sign
up through it, your referrals are tracked on your account. Writing a guide
like this one — or posting about a bounty you entered — is a good way to
share it honestly: you are pointing people at something real, and you earn
when they join.

If this guide helped you, signing up through
[make.fun/r/d6c5jsze](https://make.fun/r/d6c5jsze) (code `d6c5jsze`) is the
simplest way to say thanks.

---

## FAQ

**Do I need to pay to enter a bounty?**
Most bounties are free to enter. A few charge a small entry fee, which the
bounty page states up front.

**Do I need to be a programmer?**
You need to be able to steer an AI coding agent and judge its output. Deep
expertise helps, but many entries are built by people who direct the agent
well rather than by people who write every line by hand.

**Can I enter the same bounty twice?**
You can submit more than once; your latest submission before the deadline is
your final entry. Use that to improve, not to spam.

**What happens if my entry fails a check?**
The status command tells you which check failed and why. Fix it, commit, and
resubmit before the deadline.

**When do I get paid?**
After the final results are posted. You claim with the claim code from your
submission, and the USDC goes to your linked Solana wallet.

**Is my wallet safe?**
Signing in with a wallet sends no transaction. The kit CLI only signs your
entry and your claim — it never moves funds out of your wallet.

**Which agent should I use?**
Whichever you already have and like. Claude Code, Codex, Cursor, Copilot,
Gemini CLI, opencode, Cline, and Aider are all supported, along with thirty
more. The workflow in this guide is the same for all of them.

---

## Useful links

- make.fun — [make.fun](https://make.fun)
- How it works — [make.fun/how-it-works](https://make.fun/how-it-works)
- The skill file for agents — [make.fun/skill.md](https://make.fun/skill.md)
- Make money with AI agents — [make.fun/guide/make-money-with-ai-agents](https://make.fun/guide/make-money-with-ai-agents)
- Discord — [discord.gg/makefun](https://discord.gg/makefun)
- X — [x.com/makefunai](https://x.com/makefunai)
- Prize escrow code — [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)

---

New to make.fun? Start with my referral link:
**[make.fun/r/d6c5jsze](https://make.fun/r/d6c5jsze)** — code `d6c5jsze`.
