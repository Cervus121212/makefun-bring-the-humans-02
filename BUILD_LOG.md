# BUILD_LOG — bring-the-humans-02

Entry: tutorial README (getting-started guide) for make.fun, bounty
`bring-the-humans-02` ("Bring the humans again", $1,000, top 50 places,
entries close Sat 21 Nov 2026 10:30 UTC / 17:30 WIB, no fee).
Score = verified human signups through our referral link.

## Repo (local only — NOT pushed, NOT submitted)

- Path: `~/workspace/makefun/bring-the-humans-02/`
- Init: `node <kit>/cli/makefun.mjs init --license MIT --keypair <agent keypair>`
  - Anchor: `makefun anchor 427cce6d12f642894be20e652e26dc5ff15fe1b4 round 34065384`
  - Anchor wallet: `2LL4DixM2Q1GFfSoCzhpMfpGP519AABY61gQ9fQJqzZo`
  - Repo created 2026-11-18 10:58 UTC, after the bounty opened (10:30 UTC).
- Entry commit: `94ecb8560d5fea463fab0280ec56660dbcde1456`
  ("bring-the-humans-02: getting-started guide from zero to paid (referral hb8k835f)")
  - Files: README.md (265 lines, 21,808 bytes) + LICENSE (MIT, from init).
  - Tree clean after commit.
- This log: committed on top of the entry commit (see git log for its SHA).
  The entry commit above is the clean one to submit.

## What was built

README.md written from scratch, in my own words — draft first, then a
revision (2nd message) adding the clarification that referral bounties have
no code grade (Scored = verified signup count).

Structure (mine, not the starter's / hi5's):
title + 3 live badges + referral blockquote, "The 5-minute version",
Contents, What make.fun actually is, How a bounty runs, "The 10-minute
setup check", Steps 1–8 (account → pick a bounty → kit → build → bundle &
check → submit → verdict/fix/resubmit → claim), "Your own referral link —
how it actually pays", "Mistakes that cost people money" (8 failure modes),
FAQ, Links.

Referral: code `hb8k835f`, link `https://make.fun/r/hb8k835f` (verified via
`GET /api/me/referrals` — code + link match the API).

## Facts checked (not invented)

- Bounty facts from RULES.txt + competition.yaml: $1,000 / top 50,
  prizes 150/80/50/20/17/13, closes 21 Nov 10:30 UTC (17:30 WIB),
  max 5 submissions/day, 10 total, transcripts required, OSI license,
  repo created after opening, GitHub-repo entry only (no source bundle).
- Referral rewards from live API (`GET /api/me/referrals`):
  prize share **10% for 90 days**; signup_usd **0.00**, first_submission_usd
  **0.00**, signup_limit 20. The guide therefore quotes only the verified
  10%/90-day share and points readers to the Referrals tab for current
  signup/first-win amounts — it does NOT repeat the 0.25 USDC / 1.00 USDC
  figures (see comparison below).
- Referral rules from RULES.txt: first touch wins 60 days; only real active
  humans count (no self / same network / IP cluster / idle / lurker / bot);
  24-hour review hold per signup; final check ends 30h after deadline.
- Escrow: competition.yaml says `escrow: at_open` — guide says the prize is
  locked in on-chain escrow from opening (escrow code:
  github.com/makedotfun/prize-escrow).

## Tests (all pass)

| Test | Result |
|---|---|
| 3 badge lines, live (not in comment/code block), owner Cervus121212 / repo makefun-bring-the-humans-02 | PASS (lines 3–5) |
| Referral code present | PASS (6 mentions of `hb8k835f`, link in 5 places) |
| README ≤ 2 MB | PASS (21,808 bytes) |
| No `.github/README.md` | PASS (no .github dir) |
| Internal anchors resolve | PASS (15/15) |
| External links live | PASS (15/15 return 200; feed.json was 500 once, 200 on retry — transient) |
| Markdown renders (marked via npx) | PASS (h1, 17 h2, 3 badge imgs, 1 table, 8 code blocks; no placeholders) |
| No leftover placeholders | PASS (no `{{...}}`, TODO, FIXME; `XXXX-XXXX` is the literal code the CLI prints) |
| Read-through as a newcomer | PASS after revision — added the "no code grade" clarification, which the first draft's generic "grader runs every entry" table could have confused |

## Polish (revision after test)

One edit: added the paragraph after "How a bounty runs" clarifying that
referral bounties have no code grade. Re-tested after the edit (size,
anchors, render) — all still pass.

## Honest comparison with hi5's guide (hi5-study/hi5-bth02, 244 lines)

Where ours is better:
- Facts match the live API: hi5 quotes 0.25 USDC per signup (first 20) and
  1.00 USDC per first win; the live referrals API for our account shows
  0.00 for both right now, so our guide quotes only the verified 10% / 90-day
  share and sends readers to the Referrals tab for current amounts.
- "Mistakes that cost people money" (8 concrete failure modes) — hi5 has no
  equivalent section.
- "The 5-minute version" quick path + "The 10-minute setup check" up front —
  hi5 goes straight into sections.
- Explicitly states referral bounties have no code grade (Scored = signup
  count); hi5's phase table says the grader runs every entry twice without
  that exception (only their Step 2 example clarifies it).

Where hi5 is still better:
- Rejection handling is deeper: hi5 explains the RFC 9457 problem document
  and `closed_why`; ours only says "read the fix".
- hi5 covers filing feedback (`POST /api/feedback`) and the escrow
  challenge-window nuance in the claim step; ours mentions neither.
- hi5's prose is tighter in places; ours is ~20 lines longer for similar
  depth.

## Still to do (parent's part — NOT done here)

- Create the GitHub repo `Cervus121212/makefun-bring-the-humans-02` and push.
- Set repo About: website = https://make.fun/bounty/bring-the-humans-02,
  topic `makefun` (check repo_about).
- Take screenshot.png of the repo page on GitHub (README showing, top shows
  repo name + start of guide; ≤ 8 MB, ≤ 16,000,000 px) and commit it at root.
- Bundle transcripts + `check` + submit (repo-url form, no source bundle).
  Submission limits for this bounty: 5/day, 10 total.
- Note: r1 (bring-the-humans-01) scored 0 verified signups — this guide is a
  real tutorial, not an ad, so it has a better chance of moving humans.

## Rewrite in a Faizah-prompt session (provenance fix, 18 Nov 2026 ~18:46 WIB)

The kit-20 bundle refused the first build: its run record was handed-off
from a parent chain that never reached a session opened with Faizah's own
prompt. This session was opened with her verbatim order
("Bring the human02 ikutan, jangan asal2an submit. Pahami. Lalu submit"),
and the README was rewritten in it, so the parent chain is whole.

What changed in the rewrite (new commit on top of d7531c6; no `init` rerun,
anchor round 34065384 kept; screenshot.png untouched):
- README.md rewritten from scratch in-session: draft first, then two
  revision passes. Same verified facts (3 live badges, referral `hb8k835f`,
  $1,000 / top 50, 150/80/50/20/17/13, closes 21 Nov 10:30 UTC, 5/day +
  10 total, 10% / 90-day referral share, signup/first-win amounts NOT
  quoted — live API still shows $0.00 for both), reworded throughout.
- Added vs the first build: rejection answers as RFC 9457 problem
  documents (`closed_why`), reporting platform issues via
  `POST /api/feedback`, the escrow claim window closing on unclaimed
  prizes, and the explicit 5/day + 10 total limits in Step 7.
- Provenance check: 133 of 263 lines (50.6%) differ from the first
  version; of non-blank lines 133 of 174 (76.4%) are new/changed —
  comfortably above the 30% authored bar. Lines kept byte-identical on
  purpose: title + 3 badge lines + referral block (top 10 lines, so the
  committed screenshot.png still shows the README's start exactly),
  CLI commands, URLs, prize numbers.
- Tests re-run after the rewrite: 3 badges live (lines 3–5), referral
  `hb8k835f` ×6, 263 lines / 23,075 bytes (≤ 2 MB), no .github, 15/15
  internal anchors resolve, all real external links return 200,
  markdown renders (h1 ×1, h2 ×17, 3 badge imgs, 8 code blocks, 1 table),
  no placeholders, newcomer read-through done (two revision passes).
