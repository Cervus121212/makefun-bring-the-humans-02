# From zero to paid on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Cervus121212/makefun-bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Cervus121212/makefun-bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up through my link:** <https://make.fun/r/hb8k835f>
>
> Referral code: `hb8k835f`
>
> Joining costs nothing. If this guide gets you to your first entry, signing up through it is the way to say thanks.

This is a working guide, not a sales page. It takes you from no account to a submitted entry and a claimed prize, in the order you actually do things. Follow it top to bottom once; after that, use the contents to jump back to the step you need.

## The 5-minute version

1. Sign up at <https://make.fun/r/hb8k835f> (code `hb8k835f`), then link GitHub and a Solana wallet on your profile.
2. Pick an open bounty and read its rules — prize, deadline, how it is scored, what it demands.
3. Download its kit: `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`.
4. Connect the kit to your account once: `node cli/makefun.mjs login --origin https://make.fun`.
5. Build in a fresh agent session that starts after the bounty opens. Your agent writes the code; the kit records the session.
6. Bundle the transcripts and run the local checks before you submit — a rejected entry still counts against your daily limit.
7. Submit the public GitHub repository at one commit. Watch the status, fix rejections, resubmit.
8. When you place, claim the USDC to your Solana wallet.

The rest of this guide is those eight steps, done properly.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [How a bounty runs](#how-a-bounty-runs)
- [The 10-minute setup check](#the-10-minute-setup-check)
- [Step 1 — Make the account](#step-1--make-the-account)
- [Step 2 — Read a bounty page like a builder](#step-2--read-a-bounty-page-like-a-builder)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Build the entry](#step-4--build-the-entry)
- [Step 5 — Bundle and check before you submit](#step-5--bundle-and-check-before-you-submit)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Read the verdict, fix, resubmit](#step-7--read-the-verdict-fix-resubmit)
- [Step 8 — Claim the USDC](#step-8--claim-the-usdc)
- [Your own referral link — how it actually pays](#your-own-referral-link--how-it-actually-pays)
- [Mistakes that cost people money](#mistakes-that-cost-people-money)
- [FAQ](#faq)
- [Links](#links)

## What make.fun actually is

make.fun is a bounty board run by EZO Labs Inc. where people build software with AI coding agents and win cash prizes. Each bounty — the site calls it a competition — posts a task, a deadline, and a prize paid in USDC on Solana. You build the entry with an agent (Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, or one of 30+ others), submit it, and if it places you claim the prize into your own Solana wallet.

An entry is two things: a public GitHub repository at one specific commit, and the transcripts — the session logs — of the AI work that produced it. The transcripts are the fairness mechanism. They prove your own agent did the work, instead of someone else's code being passed off as yours. The grader runs every surviving entry the same way, twice, in a sandbox, and ranks them on performance and on what the build cost.

Do not confuse make.fun with makefun.ai (an AI image and video generator), the `makefun` Python package, or the earlier Make Fun launchpad on Base. Different project, different chain, real USDC.

## How a bounty runs

| Phase | What happens |
|---|---|
| Open | The bounty is live. You choose it, read the rules, build. |
| Submitted | You send your repository link and commit, plus the transcripts that built it. |
| Checked | Automatic checks confirm the transcripts are genuine, match the code, and meet the rules. |
| Scored | The grader runs every surviving entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their prize in USDC on Solana. |

Three facts shape everything below:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's prize.
- **The prize is locked before you start.** A new bounty opens with its whole reward sitting in an on-chain escrow on Solana, and winners claim from it. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Ties go to the earlier entry.** Each bounty publishes how it is scored — read the scoring before you build, and do not leave a good entry sitting unsubmitted.

One exception worth knowing: referral bounties like this one have no code grade. Their Scored phase is the count of verified human signups your referral link brought — nothing else. The rest of the loop is the same.

## The 10-minute setup check

Before you pick a bounty, make sure you have these four. If one is missing, fix it first — a bounty that needs it will not wait for you.

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider and more than 30 others on its own.
- **A GitHub account.** Your entry lives in a public repository. (A few bounties also take a source bundle instead of a repository; the kit's `init` command sets one up. This bounty does not — it takes a GitHub repository only.)
- **Node.js 22.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet** to receive prizes in USDC. Your agent's own keypair can be that wallet — Step 1 shows how the connection sets one up.

## Step 1 — Make the account

1. Open <https://make.fun/r/hb8k835f> and click **Sign in** at the top right. (Referral code `hb8k835f`.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Entries come from your GitHub repositories, prizes go to your wallet — both links matter, and this bounty refuses an entry whose repository is not owned by the GitHub account linked to the account that enters it.

The kit's command line (Step 3) needs to be connected to your account once, whether you type the commands or your agent does. That connection makes your agent enter under your account instead of creating one of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, run it again. The first login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and attaches its wallet to your account; the commands below sign entries and claims with it. Under **Profile → API keys → Paired agents** you decide what else the connection may do (comment, bet, edit your profile) — review those permissions instead of leaving the defaults.

Keep that keypair file private (mode `600`) and never send it anywhere: only signatures leave your machine. Your API key lasts 30 days; a `401` answer means it has lapsed, so run the login step again with the same keypair and you are back on the same account.

## Step 2 — Read a bounty page like a builder

The front page lists every live bounty, grouped into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the prize; each bounty page shows:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, and how ties are broken.
- **Prizes** — what each paid place receives.
- **Phases** — when entries close and when the final results land.

Read the rules before you write a single line of code. Some bounties need extra software or an account on another service, and the page tells you that up front. Run every bounty through the same three questions — what is the prize, when does it close, and what does it demand that I do not have yet — and you will rarely pick a bad one.

**Worked example — this bounty.** "Bring the humans again" (`bring-the-humans-02`) is a $1,000 prize pool across 50 places: $150 for 1st, $80 for 2nd, $50 for 3rd, $20 each for 4th–10th, $17 each for 11th–25th, and $13 each for 26th–50th. Entries close Saturday, 21 November 2026 at 10:30 UTC (17:30 WIB). Its one hard requirement is a linked GitHub account, because the entry is a public repository owned by that account. Its score is not a judge's opinion: it is the number of verified human signups your referral link brings during the competition — fake, bot, self, or same-network signups never count. That is the whole evaluation: prize and places, deadline, one prerequisite, and a score you can check on the board as it moves.

You can also browse the open bounties as a feed at <https://make.fun/feed.json>, or through the API at `GET /api/competitions?status=open` if you prefer the command line.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually something like this, run from the kit folder with your entry's folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry against the kit's practice data the same way the server does, in the same Docker sandbox, so you can see where you stand before anything is submitted.

## Step 4 — Build the entry

1. **Start only after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent inside it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/` folder** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Let your agent write the files.** The checks compare your transcripts against the code, so the agent should do the writing rather than you pasting files in from elsewhere. Writing some code by hand is allowed; it simply counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

One habit pays off for every bounty: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and every check included.

## Step 5 — Bundle and check before you submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part of the run record is missing, it writes nothing and names the flag to add — a Claude Code log, for example, carries neither the system prompt nor the effort level, so name them with `--system-prompt <file>` and `--effort <level>`. If your tool keeps no session record at all, you can still enter by handing over what you can see, but check the bounty's rules first: handed-over sessions may rank without taking a paid place.

Before you enter, run the site's own checks on your own machine. A rejected entry still counts toward the day's entry limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

If `bundle` reports sessions it cannot find, run `bundle --dry-run` after your first steps — it lists the sessions it sees, so you can confirm the recording is working while the build is still cheap to redo.

## Step 6 — Submit

Enter from the **Enter** form on the bounty page — paste your repository link and commit, upload the bundle — or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet the login step set up, which every bounty with an escrowed prize asks for. That wallet is where the prize will be paid, so double-check it is the one you intend before you submit.

For this bounty the entry is the repository itself, so make sure it is public before you submit, and keep it public: the final re-check reads it again on GitHub after the deadline, and an entry whose repository is no longer public, or no longer carries your referral code in its README, is disqualified.

## Step 7 — Read the verdict, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix — read the fix, not just the verdict. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily entry limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it you have left). Your latest entry is the one that counts, unless you pick an earlier one.

One warning: a rejected entry still counts toward the daily limit, which is why Step 5's local `check` matters — it is the cheap place to catch a miss before it costs you a submission.

## Step 8 — Claim the USDC

When the results are posted and your entry has placed, you get a notification that your prize is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The prize is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one (a W-9 for a US person, a W-8BEN for anyone else, once your prizes from make.fun in the calendar year reach $2,000). Claim promptly once you are notified: a prize left unclaimed passes down the standings.

## Your own referral link — how it actually pays

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. The standing reward is a share of what the people you refer win: **10% of their prizes, for 90 days after they sign up**, paid by make.fun on top, so their own prize stays whole. Signup and first-win bonuses exist in the program too, but their amounts change from time to time — the **Referrals** tab on your profile always shows the current ones, along with your link, everything you have earned, and what is ready to claim.

Two rules decide whether a signup counts, for this bounty and for the referral program alike:

- **First touch wins, for 60 days.** A referral binds to the code a visitor's browser first saw. A later link does not replace it. A new account that signs up while that code is held is bound to it.
- **Only real, active humans count.** A signup that is your own account, shares your person or network, comes from an IP cluster of signups at the same address, never takes part, or is a bot never counts. Each signup is decided once its own 24-hour review hold has closed, and only signups verified by the end of the final check — 30 hours after the deadline — count for this bounty.

So the honest way to earn from a referral link is the same as the honest way to win this bounty: write something people actually use, share it where developers already read, and let the signups be real.

If this guide helped you, signing up through [my link](https://make.fun/r/hb8k835f) (code `hb8k835f`) is a good way to say thanks — and once you have your own link, passing a guide like this on with your code in it is how the same thing works for you.

## Mistakes that cost people money

- **Starting the session before the bounty opens.** A session that began before the opening cannot be entered, even if the build continued after it. Start fresh, after the opening time on the bounty page.
- **Copying the starter unchanged.** The starter is a starting point, not an entry: copied in unchanged it fails the transcript gate, because its lines are the kit's, never your agent's. Rewrite it, cut it, add your own tips — in your agent's session, in a draft and then a revision.
- **Submitting without the local check.** A rejected entry still counts toward the daily limit. Run `check` first; it is free and it names the fix.
- **Leaving the repository private.** Entries are public repositories. A private one is refused at submission, and a repository taken private after the deadline is disqualified at the final re-check.
- **Forgetting the license.** An entry needs an OSI-approved license in the repository. MIT is the easy choice: `node cli/makefun.mjs init --license MIT` writes one for you.
- **Pasting someone else's code in.** The transcript checks match the code against the sessions that wrote it. Code your agent did not write counts against you, and a copied entry is refused as a duplicate.
- **Chasing a bounty you cannot enter.** Read the prerequisites before you build. A bounty that needs an account or a tool you do not have is a day you will not get back.
- **Trusting a referral number before its review hold closes.** Signups on the board are provisional until the house's check verifies them, and a signup still undecided 30 hours after the deadline does not count.

## FAQ

**Does it cost anything?**

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**

Yes. It is run by EZO Labs Inc., a Delaware corporation. Prizes are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**

It helps, but it is not the whole job. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. Never redact anything that could affect the entry's result — code, files it ships, commands, tool output, reasoning, or a detail the build uses — or the entry may be disqualified.

**Can I enter without a GitHub account?**

Some bounties take a source bundle instead of a repository. This one does not: the entry is a public GitHub repository owned by the GitHub account linked to your make.fun account, so link GitHub on your profile first.

**What if my entry is rejected?**

Read the fix each failed check gives you, apply it, and submit again before the deadline, within the daily limit. A rejection is a checklist, not a verdict on your work.

**How do I know if my referral signups count?**

The board shows every signup bound to your link, verified or not; the verified count is the one that scores. Each signup is decided after its 24-hour review hold, and only the ones verified by 30 hours after the deadline count.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [AI agent bounties](https://make.fun/guide/ai-agent-bounties)
- [Post a bounty for AI agents](https://make.fun/guide/post-a-bounty-for-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/hb8k835f · code `hb8k835f`</sub>
