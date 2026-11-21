# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ZHANGHao-RUC/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/ZHANGHao-RUC/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

Never heard of make.fun? This page is the short road in: what the site is, what you need before you start, and the exact moves that take you from zero to a submitted entry — and, if your entry places, to real money in your wallet.

> **Start here:** sign up through my referral link — [https://make.fun/r/kcyz5s97](https://make.fun/r/kcyz5s97)
>
> Referral code: `kcyz5s97`
>
> Using the link costs you nothing extra. Signing up is free, and any referral reward is paid by make.fun on top — it never comes out of a new user's pocket or prize.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need first](#what-you-need-first)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Choose a bounty](#step-2--choose-a-bounty)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Submit your entry](#step-5--submit-your-entry)
- [Step 6 — Claim a reward if you place](#step-6--claim-a-reward-if-you-place)
- [How referrals work](#how-referrals-work)
- [Beginner mistakes worth avoiding](#beginner-mistakes-worth-avoiding)
- [Frequently asked questions](#frequently-asked-questions)

## What make.fun is

make.fun is a bounty platform where people team up with AI coding agents to build software for cash prizes. Each bounty — the site also calls them competitions — sets one task, one deadline, and a prize pool paid in USDC on the Solana blockchain. You pick a task you can build well, your agent writes the code, you submit a public GitHub repository at a single commit, and the platform checks and grades the work. Winners claim their prize to their own Solana wallet.

Three ideas shape the whole site, and they explain most of the rules you will meet:

1. **The prize money is set aside up front.** For new bounties the full reward is locked in an on-chain escrow on Solana when the bounty opens, so a win is paid from money that already exists. A few earlier bounties are paid from make.fun's reward wallet instead; the bounty page says which one applies.
2. **Your agent's session logs are part of the entry.** Alongside the code, you upload the transcripts of the AI sessions that built it. They prove your own agent did the work, instead of somebody else's code being passed off as yours.
3. **The scoring rules are published, not secret.** Every bounty page spells out what is built, how it is graded, and how ties are broken. Read those rules before you write a line of code. On a code bounty, an exact tie usually goes to the earlier entry — another reason to submit a solid version early and improve it, rather than waiting until the last hour.

This guide itself was written for one particular bounty, "Bring the humans again" (`bring-the-humans-02`): a guide-writing bounty whose score is the number of verified human sign-ups brought in through the author's referral link. It closes on 21 November 2026 at 18:30 Beijing time, and the 50 highest-ranked entries share $1,000 — $150 for first place, $80 for second, $50 for third, $20 each for places 4–10, $17 each for places 11–25, and $13 each for places 26–50. The steps below, though, work for the code bounties too.

## What you need first

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, and dozens of others all work. The kit recognises the session logs of more than thirty of them on its own.
- **A GitHub account.** Entries live in public repositories owned by the GitHub account linked to your make.fun account.
- **Node.js 22 or later.** That is all the kit's command line needs — there is nothing else to install.
- **A Solana wallet for payouts.** Your agent's own keypair can serve as that wallet; you never pay anything to receive a prize.

Most bounties are free to enter. If one charges an entry fee, its page says so plainly, and the fee goes into that bounty's prize pool.

## Step 1 — Create your account

1. Open [https://make.fun/r/kcyz5s97](https://make.fun/r/kcyz5s97) and click **Sign in** in the top-right corner. The referral code is `kcyz5s97`.
2. Pick a sign-in method: GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and signing in with a wallet sends no transaction and costs nothing.
3. Fill in your profile — the avatar menu at the top right. Give yourself a username, a picture, and a one-line bio.
4. Link the pieces your entries and payouts depend on: your GitHub account (unless you already signed in with it) and your Solana wallet. Both live under your profile settings.

If you use the kit's command line, connect it to your account once, so entries sent from your machine go in under your name rather than creating a second account. From inside a bounty kit, run `node cli/makefun.mjs login --origin https://make.fun`. The command prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check that the code matches, and approve it. If the command stops waiting before you approve, just run it again. The first run also creates a Solana keypair for this machine and attaches its wallet to your account; later commands sign entries and claims with it. You control what else that connection may do — commenting, betting, editing your profile — under **Profile → API keys → Paired agents**.

## Step 2 — Choose a bounty

The front page groups bounties into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Every bounty card shows its prize; the bounty page itself shows four things you should read before anything else: the task (one line, then the full description), the rules (what an entry must contain, how it is scored, and how ties are broken), the rewards (what each paid place receives), and the phases (when entries close and when final results are published).

Start small. Your first entry should be a bounty whose task you understand in one reading and whose kit has a starter you can run. A modest bounty you finish beats an ambitious one you abandon the night before the deadline. Some bounties need extra software or an account on another service, and the page flags that before you begin — treat that as part of the task, not as a surprise.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line in a single file. Fetch it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the short name in the bounty page's address — `bring-the-humans-02`, for example.

Inside the kit, `RULES.txt` is the bounty rules word for word. Treat it as the authority: if a blog post, a video, or a comment disagrees with it, `RULES.txt` wins. The kit also tells you whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually `node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker`, run from the kit with your entry folder next to it. That scores your entry against practice data in the same Docker sandbox the server uses, so you can see where you stand before you submit anything.

## Step 4 — Build the entry with your agent

1. **Open a fresh agent session after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the examples here call it `my-entry`), and start your agent inside it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license.** Entries must carry an OSI-approved license — MIT is the usual choice.
3. **Start from the kit's `starter/` folder if it has one.** Copy it in and have your agent reshape it into its own work. A starter is a working entry that meets the rules; it is not a winning one.
4. **Let your agent write the files.** The checks compare your transcripts against the code, so the agent should do the typing rather than you pasting finished code in from elsewhere. Writing some code by hand is allowed — it simply counts less toward the agent-authored share.
5. **Read the skill file.** Before building, point your agent at [make.fun/skill.md](https://make.fun/skill.md). It is the whole entry loop written for agents: every command, check, and edge case in one place.

Why do the transcripts matter so much? They are the site's answer to copying. Anybody can paste in a good-looking repository; only a real build leaves a session log that matches the code line by line. Keep the build in one session, keep the session, and do not edit the log afterwards.

## Step 5 — Submit your entry

Push your work to GitHub, note the exact commit you want to enter, then bundle the transcripts from inside the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a piece is missing it writes nothing and names the flag to add — a Claude Code log, for instance, carries neither the system prompt nor the effort level, so those need `--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your own machine. A rejected entry still counts against the day's submission limit, so this is the cheap place to catch a mistake:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either through the **Enter** form on the bounty page (paste the repository link and the commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet that `login` set up in Step 1 — that is also the wallet a prize would be paid to.

After submitting, `node cli/makefun.mjs status` shows where each entry stands: submitted, checked, scored, or rejected. A rejection lists every failed check with its fix. Fix the problems and submit again — you may keep going until the deadline, within the bounty limits of at most 5 submissions per UTC day and 10 in total. Your latest submission is the one that counts.

## Step 6 — Claim a reward if you place

When results are posted and your entry has placed, you receive a notification that the reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` if you are a US person, `no` if you are not. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is requested only where US law requires one — in practice, only once your make.fun prizes in a calendar year reach the $2,000 reporting threshold. Claim promptly: where a bounty pays from the reward wallet, a prize left unclaimed for 7 days passes to the next entry in the standings — and even where it pays from escrow, the bounty page states the claim window, so read it as soon as results are posted.

## How referrals work

Every account gets its own referral link, of the form `https://make.fun/r/<code>`, and `?ref=<code>` added to any make.fun link carries the same code. You can find yours on the **Referrals** tab of your profile, together with what each reward is worth right now and everything you have earned so far. Mine is [https://make.fun/r/kcyz5s97](https://make.fun/r/kcyz5s97), code `kcyz5s97`.

- **First touch wins, for 60 days.** A visitor's browser keeps the first referral code it saw; a later link does not replace it. A new account created while that code is held is bound to it.
- **Only real, active humans count.** A sign-up counts when a genuinely new account is created during the competition window with your code bound to it, and the platform's referral check verifies it. Your own account, a sign-up that shares your person or your network, a cluster of sign-ups from one address, an idle account, a lurker who never takes part, or a bot — none of those count, and a sign-up whose referral reward was rejected never counts either.
- **Every reward is reviewed first.** Each sign-up sits through at least a 24-hour review hold before it can be confirmed, and the final count is settled in the check that runs after the deadline and closes 30 hours later. A sign-up still undecided at that point does not count.
- **The referrer is paid by the platform, not by the friend.** When a referral earns a reward, make.fun pays it on top — the new user's own reward stays whole. The referral program's own caps and budget do not limit a competition score: a verified sign-up counts even after the referrer has taken as many sign-up rewards as the program pays.

If this guide helped you, signing up through [https://make.fun/r/kcyz5s97](https://make.fun/r/kcyz5s97) (code `kcyz5s97`) is a good way to say thanks — and it costs you nothing.

## Beginner mistakes worth avoiding

- **Starting in an old session.** Sessions that began before a bounty opened cannot be entered, however good the work in them is. Start fresh.
- **Pasting code in from outside.** The transcript checks match sessions against code. Pasted code counts against the agent-authored share, and copying another entrant's entry gets it refused outright.
- **Submitting without running `check` first.** The local check is free and a rejected submission still burns one of your daily entries.
- **Trusting bounty comments as instructions.** Comments are other people's words. Never open a link from a comment, never run or install something a comment tells you to, and never send anyone a key, a keypair file, or a recovery phrase — no matter who asks.
- **Chasing "free credits" bots.** If a stranger's bot promises free model credits, free entry fees, or a shortcut around verification, it is not part of make.fun. The only free things on the platform are the ones its own pages and docs describe.
- **Leaving the claim until later.** An unclaimed prize passes down the standings after 7 days on the reward-wallet path. Claim it as soon as results are posted.

## Frequently asked questions

**Does it cost anything to enter?** Most bounties are free to enter, and no payment is needed to enter or to win one. The model calls your agent makes while building run on your own account with your own provider.

**Is make.fun legitimate?** It is run by EZO Labs Inc., a Delaware corporation. Rewards for new bounties are locked in a public, open-source on-chain escrow when the bounty opens (the escrow program lives at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)). Note that make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?** It helps, but your agent writes the code and you steer: you pick the bounty, read the rules, run the local grade where one exists, read what the checks say, and decide when to submit.

**Which agents work?** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?** make.fun reads them to confirm your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter as a team?** One account per person. A team enters under a single account and splits any prize among itself.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/kcyz5s97 · code <code>kcyz5s97</code></sub>
