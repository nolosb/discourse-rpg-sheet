You are generating an RPG-style character sheet from Discourse forum activity.

You have the Discourse MCP server available. Use it. Do not fetch Discourse data
by inventing URLs. Do not rely on memory. Do not invent quotes.

Follow these phases IN ORDER. This is intentionally interactive and should stay
close to the original Claude plugin workflow.

---

## TONE — READ THIS FIRST

This is an RPG character sheet, not a performance review. Every name, ability,
debuff, item, and quest must sound like it belongs in a fantasy game. The
workplace insights are real, but the language wrapping them must be evocative,
mythic, and fun.

### The Core Rule

**If a name could appear in an HR document, rewrite it.** "Security Scanner"
becomes "Wardbreaker". "Decision Fatigue" becomes "The Weight of Command".
"Communication Bluntness" becomes "Untempered Edge". "AI-Augmented Development"
becomes "Golem Pact".

### Good vs Bad Examples

These illustrate the right register. Do NOT reuse these names verbatim.
Every character needs unique names drawn from their specific patterns.

**Classes (Family / Trade / Temper):**

| Bad (workplace)              | Good (RPG)                    |
|------------------------------|-------------------------------|
| Cross-Team Collaborator      | Borderlander                  |
| Technical Architect          | Forgehand                     |
| Direct Communicator          | Truthsayer                    |
| Operations Lead              | Ironkeeper                    |
| Frontend Specialist          | Glazier                       |
| Backend Engineer             | Deepdelver                    |
| Product Manager              | Pathfinder                    |
| QA / Testing Lead            | Wardkeeper                    |
| Data Analyst                 | Augur                         |
| Community Manager            | Hearthwarden                  |
| Support Engineer             | Shieldbearer                  |
| DevOps Engineer              | Bridgewright                  |

**Abilities:**

| Bad (workplace)              | Good (RPG)                    |
|------------------------------|-------------------------------|
| Identifies System Gaps       | Seamsight                     |
| Builds Prototypes            | Prototype Summon              |
| Reframes Discussions         | Contrast Strike               |
| Gives Constructive Feedback  | Field Song                    |
| Writes Detailed Documentation| Lorekeeper's Ink              |
| Mentors Junior Members       | Kindling Touch                |
| Automates Repetitive Tasks   | Golem Forge                   |
| Deep-Dives into Bugs         | Spelunker's Eye               |
| Builds Stakeholder Consensus | Hearthcall                    |
| Ships MVPs Quickly           | Swift Strike                  |
| Thorough Code Reviews        | Sentinel's Gaze               |
| Escalates Issues Early       | Signal Flare                  |
| Debugs Production Issues     | Firemender                    |
| Refactors Legacy Code        | Ruin Reclaimer                |
| Writes Persuasive Proposals  | Silver Tongue                 |
| Connects User Feedback to Product | Fieldcraft                |

**Debuffs:**

| Bad (workplace)              | Good (RPG)                    |
|------------------------------|-------------------------------|
| Over-Relies on AI Tools      | Golem Pact Dependency         |
| Communication Style Too Blunt| Untempered Edge               |
| Works in Isolation           | Workshop Hermit               |
| High Delivery Load           | Delivery Drain                |
| Perfectionism                | Gilding Fever                 |
| Scope Creep                  | The Expanding Map             |
| Context Switching Penalty    | Shattered Focus               |
| Avoids Conflict              | Peacekeeper's Bind            |
| Burnout Risk                 | Ember Fade                    |
| Takes on Too Much            | Atlas Burden                  |
| Procrastinates on Docs       | Inkwell Dust                  |

**Inventory:**

| Bad (workplace)              | Good (RPG)                    |
|------------------------------|-------------------------------|
| Project Management Dashboard | War Table                     |
| Documentation                | Chronicler's Codex            |
| Slack/Chat Tool              | Sending Stone                 |
| Code Review Tool             | Sentinel's Lens               |
| CI/CD Pipeline               | The Ironworks                 |
| Testing Framework            | Proving Ground                |
| Analytics Dashboard          | The Oracle Glass              |
| Knowledge Base               | The Archive                   |
| Design System                | Pattern Codex                 |

**Quests:**

| Bad (workplace)              | Good (RPG)                    |
|------------------------------|-------------------------------|
| Reduce Tech Debt             | The Rust Purge                |
| Ship Feature V2              | The Second Forging            |
| Migrate Database             | The Great Crossing            |
| Improve Onboarding           | Opening the Gates             |
| Fix Performance Issues       | Lifting the Fog               |
| Redesign Navigation          | The Breadcrumb Reformation    |

### Tone Guidance by Section

- **Names** (Family, Trade, Temper): One or two words max. Evocative, not
  descriptive. Think character classes, not job titles.
- **Abilities**: Name is 1-2 words, mythic. Description is 2-3 sentences max.
  Explains the real behavior but through RPG framing. Include mechanical language
  (cooldowns, costs, range). Include a real quote from their posts as evidence.
  Pick quotes that show the ability in action, not just on-topic. One sentence
  is better than a paragraph.
- **Debuffs**: Name is evocative. Effect uses mechanical language ("-2 CHA",
  "40% chance of..."). Description is 2-3 sentences, explains the real pattern
  in RPG terms.
- **Inventory**: Items are metaphors for real tools/assets. "The Client Portfolio"
  not "Project List". "Agent Forge" not "AI Coding Tool". Include RPG-style tags
  (heavy, unique, recently acquired, generates resources).
- **Quests**: Quest names are evocative. "The Breadcrumb Reformation" not
  "Redesign Navigation". Steps can be concrete but the framing is mythic.
- **Origin Story**: Third person, past tense, slightly mythic. Exactly 3-4
  sentences. "Arrived at the territories" not "Joined the company".
- **Stats**: One-line descriptions only. Character-flavored, not resume-flavored.
  "Sustained heavy load without breaking" not "Handles multiple projects".

### Stat Calibration

Do not flatter. Most stats should fall in the 10-16 range. A score of 17+ is
exceptional and requires strong, specific evidence from the data. Having some
stats at 10-12 makes the character feel real, not like a performance review
that inflates everyone. Every person has weaker areas. Show them. A character
with all stats above 14 is boring and dishonest.

### The Translation Process

When you analyze someone's forum activity, you will find workplace patterns. Your
job is to translate each pattern through the RPG lens:

1. Identify the real behavior (e.g., "frequently connects separate discussions")
2. Find the fantasy metaphor (e.g., a weaver connecting threads, a cartographer
   linking territories)
3. Name it evocatively (e.g., "Thread Weave")
4. Describe it with RPG mechanics but grounded in real evidence

---

## Phase 1: Data Gathering

Use the Discourse MCP tools/resources for the selected site.

1. If needed, call `discourse_select_site`.
2. Call `discourse_get_user` for the target username.
3. Call `discourse_list_user_posts` for the target username. IMPORTANT:
   `has_more: false` can be wrong on some Discourse activity APIs, so continue
   paging until you receive an empty `posts` array or have gathered about 300
   post metadata rows for the requested timeframe. Do not stop at 15. Fifteen
   is only the old detailed-read target, not the corpus size.
4. Read about 30 substantive posts with `discourse_read_post` after you have the
   larger metadata corpus. Pick a diverse sample across dates/topics, plus
   high-signal excerpts.

Summarize what you gathered before proceeding: total post metadata rows gathered,
detailed posts read, date range, main categories/topics, and notable posts. In
later output, distinguish "posts gathered" from "detailed posts read". Do not
report "Posts analyzed: 15" if you gathered hundreds and only read 15 in full.

---

## Phase 2: Analysis

Analyze the gathered data through these lenses, using concrete examples:

- Output patterns: volume, consistency, categories
- Signature moves: recurring rhetorical/strategic patterns
- Strongest contributions: 5-7 posts with impact or clear substance
- Gaps and limitations
- Collaboration style
- Evolution over the period
- The deeper question: what this person is trying to do beyond surface tasks

Present a concise analysis summary to the user before proceeding.

---

## Phase 3: Collaborative Trait Mapping — INTERACTIVE

Use the `ask_user` tool. Do not skip this. Do not merely print questions in text.
You MUST receive at least one `ask_user` response before Phase 4. If you have
not successfully called `ask_user`, you are forbidden from writing output files.

Structure this as exactly 3 rounds of interaction:

### Round 1: Identity & Stats

Present your full proposal for:

- **Name**: A character name that evokes who they are. Not their real name with
  "the" in front. Think: "Manuel of the Seam", "Bryce the Bridgewright".
  Offer 2-3 options.
- **Family**: Where they come from / how they are positioned.
  Examples: Borderlander, Guildmaster, Wayfinder, Sentinel, Chronicler.
  Offer 2-3 options, each with a one-line reason.
- **Trade**: Their craft / building mode.
  Examples: Artificer, Architect, Forgehand, Scribe, Cartographer.
  Offer 2-3 options, each with a one-line reason.
- **Temper**: How they influence others.
  Examples: Field Bard, Truthsayer, Tactician, Hearthkeeper, Signalfire.
  Offer 2-3 options, each with a one-line reason.
- **Level** (1-20, based on tenure and impact)
- **Alignment** (D&D style with a workplace twist, e.g., "Pragmatic Good",
  "Chaotic Builder")
- **Six stats** on a 1-20 scale with one-line justification each:
  - STR: raw output / delivery volume
  - DEX: versatility / context switching
  - CON: endurance / sustained load over time
  - INT: systems thinking / pattern recognition
  - WIS: judgment / knowing when and where to act
  - CHA: influence / ability to shift others' thinking

Use `ask_user` to let the user pick identity options and adjust stats.

### Round 2: Abilities & Debuffs

Present your full proposal for:

- **1 passive ability** and **3-5 active abilities** based on signature patterns.
  Each ability needs:
  - Name: 1-2 evocative words. NOT workplace language.
  - Type: Passive or Active
  - For active: Range (Melee/Ranged/Ritual/Utility/Bardic), Cooldown
    (None/Medium/Long/Days), Cost
  - Description: 2-3 sentences. What it does, when it works, when it fails.
    Use RPG framing.
  - Evidence quote: a real quote from their posts that demonstrates the ability.
    Pick quotes that show the ability in action. One sentence is better than a
    paragraph.

- **2-4 debuffs** based on gaps. Each needs:
  - Name: Evocative, not clinical
  - Type: persistent (structural, can't self-remove), removable (habitual, can
    be worked on), or environmental (caused by context, not character)
  - Effect: Mechanical description with stat penalties (e.g., "-2 CHA when...")
  - Description: 2-3 sentences. What causes it and how it manifests, in RPG terms.

Use `ask_user` to let the user accept, adjust tone, or rewrite specific entries.

### Round 3: Everything Else & Final Approval

Present your full proposal for:

- **Equipped items** (3): Major tools/assets with RPG-style tags and descriptions.
  Think "The Seam Map (passive, unique)" not "Mental Model of Architecture".
- **Pack items** (4-6): Smaller artifacts, documents, prototypes
- **Active quest** (1): The big thing they are working toward, with progress steps
- **Side quests** (2-4): Parallel efforts
- **Completed quests** (2-3): Things they have shipped
- **Allies** (4-6): People they collaborate with and how
- **Relationship style**: One sentence
- **Party role**: One sentence, using RPG party language ("the tank", "the scout",
  "the one who reads the map")
- **Origin story**: 3-4 sentences, third person, past tense, slightly mythic tone.
  Use language like "arrived at the territories", "the guild noticed", "started
  telling stories about what was seen at the seams". Covers: arrival, early work,
  the moment of noticing something deeper, and current state.

Use `ask_user` for final approval. Once approved, proceed to Phase 4.

---

## Rate limits

If the Discourse MCP server reports rate limiting or asks you to wait, use the
shell tool to run `sleep N` for the requested delay, then continue. Only use
shell for sleeping; do not run arbitrary commands.

---

## Phase 4: Generate Output

After user approval through `ask_user`, write exactly two files using the
`write_file` tool:

- `{username}-character-sheet.md`
- `{username}-character-sheet.html`

Do not merely print the files in chat. Actually write them to the requested
output directory. After writing, give a short summary of the files written.

### Before Writing: Tone Check

Review every name in your output. For each ability, debuff, item, and quest name,
ask yourself: "Could this appear in a performance review?" If yes, rewrite it.
This is the single most important quality check.

### 4a. Markdown Character Sheet

Use this structure:

```markdown
# Character Sheet

**Name:** [Character Name]
**Family:** [Family] — [description]
**Trade:** [Trade] — [description]
**Temper:** [Temper] — [description]

**Level:** [N]
**Alignment:** [Alignment]

---

## Evidence Summary

- Posts gathered: [N]
- Detailed posts read: [N]
- Date range: [dates]
- Main categories/topics: [list]
- Caveats: [any notes]

---

## STATS (1–20 scale)

**STR** [N] `[bar visualization]` [description]
**DEX** [N] `[bar visualization]` [description]
**CON** [N] `[bar visualization]` [description]
**INT** [N] `[bar visualization]` [description]
**WIS** [N] `[bar visualization]` [description]
**CHA** [N] `[bar visualization]` [description]

---

## PASSIVE ABILITY

**[Name]** *(always active)*
[Description]

---

## ACTIVE ABILITIES

### [Ability Name]
*[Type] / Cooldown: [X] / Cost: [Y]*
[Description]

> "[Real quote from posts]"

---

## DEBUFFS

### [Debuff Name] *([type])*
**Effect:** [Mechanical effect with stat penalties]
[Description]

---

## INVENTORY

### Equipped
- **[Item Name]** *([RPG tags])*
  [Description]

### In Pack
- [Item] *([tags])*

---

## QUEST LOG

### Active Quest: [Evocative Name]
[Description]
- [x] [Completed step]
- [ ] [Pending step]

### Side Quests
- **[Quest]:** [Description]

### Completed Quests
- [Quest]: [Description]

---

## PARTY DYNAMICS

**Natural allies:** [Names and roles]
**Relationship style:** [Description]
**Role in party:** [Description]

---

## ORIGIN STORY

*[Origin text in mythic tone]*
```

### 4b. Interactive HTML Character Page

Use the EXACT HTML template below. Fill in all placeholders marked with
[BRACKETS]. Do not change the CSS, class names, or structure. Repeat blocks
as indicated by comments (e.g., one stat-row-wrap per stat, one ability div
per ability, etc.).

For stat bars, calculate width as: (stat_value / 20) * 100 percent.

Pick contextually appropriate Font Awesome icons for inventory items. Good
RPG-fitting options: fa-briefcase, fa-hammer, fa-map, fa-scroll, fa-gem,
fa-crown, fa-flask, fa-compass-drafting, fa-cubes, fa-shield, fa-wand-sparkles,
fa-book, fa-gavel, fa-wrench, fa-fire, fa-feather, fa-chess-rook, fa-landmark

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[CHARACTER NAME]</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Crimson+Text:ital,wght@0,400;0,600;1,400&display=swap');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #1a1a2e;
    color: #e0d5c1;
    font-family: 'Crimson Text', Georgia, serif;
    font-size: 17px;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    padding: 20px;
  }

  .page {
    max-width: 920px;
    width: 100%;
  }

  .header {
    display: flex;
    gap: 28px;
    padding: 28px;
    background: #16213e;
    border: 2px solid #534320;
    margin-bottom: 2px;
  }

  .portrait {
    width: 240px;
    height: 240px;
    flex-shrink: 0;
    overflow: hidden;
    border: 4px solid #534320;
    outline: 2px solid #1a1a2e;
    box-shadow: 0 0 0 3px #2a2015;
  }

  .portrait img {
    width: 116%;
    height: 116%;
    margin: -8% 0 0 -8%;
    display: block;
    image-rendering: pixelated;
  }

  .identity {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .name {
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 26px;
    color: #d4a853;
    margin-bottom: 14px;
    letter-spacing: 1px;
  }

  .tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 14px;
  }

  .tag {
    background: #534320;
    color: #e0d5c1;
    padding: 5px 12px;
    font-family: 'Crimson Text', serif;
    font-size: 16px;
    border: 1px solid #6b5a30;
  }

  .tag-label {
    color: #8a7a5a;
    margin-right: 4px;
    font-style: italic;
  }

  .level-alignment {
    font-size: 16px;
    color: #8a7a5a;
    font-style: italic;
    letter-spacing: 0.5px;
  }

  .tabs {
    display: flex;
    background: #0f1a30;
    border-left: 2px solid #534320;
    border-right: 2px solid #534320;
  }

  .tab {
    flex: 1;
    padding: 11px 8px;
    text-align: center;
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 12px;
    letter-spacing: 1.5px;
    color: #6b5a30;
    background: #0f1a30;
    border: none;
    border-bottom: 2px solid #534320;
    cursor: pointer;
    transition: all 0.15s;
  }

  .tab:hover {
    color: #d4a853;
    background: #16213e;
  }

  .tab.active {
    color: #d4a853;
    background: #16213e;
    border-bottom: 2px solid #d4a853;
  }

  .panel {
    display: none;
    background: #16213e;
    border: 2px solid #534320;
    border-top: none;
    padding: 28px;
    min-height: 400px;
  }

  .panel.active { display: block; }

  .panel h2 {
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 14px;
    letter-spacing: 2px;
    color: #d4a853;
    margin: 28px 0 14px 0;
    padding-bottom: 8px;
    border-bottom: 1px solid #2a2a4a;
    text-transform: uppercase;
  }

  .panel h2:first-child { margin-top: 0; }

  .panel p, .panel li {
    line-height: 1.7;
    margin-bottom: 8px;
  }

  .panel ul {
    list-style: none;
    padding-left: 0;
  }

  .panel ul li::before {
    content: '\f0da  ';
    font-family: 'Font Awesome 6 Free';
    font-weight: 900;
    color: #d4a853;
    font-size: 12px;
  }

  .overview-columns {
    display: flex;
    gap: 32px;
  }

  .overview-left { flex: 1; }
  .overview-right { flex: 1; }

  .origin-intro {
    background: #0f1a30;
    border: 1px solid #2a2a4a;
    padding: 20px;
    line-height: 1.8;
    color: #b0a890;
    font-style: italic;
    font-size: 16px;
    margin-bottom: 16px;
  }

  .class-detail {
    background: #0f1a30;
    border: 1px solid #2a2a4a;
    padding: 14px 18px;
    margin-bottom: 10px;
  }

  .class-detail-label {
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 13px;
    color: #d4a853;
    letter-spacing: 1px;
    margin-bottom: 4px;
  }

  .class-detail-name {
    color: #e0d5c1;
    font-size: 18px;
    font-weight: 600;
  }

  .class-detail-desc {
    color: #8a7a5a;
    font-size: 16px;
    font-style: italic;
    margin-top: 4px;
    line-height: 1.5;
  }

  .stat-row {
    display: flex;
    align-items: center;
    margin-bottom: 6px;
    gap: 10px;
  }

  .stat-name {
    width: 36px;
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 12px;
    color: #d4a853;
    letter-spacing: 1px;
  }

  .stat-value {
    width: 24px;
    text-align: center;
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 14px;
    color: #e0d5c1;
  }

  .stat-bar-bg {
    flex: 1;
    height: 14px;
    background: #0f1a30;
    border: 1px solid #2a2a4a;
  }

  .stat-bar {
    height: 100%;
    transition: width 0.5s;
  }

  .stat-desc {
    font-size: 15px;
    color: #c8a960;
    padding-left: 70px;
    margin-top: -2px;
    margin-bottom: 10px;
    font-style: italic;
  }

  .stat-row-wrap {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    margin-bottom: 2px;
  }

  .str .stat-bar { background: #a84040; }
  .dex .stat-bar { background: #40a848; }
  .con .stat-bar { background: #c89040; }
  .int .stat-bar { background: #4068c8; }
  .wis .stat-bar { background: #8848b8; }
  .cha .stat-bar { background: #c85888; }

  .ability {
    background: #0f1a30;
    border: 1px solid #2a2a4a;
    padding: 18px;
    margin-bottom: 12px;
  }

  .ability-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 8px;
  }

  .ability-name {
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 14px;
    color: #d4a853;
    letter-spacing: 0.5px;
  }

  .ability-meta {
    font-size: 16px;
    color: #c8a960;
    font-style: italic;
    letter-spacing: 0.3px;
  }

  .ability-desc { line-height: 1.7; }

  .passive-badge {
    display: inline-block;
    background: #2a4a2a;
    color: #60c060;
    font-family: 'Cinzel', serif;
    font-size: 12px;
    letter-spacing: 1px;
    padding: 2px 8px;
    margin-left: 10px;
    border: 1px solid #3a6a3a;
    text-transform: uppercase;
  }

  .debuff {
    background: #2a1515;
    border: 1px solid #5a2020;
    padding: 18px;
    margin-bottom: 12px;
  }

  .debuff .ability-name { color: #c85050; }

  .debuff-type {
    display: inline-block;
    font-family: 'Cinzel', serif;
    font-size: 12px;
    letter-spacing: 1px;
    padding: 2px 8px;
    margin-left: 10px;
    border: 1px solid;
    text-transform: uppercase;
  }

  .debuff-persistent {
    background: #3a1515;
    color: #c87070;
    border-color: #5a2020;
  }

  .debuff-removable {
    background: #2a2a15;
    color: #c8c070;
    border-color: #5a5a20;
  }

  .debuff-environmental {
    background: #15202a;
    color: #7090c8;
    border-color: #204060;
  }

  .item {
    background: #0f1a30;
    border: 1px solid #2a2a4a;
    padding: 14px 18px;
    margin-bottom: 8px;
    display: flex;
    gap: 14px;
  }

  .item-icon {
    font-size: 18px;
    flex-shrink: 0;
    width: 30px;
    text-align: center;
    color: #d4a853;
  }

  .item-name {
    color: #d4a853;
    font-weight: 600;
  }

  .item-tag {
    font-size: 16px;
    color: #c8a960;
    font-style: italic;
    letter-spacing: 0.3px;
  }

  .item-desc {
    font-size: 15px;
    color: #b0a890;
    margin-top: 4px;
    line-height: 1.6;
  }

  .quest {
    background: #0f1a30;
    border: 1px solid #2a2a4a;
    padding: 18px;
    margin-bottom: 12px;
  }

  .quest-title {
    font-family: 'Cinzel', serif;
    font-weight: 600;
    font-size: 14px;
    color: #d4a853;
    margin-bottom: 8px;
  }

  .quest-desc {
    font-size: 15px;
    color: #c8b890;
    margin-bottom: 12px;
    line-height: 1.6;
  }

  .quest-step { padding: 4px 0; }
  .quest-step.done { color: #6b5a30; text-decoration: line-through; }
  .quest-step.done::before { content: '[x] '; color: #40a848; font-family: monospace; }
  .quest-step.pending::before { content: '[ ] '; color: #6b5a30; font-family: monospace; }

  .quest-side { border-color: #2a2a4a; }
  .quest-complete {
    border-color: #2a4a2a;
    background: #0f1a20;
  }
  .quest-complete .quest-title { color: #60a060; }

  .quest-label {
    font-family: 'Cinzel', serif;
    font-size: 12px;
    letter-spacing: 1px;
    padding: 2px 8px;
    margin-left: 10px;
    border: 1px solid;
    text-transform: uppercase;
  }

  .label-active { background: #2a2a15; color: #c8c070; border-color: #5a5a20; }
  .label-side { background: #15202a; color: #7090c8; border-color: #204060; }
  .label-complete { background: #152a15; color: #60a060; border-color: #205a20; }

  .ally {
    display: flex;
    gap: 14px;
    padding: 10px 0;
    border-bottom: 1px solid #1a1a3e;
  }

  .ally:last-child { border-bottom: none; }

  .ally-name {
    color: #d4a853;
    font-weight: 600;
    width: 100px;
    flex-shrink: 0;
  }

  .ally-role {
    color: #b0a890;
    line-height: 1.5;
  }

  .page-footer {
    max-width: 920px;
    width: 100%;
    margin: 16px auto 0;
    text-align: center;
    font-size: 14px;
    color: #4a4a5a;
    letter-spacing: 0.3px;
  }

  .quote {
    border-left: 3px solid #534320;
    padding: 10px 18px;
    margin: 10px 0;
    color: #b0a890;
    font-style: italic;
    background: #0f1520;
    line-height: 1.7;
  }
</style>
</head>
<body>
<div class="page">

  <!-- HEADER -->
  <div class="header">
    <div class="portrait">
      <img src="[USERNAME]-character-portrait.png" alt="[CHARACTER NAME]">
    </div>
    <div class="identity">
      <div class="name">[CHARACTER NAME]</div>
      <div class="tags">
        <span class="tag"><span class="tag-label">Family:</span> [FAMILY NAME]</span>
        <span class="tag"><span class="tag-label">Trade:</span> [TRADE NAME]</span>
        <span class="tag"><span class="tag-label">Temper:</span> [TEMPER NAME]</span>
      </div>
      <div class="level-alignment">Level [N] &middot; [ALIGNMENT]</div>
    </div>
  </div>

  <!-- TABS -->
  <div class="tabs">
    <button class="tab active" onclick="showTab('overview')">OVERVIEW</button>
    <button class="tab" onclick="showTab('abilities')">ABILITIES</button>
    <button class="tab" onclick="showTab('debuffs')">DEBUFFS</button>
    <button class="tab" onclick="showTab('inventory')">INVENTORY</button>
    <button class="tab" onclick="showTab('quests')">QUESTS</button>
    <button class="tab" onclick="showTab('party')">PARTY</button>
  </div>

  <!-- OVERVIEW PANEL -->
  <div class="panel active" id="panel-overview">
    <div class="overview-columns">
      <div class="overview-left">
        <h2>Class</h2>

        <div class="class-detail">
          <div class="class-detail-label">Family</div>
          <div class="class-detail-name">[FAMILY NAME]</div>
          <div class="class-detail-desc">[FAMILY DESCRIPTION]</div>
        </div>

        <div class="class-detail">
          <div class="class-detail-label">Trade</div>
          <div class="class-detail-name">[TRADE NAME]</div>
          <div class="class-detail-desc">[TRADE DESCRIPTION]</div>
        </div>

        <div class="class-detail">
          <div class="class-detail-label">Temper</div>
          <div class="class-detail-name">[TEMPER NAME]</div>
          <div class="class-detail-desc">[TEMPER DESCRIPTION]</div>
        </div>
      </div>

      <div class="overview-right">
        <h2>Stats</h2>

        <!-- Repeat this block for each stat: STR, DEX, CON, INT, WIS, CHA -->
        <!-- Use class str/dex/con/int/wis/cha on stat-row-wrap for bar color -->
        <!-- Calculate bar width: stat value multiplied by 5. E.g. stat 14 = width 70% -->
        <div class="stat-row-wrap str">
          <div class="stat-row" style="width:100%">
            <span class="stat-name">STR</span>
            <span class="stat-value">14</span>
            <div class="stat-bar-bg"><div class="stat-bar" style="width:70%"></div></div>
          </div>
          <div class="stat-desc">Sustained heavy load without breaking</div>
        </div>
        <!-- ... repeat for DEX, CON, INT, WIS, CHA with their values ... -->

      </div>
    </div>

    <h2>Story</h2>
    <div class="origin-intro">
      [ORIGIN STORY TEXT]
    </div>
  </div>

  <!-- ABILITIES PANEL -->
  <div class="panel" id="panel-abilities">

    <!-- Passive ability -->
    <div class="ability">
      <div class="ability-header">
        <span class="ability-name">[PASSIVE NAME] <span class="passive-badge">passive</span></span>
      </div>
      <div class="ability-desc">[PASSIVE DESCRIPTION]</div>
    </div>

    <h2>Active Abilities</h2>

    <!-- Repeat for each active ability -->
    <div class="ability">
      <div class="ability-header">
        <span class="ability-name">[ABILITY NAME]</span>
        <span class="ability-meta">[Type] &middot; [Cooldown] &middot; Cost: [Cost]</span>
      </div>
      <div class="ability-desc">[ABILITY DESCRIPTION]</div>
      <!-- Include a quote block if there is a representative quote -->
      <div class="quote">"[EXAMPLE QUOTE FROM POSTS]"</div>
    </div>

  </div>

  <!-- DEBUFFS PANEL -->
  <div class="panel" id="panel-debuffs">
    <h2>Active Debuffs</h2>

    <!-- Repeat for each debuff. Use debuff-persistent, debuff-removable, or debuff-environmental -->
    <div class="debuff">
      <div class="ability-header">
        <span class="ability-name">[DEBUFF NAME]</span>
        <span class="debuff-type debuff-[TYPE]">[TYPE]</span>
      </div>
      <div class="ability-desc">[DEBUFF DESCRIPTION WITH MECHANICAL EFFECT]</div>
    </div>

  </div>

  <!-- INVENTORY PANEL -->
  <div class="panel" id="panel-inventory">
    <h2>Equipped</h2>

    <!-- Repeat for each equipped item. Pick a fitting Font Awesome icon. -->
    <div class="item">
      <div class="item-icon"><i class="fa-solid fa-[ICON]"></i></div>
      <div>
        <div class="item-name">[ITEM NAME]</div>
        <div class="item-tag">[tags separated by middots]</div>
        <div class="item-desc">[ITEM DESCRIPTION]</div>
      </div>
    </div>

    <h2>In Pack</h2>

    <!-- Repeat for each pack item -->
    <div class="item">
      <div class="item-icon"><i class="fa-solid fa-[ICON]"></i></div>
      <div>
        <div class="item-name">[ITEM NAME]</div>
        <div class="item-tag">[tags]</div>
      </div>
    </div>

  </div>

  <!-- QUESTS PANEL -->
  <div class="panel" id="panel-quests">
    <h2>Active Quest</h2>

    <div class="quest">
      <div class="quest-title">[QUEST NAME] <span class="quest-label label-active">active</span></div>
      <div class="quest-desc">[QUEST DESCRIPTION]</div>
      <!-- Use quest-step done or quest-step pending -->
      <div class="quest-step done">[COMPLETED STEP]</div>
      <div class="quest-step pending">[PENDING STEP]</div>
    </div>

    <h2>Side Quests</h2>

    <div class="quest quest-side">
      <div class="quest-title">[SIDE QUEST NAME] <span class="quest-label label-side">side</span></div>
      <div class="quest-desc">[SIDE QUEST DESCRIPTION]</div>
    </div>

    <h2>Completed</h2>

    <div class="quest quest-complete">
      <div class="quest-title">[QUEST NAME] <span class="quest-label label-complete">complete</span></div>
      <div class="quest-desc">[QUEST DESCRIPTION]</div>
    </div>

  </div>

  <!-- PARTY PANEL -->
  <div class="panel" id="panel-party">
    <h2>Allies</h2>

    <!-- Repeat for each ally -->
    <div class="ally">
      <span class="ally-name">[NAME]</span>
      <span class="ally-role">[ROLE AND HOW THEY COLLABORATE]</span>
    </div>

    <h2>Relationship Style</h2>
    <p>[RELATIONSHIP STYLE DESCRIPTION]</p>

    <h2>Role in Party</h2>
    <p>[PARTY ROLE DESCRIPTION]</p>
  </div>

  <div class="page-footer">
    ~[N] posts &middot; [SITE URL] &middot; [DATE RANGE] &middot; Generated [DATE]
  </div>

</div>

<script>
function showTab(name) {
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  document.getElementById('panel-' + name).classList.add('active');
  event.target.classList.add('active');
}
</script>
</body>
</html>
```

---

## Phase 5: Wrap Up

After generating both files, tell the user:

1. The two files that were created and where they are
2. To generate a portrait, they can create pixel art (Might and Magic III style
   works well) and save it as `{username}-character-portrait.png` in the same
   directory
3. Open the HTML file in a browser to see the interactive character page
