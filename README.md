# Australian Metascience Co-authorship Network

An interactive map of the researchers who do **metascience** (research on research) while
based in Australia — how they cluster into research strands, who they publish with, and how
they connect to international leaders in the field.

`index.html` is a single self-contained web page; open it in any browser.

This document explains how the map is **generated** — starting from a hand-picked seed of
key papers and authors, how that seed is enriched into a full network, and how each person
is assigned to a research strand.

---

## 1. Start: a seed list

The process begins with a curated **seed list of key papers** (with a few key authors),
supplied as a bibliography (`seed.ris`) — currently ~70 papers. This is the only hand-built
input. Everything else is derived from it automatically, using the open
[OpenAlex](https://openalex.org) scholarly database.

## 2. Enriching the seed into a network

The seed papers are the anchor points, but on their own they are just a reading list. Four
enrichment steps turn them into a connected map of people:

**a. Resolve the seed and pull in every co-author.**
Each seed paper is looked up in OpenAlex, which returns its full author list. Crucially, the
network includes **everyone who co-authored a seed paper**, not just the authors named in the
seed. This is the primary source of expansion: the named authors bring in their collaborators,
and co-authorship links between them form the edges of the map.

**b. Hydrate key figures who are thin or missing in the seed.**
Some important researchers appear on few (or none) of the seed papers. These are pulled in
by their **ORCID** (a researcher's unique ID): the system fetches their publications and keeps
only the ones that (i) are recognisably about metascience and (ii) share a co-author with
someone already in the network. This adds people through *genuine* collaboration links rather
than dropping in isolated names.

**c. Add international leaders and verify the links.**
A curated set of global metascience figures (e.g. leaders of major reproducibility and
research-integrity centres) is added as reference points. An Australia-based researcher is
connected to one of these leaders **only when OpenAlex confirms a real co-authored paper
between them**, and only when that shared work is itself about metascience — so unrelated
collaborations don't leak in.

**d. Clean up duplicate identities.**
OpenAlex occasionally splits one person across several author IDs (for example, when a new
preprint lists them under a fresh identity). Known cases are merged so each real person is a
single node, with their citations and links correctly combined.

Alongside this, each person's **citation counts** and **affiliations** are read from OpenAlex.
Affiliations (plus the seed author list) determine who is treated as **Australia-based** — the
people shown in full colour, versus international collaborators shown faded.

The current seed of ~70 papers expands, through these steps, into roughly **400 researchers**
and **1,650 co-authorship links**, including **13 international leaders**.

## 3. Assigning people to research strands

Every researcher is placed in one of **nine research strands**. The assignment is done in
three stages:

**a. Classify each paper.**
Each paper is sorted into a strand using a keyword-and-topic rule: it looks at the paper's
title and its OpenAlex research topics and matches them to a strand (for example, "systematic
review" or "PRISMA" → *Evidence synthesis*; "open knowledge" or "bibliometric" →
*Scientometrics & open knowledge*; "funding", "grant" or "research impact" → *Research funding
& evaluation*).

**b. Give each person the strand they publish in most.**
A researcher is assigned the strand that the **majority of their papers** fall into. Someone
who writes mostly about statistical reform lands in *Statistical reform*, even if they have the
odd paper elsewhere. (Ties are broken by a fixed strand priority.)

**c. Two adjustments on top of the vote.**
- **International leaders** are given a strand by hand, reflecting the area they are known for.
- A **small number of manual overrides** correct the handful of cases where the majority vote
  is misleading — typically someone whose primary field is one strand but who has co-authored
  enough papers in an adjacent area to be miscounted. (A researcher who connects to the network
  *only* through a leader inherits that leader's strand.)

Because strand assignment is a heuristic based on titles and topics, it captures the broad
shape of the field well but is not a definitive taxonomy; a few researchers who work across
areas are inevitably judgement calls.

### The nine strands

| Strand | What it covers |
|--------|----------------|
| Statistical reform | Significance testing, confidence intervals, estimation, error reporting |
| Expert elicitation & replication | Structured expert judgement, replication prediction (e.g. repliCATS) |
| Evidence synthesis | Systematic reviews, reporting guidelines (PRISMA, TIDieR), research waste |
| Research integrity | Misconduct, fraud, retractions, paper mills, questionable practices |
| Publication & peer-review reform | Registered reports, preregistration, peer-review and journal reform |
| Scientometrics & open knowledge | Bibliometrics, open access / open knowledge, the COKI programme |
| Research funding & evaluation | Funding, grants, grant peer review, research-impact evaluation |
| Science communication & STS | Public engagement, science communication, science & technology studies |
| Indigenous research & data sovereignty | Indigenous data sovereignty, ethics for First Nations research, evaluation of First Nations research |

## 4. What the map shows

- **Each dot is a researcher**; its **strand** is its colour and its position on the wheel.
- **Lines are co-authorship** — either between two people in the network, or a verified link
  from an Australia-based researcher to an international leader.
- **Australia-based researchers** are drawn in full colour; international collaborators are faded.

---

*Data source: [OpenAlex](https://openalex.org). Figures update as OpenAlex refreshes
affiliations and citation counts, so exact counts drift slightly between rebuilds.*
