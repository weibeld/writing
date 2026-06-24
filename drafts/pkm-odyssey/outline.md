# My Personal Knowledge Management Odyssey - Outline

## Core Motivation

Goal: externalise knowledge — transform what's in your head into text, incrementally over time.

Reasons:

1. Documentation: a persistent record of what you know — your knowledge in textual form
2. Reuse: never start from zero — pick up where you left off

## Core Preferences

- Local first: text files on local disk, not proprietary data formats on tool provider's infrastructure
- Git version control: full version control capabilities, not limited or paywalled feature set defined by tool provider
- Vim editing: fully keyboard-based editing, no clicking in GUIs (relevant for existing Vim users only)

## Stage 1: Exploring Existing Note-Taking Apps

**Period:** 2023

**Assumption:** knowledge externalisation is done by writing notes (uniform set of notes).

**Summary:** tried various existing note-taking apps to find one that does what is needed out of the box.

**Apps explored:** Notion, Obsidian, Dendron, Notational Velocity

**Outcome:** none of the existing apps provided a suitable solution. Each imposed trade-offs that didn't fit.

**References:**

- [my-journey-to-the-ideal-note-taking-app](https://github.com/weibeld/nightingale/tree/main/drafts/my-journey-to-the-ideal-note-taking-app)

## Stage 2: Explore existing PKM methodologies

**Period:** 2023

**Motivation:** possibility to create additional value by structuring notes according to proven system rather than uniform set of plain notes.

**Methodologies studied:** GTD, PARA, Zettelkasten

## Stage 3: Develop custom PKM methodology (Desk-Drawer-Shelf Method)

**Period:** 2023

**Motivation:** none of the existing PKM methodologies matches my needs exactly. 

**Summary:** a three-tier note organisation method extending Zettelkasten, with influences from GTD and PARA. Notes are categorised by volatility/persistence and promoted through tiers as they mature.

**Structure:**

- **Desk** (ephemeral, supports daily work)
  - Inbox — dumping ground for thoughts, regularly processed (from GTD)
  - Tasks — reminders for immediate tasks
  - Project Overview — overview of current projects
- **Drawer** (temporary, starting point for something more permanent)
  - Ideas — project and article ideas, shaped before committing to them
  - Drafts — preliminary research not yet ready for the knowledge base
- **Shelf** (permanent knowledge base)
  - Box — Zettelkasten-style linked notes
  - Records — structured notes with a fixed schema for instances of a concept (e.g. "cloud instance creation" across AWS, GCP, Azure)

**Key ideas that survived to Owl:**

- The system is complementary to other tools rather than all-encompassing — never replicate a source of truth
- Git-backed storage and version control
- Separate vaults/buckets for completely different domains

**Ideas now obsolete:**

- Three-tier promotion model (desk → drawer → shelf) — replaced by append-only capture
- Zettelkasten linking and manual organisation — replaced by LLM-based retrieval
- Curation and grooming of notes — eliminated entirely
- Tool-specific implementation (Obsidian, Dendron, VimWiki features like backlinks, templates, refactoring) — bypassed by CLI and LLM-based retrieval
- Public/private vault distinction — deferred to frontend/publishing layer

**Mapping to current project suite:**

| DDS subcategory | Stage 5 projects|
|---|---|
| Desk → Inbox | Not directly covered (permanent insights go to Owl) |
| Desk → Tasks | Not covered (use traditional todo apps) |
| Desk → Project Overview | Dracula (with a more implicit, capture-first approach) |
| Drawer → Ideas | Calimero (idea incubation with LLM agent support) |
| Drawer → Drafts | Nightingale (Owl insights don't have drafts, so must be draft for a Nightingale story) |
| Shelf → Box | Owl (for insights)/Nightingale (for stories) |
| Shelf → Records | Giraffe (structured data as a separate tool) |

TODO: should we rename Shelf/Box to Shelf/Heap (the name "heap" was being used but I don't remember if it was before or after "box")

**References:**

- [desk-drawer-shelf-method.md](https://github.com/weibeld/nightingale/blob/main/drafts/pkm-odyssey/sources/stage-3/desk-drawer-shelf-method.md): detailed description of the desk-drawer-shelf method

## Stage 4: Abandon DDS method and focus on Vim and Git-based system for notes and records

**Period:** 2023-2025

- Same system for both unstructured notes and structured records
- Entries are organised in "areas" which may be either notes or records and live in their own repositories
- Transition from DDS method.
  - Handle temporary notes off-the-loop in Google Keep or similar
  - Handle todo tasks off-the-loop in Todoist or similar
  - Handle project ideas, events etc in separate repositories
- TODO: sources from https://github.com/users/weibeld/projects/18/views/1?pane=issue&itemId=105199840 (Old Notes) that were previously on Google Keep.

## Stage 5: Split into separate tools for unstructured notes and structured data

**Period:** 2025

**Motivation:**

- Insight that one monolithic app isn't ideal
- Separate main apps for unstructured notes and structured data

**Projects:** 
- Toshokan: unstructured notes (Vim and Git-based)
- My Database: structured data recording (Vim and Git-based)

**Exploration:** tools are heavily Vim-based, most features emerge through some Vim functionality. Explored Vim tools: VimWiki (https://github.com/vimwiki/vimwiki), wiki.vim (https://github.com/lervag/wiki.vim). Probably converged to wiki.vim.

### Toshokan

- GitHub Project: https://github.com/users/weibeld/projects/18 (formerly *Toshokan*, transformed into *Owl*)

**Common problem:**

- Main interface is Vim-based but for usage on mobile, another type of interface is needed
- Usage on mobile has also been deemed important to reduce capture friction since ideas and thoughts may often come when one the move or just currently on the mobile phone
- Considered options for mobile interace include: [GitJournal](https://gitjournal.io/), Notion (using Notion API to move content into Git repo), Obsidian with [Syncthing](https://syncthing.net/) (apparently, the Syncthing Android app has been [retired in October 2024](https://forum.syncthing.net/t/discontinuing-syncthing-android/23002))

### My Database

- GitHub Project: https://github.com/users/weibeld/projects/19

## Stage 6: LLM Pivot - Make core solutions viable

**Period:** 2026

**Summary:** the introduction and maturity of LLMs allow shifting the focus away from optimising for retrieval at capture time (e.g. organisation and linking of content). Instead, capture can be a simple "dumping" operation and meaning and organisation is based by LLM-based retrieval. this allows addressing a crucial weakness of all previous approaches: the focus on organisation.

**Previous weaknesses:** all previous approaches put focus on the organisation of information, for example, the interlinking of notes or choosing a category for it. This has two big disadvantages: first, it introduces friction at capture time; second, and most importantly, it facilitates "encyclopedia drift", i.e. the tendendcy of entries in the knwledge base to evolve into a encyclopedia-like form.

**Encyclopedia drift/pitfall/rabbit hole:** the reason for "encyclopedia drift" is that if you're forced to organise notes and put them into context with other notes (for categorising, linking, etc.), you automtatically deal with more than just the current note itself. this widens the scope of action and increases the perceived number of action items. For example:
- Adapting the curent entry to match a related entry's style of level of detail
- Edit other related entries in response to the current entry's editing
- Harmonising terminology or style across entries
- Restructure the current or other entries (e.g. split, merge, etc.)
- Creating new content or entire entries only for the sake of completeness to avoid "gaps" in the wholistic view of the content
The consequence of this is that it's very easy to be drawn into heavy and possibly endless edidting and curation work, which may block the original task that lead to the creation of the entries in the first place. Moreover, the value of this editing and curation work is not clear, as it is done only for the unintended encyclopedia drift, not to address a specific task.

**Where LLMs come in:** LLMs allow to break this vicious cycle in that they allow eliminating the organisation of information. The application's main usage can now be capture-only. And organisation and inference of meaning is deferred to a later asnychronous LLM-based retrieval stage. This works well because the information accumulation produced by the capture-only stage is the prime use case for LLMs, namely, the inference of semantic structure from textual data.

**Core consequences:** most profound consequences for Owl and Nightingale (successors of Toshokan) while in a lighter degree to Giraffe :
- Owl becomes a capture-first append-only store for fleeing insights. No organisation, editing and curation
- Nightingale is the place for actual edited and curated texts. It has a focus on publication and "stories" to bias the content towards general usefulness (i.e. writing for an audience), to prevent a mere shift of encyclopedia drift into Nightingale
- Giraffe stays conceptually similar to My Database but LLM facilities greatly faciliate the determination and filling in of information in the structured data records

**Core Projects:**

| Project | Content type | Scope | DDS Correspondance |
|---|---|---|---|
| [Owl](https://github.com/weibeld/owl) | Insights | Quick one-off capture of things learned — append-only, no organisation, editing, or curation. Successor of Toshokan | Desk/Inbox, Shelf/Box |
| [Giraffe](https://github.com/weibeld/giraffe) | Structured data | Maintenance of tabular record-like data — typically worked on and completed over time. Successor of My Database | Shelf/Records |
| [Nightingale](https://github.com/weibeld/nightingale) | Stories | Self-contained texts about selected topics — may be based on info from other projects of suite | Drawer/Drafts, Shelf/Box |

**Further consequences:** the related concerns of activity tracking/journaling and idea management are also impacted by the availability of LLMs:
- Dracula: append-only log of each day's activity, meanign and intelligance derived by LLM retrieval
- Calimero: elevating mere writing down of ideas to to a full file-based and Git-tracked LLM agent discussion

**Peripheral projects:**

| Project | Content type | Scope | DDS Correspondance |
|---|---|---|---|
| [Dracula](https://github.com/weibeld/dracula) | Activity | Work tracking — minimal input ideally consisting of checkboxes or one-liners.  in DDS method   | Desk/Project Overview |
| [Calimero](https://github.com/weibeld/calimero) | Ideas | Idea development — LLM agent tool for developing ideas as Git-tracked files from the start. | Drawer/Ideas |

**Note:** currently missing in Stage 5 with respect to the DDS method (Stage 3) is the task management concern. While this is a common and very popular concern, it's omitted by default here since my personal workflow is not very heavily based on task management.

## General references

- [GitHub Projects - Notes Repositories Consolidation](https://github.com/users/weibeld/projects/69): list of repositories containing notes that have been created during this journey in different formats.
