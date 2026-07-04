# Project documentation sets: multi-file docs, RFCs, diagrams

Single-text rules are not enough when the deliverable is a documentation set: a docs/ folder, a Docusaurus or MkDocs site, an architecture section with RFCs. Read this file when writing or editing anything with an index page, cross-links between files, or design-decision records.

## One source of truth

A topic is explained in exactly one place; everywhere else links to it. This applies to facts as much as to explanations: a hostname, a version, or a limit stated in two files will diverge — one of them silently goes stale. Real case: an index page names one jumphost in prose while every ssh command on the next page uses a different one. If a fact must physically appear twice, one occurrence is generated, linked, or explicitly marked as a copy of the other.

Diagrams obey the same rule. One canonical diagram per view of the system. If a variant appears in another doc, it must differ deliberately (zoomed into one zone, one consumer type highlighted) — not be a drifting copy that someone forgot to update.

## Hub page

The index of a section is a router, not an essay: two or three sentences on what this is, then a table mapping section → what question it answers ("Control Plane — components, why kubeapi"; "Packet path — encap / fabric / decap, anycast"). A reader should find their door in ten seconds. Reading order across files is set by numbered filenames (01-, 02-) — keep the numbering gapless and the sidebar labels short.

## Page budget: ~200 lines

A page that scrolls past ~200 lines stops being read and starts being skimmed — and reviewers rubber-stamp what they skim. When a document outgrows the budget, split it by question, not by size: the decision stays on the main page; "how it works today" and "what prior documents missed" become their own pages, linked from the exact sentence that needs them. Real case: a 400-line ADR became four pages — the decision, current state, review of prior docs, and the near-term plan as a separate document; every page under budget, each answering one question. A split by size (part 1 / part 2) just hides the scroll bar.

## Link text

A link names what's behind it: "RFC-001, Withdrawal scenarios" — good. "wiki: pageId=8098808754" — bad: the reader can't decide whether to click. When pointing to detail that's out of scope here, say so and point precisely: "The slice-reconcile algorithm is out of scope for this doc — see RFC-001, Key decisions."

## Diagrams

A diagram earns its place when it shows relationships prose can't: topology, flows between components, sequences. A sequence diagram for protocols and lifecycles, a flowchart for topology, a state diagram for verdicts and statuses; don't draw what a three-row table says better.

The reverse smell: three paragraphs narrating states, transitions, or who-calls-whom ARE a diagram request. A flow with three or more participants, a lifecycle with more than three states — draw it and delete the narration.

Every diagram is followed by prose pointing at what to notice — a "What matters in this picture" paragraph. A diagram without commentary is decoration: the reader sees boxes and arrows but not the point. But pointing is one paragraph — the counterintuitive edge, the transition people get wrong. If the text after a state machine re-tells every state and arrow in bullets, the same content lives twice and one copy will go stale. The diagram replaces the prose, it doesn't duplicate it.

## Bridge tables: explaining through the known

When introducing a new model, map it onto the system the reader already knows — a table column "analog in BGP" or "analog in the old system" next to each new field. This is the reader's-world principle in table form: a network engineer reads "permittedPrefixes ≈ your prefix-list" and understands instantly what three paragraphs would explain slowly.

## Negative space

A section on what the system does NOT do prevents the most expensive misunderstandings: "No traffic state on the control plane. No SRv6 state on transit nodes. No back-channel from data plane." Readers arrive with assumptions from systems they know; naming the absent mechanisms explicitly kills wrong assumptions before they become wrong designs.

## Term discipline

One canonical form per term. Declare the abbreviation at first mention — "EndhostRoutingSlice (ERS)" — then use exactly one short form everywhere. Four coexisting forms of the same noun (ERS / ers / slice'ы / EndhostRoutingSlice'ы) make both reading and grep harder. Same for spelling of multi-word terms: pick "data plane" or "data-plane" or "dataplane" once per docs set, including capitalization.

Russian text with English terms: pick one declension convention — apostrophe («slice'ы», «watch'ит») or invariant form («объекты slice») — and apply it across all files. Never decline identifiers inside backticks: `EndhostRoutingSlice` stays exactly as the API spells it.

## Placeholders

One convention per docs set: either `<angle-brackets>` or `$UPPER_VARS`, declared once ("replace `<user>` with your FreeIPA username"). Mixing `<freeIPA-user>` and `${K8S_VERSION}` in one guide makes readers wonder whether the difference means something. It usually doesn't — which is worse.

## Formatting across files

Horizontal rules (`---`) are almost never needed: headings already separate sections. Ten rules per file is separator spam — the visual noise of a document shouting "NEW SECTION" at a reader who can see the heading.

The first line under a title must add information beyond the title. "Server preparation" followed by "Preparing the server infrastructure for deployment" says the same thing twice — an echo intro. Either state something new (prerequisites, how long it takes, what you'll have at the end) or start with step one.

Parenthesis depth ≤ 1. A sentence with nested parentheses, plus-signs joining clauses, and a quoted aside inside the parens is a table or two sentences trying not to be born.

## RFC / ADR specifics

A header block: status (Draft / In review / Accepted / Superseded by NNN), date, owner. Without a status line the reader can't tell a binding decision from a sketch someone abandoned.

Problem first, then the decision. Out of scope with reasons — not a bare list of absent things, but why each is absent and what the absence costs: "the price is no single point of truth for the anycast group; configs must be kept consistent on the NMS side." Alternatives considered, each with why it was rejected. When mentioning a future extension, say whether it lands additively or breaks the contract. Naming the weak spots of your own design is what makes the strong parts believable.

An open question earns its slot by being genuinely open: what exactly is unresolved, who decides, by when, and what it blocks. "Approve the service name" is a task for a chat, not an open question; a question the body already answers is residue — move the answer into the body and delete the question. Nine open questions where four are real hide the four.

Template residue — commented-out status variants, `<!-- what do we want to get -->` prompts left from the RFC template, "(?)" placeholders — is cleaned out before review. A reviewer who sees scaffolding assumes the thinking is scaffolding too.
