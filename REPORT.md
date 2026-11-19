# Amazon SDE Online Assessment (HackerRank) — Research Report
### Current (2025–2026) format — a readiness and preparation guide

*Researched November 2026. No leaked actual assessment questions or answers are included. Problem names below are generic practice types / patterns only. One first-hand post found in research did paraphrase an actual problem — it is deliberately not reproduced here.*

**How to read the labels:** **[Official]** = Amazon (amazon.jobs / aboutamazon.com) or HackerRank Candidate Support. **[Reported]** = candidate reports / aggregators synthesising Reddit, LeetCode Discuss, Blind, Levels.fyi in 2026 — useful, but anecdotal and variable. **[Conflict]** = sources disagree; the invitation email / test landing page wins.

---

## 1-Page Executive Summary

**Trust the invite over every public prep page.** The current invite describes the *new* format: 100-minute Coding Challenge (Q1 traditional code-writing + Q2 code-repository with a built-in AI assistant), then ~15-minute Work Simulation on software-development decisions, then ~10 minutes of two Work Style Surveys, in one sitting, single monitor, latest Chrome/Edge, no outside help except the Q2 assistant.

That format is real and current, but Amazon's own public pages have not caught up:

- **Amazon officially announced it on 22 Jan 2026:** it had “reimagined our technical assessments” so candidates “work with an interactive AI assistant on a real coding platform,” mirroring how its SDEs use Amazon Q, Cline and Kiro for debugging/refactoring/testing. [Official — About Amazon, 22 Jan 2026: https://www.aboutamazon.com/news/workplace/artificial-intelligence-resume-jobs-hiring-amazon]
- **HackerRank's official Amazon OA guide confirms the mechanics:** two sections — Coding, then Project (Code Repository); *finish Coding first, you cannot go back*; you pick the repository framework *before* starting and *cannot switch once the test starts*; you pick the Coding language inside the test. [Official — HackerRank: https://candidatesupport.hackerrank.com/articles/1494260168-preparing-for-your-amazon-oa]
- **Amazon.jobs prep pages still describe the old format** (70 min / 2 coding problems + 60-min Work Simulation for new-grad/full-time; 90 min / 2 problems + system-design scenarios for SDE II) and never mention the AI repo task. Treat those pages as authoritative for *general* rules (timelines, Leadership Principles, code quality) and outdated for *section structure*. [Conflict — summarised in OphyAI, checked 3 Nov 2026: https://ophyai.com/amazon-oa ; Calibrd, checked Oct 2026: https://www.calibrd.com/interview-prep/amazon-interview]

**What decides the outcome, in practice:**

1. **Q1 is harder than old guides imply.** In the old two-problem format it was typically LeetCode Medium. In the new one-problem format, 2026 candidates consistently call the single remaining problem **Medium to Medium-Hard, ~40 minutes** — expect arrays/strings with hash maps, sliding window / two pointers, prefix sums, greedy, binary-search-on-answer, BFS/DFS on a grid/graph, heap, or a modest DP / string-partition DP. Partial credit is real (test cases), but a weak Q1 is not rescued by a strong Q2. [Reported — Nyrion, 31 threads to 31 Oct 2026: https://nyrion.ai/companies/amazon ; TakeUForward first-hand SDE II: https://takeuforward.org/community/interview-experiences/amazon-sde-2-oa-assessment-experience-rejected]
2. **Q2 (~60 minutes) is a throughput test, not an algorithms test.** Small multi-file web app, README = contract, ~6 failing tests (reports range 3–8), 2–4 broken behaviours named in a ticket — plus sometimes one bug *not* in the ticket, found only by reading failing tests. Bugs are shallow handler bugs: missing validation (500 instead of 400), missing existence check (no 404), modify-but-never-save, wrong route/path, wrong status/shape, case-sensitive search, wrong sort, wrong-type comparison. The assistant **navigates and explains; it usually refuses to write or apply the fix.** Candidates who lose do so by reading the whole codebase, picking an unfamiliar stack, or running out of clock — not because a bug was deep. [Reported — Nyrion; Bugnik, 22 Oct 2026: https://bugnik.com/guides/amazon-oa-code-repository-question]
3. **The behavioural ~25 minutes can sink a coding pass.** Work Simulation is scored against Amazon's 16 Leadership Principles (expert-model / effectiveness ratings); Work Style Surveys check LP-aligned preferences *and consistency* across reworded items. Multiple aggregators and first-hand reports show rejection after passing all repo tests. Do not click through these sections. [Reported/Official mix — see §3–4]

**Bottom line:** A candidate strong in JS/TS has a *structural advantage in Q2 if — and only if — they choose Node.js* and have rehearsed the README → run tests → trace route→handler→model → smallest fix → re-run loop tonight. Q1 is the risk. **Take it the next day only if the night before you can (a) complete the official HackerRank demo/sample for *both* formats, (b) solve 2 unseen Mediums in JS in ~40 min each with most test cases passing, and (c) fix 3 planted bugs in an unfamiliar small Express app in ~45 min. If any of those fail badly, use the rest of the 1-week window — the expected gain from 3–4 focused days outweighs any benefit of going a day early. Amazon hires on a rolling basis, but there is no reported bonus for submitting on day 1 vs day 5.** Full go/no-go checklist in §6.

---

## Findings

### 1. Coding Q1 (Traditional)

#### Format and timing — official
- Single-file problem in HackerRank's Monaco (VS Code-like) editor, multiple languages including JavaScript, autocomplete/IntelliSense. Most questions expect a *returned value*; `console.log` goes to Debug Output and does not affect score — but if a question expects printed output, remove debug prints before submitting, or it can fail. [Official — HackerRank Amazon guide, above]
- **Test cases: 2 sample + 13 hidden**, marked with a lock icon; hidden inputs/outputs are hidden, your output/debug logs are shown. Validation is exact string matching. If slow, optimise to avoid time-limit errors. [Official — HackerRank]
- “Save & Proceed” submits; you can revise *within the Coding section* until its timer runs out. **Once you switch to the Code Repository section, you cannot go back to Coding.** [Official — HackerRank]
- Amazon's general guidance (older pages, still the only official statement on quality): it assesses CS fundamentals, problem-solving approach, and **clarity, maintainability and efficiency of code**; for SDE II, efficient solutions earn more than brute force and code must compile. [Official via OphyAI/Calibrd summaries of amazon.jobs]

#### Time split within the 100 minutes — reported, treat as plan not guarantee
- Candidates in 2026 consistently report **~40 min Q1 / ~60 min Q2**, often as separately-timed parts. One aggregator recalls a candidate saying leftover Q1 time did **not** carry over — single-source, flag as anecdotal. [Reported — Bugnik; Calibrd; AceOffer synthesis of 198 reports, Oct 2025–Nov 2026: https://aceoffer.app/interviews/amazon/interview-process]
- **Practical implication:** do not plan to “borrow” Q2 time for Q1 or vice versa. Work to a hard 40-minute Q1 budget: at ~30 min, if no optimal path is in sight, lock in the best correct/brute-force version that passes samples, run it, and move on. Partial credit beats a perfect-but-unsubmitted idea — and you cannot return later.

#### Difficulty and topics
| Tier | Assessment |
|---|---|
| Old format (2 problems, 70–90 min) | Typically LeetCode **Medium**; first problem sometimes Easy-Medium, second Medium-Hard. [Reported — IGotAnOffer, updated 2 Oct 2026: https://igotanoffer.com/en/advice/amazon-online-assessment ; PapersAdda topic aggregation 2022–2025] |
| **New format (the invite, 1 problem, ~40 min)** | **Medium to Medium-Hard.** Nyrion: “it got harder, not easier… the old advice about Amazon OAs being easy is out of date.” A first-hand SDE II candidate rated his string/game problem Medium-Hard and ran out of time despite being close. [Reported — Nyrion; TakeUForward] |
| Hard / exotic | Rare in the OA itself (more a loop phenomenon). Do not spend tonight on Hard DP, advanced graphs (Dijkstra with complex state, union-find variants beyond basics), segment trees, or trie exotica at the expense of Medium fluency. |

**Most commonly reported topic clusters (2025–2026 candidate reports, convergent across sources):**
1. **Arrays / strings + hash map/set counting** — frequency maps, grouping, deduplication, subarray/substring conditions.
2. **Sliding window + two pointers** — longest/shortest substring or subarray under a constraint, container/pair problems.
3. **Prefix sums + binary search (incl. binary-search-on-answer / partitioning an array to minimise the largest part).**
4. **Greedy + sorting / intervals** — merge/sweep intervals, scheduling, lexicographically-best construction, monotonic stack in some reports.
5. **Graphs / grids: BFS, DFS, multi-source BFS** — shortest steps, spread/rotting-style propagation, connected components on a grid.
6. **Heaps / priority queues** — top-K, merging, streaming extremes.
7. **Modest DP** — 1-D partition/string DP, knapsack-like or job-scheduling DP; coordinate/segment problems reported occasionally.
8. **Simulation / rates** — process events in order, simulate a queue/machine/warehouse flow exactly as specified; careful reading beats cleverness.

Sources: Calibrd (Q1 topics: DP, two pointers, sliding window, prefix sums); PraxisAI (graphs, binary search, DP, array partitioning: https://www.praxisai.site/guides/amazon-ai-assisted-online-assessment); DevInterview/FinalRound syntheses (arrays, strings, hash maps, greedy favoured over exotic DP). Topic-frequency percentages circulating on some blogs (e.g. “arrays 76%”) are **unverifiable estimates from candidate-report scraping — do not treat them as data.**

**Amazon flavour:** problems are usually wrapped in a logistics/operations story — warehouse/delivery/grid placement, drone/delivery routes, merging shipments, server/request rates, inventory, returns — but the underlying pattern is a standard one above. The skill is *stripping the story*: rewrite inputs/outputs in plain terms, note constraints, identify the pattern before coding. Long statements and large constraints are a signal the intended solution is O(n log n) or O(n), not O(n²).

#### Scoring: hidden tests, partial credit, code quality
- **Hidden tests dominate.** HackerRank scores by test cases passed, including hidden ones, so **partial credit is possible** and a brute force passing some cases beats nothing. [Official platform behaviour via HackerRank + OphyAI summary]
- **Visible/sample tests prove almost nothing** — 2 samples only check basic logic. Always self-test: empty/minimum input, single element, duplicates, already-sorted/reverse, max-constraint performance shape, negative/zero if allowed.
- **Efficiency matters in two ways:** (i) directly — slow code fails hidden performance/edge cases with time-limit errors [Official — HackerRank]; (ii) per Amazon, optimised solutions earn more than brute force [Official — amazon.jobs via secondary summaries]. No passing score / threshold is published by Amazon, and reports conflict on cut-offs — some candidates advanced with 4–5/6 on Q2, others were rejected with full repo marks (Q1 and/or behavioural sections presumably decided it). Treat “% needed to pass” claims on prep sites as **anecdotal / invented — unverified**.
- **Does explaining complexity / code quality matter in Q1?** There is no interviewer and no reported free-text complexity question in this OA format. Automated scoring is test-case based. Clean names, a helper function where it clarifies, and a 1-line comment on a non-obvious invariant are cheap insurance *if* any human/code-quality review occurs (Amazon says clarity/maintainability are assessed generally), but **do not spend timed minutes writing an essay or complexity analysis** — one anecdote of a candidate advancing after leaving an “how I'd improve it” comment is single-source and low-weight. [Reported anecdote via IGotAnOffer; Official general statement via amazon.jobs]

**Q1 workflow (40 min):** 0–5 read + restate + constraints + brute force in head · 5–10 pick pattern, sanity-check on sample by hand · 10–30 code optimal-or-better · 30–35 run samples + your own edge cases, fix · 35–40 optimise the obvious bottleneck or lock in partial credit and Save & Proceed.

---

### 2. Coding Q2 (Repo + AI Assistant)

#### What it actually is — official + reported
- **Official (HackerRank):** Multi-file, real-world problem in a full browser VS Code IDE. Same repo for all tasks in the question. Example scaffold given by HackerRank: a React app or Express server; tasks such as “fix a bug on the Customer dashboard” and “add a feature to check whether Express delivery is available.” IDE autosaves; click Submit / Save & Proceed; you can revise and resubmit as often as you like until time ends; if time elapses you are logged out and **the most recent auto-saved version is evaluated**. Run Tests runs a predefined set per task, showing passes/failures with errors/assertions and debug output. Do **not** modify `README.md` / read-only files, and do not modify IDs/classes of existing UI elements (tests depend on them). A live preview may be available. [Official — HackerRank]
- **Reported shape (convergent):** README states the API/app contract. A short ticket names **2–4 broken behaviours**; test suite has **~6 tests** (range reported 3–8). Most tasks are **bug-fixing**; some are **feature-building / finish a missing piece** — HackerRank itself lists exactly those two task kinds. Domains rotate (movie/watchlist, issue tracker, wallet/bank transactions, loan, car rental, blog/comments, returns engine — domain is irrelevant, handler shape is constant). [Reported — HackerRank task taxonomy + Nyrion/Bugnik/IGotAnOffer]

#### Bug / task types to expect (patterns, not leaked questions)
Validate body → 400 not 500 · lookup missing → 404 · permission/auth check missing → 401/403 handling · mutate-but-never-persist (missing save/update call) · wrong route/path or method registration · wrong response status or response shape/field name · duplicate check comparing wrong type / wrong field · search filter missing (e.g. unpublished excluded), case-sensitivity, wrong sort direction · validation rule off (length/format) · frontend: page showing wrong user's / wrong filtered data because the API/query is wrong — fix the API layer first.

#### Language / framework choice — locks
- **Official:** “Open the test invite and select the framework you want for the Code Repository section… **Once the test starts, you cannot switch the frameworks.** You can select the language for the Coding section inside the test.” [Official — HackerRank]
- **Reported options:** Node.js (MERN / Express + MongoDB), Java + Spring Boot, Python + Django, and C++ in at least some reports; Flask mentioned in one synthesis. Lists vary by role/cycle — **the list in *your* invite/demo is the only authoritative one.** [Reported — Bugnik; IGotAnOffer; Nyrion]
- **Recommendation: choose Node.js if that is your daily stack.** It is the only stack matching senior JS/TS daily work. Candidates who picked Spring Boot without daily Spring fluency report losing most of the hour to framework friction and finishing 2/6. Pick the stack you can *read and debug blind*, not the most impressive-sounding. [Reported — Nyrion]

#### The AI assistant — what it will and won't do
- **Official (HackerRank):** Built into the repo IDE (preview pane). “Provides contextual and coding guidance, **without providing the full solution**.” Capabilities listed: understand codebase (ask about files/functions), navigate project (where to make changes), debug errors (share terminal errors), platform support, syntax help (may suggest templates/syntax you can Apply at cursor). **Optional; you will not be penalised for using it; interactions are not considered in your score — but the conversation is recorded and the transcript is visible to your evaluator.** GenAI is **not permitted in the Coding (Q1) section** — assistant is repo-only. [Official — HackerRank]
- **Reported experience:** closer to a *librarian/navigator* than Cursor. It will say which file handles a route, explain a block, say what a test checks. Ask it to fix the bug / edit the file and it usually **declines**; narrow questions about one specific error occasionally yielded a hint/corrected snippet (2 reports). Some found it slow, misleading, or limited to the open file. **Verify everything it says by running tests.** [Reported — Nyrion; TakeUForward (“AI was blocked from providing any solutions, but could help with basic analysis”)]
- **Do not confuse this with HackerRank's newer Chakra/ADE interview product**, where Agent Mode *can* edit files — that is a different product/configuration. Amazon OA reports show a guarded, non-editing assistant. Plan to write every fix yourself.

#### Best workflow / prompting strategy (reported + official guidance)
```
0–5   Read README fully. Run Tests BEFORE touching code. Failing test names = your map.
5–10  If it doesn't build/install: fix that first (compiler names file/line).
      Ask assistant ONLY for orientation: "Which file/route handles X?" "What does [function] do?"
10–45 One failing test at a time: read the test → trace route → controller/handler →
      service → model/repository/helper → find the line that disagrees with README →
      smallest possible fix → Run ALL tests (not just that one).
45–55 Visible tests green? Re-read README rules; check edges it mentions:
      boundaries, empty/missing fields, duplicates, wrong-user, error codes.
      Hunt the unlisted bug in any still-failing / suspicious test.
55–60 Final full Run Tests. Confirm last change saved. Submit.
```
Prompting rules: ask **where / what / why-this-error**, never “fix it”; paste the *exact* error + failing test name; ask about one file/function at a time; never wait on the assistant — keep tracing while it answers; never Apply a syntax suggestion you don't understand.

#### Time vs Q1
Q2 gets the larger share (~60 of 100) and, for an experienced web engineer, is usually the *more bankable* share — bugs are shallow, partial credit per test is real (reports of advancing at 4–5/6). Its difficulty is throughput in an unfamiliar browser IDE. Budget **~10 minutes per bug/test** as your pace check: if you're at minute 30 with 0–1 tests green, stop deep-diving, triage the cheapest-looking failures first.

---

### 3. Work Simulation (~15 min in the invite)

#### What it looks like
- **General official description:** a simulated day in the role — emails, videos and chat/IM messages from virtual managers/teammates, plus supporting materials (wikis, code snippets, roadmaps). For each scenario you **rate 4–5 possible responses for effectiveness, or pick the best one**. Amazon says to actually open the work materials before rating. [Official via Verve/OphyAI summaries of amazon.jobs: https://www.vervecopilot.com/hot-blogs/amazon-online-assessment-design]
- **The invite's variant (SDE, ~15 min, software-development decisions):** 2026 reports matching this timing describe a *shorter, design/decision-focused* version — e.g. **3 scenarios, ~8 tasks**, each action rated individually on a 5-step effectiveness scale, plus occasional priority ratings (Low / High / Essential). **Warning:** several candidates say the *quoted* 15 minutes understated reality — one needed ~40; others found the (longer, new-grad) simulation untimed in practice and finished in ~15. **Do not assume you can rush it in 15; block 30–45 minutes of your sitting for it.** Check the rating-scale direction before your first answer — one report warns it's easy to read backwards. [Reported/Conflict — Inbyte; AceOffer; TakeUForward (15-min simulation, simulated texts/emails, choose action)]
- The SDE II public page's “system design scenarios” (rate most/least effective actions, no whiteboard/diagrams, concepts: maintainability, trade-offs, ambiguity) appear to be the *same family* of exercise described under a different name/timing — another reason public pages and invites diverge in wording. [Official via secondary summaries]

#### How it's scored
Amazon does not publish the rubric. Secondary/prep sources describe scoring against an **expert model** (the key developed from high-performing Amazon managers): most-effective gets full marks, least-effective zero, intermediates partial — treat the mechanism as plausible-but-unverified; the *direction* (LP-aligned judgement, graded not binary) is consistent across sources. What is official: the simulation measures Leadership Principles. [Official principle + Reported mechanism — CareerTestPrep synthesis]

#### Leadership Principles most directly tested here
All 16 can appear and no source credibly shows a weighting, so don't study a shortlist only — but in SDE decision scenarios these recur most: **Customer Obsession, Ownership, Bias for Action, Dive Deep, Are Right A Lot, Earn Trust, Have Backbone; Disagree and Commit, Insist on the Highest Standards, Deliver Results, Invent and Simplify, Think Big.** Full official list (16): Customer Obsession; Ownership; Invent and Simplify; Are Right, A Lot; Learn and Be Curious; Hire and Develop the Best; Insist on the Highest Standards; Think Big; Bias for Action; Frugality; Earn Trust; Dive Deep; Have Backbone, Disagree and Commit; Deliver Results; Strive to be Earth's Best Employer; Success and Scale Bring Broad Responsibility. (Any source listing 14 is pre-July 2021 and outdated.)

#### Answer patterns: what scores well vs poorly (with trade-offs)
| Dilemma | Scores well (rate high) | Scores poorly (rate low) |
|---|---|---|
| Deadline slips / dependency late | Own it early: tell manager/PM promptly *with* impact, options (de-scope, feature-flag, phased rollout) and a revised plan; protect the customer launch | Hide it / quietly work overtime hoping; surprise stakeholders at the deadline; escalate to a director/senior leadership demanding the other team re-prioritise |
| Deadline vs quality / shortcut | Ship the safe subset on time; flag/gate the risky part; document the trade-off. “Disagree and commit” once a decision is made | Ship known-broken code to hit the date; cut a correctness/security corner silently; refuse to commit after losing the argument |
| Own vs escalate | Handle what is within your scope/authority yourself; escalate *with data, a recommendation, and what you've already tried* when it's genuinely above scope or cross-team | Escalate a decision that is yours to a VP/manager to decide for you (fails Ownership — repeatedly flagged); never escalate anything, even a customer/legal risk |
| Data vs anecdote | Dive Deep: check the dashboard/logs/code/wiki provided *in the scenario materials* before deciding; if metrics and anecdote differ, investigate both; decide on the best available data when time is short | Decide on gut / single anecdote / HiPPO; analysis-paralysis — demand perfect data while a customer issue burns (fails Bias for Action) |
| Customer issue | Customer Obsession first: mitigate customer impact now, root-cause second, follow up in writing; long-term fix over short-term optics | Blame another team/customer; prioritise internal convenience or a metric over a clear customer harm |
| Disagreement / bad plan from peer or manager | Have Backbone: raise the concern directly, with data, to the decision-maker; propose an alternative; then commit | Stay silent to keep the peace; go around the person / undermine after the meeting; agree publicly, sabotage privately |
| Ambiguous task | Ask clarifying questions *and* propose a plan in parallel; pull in the right person directly; make assumptions explicit | Wait passively for perfect instructions; guess silently on a high-blast-radius change; broadcast to everyone instead of the owner |
| Teammate underperforming / conflict | Address directly, promptly, privately, with specifics and support; involve manager with facts if it persists | Ignore it; complain to peers; public criticism; do their work silently forever (fails Ownership + Earn Trust) |

Heuristic that covers most items: **Rate highest the option that (1) protects the customer, (2) is owned by *you*, (3) acts promptly, (4) is based on the data/materials given, and (5) communicates early and in writing. Rate lowest anything that hides, blames, defers ownership upward, cuts a hidden corner, or waits.**

---

### 4. Work Style Surveys (~10 min in the invite — two surveys)

- **What they are:** Forced-choice / rating items built around the 16 Leadership Principles. Typical format: two statements side-by-side — pick which is more/most like you (sometimes most *and* least), on a “Most like me / More like me” scale with **no neutral middle**; some versions use Likert agreement ratings. Examples of the *kind* of pair (from prep guides, not leaked items): “I like things clearly structured” vs “I look forward to learning new things.” The invite's “two surveys” matches July 2026 reports of ~15 single-answer items + ~35 forced-choice pairs — which took that candidate 25–30 min despite a ~10-min quote, so again budget more time than the label. [Reported — IGotAnOffer; Inbyte]
- **What they measure:** Whether your *work preferences* pattern-match LP-aligned behaviour (ownership, customer focus, bias for action, learning, high standards, trust) — profile fit, not knowledge. Amazon's own line (via summaries) is that Workstyles needs no practice and to answer as the authentic you / don't overthink.
- **Are there “right” answers?** Not in the maths sense — there is no single key per item, because pairs often pit two desirable traits against each other. But there *is* a coherent vs incoherent profile: sources converge that scoring compares your pattern to LP-aligned profiles. Claims of a secret answer key, or that “every item has one Amazon-correct side,” are prep-site marketing — **unverified**.
- **Consistency traps — the real risk:** the same trait returns several times in different wording / paired against different alternatives. Inconsistent choices (endorsing both “I decide fast on available data” and later “I always wait for complete data” as *most* like you), extreme/social-desirability inflation (claiming the most flattering extreme on everything), and answering as an idealised “Amazonian” rather than your actual work self produce contradictions that are detectable. This consistency inference is reported by multiple independent guides; Amazon does not publish the scoring algorithm, so treat the exact penalty as unknown. [Reported — DesignGurus/MakingMoves/PracticeTestGeeks syntheses]
- **Honest-but-strategic approach:** (1) Read the 16 LPs once tonight so the vocabulary isn't new. (2) Answer as **yourself at work on a good day** — first instinct, a few seconds per item, don't deliberate. (3) When two good traits collide, pick the one that is *truly more characteristic of you* — that's what keeps reworded repeats consistent. (4) Never pick a statement endorsing dishonesty, blame, passivity, or “not my job” as most-like-you if it isn't — and if it is, no survey strategy fixes the underlying fit question. (5) Keep a steady pace; don't reverse your philosophy halfway through.

---

### 5. Logistics & Rules

**The invite controls.** Below separates what is official/platform-standard from what varies.

#### Setup (official / invite)
- Latest Chrome/Edge (HackerRank also lists Firefox; Safari 16.4+ — but follow the invite: Chrome/Edge), **disable browser extensions**, enable third-party cookies, stable network (HackerRank “good” = ~10 Mbps). Repo IDE initialisation can take up to a minute and is **not** counted in test time. Watch the instructional video and do the sample test *before* Start. [Official — HackerRank]
- **Single monitor** per the invite. HackerRank Secure Mode (when enabled by the employer) enforces full-screen, single monitor, and blocks external paste — whether Amazon enabled each add-on for *your* test is not published, so comply with the strictest reading of the invite. [Platform — HackerRank via OphyAI/Cohesyve]

#### Proctoring / monitoring — what is actually tracked
- **Amazon (official, via summaries):** browser usage is **logged** during the coding assessment; **using Print Screen may terminate your session / lock you out**; avoid copy-pasting; parts of the OA need a **webcam** (takes your picture); candidates in **North America need a student/government photo ID**. Some student-page summaries add: you may use publicly accessible online resources but not login-gated sites, and your code must be your own — wording varies by page/version, and the invite's “no external assistance/resources except the Q2 AI assistant” is stricter and therefore the rule to follow. [Official via OphyAI/Nyrion summaries — Conflict on the “public resources” line vs invite; invite wins]
- **HackerRank default (every test):** copy-paste tracking (pasted content appears in the report), tab/focus tracking (frequency + duration away), and MOSS code-similarity comparison with other submissions. Optional employer add-ons: AI plagiarism detection, periodic webcam image proctoring, Secure Mode, Proctor Mode (screen recording + AI review), Desktop App mode (blocks AI apps/VMs). Amazon does not say which add-ons it turns on. [Platform — HackerRank via OphyAI/HackerRank-test guide, checked 3 Nov 2026: https://ophyai.com/hackerrank-test]
- **Candidate reports conflict on webcam:** Oct 2026 reports describe webcam + face snapshot + ID photo before start; Apr–Aug reports (and one systems-track report) describe no camera / no browser lock, only a paste warning. **Conclusion: proctoring is configured per req/level/track. Assume webcam + screen + ID are on; be pleasantly surprised if not.** [Conflict — Inbyte]
- **AI assistant transcript** is recorded and visible to the evaluator (not scored) — write prompts as if a hiring manager will read them, because one may. [Official — HackerRank]

#### What counts as a violation
Using any outside AI/person/website/device in Q1 or outside the built-in assistant in Q2; having another person help; copying code (MOSS + paste logs); leaving/switching tabs repeatedly; Print Screen; a second monitor; impersonation / ID mismatch. Business Insider (Feb 2025, via summaries) reported Amazon's internal guidance that undisclosed generative-AI use in interviews can disqualify — consistent with the invite rule. A plagiarism *flag* is reportedly surfaced to the hiring team for a human decision, not an automatic fail — single-source, don't rely on leniency. **This report provides no instructions for evading any of this; several sites found in research actively market cheating overlays — they were not followed and must not be used (see note in Sources).**

#### Technical issues
- **HackerRank FAQ (official):** if you lose internet, submitted work is saved, **the timer keeps running while offline**, the test ends at the scheduled time even if disconnected; you can log back in and continue *if time remains*. **Logging out ends your attempt immediately — never log out.** For in-test issues use the **? → Report a problem** control. HackerRank cannot extend time, reschedule, or share results — **the recruiter/hiring company decides** whether to extend or re-invite. [Official — HackerRank FAQ: https://candidatesupport.hackerrank.com/articles/2859650598-frequently-asked-questions-during-the-test]
- Practical: wired connection if possible, charger plugged in, notifications off, nothing else running, phone away (not as a second screen). If something breaks: note the time/error, use Report a problem *in the test*, reconnect fast, and email the recruiter contact from the invite *the same day* with facts — do not start a second attempt/browser unless the recruiter authorises it.

#### Results, validity, cooldown, reuse
- **No published passing score; HackerRank does not send scores to candidates** — Amazon owns the report and decides what to share. [Platform/Official]
- **Timing:** SDE II official line (via summaries): notified **within 2 days** of completing, and a passed loop outcome within 5 business days. Candidate reality ranges from **next day to ~2 weeks** (manual review / volume); a first-hand SDE II rejection arrived at 2 days; check spam; for multi-part OAs, contact Amazon if no completion email within 24 hours of a part, and **complete the final feedback survey — skipping it reportedly delays results**. [Official + Reported — IGotAnOffer; OphyAI; TakeUForward]
- **Cooldown if you fail:** SDE II official line: **encouraged to reapply in 6 months.** For university/new-grad OAs **no retake rule is published** and candidate reports conflict (some told 6 months, some no cooldown). There is **no self-serve retake** on HackerRank — only a recruiter re-invite. Candidates should ask their recruiter if their level isn't SDE II. [Official for SDE II; Conflict otherwise]
- **Reuse across roles:** SDE II official line: **one OA result counts for several SDE II roles** — you should not need to re-sit for every SDE II application. For SDE I/intern, candidates report a second related job ID showing “assessment already completed,” but that's candidate-reported, not a universal policy; hiring decisions still stay per-requisition. **No published validity period (e.g. “valid 6/12 months”) was found for the SDE OA score itself** — do not assume a CodeSignal-style 180-day rule applies. [Official for SDE II via Calibrd; Reported for SDE I]
- **Deadline:** typically **7 days from send date** to complete (SDE II official; most other tracks report ~a week). Missed deadlines generally cannot be extended per Amazon's general assessments page, though the university page suggests contacting Amazon *before* the deadline for special circumstances — if you need the full week, that's normal and expected; don't ask for an extension you don't need, and don't let the link expire silently.

---

### 6. Readiness — Cram Plan for a JavaScript/TypeScript Candidate (not a daily LeetCode grinder)

#### Edge and gap — honestly
- **Edge (for web/JS candidates):** Q2 in Node (Express routing/middleware, REST status codes, async handlers, data-layer saves) is everyday web work. Work Simulation rewards sound engineering judgement (trade-offs, escalation, ownership).
- **Gap:** Q1 pattern-recognition *speed* in vanilla JS under a 40-min clock, and JS-specific traps: `Array.sort()` is lexicographic without `(a,b)=>a-b`; `Map/Set` iteration; no built-in heap or deque in JS (implement a simple binary heap / use index-pointer queue — don't slice-shift a BFS queue on large inputs); string immutability costs; integer/precision assumptions.
- **Therefore tonight is not “learn DP.” Tonight is: (1) demo fluency, (2) pattern templates in JS, (3) one timed repo drill, (4) LPs skim. In that order.**

#### Prioritised topic checklist (in order — stop when time runs out)
- [ ] **P0 — Hash map/set + sliding window + two pointers + prefix sums.** Templates you can type from memory in JS.
- [ ] **P0 — Sorting + intervals/greedy** (sort by start, sweep, merge; sort + two pointers).
- [ ] **P0 — BFS/DFS on grid/array graph** (directions array, visited, queue with index pointer; multi-source BFS = seed all sources at distance 0).
- [ ] **P1 — Binary search** (classic + “smallest value such that feasible(x)” on-answer template).
- [ ] **P1 — Stack** (matching, monotonic stack idea) and **heap** (write a minimal MinHeap class once tonight; top-K pattern).
- [ ] **P1 — Node/Express handler shape** (route → validate → lookup/404 → auth/permission → mutate → **save** → status/shape) + status codes 200/201/400/401/403/404/500.
- [ ] **P2 — 1-D DP** (climb/partition/min-cost recurrence shape) — recognition only; don't sink hours here.
- [ ] **Skip tonight:** advanced DP, Dijkstra/union-find deep dives, segment trees, complex string algorithms, system-design study (not in the invite's Work Sim description beyond decision rating).

#### Specific practice problem *types* (generic LeetCode-style types — not leaked questions)
Do **one of each, timed, in JavaScript, in a plain editor** — breadth of first-recognition beats depth tonight:
1. Longest substring without repeating characters (sliding window + Map) — Medium
2. Two-sum / subarray-sum-equals-K family (hash map / prefix sum) — Easy/Medium
3. Merge intervals + meeting-rooms-style sweep (sort + greedy) — Medium
4. Grid BFS shortest path / rotting-spread multi-source BFS — Medium
5. Top-K frequent / K-closest (heap or sort fallback) — Medium
6. Binary-search-on-answer: split array / capacity-to-ship style — Medium
7. Container / pair with sorted two pointers — Medium
8. Valid parentheses + monotonic-stack “next greater” — Easy/Medium
9. A string/array 1-D DP partition or min-cost — Medium (stretch only)

#### How to use Amazon's official HackerRank demo / practice test effectively (do this FIRST tonight, ~30–40 min)
Per HackerRank/Amazon: take the sample/practice test linked from the invite, watch the instructional video, and — if a separate repo-format practice is offered — take that too. The Amazon practice test has **2 questions, is not scored, and does not affect the outcome**; the sample coding challenge can be repeated. [Official — HackerRank (“strongly recommend… try the sample test before you begin”); Amazon practice via OphyAI/IGotAnOffer]
Use it as a **systems check, not a knowledge test**:
1. Confirm your **framework choice = Node.js** and practise the exact selection step (it locks — rehearse choosing correctly).
2. In Q1 demo: set language to JavaScript/Node, find Run, custom test input, Debug Output, Save & Proceed. Type your sort/Map templates once to check autocomplete behaviour.
3. In Q2 demo: find README, file explorer, terminal, **Run Tests**, preview, debugger, and the **AI Assistant panel**. Practise asking it an orientation question (“which file handles X?”) and see how it refuses/limits a “write the fix” request — so the real behaviour isn't a surprise.
4. Confirm: timer display (is it 100 total or 40/60 split on *your* landing page?), the cannot-go-back warning, webcam/ID/system-check steps, single-monitor behaviour, and what the final Submit/confirmation looks like.
5. Verify Chrome/Edge version, extensions disabled, cookies allowed, webcam/mic, ID ready, speed test.
*If the demo reveals a stack list or timer different from the invite email, believe the demo/landing page for mechanics and email the recruiter only if they directly contradict each other.*

#### Evening-before + morning-of schedule (~12–18 h window; assumes an evening start, test the following morning at the earliest sensible hour)
**Tonight ( ~3.5–4 h max, then stop — sleep is a performance input):**
| Block | Time | Do |
|---|---|---|
| 1 | 35 min | Official demo/sample for both formats (checklist above). Write down timer split + framework list. |
| 2 | 80 min | Timed Q1 reps: 2 × 40-min Mediums from types 1–6 above, in JS, no AI, no notes. Review *only* the pattern you missed after each. |
| 3 | 60 min | Repo drill: clone/find a tiny Express app you didn't write (or use a practice repo task), plant or find 3 bugs (remove a save, break a status code, drop a validation), then fix from failing tests in ≤45 min using the §2 workflow. If no repo handy: trace one open-source Express example route→handler→model on paper and rehearse status-code table. |
| 4 | 25 min | Read the 16 LPs (official list). Read §3 table above once. No story-writing — that's for the loop, not the OA. |
| 5 | 10 min | Lay out logistics: ID, charger, wired net if possible, single monitor (disconnect others tonight), quiet room booked, water, test-time chosen. **Stop. Sleep.** |

**Morning of the assessment (if going ahead):**
| When | Do |
|---|---|
| Wake – T-2h | Normal routine, food, no new topics. |
| T-90 min | 20-min warm-up only: re-type (don't just read) sliding-window, BFS, binary-search-on-answer, and MinHeap skeletons in JS; re-read the handler-shape sequence for Q2. |
| T-60 min | Light re-check: browser, extensions off, other apps/monitors off, webcam, ID, network. Close everything else. |
| T-15 min | Bathroom, water, notifications off. Re-read your one-line plans: Q1 hard-stop at ~40; Q2 README→tests first; Work Sim scale-direction check; Work Style first-instinct consistency. |
| Start | Start only when you can give the *full* sitting uninterrupted (~2–2.5 h elapsed including simulation/surveys overrunning their labels). |

#### Go / No-Go signals
**GO the next day if ALL are true:**
- ✅ Demo completed for both formats; you know where Run Tests / AI panel / Submit are, and you've confirmed Node.js as your repo choice.
- ✅ Tonight's 2 timed Mediums: at least one fully passing (samples + your edge cases) within 40 min, and the other at least a correct brute-force / majority-of-cases solution within 40 min.
- ✅ Repo drill: ≥3 bugs fixed from test failures within ~45–60 min without needing framework documentation.
- ✅ You can type the P0 templates (hash/sliding window, BFS, sort-merge) in JS without looking them up, including numeric sort comparator.
- ✅ You're rested, healthy, have a quiet single-monitor setup for the full sitting, and no foreseeable interruption.

**WAIT (use days 3–6 of the 1-week window) if ANY are true:**
- ❌ You haven't run the demo, or the demo's IDE/framework selection confused you for >15 min.
- ❌ Both timed Mediums timed out with no working solution — 3–4 days of pattern reps is the highest-value intervention available to you, far larger than any day-1 advantage.
- ❌ The repo drill showed you can't trace an Express request flow or don't know the 400/404/save/status basics in Node — fixable in 1–2 evenings of handler drills, fatal if discovered in the real Q2.
- ❌ You're ill, severely sleep-deprived, travelling, or can't secure a quiet single-monitor block — a disrupted sitting (timer keeps running through outages) is worse than a later clean one.
- ❌ You were counting on outside resources/AI in Q1 — that plan is both prohibited and monitored; rebuild the plan around unaided Q1 before starting.

**Middle path (often optimal):** if Q1 reps were borderline but Q2 drill was strong, take **2 extra days**: Day A = 6–8 timed Mediums across P0/P1 only; Day B = one full mock (40-min Medium + 60-min repo drill back-to-back, no pause, no return to Q1) + LP re-read. Then sit on day 3–4, leaving buffer days for a technical-issue/re-invite contingency before the deadline.

---

## Could Not Verify
- **Exact pass threshold / section weightings** (Q1 vs Q2 vs Work Sim vs Work Style). Amazon publishes none; prep-site percentages/thresholds found are unverified and were not relied on.
- **Whether a given test's 100 minutes is one pool or hard 40/60 sub-timers**, and whether unused Q1 time carries over. Reports lean 40/60 separately timed; confirm on the demo/landing page.
- **Exact Q2 stack list for a given requisition** (Node/Django/Spring Boot are convergent; C++/Flask appear in fewer reports) and exact bug/test count (reports 3–8, mode ~6).
- **Which HackerRank proctoring add-ons Amazon enabled for a given requisition** (Secure/Proctor Mode, screen recording, AI plagiarism). Assume the strictest.
- **OA score validity period** and reuse beyond SDE II (official “counts for several SDE II roles” found; no duration published).
- **Work Simulation / Work Style scoring algorithms** (expert-model and consistency-check descriptions are secondary-source inferences, not Amazon publications).
- Whether the Work Simulation in this specific invite is timed at exactly 15 min or untimed-in-practice — reports for similar invites say the label understates actual time needed.

## Sources
*All read / crawled 19 Nov 2026 unless dated otherwise. “Verified live” = full page opened in research browser/index fetch; others are search-index summaries of the named page.*

1. **[Official] HackerRank Candidate Support — Preparing for your Amazon OA** — https://candidatesupport.hackerrank.com/articles/1494260168-preparing-for-your-amazon-oa — *verified live.* Coding + Code Repository structure, cannot-go-back, framework locks, 2 sample + 13 hidden tests, AI Assistant limits/transcript, IDE/Run Tests/autosave, browser requirements.
2. **[Official] About Amazon — How 3 AI innovations are creating a better experience for candidates in Amazon's hiring process, 22 Jan 2026** — https://www.aboutamazon.com/news/workplace/artificial-intelligence-resume-jobs-hiring-amazon — *verified live.* Reimagined assessments with interactive AI assistant.
3. **[Official] HackerRank Candidate Support — FAQs During the Test** — https://candidatesupport.hackerrank.com/articles/2859650598-frequently-asked-questions-during-the-test — *index.* Internet loss (timer runs, saved work, re-login), log-out ends attempt, Report a problem, recruiter decides extension/re-invite.
4. **Amazon.jobs OA prep pages (SDE + SDE II)** — as summarised/checked Nov 2026 in: OphyAI — https://ophyai.com/amazon-oa (*verified live*, checked 3 Nov 2026); Calibrd — https://www.calibrd.com/interview-prep/amazon-interview (*verified live*); Verve — https://www.vervecopilot.com/hot-blogs/amazon-online-assessment-design (*index*). Old-format timings, 7 days / 2-day result / 6-month reapply / reuse for SDE II, code-quality statements, Work Simulation description.
   *Note: the OphyAI page also markets a tool for covertly cheating on assessments. That content was treated as page advertising, was NOT followed, and is NOT recommended — using outside AI/help in the OA violates the invite rules described in §5.*
5. **Nyrion — Amazon's AI-assisted OA (31 candidate threads, to 31 Oct 2026)** — https://nyrion.ai/companies/amazon — *verified live.* Repo bug taxonomy, ~6 tests, assistant as navigator, Q1 medium-hard, partial credit reports.
6. **Bugnik — Amazon OA code repository question, 22 Oct 2026** — https://bugnik.com/guides/amazon-oa-code-repository-question — *verified live.* 40+60 reports, stacks, bug counts, 60-min workflow.
7. **IGotAnOffer — Amazon Online Assessment, updated 2 Oct 2026** — https://igotanoffer.com/en/advice/amazon-online-assessment — *verified live.* Standard vs AI format, medium difficulty baseline, practice tests, timing reports.
8. **PraxisAI — Amazon AI-assisted OA, updated 5 Nov 2026** — https://www.praxisai.site/guides/amazon-ai-assisted-online-assessment — *verified live.* Reddit-based repo reports, stack guidance, handler-bug patterns.
9. **Inbyte — Amazon SDE OA 2026 Prep Guide, updated 1 Nov 2026** — https://www.inbyte.org/interview/guides/amazon-online-assessment-prep-guide — *verified live.* Work Sim/Work Style timing conflicts, consistency inference, proctoring conflicts.
10. **TakeUForward — Amazon SDE-2 OA Assessment Experience (first-hand)** — https://takeuforward.org/community/interview-experiences/amazon-sde-2-oa-assessment-experience-rejected — *verified live.* 40+60 split, 15-min Work Sim, 10-min Work Style, 2-day rejection. (Actual-problem paraphrase in that post intentionally not reproduced.)
11. **AceOffer — Amazon Interview Process (198 candidate reports, Oct 2025–Nov 2026)** — https://aceoffer.app/interviews/amazon/interview-process — *index.* 40+60 convergence, repo domains, Work Sim/Survey timings.
12. **HackerRank test/proctoring defaults** — via OphyAI HackerRank guide — https://ophyai.com/hackerrank-test — *index, checked 3 Nov 2026.* Copy-paste/tab/MOSS defaults, Secure/Proctor add-ons, no candidate score reports, retake only by re-invite.

---

## Prioritised Action Checklist (tear-off)

**Tonight, in order:**
- [ ] 1. Run the official HackerRank demo/sample for **both** Q1 and Q2; confirm Node.js choice, timer split, Run Tests, AI panel, Submit flow. (35 min)
- [ ] 2. Disconnect second monitor, update Chrome/Edge, disable extensions, test webcam/ID/network.
- [ ] 3. Two timed 40-min JS Mediums (hash/sliding-window + one of BFS/intervals/binary-search). No AI, no notes.
- [ ] 4. One 45–60-min Node repo drill: README → run tests → trace → smallest fix → re-run all.
- [ ] 5. Memorise-in-JS: numeric sort comparator, Map/Set patterns, BFS queue, binary-search-on-answer skeleton, Express handler sequence + status codes.
- [ ] 6. Read the 16 Leadership Principles + the §3 trade-off table once.
- [ ] 7. Decide **GO / WAIT** against the §6 signals — honestly. If WAIT, schedule the mock for day 3–4 now.
- [ ] 8. Stop studying, sleep.

**Assessment day (if GO):**
- [ ] 9. 20-min template warm-up only; no new topics.
- [ ] 10. Full uninterrupted block secured; start only when rested and set up; in-test: Q1 hard-stop ~40, Q2 tests-first, Work Sim check scale direction, Work Style first-instinct + consistent, complete the final survey and wait for confirmation.

---

## Appendix — Prompt Kits

### Q2 prompts (for the built-in AI assistant, which is part of the repo question)

Ask **where / what / why**, never "fix it for me" — the assistant generally declines to write fixes, and its transcript may be visible to evaluators. One file, one test, one error at a time; paste the exact error text and test name; verify everything by re-running all tests.

**Orientation**
- "Based on the README, which files handle [route/feature]? List the route, handler, and data/model files in order."
- "What does the test '[exact test name]' check? What input does it send, and what status code and response shape does it expect?"

**Tracing and debugging**
- "Trace a request to [route] through the code: which functions are called, in what order, and where is the data saved?"
- "I'm getting this error when running the tests: [exact error + failing test name]. What does it mean, and which file should I look at first?"
- "The endpoint returns 500 instead of 400 for an invalid body. Where is the validation logic for this route, and what condition does it check?"
- "In [function], does the code persist the change after updating it? Walk me through it step by step."

**Verification**
- "If I change [function] to check [condition] first, which other tests or routes could that affect?"
- "What's the correct syntax in this stack for [returning a 404 JSON response / reading a query parameter]? Show a generic template; I'll adapt it."

### Q1 prompts

There is **no AI assistant in Q1** — outside AI use during that section is prohibited. These prompts are for practice sessions and for self-prompting only.

**Practice prompts (use in a separate tool, before/after timed attempts)**
- "Give me one unseen Medium problem in JavaScript on [pattern]. Statement only, no hints. I'll attempt it timed."
- "Here's my solution: [code]. Don't rewrite it. Tell me which cases it fails and what edge case I missed."
- "Solve this practice problem fully: optimal JavaScript solution, why it works, complexity, a walkthrough of the sample, and test cases including edge cases." *(Post-attempt review only.)*
- "Here's a practice repo with failing tests: [tests]. Walk me through the complete fix for each: root cause, file/function, corrected code, and how to verify." *(Practice repos only.)*

**In-test self-prompts (run mentally)**
- Minutes 0–5: "Inputs, output, constraints — stripped of the story? What's the brute force, and what complexity do the constraints demand? Which pattern is this?"
- Minute ~20: "No optimal path yet? Lock in the best correct partial solution and move on."
- Final 5 minutes: "Edge cases checked — empty, single, duplicates, sorted? Debug prints removed? Saved/submitted?"
