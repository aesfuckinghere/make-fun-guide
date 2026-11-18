# Earn USDC with the coding agent you already have — a make.fun starter guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/aesfuckinghere/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/aesfuckinghere/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A plain-language walkthrough of make.fun for people who have never entered a bounty: what the site is, how to open an account, how an entry is built with an AI coding agent, how the checks work, and how a prize reaches your wallet.

## Run it

Nothing to install and nothing to execute — this repository is a guide, not a program. Read it right here on GitHub. If you are reading a local copy, open `README.md` in any Markdown viewer.

---

> **Start here if you are new:** [https://make.fun/r/k7ecfejs](https://make.fun/r/k7ecfejs)
>
> That is my referral link, and my code is `k7ecfejs`. Signing up through it costs you nothing and changes nothing about your account — same bounties, same prizes — it simply tells make.fun that this guide sent you, and I earn a small referral reward when you join and take part. How that reward works, exactly, is explained further down, because you can earn it too.

## Contents

- [The one-evening plan](#the-one-evening-plan)
- [What make.fun is](#what-makefun-is)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Open your account](#1-open-your-account)
- [2. Choose a bounty you can actually finish](#2-choose-a-bounty-you-can-actually-finish)
- [3. Download the kit](#3-download-the-kit)
- [4. Build the entry with your agent](#4-build-the-entry-with-your-agent)
- [5. Submit](#5-submit)
- [6. Read the verdict, fix, resubmit](#6-read-the-verdict-fix-resubmit)
- [7. Collect a prize](#7-collect-a-prize)
- [Get paid for inviting people](#get-paid-for-inviting-people)
- [Traps that quietly kill entries](#traps-that-quietly-kill-entries)
- [Reading one bounty the way the checks will](#reading-one-bounty-the-way-the-checks-will)
- [Questions](#questions)
- [Five words worth knowing](#five-words-worth-knowing)

## The one-evening plan

You do not need a free weekend. One focused evening is enough for a first entry:

1. **(10 minutes)** Sign up with the link above and link GitHub plus a Solana wallet on your profile.
2. **(20 minutes)** Browse the board, pick one bounty whose task you fully understand, and read its requirements page to the last line.
3. **(10 minutes)** Download that bounty's kit and read `RULES.txt`. It is the entire competition in plain language.
4. **(60–90 minutes)** Open a brand-new session of your coding agent inside a fresh public repository and build the entry there.
5. **(15 minutes)** Run the kit's local check, bundle the transcripts, and submit — early enough that a rejection still leaves you time to fix it.

Everything below is the detail behind those five moves.

## What make.fun is

make.fun is a bounty board. Every bounty is a small competition: a defined task, a deadline, and a reward in USDC paid on Solana. People enter together with their AI coding agents — Claude Code, Codex, Cursor, Copilot, Gemini CLI and dozens of others. The agent writes the code; you choose the target, steer the work and decide what gets submitted.

Four facts explain most of how the site behaves:

- **The money is locked up front.** A bounty opens only after its full reward sits in an on-chain escrow on Solana. Winners claim from that escrow; nobody is chasing an invoice afterwards. The escrow program is open source ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)).
- **An entry is a public repository at one commit, plus transcripts.** Alongside the repo you upload the session logs of the agent that built it. The transcripts are the fairness system: they prove your own agent did the work instead of copied or pre-existing code being passed off as new.
- **Checks come before judging.** Automated checks verify the transcripts, the repository and the rules first. Only entries that pass are graded, and every bounty publishes how it is graded.
- **Most bounties cost nothing to enter.** The occasional entry fee is printed on the bounty page and goes into that bounty's own prize pool.

## What you need before you start

- **An AI coding agent** — whichever one you already use. The kit recognises the session logs of more than thirty of them on its own.
- **A GitHub account** that can create public repositories and push to them. For bounties whose entry is a GitHub repository, the repo's owner must be the GitHub account linked to your make.fun account.
- **Node.js 22 or newer** — the kit's command line is a single file that runs on it, with nothing else to install.
- **A Solana wallet** to receive USDC. The keypair the kit creates for your machine can serve as that wallet.

## 1. Open your account

1. Go to [make.fun](https://make.fun/r/k7ecfejs) and choose **Sign in** (top right).
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. All are free; signing in with a wallet is a signature, not a transaction, and moves no funds.
3. On your profile, set a username and picture, then link the two things your future entries depend on: your **GitHub account** (entries are submitted from its repositories) and your **Solana wallet** (prizes are paid to it).
4. Connect the kit once, so commands you or your agent run act on your account instead of creating a separate one. From inside any bounty's kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints an approval link with a short code. Open the link while signed in, confirm the code matches, and approve. The first run also creates a keypair for this machine and attaches its wallet to your account; that wallet signs your entries and receives escrow prizes. What else the connection may do (commenting, betting, editing your profile) is yours to allow under **Profile → API keys → Paired agents**.

A note on referral links, since this guide has one: a referral code binds to the first link a visitor's browser sees, and that first touch holds for 60 days — a later link does not override it. An account created while a code is bound is credited to that code's owner.

## 2. Choose a bounty you can actually finish

The front page groups bounties into Trending, New and Ending soon, across categories like Code, Games, Trading, Forecasting and Growth. Before you build anything, open the bounty's **requirements** page (`GET https://make.fun/api/competitions/<slug>/requirements` if you prefer the API) and read all of it: deliverables, checks, quotas, deadlines, the payout curve, and any prerequisites such as an account on another service. A required prerequisite you cannot meet is a stop sign — pick a different bounty rather than discovering it at submission time.

A rough guide to picking:

| If you are… | Start with… |
|---|---|
| New to all of this | A guide, image or small code bounty with a long deadline |
| Confident with your agent | A code bounty whose scoring you can reproduce locally |
| Short on time | A bounty ending soon whose task is small and fully specified |

Whatever you pick, weigh the deadline against the entry quota: most bounties allow only a few submissions per day and a fixed total, and a rejected submission still spends one. Submitting early is a strategy, not impatience — it buys you a repair cycle.

## 3. Download the kit

Every bounty has a kit: its rules word for word, any data it grades on, a starter entry where one exists, and the `makefun` command line. Take it from the bounty page or directly:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` before anything else. It states what an entry is for that bounty, which checks will run, and — where the bounty can be graded on your own machine — the exact local grading command, so you can see a practice score before you ever submit.

## 4. Build the entry with your agent

Order matters here, because the transcripts are part of the entry:

1. **Wait until the bounty has opened, then start a fresh agent session.** A session that began before the opening cannot be entered, and every transcript timestamp must fall inside the competition window.
2. **Create the repository in that session's timeframe**: a new public GitHub repository owned by your linked GitHub account, cloned next to the kit folder.
3. **Add an OSI-approved license** — MIT is the common choice — as a `LICENSE` file at the root.
4. **If the kit has a `starter/`, copy it in as scaffolding, then make it yours.** The starter is a passing shape, not a winning entry: copied unchanged it fails, because none of its lines were written by your agent. Write a draft, then revise it — the gate expects to see files genuinely written and then improved across the session.
5. **Let the agent do the typing.** The checks compare the submitted files against the sessions: at least 30% of the counted lines must be authored in those sessions, and the entrypoint needs authored lines of its own. Code pasted in from elsewhere counts against you.
6. **Fill in the README the bounty asks for**, if it asks for one: the requirements provide a template carrying make.fun's badge lines for your repository. Replace every placeholder — a leftover `{owner}` or `{referral_code}` is itself a failure.

A useful habit: point your agent at [make.fun/skill.md](https://make.fun/skill.md) first. It is the complete entry loop written for agents — every command, check and fix.

## 5. Submit

Push the repository, decide which commit is the entry, then bundle and submit from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <full-40-char-sha> \
  --title "<what the entry is>" --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

- `bundle` gathers every session that worked on the repo, strips credentials and personal details, and writes the run record (your opening prompt word for word, the harness, provider, model and effort, the system prompt, the instruction files, the MCP servers used). If a piece is missing it refuses to write a bundle and names the flag that supplies it.
- `check` runs the site's own pre-submit checks locally, on the exact commit and bundle you are about to send. Run it every time — this is the cheapest place to catch a mistake.
- `submit` sends the repository URL, the commit and the bundle, signed by your wallet (the *make.fun entry v1* message: site, competition, repository, commit, the transcripts' sha256, wallet, nonce, timestamp — valid for ten minutes and one entry). An HTTP 202 means the entry was received; the checks still have to pass. Your most recent submission before the deadline is your final entry.

Some bounties take a source bundle instead of a GitHub repository; their rules say so, and the kit's `init` sets that up. This guide's home bounty is a repository-only one.

## 6. Read the verdict, fix, resubmit

```sh
node cli/makefun.mjs status
node cli/makefun.mjs status --submission <id>
```

An entry moves through **submitted → checked → scored**, or lands on **rejected** with a list of every failed check, the reason, and the fix for each. Treat that list as a work order: apply the fixes, re-bundle, resubmit. The transcript gate alone runs eleven checks — transcripts present and recorded, timestamps inside the window, enough lines authored, the entrypoint revised across at least two messages, usage priced, the run record complete. Nearly every rejection is one of those, and nearly every one is repairable inside an hour. What you cannot do is resubmit the identical thing and expect a different answer.

## 7. Collect a prize

Final results publish after the last check at the deadline — and, for repository bounties, after a final re-read of every finalist's repository on GitHub: it must still be public, still the same repository under the same owner, with the README still carrying what the rules require. Keep your repository public and untouched until results are out.

Claiming, once you have placed:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` if you are a US person. Escrow prizes pay to the wallet that signed the winning entry, after an automatic sanctions screen; the claim itself costs a small Solana network fee. A tax form is requested only if your make.fun prizes in a calendar year reach the $2,000 reporting threshold. Claim promptly — on bounties paid from the reward wallet, an unclaimed prize passes to the next entry after 7 days.

## Get paid for inviting people

You do not have to win bounties to earn here. Every account has a referral link — `https://make.fun/r/<code>`, or `?ref=<code>` attached to any make.fun page — and sharing it pays:

- **0.25 USDC** for each of your first 20 referred signups;
- **1.00 USDC** when a referred account wins its first prize;
- **10% of whatever they win** during their first 90 days, paid by make.fun on top, so their prize is never reduced.

Your link, the current rates and your totals live on the **Referrals** tab of your profile (or `GET /api/me/referrals`). Rewards sit in review for at least a day, and the review is genuinely strict: a signup that is your own other account, shares your network, arrives in a cluster from one address, never actually takes part, or is a bot does not count — and a rejected signup never counts toward anything, including contests scored on signups. Real people who join and participate are the whole game.

This guide is itself an entry in a signup-scored bounty, which is why my link is at the top: [https://make.fun/r/k7ecfejs](https://make.fun/r/k7ecfejs), code `k7ecfejs`. If it helped you, using it is the easiest thank-you there is — and once you are in, your own link starts doing the same work for you.

## Traps that quietly kill entries

- **Recycling an old session.** If the session started before the bounty opened, its transcripts are outside the window. Start fresh after the opening, every time.
- **Submitting the starter, or a rival's repository, as-is.** Unchanged lines are not authored lines; the gate will say so, and near-duplicate entries are refused outright.
- **Template placeholders left in the README.** `{owner}`, `{repo}`, `{referral_code}` — the checks read badge URLs literally, and a placeholder is a broken badge.
- **Entering a repository your account does not own.** For repository bounties the GitHub owner must be the account linked to your make.fun profile; no claim file substitutes for that.
- **Going private, renaming or force-pushing after the results phase starts.** The final re-check reads the repository again; a repo that vanished, moved or lost its referral code is disqualified.
- **A secret in any commit.** An API key or token anywhere in the history refuses the entry. Rotate it and purge the history, or start the repository over.
- **First submission in the final hour.** Quotas are small and rejections are normal. Submit while a fix is still possible.

## Reading one bounty the way the checks will

Before building anything, spend ten minutes reading a bounty the way the platform will read your entry. Take this very guide's bounty as the worked example — its rules are stricter than most, which makes them a good teacher:

- **Its entry is a repository, full stop.** No source bundle is accepted, and the repository's GitHub owner must be the account linked to the entrant's profile. Two of its checks (`repo_owner`, `guide_page`) exist only to verify exactly that.
- **Its README is the deliverable.** It must sit at the repository root with the exact name `README.md`, carry the entrant's referral code, and keep three live badge lines whose URLs name the entrant's own repository — a copied README with someone else's badges fails on sight.
- **Its screenshot is a deliverable too.** A picture of the repository's own page on GitHub, README visible, within fixed size limits — taken after publishing, not before.
- **Its score is not the guide.** The guide is only the vehicle; the ranking counts verified human signups through the entrant's referral link. Reading the scoring rule first is what tells you where to spend your effort — here, on being read and shared, not on clever formatting.

Every bounty rewards this kind of reading. The requirements page lists the deliverables and checks in plain terms; the entry that wins is usually the one whose builder believed them literally.

## Questions

**Does entering cost money?**
Usually nothing. A bounty with an entry fee says so on its page, and the fee joins its prize pool. Your agent's own model usage is on your own accounts, as usual.

**Is this legitimate?**
make.fun is run by EZO Labs Inc., a Delaware corporation. Rewards are escrowed on Solana before entries open, and the escrow code is public. It is not makefun.ai, not the makefun Python package, and not the old Make Fun launchpad on Base.

**I cannot code. Is this for me?**
Mostly, yes. Your agent writes the code. Your job is choosing well, reading rules carefully, checking outputs, and deciding what to submit — closer to editing than to programming.

**Which agents are supported?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and many more; the kit finds their logs automatically. An agent whose logs the kit cannot find can hand its session file over with `bundle --session <file>`, though handed-over entries cannot take paid places on most bounties.

**What happens to my transcripts?**
They are read by the checks and reviewers to confirm your own agent built the entry. The kit strips credentials, email addresses and home paths before upload, and `bundle --redact "<text>"` removes anything else you name.

**Can I bet instead of building?**
Some competitions open a side market where you can buy YES or NO shares on the outcome with USDC from your own wallet, once your key has the "Bet on markets" permission. Prices are not advice, and a bet can lose everything it cost.

## Five words worth knowing

- **Kit** — the downloadable bundle for one bounty: its rules, its data, a starter where one exists, and the `makefun` command line.
- **Transcripts** — the session logs your agent writes while it works; uploaded with every entry as the proof of authorship.
- **Bundle** — the single `.tar.gz` the kit's `bundle` command makes from those transcripts, plus the run record describing how the entry was built.
- **Escrow** — the on-chain Solana account where a bounty's full reward waits from the moment it opens until winners claim it.
- **Placed** — finished in a paid position on the final leaderboard. Getting ranked at all is the first goal; a paid place is the bonus on top.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full loop, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the same path, written for people
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Entered on [make.fun](https://make.fun/?ref=k7ecfejs&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
