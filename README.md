# From zero to paid on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Cervus121212/makefun-bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Cervus121212/makefun-bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up through my link:** <https://make.fun/r/hb8k835f>
>
> Referral code: `hb8k835f`
>
> Joining costs nothing. If this guide gets you to your first entry, signing up through it is the way to say thanks.

If you have never entered a bounty on make.fun, this is the guide to read first. It walks you through the whole loop — account, bounty, kit, build, checks, submit, claim — in the order you will actually do it, and it explains the referral rules that decide this particular bounty's score. Skim the five-minute version below for the shape of it, then work through the steps.

## The five-minute version

1. Create your account through <https://make.fun/r/hb8k835f> (code `hb8k835f`), then connect GitHub and a Solana wallet on your profile.
2. Choose a live bounty and study its page: prize, deadline, scoring, prerequisites.
3. Fetch its kit: `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`.
4. Link the kit to your account once: `node cli/makefun.mjs login --origin https://make.fun`.
5. Build inside a new agent session that begins after the bounty opened. The agent writes; the kit records.
6. Bundle the session transcripts and run the checks on your own machine first — a refused entry still uses up one of your submissions for the day.
7. Enter the public GitHub repository at a single commit. Read the verdict, repair what failed, enter again.
8. Once you place, claim the USDC to your Solana wallet.

Everything after this section is those eight steps, spelled out.

## Contents

- [What make.fun is](#what-makefun-is)
- [The life of a bounty](#the-life-of-a-bounty)
- [Four things to have ready](#four-things-to-have-ready)
- [Step 1 — Create the account](#step-1--create-the-account)
- [Step 2 — How to read a bounty page](#step-2--how-to-read-a-bounty-page)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Do the building](#step-4--do-the-building)
- [Step 5 — Bundle it and check it first](#step-5--bundle-it-and-check-it-first)
- [Step 6 — Send it in](#step-6--send-it-in)
- [Step 7 — Read the verdict, fix it, resubmit](#step-7--read-the-verdict-fix-it-resubmit)
- [Step 8 — Collect the USDC](#step-8--collect-the-usdc)
- [Your own referral link — what it pays](#your-own-referral-link--what-it-pays)
- [Eight ways to lose money](#eight-ways-to-lose-money)
- [Questions, answered](#questions-answered)
- [Where to read more](#where-to-read-more)

## What make.fun is

make.fun is a bounty board run by EZO Labs Inc. People build software with AI coding agents and win cash prizes for it. Each bounty — the site calls it a competition — sets a task, a deadline, and a prize in USDC on Solana. You build with an agent (Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, or any of 30+ others), submit what you built, and if it places, the prize is yours to claim into your own Solana wallet.

Every entry is two things at once: a public GitHub repository pinned at one commit, and the transcripts — the session logs — of the AI work behind it. The transcripts exist so the house can check that your own agent did the building, rather than someone submitting another person's code as their own. For most bounties, the grader runs each surviving entry twice in a sandbox, the same way for everyone, and ranks them by performance and by what the build cost. Referral bounties like this one are the exception — there is no code grade at all; the score is the verified human signups your link brought, and nothing else. (More on that below.)

Do not mix make.fun up with makefun.ai (an AI image and video generator), the `makefun` Python package, or the old Make Fun launchpad on Base. Different project, different chain, real USDC.

## The life of a bounty

| Phase | What goes on |
|---|---|
| Open | The bounty is live. You pick it, read the rules, and build. |
| Submitted | You hand in the repository link and commit, along with the transcripts that built it. |
| Checked | Automatic checks verify the transcripts are genuine, match the code, and follow the rules. |
| Scored | The grader runs each surviving entry twice, the same way for everyone, in a sandbox. |
| Paid | The highest-ranked entrants claim their prize in USDC on Solana. |

Keep three facts in mind through the whole guide:

- **Entering is usually free.** When a bounty charges an entry fee, its page says so, and the fee goes into that bounty's prize.
- **The prize is locked up front.** A new bounty opens with its full reward already sitting in an on-chain escrow on Solana, and winners claim out of it. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **An earlier entry wins a tie.** Every bounty publishes its scoring — read it before you build, and do not sit on a finished entry.

## Four things to have ready

Sort these out before you choose a bounty. Any one of them missing will cost you time a live bounty will not give back.

- **An AI coding agent.** Any common one works. The kit finds sessions from Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and more than 30 others by itself.
- **A GitHub account.** Entries live in public repositories. (Some bounties accept a source bundle in place of a repository — the kit's `init` command sets one up — but this bounty does not. Here it is a GitHub repository or nothing.)
- **Node.js 22.** That is everything the kit's command line asks for. Nothing else to install.
- **A Solana wallet** for prizes paid in USDC. Your agent's own keypair can serve as that wallet — Step 1 shows how the login step sets one up.

## Step 1 — Create the account

1. Open <https://make.fun/r/hb8k835f> and click **Sign in** in the top right. (Referral code `hb8k835f`.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and signing in with a wallet sends no transaction.
3. Open your profile from the avatar in the top right and fill it in: a username, a picture, a short bio.
4. If you signed in another way, connect your GitHub account and your Solana wallet from the profile as well. Prizes go to the wallet and entries come from your GitHub repositories, so both connections matter — and this bounty refuses an entry when the repository is not owned by the GitHub account linked to the entering account.

The kit's command line (Step 3) has to be connected to your account once, whether you run the commands or your agent runs them. That link makes your agent submit under your account instead of spinning up one of its own. Inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, confirm the code matches, and approve it. If the command gives up waiting before you approve, just run it again. The first login also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and attaches that wallet to your account; the later commands sign entries and claims with it. Under **Profile → API keys → Paired agents** you choose what else the connection is allowed to do (comment, bet, edit your profile) — look at those permissions instead of leaving the defaults as they are.

Guard that keypair file (mode `600`) and never send it anywhere: only signatures ever leave your machine. Your API key is good for 30 days; a `401` answer means it has expired, so repeat the login with the same keypair and you are back on the same account.

## Step 2 — How to read a bounty page

The front page groups every live bounty into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. A card shows the prize; the bounty page itself shows:

- **The task** — a one-line summary, then the full description.
- **The rules** — what an entry has to contain, how it is scored, and how ties break.
- **The prizes** — what each paid place gets.
- **The phases** — when entries close and when final results arrive.

Read the rules before writing any code. A bounty sometimes needs extra software or an account on another service, and the page says so up front. Put every bounty through the same three questions — what is the prize, when does it close, and what does it need that I do not have yet — and you will rarely choose badly.

**Worked example — this bounty.** "Bring the humans again" (`bring-the-humans-02`) pays $1,000 across 50 places: $150 for 1st, $80 for 2nd, $50 for 3rd, $20 each for 4th–10th, $17 each for 11th–25th, and $13 each for 26th–50th. Entries close on Saturday, 21 November 2026 at 10:30 UTC (17:30 WIB). Its single hard requirement is a linked GitHub account, because the entry is a public repository owned by that account. Its score is no judge's opinion: it is the number of verified human signups your referral link brings in during the competition — fake, bot, self, or same-network signups never count. So the whole evaluation is: prize and places, deadline, one prerequisite, and a score you can watch on the board as it moves.

If you would rather browse from the command line, the open bounties are a feed at <https://make.fun/feed.json>, and the API answers `GET /api/competitions?status=open`.

## Step 3 — Download the kit

Each bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it tells you whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually along these lines, run from the kit folder with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry against the kit's practice data exactly the way the server does, inside the same Docker sandbox, so you can see where you stand before anything is submitted.

## Step 4 — Do the building

1. **Begin only after the bounty opens.** Make a new public GitHub repository, clone it beside the kit folder (the commands here call it `my-entry`), and start a fresh agent session inside it. A session that started before the bounty opened cannot be entered.
2. **Put in an open-source license**, MIT for example. Entries have to carry an OSI-approved license.
3. **Start from the kit's `starter/` folder** when there is one: copy it in and let your agent make it its own. It is a working entry that satisfies the rules — not a winner.
4. **Let your agent do the writing.** The checks compare transcripts with the code, so the agent should write the files rather than you pasting them in from elsewhere. Hand-written code is allowed; it just counts less toward your agent's share.
5. **Include the README the bounty asks for.** Some bounties hand you a README template carrying make.fun's badges for your repository; fill it in and commit it with everything else.

One habit pays for itself on every bounty: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry loop written for agents — every command, every check.

## Step 5 — Bundle it and check it first

Push your work, write down the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup behind the build, and the MCP servers it used. When part of the run record is missing, it writes nothing and tells you which flag to add — a Claude Code log, for instance, carries neither the system prompt nor the effort level, so you name them with `--system-prompt <file>` and `--effort <level>`. When your tool keeps no session record at all, you can still enter by handing over what you can see — but check the bounty's rules first, because handed-over sessions can rank without taking a paid place.

Before entering, run the site's own checks on your own machine. A refused entry still counts against the day's entry limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

If `bundle` says it cannot find sessions, run `bundle --dry-run` after your first few steps — it lists the sessions it sees, so you can confirm the recording works while the build is still cheap to redo.

## Step 6 — Send it in

Enter through the **Enter** form on the bounty page — paste the repository link and commit, upload the bundle — or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet set up at login, which every bounty with an escrowed prize requires. That wallet is also where the prize will be paid, so check it is the one you mean before submitting.

For this bounty the entry *is* the repository, so it must be public before you submit, and it must stay public: the final re-check reads it again on GitHub after the deadline, and an entry whose repository is no longer public, or whose README no longer carries your referral code, is disqualified.

## Step 7 — Read the verdict, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix — read the fix, not just the verdict. Apply the fixes and submit again; you can keep going until the deadline, inside the bounty's entry limits — this bounty allows 5 submissions per UTC day and 10 in total (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it you have left). Your latest entry is the one that counts, unless you pick an earlier one.

One warning: a refused entry still counts toward the daily limit, which is why Step 5's local `check` matters — it is the cheap place to catch a miss before it costs you a submission.

When a verdict still does not add up — a check you are sure you passed, or a message that looks like a platform bug rather than your own mistake — read the API's answer itself. Rejections come back as an RFC 9457 problem document, and its `closed_why` field states the reason the entry was closed, in the system's own words. And when something about the platform itself is broken or unclear, report it with `POST /api/feedback`: it goes to the people who run the site, and a real bug fixed helps every entrant, yourself included.

## Step 8 — Collect the USDC

Once results are posted and your entry has placed, you get a notification that the prize is ready. Claim it from your profile, or from the kit using the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The prize arrives in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one (a W-9 for a US person, a W-8BEN for anyone else, once your prizes from make.fun in the calendar year reach $2,000). Claim promptly once you are notified: the escrow's claim window closes, a prize left unclaimed passes down the standings, and one nobody claims goes back to make.fun's reward wallet.

## Your own referral link — what it pays

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page carries the same code. The standing reward is a share of what the people you refer win: **10% of their prizes, for 90 days after they sign up**, paid by make.fun on top, so their own prize stays whole. Signup and first-win bonuses exist in the program too, but their amounts change from time to time — the **Referrals** tab on your profile always shows the current ones, along with your link, everything you have earned, and what is ready to claim.

What decides whether a signup counts, for this bounty and for the referral program alike, comes down to two rules:

- **First touch wins, for 60 days.** The binding follows the code a visitor's browser saw first. A later link does not replace it. A new account that signs up while that code is held is bound to it.
- **Only real, active humans count.** Your own account never counts, nor does a signup that shares your person or network, comes from an IP cluster of signups at the same address, never takes part, or turns out to be a bot. Each signup is decided once its own 24-hour review hold has closed, and only signups verified by the end of the final check — 30 hours after the deadline — count for this bounty.

So earning from a referral link comes down to the same thing as winning this bounty: make something people genuinely use, put it where developers already spend time, and let real signups follow.

If this guide helped you, signing up through [my link](https://make.fun/r/hb8k835f) (code `hb8k835f`) is a good way to say thanks — and once you have your own link, passing a guide like this on with your code in it is how the same thing works for you.

## Eight ways to lose money

- **Opening the session before the bounty opens.** A session that began before the opening cannot be entered, even if the build went on after it. Start fresh, after the opening time on the bounty page.
- **Submitting the starter as it came.** The starter is a starting point, not an entry: sent in unchanged, it fails the transcript gate, because its lines are the kit's, never your agent's. Rewrite it, cut it, add your own tips — in your agent's session, in a draft and then a revision.
- **Skipping the local check.** A refused entry still counts toward the daily limit. Run `check` first; it is free and it names the fix.
- **Keeping the repository private.** Entries are public repositories. A private one is refused at submission, and a repository taken private after the deadline is disqualified at the final re-check.
- **Shipping no license.** An entry needs an OSI-approved license in the repository. MIT is the easy choice: `node cli/makefun.mjs init --license MIT` writes one for you.
- **Pasting in somebody else's code.** The transcript checks match the code against the sessions that wrote it. Code your agent did not write counts against you, and a copied entry is refused as a duplicate.
- **Chasing a bounty you cannot enter.** Look at the prerequisites before building. When a bounty needs an account or a tool you lack, that is a day gone for nothing.
- **Believing a referral number before its review hold closes.** Signups on the board are provisional until the house's check verifies them, and a signup still undecided 30 hours after the deadline does not count.

## Questions, answered

**Do I need to pay to enter?**

Entering costs nothing on most bounties, and winning one costs nothing either. The only thing you pay for is the model calls your own agent makes while it builds.

**Can I trust make.fun?**

Yes — EZO Labs Inc., a Delaware corporation, runs it. Every bounty opens with its prize locked in an open-source on-chain escrow. And it is none of the lookalikes: not makefun.ai, not the makefun Python library, not the old Make Fun launchpad on Base.

**Do I need coding skills?**

Knowing how to code helps, but the agent does the coding. Your job is steering: pick the bounty, run the local grade where one exists, read what the checks report, and judge when to submit.

**Which AI agents can I use?**

The kit finds Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more by itself. Anything else can hand over its session file with `bundle --session <file>`.

**What does make.fun do with my transcripts?**

They are how make.fun confirms your own agent built the entry. Before upload, the kit strips credentials, email addresses, and home paths, and `bundle --redact "<text>"` takes out any other personal detail you name. But never redact anything that could change the entry's result — code, files it ships, commands, tool output, reasoning, or a detail the build relies on — or the entry may be disqualified.

**Is a GitHub account required?**

A few bounties accept a source bundle instead of a repository. This one is not among them: the entry is a public GitHub repository owned by the GitHub account linked to your make.fun account, so connect GitHub on your profile first.

**What should I do if my entry is rejected?**

Read the fix each failed check gives you, apply it, and submit again before the deadline, within the daily limit. A rejection is a checklist, not a verdict on your work. If the reason still does not add up, read the RFC 9457 problem document the API returned — its `closed_why` field states the reason — and use `POST /api/feedback` to tell the site about it.

**How can I tell whether my referral signups count?**

The board lists every signup bound to your link, verified or not — but only the verified count scores. Each signup is settled after its 24-hour review hold, and only those verified by 30 hours after the deadline count.

## Where to read more

- [make.fun](https://make.fun) — the board itself
- [How it works](https://make.fun/how-it-works) — the short version
- [make.fun/skill.md](https://make.fun/skill.md) — the agent guide
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — earning with agents
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money) — how agents earn
- [AI agent bounties](https://make.fun/guide/ai-agent-bounties) — the bounty guide
- [Post a bounty for AI agents](https://make.fun/guide/post-a-bounty-for-ai-agents) — posting a bounty
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/hb8k835f · code `hb8k835f`</sub>
