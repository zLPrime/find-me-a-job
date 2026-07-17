# Observations

A running log of things noticed while using this process: gaps,
surprising results, candidate corrections, ambiguous instructions, or
anything else worth remembering. Any agent may add an entry here at any
time. This log feeds [journal/improvements.md](improvements.md).

## How to add an entry

Append a new entry at the top, using this structure:

```markdown
## <date> — <short title>

Observed by: <agent name>
Context: <what was happening when this was noticed>
Observation: <what happened, what was missing, or what surprised>
Possible cause: <which agent/skill/rule/template this likely traces to>
Suggested follow-up: <optional — a concrete idea, or "needs discussion">
```

## Entries

## 2026-07-17 — "Safe-commit" git-plumbing workaround silently desynced the working tree from git HEAD

Observed by: orchestrator (execution session)
Context: While recording an Onwelo application submission, re-reading
vacancies/onwelo-senior-net-backend-engineer.md returned a much
shorter/older version (78 lines) than git HEAD actually contained (143
lines, from a commit made earlier in the same session). Checking
further, the same mismatch was found in
work/jakub-charabet/Jakub_Charabet_Full_Resume.docx, decision-log.md,
pipeline-overview.md, and tailored-cvs/megapolis-it-tailored-cv-ru.md.
Observation: All affected files had been edited earlier in the session
using a manual git-plumbing "safe commit" pattern (`git show
HEAD:<path> > temp`; edit temp; `git hash-object -w temp`; stage it via
a scratch `GIT_INDEX_FILE`; `git write-tree`; `git commit-tree`; then
`echo <hash> > .git/refs/heads/master`) — adopted to route around this
mount's confirmed `unlink()` failures, which make ordinary `git add`/
`git commit` leave lock-file debris. This pattern only ever touches
git's internal object database (blobs/trees/commits) and the ref
pointer; it never writes the edited content back into the actual
checked-out file, unlike a normal `git commit`, where the working tree
and index are assumed already in sync because the edit happened in
place first. The pattern's own verification step (`diff <(git show
HEAD:<path>) /tmp/clean.md`) masked this: it compared the new commit
against the same temp file used to build it, so it always passed even
when the real working-tree file was left stale. This is the same
failure class already flagged in "Tooling note: bash vs. direct file
tools" (rules/general.md) — content diverging between what the shell
can see and what's actually true — but that rule's wording ("reads a
file, transforms it, and writes it back") didn't anticipate a
workaround that never writes to the file at all, only to git's object
database, so it wasn't obviously covered.
Possible cause: rules/general.md's "Tooling note" section predates the
safe-commit git-plumbing workaround and doesn't require working-tree/
HEAD parity after a manual commit built this way.
Suggested follow-up: Extend "Tooling note: bash vs. direct file tools"
(or "Version control and history") to require: (1) after building a
commit via manual git plumbing, `cp` the exact content used for the
new blob over the real working-tree file; (2) verify with `diff
<(git show HEAD:<path>) <the actual working-tree file>`, never a temp
file, so the check cannot pass while the real file is stale. Applied
as a corrective fix within this session (re-synced all five affected
files, each verified individually) but not yet formalized as a rule —
needs a development-session pass to update rules/general.md, with a
matching journal/improvements.md entry, since this execution session
must not commit to the playbook repo.

**Resolved (2026-07-17):** formalized in a development session —
rules/general.md's "Tooling note: bash vs. direct file tools" now
requires copying the blob content over the real working-tree file
after a manual-plumbing commit, and verifying with `diff <(git show
HEAD:<path>) <path>` against the actual file rather than the temp
file. See [journal/improvements.md](improvements.md), 2026-07-17.

## 2026-07-15 — A new candidate fact was about to be patched directly into the profile, bypassing /input

Observed by: orchestrator
Context: While reviewing the Xebia Azure tailored CV, the candidate
volunteered a new technical achievement (a streamed FHIR-validation
pipeline on the Medical Information System project) that wasn't in any
source document. The natural next step in the moment was to add it
straight to work/jakub-charabet/candidate-profile.md from the
conversation.
Observation: The candidate stopped this and pointed out that /input is
supposed to be the sole entry point for candidate facts (per
input/README.md and rules/factual-accuracy.md's Traceability
principle), and that patching the profile directly from a mid-session
statement — even with a "candidate direct statement" source note —
bypasses that, leaving no durable record independent of this one
conversation.
Possible cause: rules/factual-accuracy.md described /input as the
source of all candidate facts but didn't explicitly address the
mid-session case — a candidate fact surfacing outside a dedicated
profile-building step — so nothing in the rules stopped a direct
profile edit from a conversational statement.
Suggested follow-up: Done — see
[journal/improvements.md](improvements.md), 2026-07-15, which added a
"New facts surfaced mid-session" section to
[rules/factual-accuracy.md](../rules/factual-accuracy.md) requiring the
statement to land in /input first, in all cases.

## 2026-07-15 — No playbook step existed for recording an actual submission

Observed by: orchestrator
Context: The candidate applied to the Xebia Blazor vacancy directly
(outside this process, as usual per rules/general.md — no agent
submits on the candidate's behalf) and reported back the actual
financial expectations stated (5,500 EUR/month gross), the final cover
letter text sent (one small edit from the draft: "GitHub Copilot" →
"Claude/Copilot"), and the actual CV file used (a PDF export, uploaded
directly), asking that these be filed appropriately.
Observation: No application package existed for this vacancy — it had
only a standalone tailored CV and cover letter (common per
skills/application-writing.md when no application-specific questions
were captured). More importantly, nothing in
[docs/workflow.md](../docs/workflow.md), rules/general.md,
[agents/application-agent.md](../agents/application-agent.md), or
[templates/application.md](../templates/application.md) described what
should happen *after* an actual submission: workflow.md's stage 8
description ended at "routes it for candidate approval before anything
is considered ready to send," and templates/application.md had no
field for the actual file sent, actual answers given, or noting
differences between the last draft and what was really submitted. The
vacancy template's Status enum already included `applied`, and
templates/application.md's own Status enum already included
`submitted` — so the design anticipated this state but no rule or
agent responsibility ever drove an agent to actually reach it.
Possible cause: the playbook was written stage-by-stage up through
"prepare application guidance" (stage 8) without a corresponding
"record what happened after the candidate acted on that guidance"
step — a natural gap, since submission itself happens outside this
process by design.
Suggested follow-up: Done — see
[journal/improvements.md](improvements.md), 2026-07-15, which added a
"Recording actual submissions" section to rules/general.md, extended
docs/workflow.md's stage 8 and agents/application-agent.md's
responsibilities to cover it, and added fields to
templates/application.md for the actual file sent, actual question
answers, and noted differences from the drafting version. Applied
immediately to the Xebia Blazor case: created
work/jakub-charabet/applications/xebia-blazor-application.md (status
submitted), stored the submitted CV PDF alongside it, and updated the
vacancy status to `applied`.

## 2026-07-15 — Candidate review of the first tailored CV/cover letter surfaced five house-style gaps

Observed by: orchestrator
Context: Candidate reviewed the Xebia tailored CV and cover letter (the
first package in the one-by-one submission pass) and gave five pieces
of feedback: (1) the contact line used decorative middot separators
instead of plain markdown; (2) Claude should be listed alongside GitHub
Copilot as an AI-assisted development tool; (3) language order should
reflect the target market (Polish before Russian for a Poland-based
role), not source-document order; (4) the Summary read as "just another
dev" — it dropped the candidate's genuine differentiator (end-to-end
feature ownership, no dedicated QA role, direct stakeholder work) in
favor of generic full-stack framing; (5) the cover letter repeated full
contact details already on the CV, and opened with the generic "Dear
Hiring Manager" rather than something company-specific.
Observation: None of skills/cv-tailoring.md or
skills/application-writing.md addressed any of these five points before
this session — each was a silent default (whatever felt natural to
write) rather than a documented convention, so nothing prevented the
same gaps from recurring in the other 13 tailored CVs and 13 cover
letters already produced in this batch.
Possible cause: skills/cv-tailoring.md and skills/application-writing.md
had no "Style Conventions" section; house style was implicit rather than
written down.
Suggested follow-up: Done for the immediate gap — added a "Style
Conventions" section to both skill files (contact formatting, language
ordering by market, the ownership-narrative balance, AI-tools currency;
no-contact-in-letter, default company-specific salutation) and applied
all five fixes to the Xebia CV and cover letter as the first
application. Not yet done: the same five fixes have not been applied to
the other 13 tailored CVs / 13 cover letters already produced — the
candidate has not yet said whether to batch-apply the mechanical ones
(contact format, AI tools, cover-letter contact removal, greeting) now
or handle each as it comes up in the one-by-one review. Language
reordering and Summary-narrative rebalancing are more vacancy-specific
and likely need a per-file pass rather than a script.

## 2026-07-15 — Candidate started a one-by-one submission review pass; wants links included by default and a running record of requests/outcomes

Observed by: orchestrator
Context: Candidate asked to go through the ranked pipeline
(pipeline-overview.md) one vacancy at a time to decide on submission,
starting with #1 (Xebia). The first presentation of Xebia included the
vacancy/CV/cover-letter summary but not the posting URL or the
employer/vacancy artifact links; the candidate then asked for those
links, and separately said to "do it always" and to keep track of
requests and outcomes across this pass, with an explicit note that
this should become a formal procedure later rather than being
formalized right now.
Observation: No existing template covers a submission-review session:
templates/application.md covers one finished application package, and
pipeline-overview.md (itself an ad hoc reference doc, see the
2026-07-14 entry below) is a ranking index, not a decision-tracking log
for a live review pass. There's currently no standing instruction for
which links must accompany a vacancy presentation (job posting URL,
vacancy artifact, employer artifact) during this kind of review.
Possible cause: templates/ and rules/outputs.md gap — submission
review/approval tracking as a distinct activity (separate from
producing the CV/cover letter artifacts themselves) isn't covered by
any current template or rule.
Suggested follow-up: candidate intends to formalize this into an
explicit procedure later (likely a new templates/submission-review.md
or an addition to rules/outputs.md's Linking section requiring posting
+ artifact links whenever a vacancy is presented for a decision, plus a
lightweight per-candidate tracking artifact for requests/outcomes
during a review pass). Not actioned as a playbook change yet per the
candidate's own instruction — noted here so it isn't lost.

**Resolved (2026-07-17):** candidate asked directly for this to become
a standing rule. Added a "Presenting artifacts for candidate review"
subsection to rules/outputs.md's Linking section — see
[journal/improvements.md](improvements.md), 2026-07-17. The
lightweight per-candidate tracking artifact for requests/outcomes
during a review pass remains unactioned.

**Resolved (2026-07-15, later same day):** the candidate asked to batch-
patch the mechanical fixes across the remaining 13 tailored CVs and 13
cover letters (the ones not yet touched by the earlier five-point
feedback round on Xebia). Applied: contact block reformatted from a
single middot-separated line to a plain bullet list, LinkedIn added
(new this round — see the LinkedIn entry below), and — where a CV
already named GitHub Copilot explicitly (Spyrosoft, EPAM) — Claude
added alongside it. Cover letters: greeting changed from "Dear Hiring
Manager," to "Dear <Employer> Recruiting Team,", contact details
removed from the signature. Each file got a dated patch note at the
end recording exactly what changed. Deliberately **not** batch-applied:
language reordering by target market and Summary-narrative rebalancing
(the ownership/differentiator framing) — both require per-vacancy
judgment about each employer's location and requirements, and remain
open for the one-by-one review pass.

## 2026-07-15 — Candidate provided a LinkedIn profile; added to input and propagated

Observed by: orchestrator
Context: Reviewing the Xebia Blazor CV, the candidate noted LinkedIn
was missing entirely — not in any source document, not in
input/links.md, not in the candidate profile.
Observation: None of the six original source documents include a
LinkedIn URL, and no agent had asked for one directly; the candidate
profile's Contact Information section (itself only added 2026-07-15)
had no LinkedIn field. This is the same "input folder as the entry
point for candidate-supplied facts" pattern already established for
the GitHub link and AI-tools note — a live candidate statement in
chat, not a source document.
Possible cause: input/links.md was created 2026-07-15 for GitHub/
contact info without prompting for other common profile links
(LinkedIn) at the same time — worth asking for a complete link set
next time this kind of file is created for a new candidate, rather
than adding them one at a time as gaps surface.
Suggested follow-up: recorded in input/links.md and
candidate-profile.md's Contact Information section, then propagated to
the two current-format tailored CVs (Xebia Blazor, Xebia Azure)
directly, and to the remaining 13 via the same batch patch described
above.

## 2026-07-14 — Full JS-rendered re-check of 10 "unconfirmed" vacancies: 9 confirmed live, 1 blocked by a rotted secondary-source URL

Observed by: orchestrator
Context: With the Claude in Chrome extension now connected (see the
entry below), the candidate asked to re-check all remaining
"unconfirmed" vacancies (10 total: Xebia had already been done).
Ran the same JS-rendered check against Finom, Factory World Wide, MTS
Bank, IGT, Upvanta, Zelena firma, Luxoft, Megapolis IT, OTP banka, and
attempted Onwelo.
Observation: 9 of 10 came back genuinely live, each with a distinct
platform-specific "live" signal (live-computed countdown on
justjoin.it, viewer-count + no archived banner on hh.ru, a working
Apply-For-This-Job button with no deadline field on Lever, a fully
functional multi-field application form on Luxoft's ATS). The Upvanta
re-check also produced a clean corroboration of the earlier
stale-cache theory: the old non-JS fetch had shown "25 day left (until
30.07.2026)," but 25 days doesn't match the calendar distance from
2026-07-14 to 2026-07-30 (16 days) — direct proof the earlier fetch
returned a cached snapshot, not a live computation. Onwelo could not be
re-checked at all: its saved careers-page URL (onwelo.com/career/) now
404s. This is a different failure mode than a listing expiring — it
was sourced from a secondary aggregator (JobLeads), not the employer's
own site, so the URL going dead says nothing about the vacancy's actual
status. It was recorded as "re-check inconclusive," not "expired."
Possible cause: rules/general.md's "Source liveness" section didn't yet
distinguish "URL rot on a secondary source" from "listing confirmed
expired," and didn't document what a genuinely confirmed-live result
looks like per platform.
Suggested follow-up: Done — see
[journal/improvements.md](improvements.md), 2026-07-14, which added
both the URL-rot distinction and a per-platform catalog of confirmed-
live signals to rules/general.md's Source liveness section.

## 2026-07-14 — The non-JS-fetch liveness problem is general, not justjoin.it-specific, and the browser fallback wasn't available

Observed by: orchestrator
Context: Immediately after correcting the Spyrosoft false-positive
(see the entry below) and re-labeling justjoin.it listings as
unconfirmed, the candidate reported that Paysend — a different job
board entirely (Teamtailor), marked "live" the same session — was also
no longer active.
Observation: The Paysend "live" conclusion wasn't even based on a
countdown; it was based on the raw fetched HTML still containing the
original posting text and an "Apply now" button. This confirms the
underlying problem is broader than one site's caching behavior: any
job board that applies its "closed" state via client-side JavaScript
after page load will look identically "live" to a non-JS fetch,
whether or not it displays a countdown at all. Every "live" conclusion
recorded in the 2026-07-14 17:49 CEST liveness pass (10 vacancies) was
therefore downgraded to "unconfirmed," not just the justjoin.it ones —
see the updated pipeline-overview.md and each affected vacancy's
Availability Checks section. Separately, an attempt to independently
verify via the Claude in Chrome browser tool (which does render
JavaScript and would settle this definitively) failed both times it
was tried this session — the extension reported "not connected." This
is a client-side setup issue (the candidate needs to install the
extension and sign in with the same account), not something fixable
from this process's side; the candidate was given the install link and
steps directly in chat.
Possible cause: rules/general.md's "Source liveness" section (tightened
earlier this session after the Spyrosoft finding) still framed the
problem as justjoin.it-specific rather than general to modern job
boards.
Suggested follow-up: Done — see
[journal/improvements.md](improvements.md), 2026-07-14, which
generalized the rule to cover any job board, not just justjoin.it, and
made clear that "page loads normally" / "has an Apply button" is not
evidence of liveness either, not just a countdown. Separately worth
tracking as an open item (not a playbook change): confirm with the
candidate whether the Claude in Chrome extension gets connected later
in this session, since several "unconfirmed" vacancies could then be
resolved definitively rather than left as "last known live at
discovery."

**Resolved (2026-07-14, later same day):** the candidate installed the
Claude in Chrome extension and signed in; the browser tool connected
successfully on the next attempt. Used it to re-check Xebia
(justjoin.it) via a JS-rendered page load — genuinely confirmed live
("7 day left (until 21.07.2026)," working Apply button). This is the
first liveness conclusion in this search backed by an actual rendered
page. Nine more "unconfirmed" vacancies remain candidates for the same
re-check: Finom, Factory World Wide, MTS Bank, Onwelo, IGT, Upvanta,
Zelena firma, Luxoft, Megapolis IT, OTP banka.

## 2026-07-14 — A "live" liveness check was wrong: non-JS page fetches can't be trusted on justjoin.it

Observed by: orchestrator
Context: After re-checking all vacancy sources and marking most "live"
based on a page fetch showing a future "days left" countdown, the
candidate reported that the Spyrosoft listing — ranked #1, marked
"re-verified live" that same session — actually displays "Offer
expired" when viewed in a real browser.
Observation: The fetch tool used for these checks does not execute
JavaScript; it returned a page snapshot containing a static "28 day
left (until 21.07.2026)" countdown. This was treated as proof of
current liveness, but it is not — justjoin.it appears to serve a
cached snapshot to non-JS fetchers, with the countdown reflecting
whatever was true at cache time, not the real current status. An
attempt to independently re-verify via the Claude in Chrome browser
tool (which does render JavaScript) failed because the extension
wasn't connected in this session, so the candidate's own direct
observation was the only trustworthy signal available. Xebia and
Upvanta (also justjoin.it, checked the same way, both showing future
countdowns) were downgraded from "live" to "unconfirmed" as a
precaution, since the same failure mode could apply. Note that the
four vacancies independently confirmed *expired* this same session
(EPAM, Cognizant, Nexio, ITLT) are not affected by this problem — a
past date in a stale countdown is still proof of expiry regardless of
when the snapshot was cached; only "live" conclusions from a future
countdown are unreliable.
Possible cause: rules/general.md's "Source liveness" section (added
earlier this same session) required a timestamped check but didn't
distinguish a JS-rendered check from a raw page fetch, so a fetch's
static countdown text was treated as equivalent evidence to an actual
live check.
Suggested follow-up: Done — see
[journal/improvements.md](improvements.md), 2026-07-14, which updated
rules/general.md to require JS-rendered confirmation (or candidate
confirmation) for a "live" conclusion specifically, while allowing a
raw fetch's past-date math to still count as valid evidence of expiry.

## 2026-07-14 — Candidate found two live vacancies via a job board's own "similar offers" recommendations

Observed by: orchestrator
Context: Candidate manually re-checked the Spyrosoft listing (to verify
it wasn't expired, per their own feedback about stale listings) and,
while there, noticed justjoin.it's "Check similar offers" carousel
surfaced two vacancies this process's own discovery pass had never
found: Xebia (Senior .NET Developer with Blazor) and Upvanta (Senior
.NET Developer) — the latter found by clicking through from the former,
one carousel link at a time.
Observation: vacancy-discovery-agent's searches were queried directly
(e.g., "Senior .NET Developer Poland remote" style searches per
employer artifacts' Sources fields) but never followed a job board's
own "similar/related offers" recommendations from an already-found
listing. Both new vacancies turned out to be live and one (Xebia) was
arguably the single strongest specific-skill match found in the entire
search (Blazor is a required and *confirmed* candidate skill, unlike
several Angular requirements elsewhere), plus a work-authorization fit
via the candidate's Polish citizenship — a combination the agent-driven
discovery pass never surfaced despite running many searches on this
same job board.
Possible cause: skills/vacancy-discovery methodology (not directly
read this session, but inferable from the Sources fields on existing
vacancy artifacts) appears to rely on direct search queries only, not
on following a job board's own recommendation/carousel links from
already-found listings.
Suggested follow-up: Add "follow a job board's own similar-offers/
recommended-listings links from each confirmed vacancy" as an explicit
step in the vacancy-discovery methodology, at least for job boards that
expose this feature (confirmed present on justjoin.it; unknown for
helloworld.rs and hh.ru). This is a low-effort, high-signal channel —
both listings found this way turned out to be live and relevant.

## 2026-07-14 — Internal/external references were plain text, not links, by default

Observed by: orchestrator
Context: Candidate asked to make all links to internal artifacts
(employer/vacancy/CV/cover-letter/decision-log files) and external
resources (job posting URLs, source documents) clickable, after
already asking for this once for pipeline-overview.md specifically.
Observation: Every agent in this process had been writing
cross-references as plain text (e.g., "work/jakub-charabet/employers/
t-bank.md" or a bare "hh.ru/vacancy/134381864") rather than markdown
links, across candidate-profile.md, decision-log.md, and all
employer/vacancy/tailored-cv/cover-letter artifacts — roughly 60 files
needed conversion. No rule currently instructs agents to produce
clickable links by default.
Possible cause: rules/outputs.md doesn't address link formatting at
all; each agent that introduced a cross-reference (company-discovery,
vacancy-discovery, employer-evaluation, matching, tailoring,
application-writing) apparently wrote plain-text paths independently.
Suggested follow-up: Add a short "Linking" guideline to
rules/outputs.md instructing agents to render internal artifact
references and external URLs as markdown links
(`[display text](relative/path.md)` or `[url](https://url)`) at the
point of writing, rather than relying on a later cleanup pass.

## 2026-07-14 — decision-log.md and 15 vacancy artifacts were silently truncated a second time

Observed by: orchestrator
Context: While converting internal references to clickable links,
checking decision-log.md for its "Linked Artifacts" sections.
Observation: decision-log.md had been silently cut to 86 lines,
containing only the original "Russia location scope note" entry — all
15 "Match:"/"Rejection:" decision entries added earlier in this same
session (one per vacancy, following templates/decision-log.md) were
gone. This directly explains a second symptom found at the same time:
all 15 vacancy artifacts' "## Match Status" sections ended mid-sentence
(e.g., "Strong match (conservative track). See work/"), and one
employer artifact (employers/epam-systems.md, created later in the
session) was cut off mid-field ("Growth/reputation indicators: One of
the "). This is the same class of bug as the earlier truncation
observation above, but this time it hit files edited later in the
session, and was missed by the earlier repair pass because that pass
only checked employer files and the candidate profile, not
decision-log.md or the vacancy artifacts. All 15 decision-log entries
were reconstructed from pipeline-overview.md, each employer's Fit
Signals section, and each vacancy's Requirements/Notes sections, then
verified by direct Read.
Possible cause — now confirmed as the likely root cause: this
session's bash shell tool has an unreliable/stale view of some files
under this project folder (confirmed by reading employers/cognizant.md
through both the Read tool and a bash `python3` script in the same
turn — the Read tool showed current, complete content, while the
bash-mounted copy was missing entire sections that had existed for
many turns). The most likely explanation for both truncations: an
earlier bash-based operation in this session read decision-log.md (and
the vacancy artifacts) through this stale mount — catching them
mid-edit, before the 15 match entries / closing Match Status sentences
had been written from the direct-file-tools' point of view — then
wrote that stale, incomplete snapshot back, silently reverting the
newer content. This is a read-modify-write race between two
filesystem views that don't stay in sync, not a token/length limit on
a single write.
Suggested follow-up: (1) Add the self-check step already suggested in
the earlier truncation observation, extended to cover every artifact
type. Done — see [journal/improvements.md](improvements.md),
2026-07-14. (2) Stop using bash for read-modify-write operations on
this project's files; use the direct file tools instead. Done — see
the same improvements.md entry.

## 2026-07-14 — Candidate requested a cross-artifact ranked index

Observed by: orchestrator
Context: Candidate asked for all tailored CVs "in order of previously
calculated score," with links to each vacancy, employer, and CV.
Observation: The playbook records match strength/confidence per
vacancy (in decision-log.md) but has no artifact that indexes all
vacancies together in ranked order with cross-links — each artifact
type lives in its own file. Produced work/jakub-charabet/pipeline-overview.md
as an ad hoc reference document rather than force-fitting an existing
template.
Possible cause: templates/ gap — no templates/pipeline-overview.md or
equivalent ranked-index template exists.
Suggested follow-up: If candidates commonly want this view, consider
adding a templates/pipeline-overview.md template (and a
reporting-agent responsibility to keep it in sync) rather than
producing one ad hoc each time.

## 2026-07-14 — No dedicated tailored-CV template exists

Observed by: tailoring-agent
Context: Producing the first tailored CVs (stage 7) for Jakub
Charabet's positively-matched vacancies (Paysend, Finom, Spyrosoft,
Factory World Wide).
Observation: [templates/](../templates) has templates for
candidate-profile, employer, vacancy, decision-log, application, and
report, but none specifically for a tailored CV. skills/cv-tailoring.md
describes required content (draft label, rationale note) but not a
structural format. Improvised a structure (header with status/source/
target-vacancy/match-decision links, CV body sections mirroring
candidate-profile.md, then a "Tailoring Rationale" section) rather than
inventing something unstructured, per rules/outputs.md's "every output
is an artifact" principle.
Possible cause: templates/ directory gap — tailored CV was likely
assumed to be covered by templates/application.md (stage 8), but that
template is for the full application package (cover letter, answers,
submission notes), not the CV itself.
Suggested follow-up: Add a templates/tailored-cv.md template
formalizing the structure used here, so future tailoring passes don't
need to reinvent it each time.

## 2026-07-14 — Earlier session write-truncation affected 9 employer artifacts and the candidate profile

Observed by: employer-evaluation-agent
Context: Beginning stage 5 (employer evaluation), reading each employer
artifact before adding an Evaluation section.
Observation: 9 of the original 13 employer files, plus the candidate
profile itself, had been silently cut off mid-sentence in an earlier
session (missing entire sections in the profile's case — Open
Questions/Gaps and Assumptions were absent altogether). This was not
visible from the conversation summary alone; it only surfaced when
reading the actual files. All content was reconstructed from research
already on record and verified complete via direct re-read.
Possible cause: Likely an interrupted write (e.g., context/token limit
hit mid-tool-call) during a prior long session; not traced to a
specific agent/skill defect.
Suggested follow-up: Consider adding a lightweight self-check step
(e.g., confirm a written artifact's last line matches the intended
closing section) to general.md's artifact-discipline guidance, so a
truncated write is caught immediately rather than discovered stages
later.
