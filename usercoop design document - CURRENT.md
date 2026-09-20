# USERCOOP Design Document

## Contents

- [Purpose](#purpose)
- [A personal programmable expert system](#a-personal-programmable-expert-system)
  - [Knowledge and programming](#knowledge-and-programming)
  - [Teaching and use](#teaching-and-use)
  - [Subjective upper ontology](#subjective-upper-ontology)
  - [Initiative and bounded autonomy](#initiative-and-bounded-autonomy)
  - [The device as a known world](#the-device-as-a-known-world)
  - [The session as point of contact](#the-session-as-point-of-contact)
  - [Cooperation in lived time](#cooperation-in-lived-time)
- [Core proposition](#core-proposition)
- [Design principles](#design-principles)
- [Offline by construction](#offline-by-construction)
  - [Local communication](#local-communication)
  - [External network boundary](#external-network-boundary)
- [Activities and contextual vocabulary](#activities-and-contextual-vocabulary)
  - [Activity stack](#activity-stack)
  - [Contextual language sources](#contextual-language-sources)
  - [Entering and leaving activities](#entering-and-leaving-activities)
- [Command language](#command-language)
  - [Deterministic interpretation](#deterministic-interpretation)
  - [Patterns and composition](#patterns-and-composition)
  - [Pipes and variables](#pipes-and-variables)
- [Live composition](#live-composition)
  - [Incremental semantic state](#incremental-semantic-state)
  - [Valid continuations](#valid-continuations)
  - [Case-shifting parser feedback](#case-shifting-parser-feedback)
  - [Provisional cognitive context](#provisional-cognitive-context)
- [User-authored and system-generated information](#user-authored-and-system-generated-information)
  - [Typed-line information](#typed-line-information)
  - [Spaces showing typed lines](#spaces-showing-typed-lines)
  - [Command failure events](#command-failure-events)
  - [History and citation](#history-and-citation)
- [Information and spaces](#information-and-spaces)
  - [Semantic content](#semantic-content)
  - [Presentation belongs to USERCOOP](#presentation-belongs-to-usercoop)
  - [Multiple representations](#multiple-representations)
- [Typography](#typography)
  - [Font system](#font-system)
  - [Monospace scales](#monospace-scales)
  - [Case as parser feedback](#case-as-parser-feedback)
  - [Text arrives through time](#text-arrives-through-time)
  - [Text without visible containers](#text-without-visible-containers)
  - [Writing discipline](#writing-discipline)
- [Presentation preferences](#presentation-preferences)
  - [Granularity](#granularity)
  - [Occupancy](#occupancy)
  - [Sport-to-zen pace](#sport-to-zen-pace)
  - [Preferences are equilibria](#preferences-are-equilibria)
- [Automatic composition and attention](#automatic-composition-and-attention)
  - [Attention from command traffic](#attention-from-command-traffic)
  - [Importance and task distance](#importance-and-task-distance)
  - [Value versus handling time](#value-versus-handling-time)
  - [Criticality](#criticality)
  - [Shared scales](#shared-scales)
- [Spatial composition](#spatial-composition)
  - [Rendering layers](#rendering-layers)
  - [Projected information spaces](#projected-information-spaces)
  - [The developing wall](#the-developing-wall)
  - [Directional grammar](#directional-grammar)
  - [Overview and ongoing activities](#overview-and-ongoing-activities)
  - [Camera language](#camera-language)
- [Motion, reactivity, and stability](#motion-reactivity-and-stability)
  - [Foreground reactivity](#foreground-reactivity)
  - [Background hysteresis](#background-hysteresis)
  - [Returning to equilibrium](#returning-to-equilibrium)
- [Interaction and accessibility](#interaction-and-accessibility)
- [Visual direction](#visual-direction)
- [System boundary](#system-boundary)
  - [Semantic kernel](#semantic-kernel)
  - [Session and inference runtime](#session-and-inference-runtime)
  - [Device observation and action](#device-observation-and-action)
  - [Applications and command execution](#applications-and-command-execution)
  - [Operating-system authority](#operating-system-authority)
  - [Godot application boundary](#godot-application-boundary)
- [Personal-device targets](#personal-device-targets)
- [Implementation](#implementation)
  - [Initial application structure](#initial-application-structure)
  - [Semantic data is not the scene tree](#semantic-data-is-not-the-scene-tree)
  - [Knowledge language](#knowledge-language)
  - [Reasoning capabilities](#reasoning-capabilities)
  - [Incremental inference](#incremental-inference)
  - [Persistence](#persistence)
  - [Initial implementation direction](#initial-implementation-direction)

## Purpose

This document specifies an interaction system, command model and display model, independent of any one application.

The intended end product is a Godot application that provides a calm, quiet, and restrained alternative to both text-mode terminals and conventional windowing systems. It offers a different way to operate a computer, smartphone, or tablet. Smartphones and tablets are first-class targets: their personal, continuous, touch-oriented use makes them especially appropriate devices for USERCOOP.

USERCOOP acts as a global interaction identity for the device. Here, identity refers to the coherent way the device presents itself and responds to its user, not to the identity of the user. By running USERCOOP, the device acquires a consistent activity model, command language, presentation logic, and interaction character across the capabilities it makes available.

The project is primarily about maintaining and applying personal knowledge through lived sessions, including knowledge of and action upon the device itself. User accounts, online identity, and service aggregation are not its organizing concern.

## A personal programmable expert system

USERCOOP is an offline, personal, programmable expert system. It lets the user build, examine, extend, and apply knowledge about a locally defined world, and it can operate the device as part of that world.

It is not primarily an application launcher, conversational assistant, or integration layer. It may operate applications as objects on the device, but it is itself the persistent knowledge and action system with which the user cooperates.

"Personal" means that its concepts, vocabulary, classifications, rules, procedures, and stored knowledge belong to the user and remain on the device. It does not refer to an online identity, behavioral profile, or service account.

### Knowledge and programming

USERCOOP may know and manage:

- Objects and stable identities.
- Types, categories, properties, and values.
- Relationships among objects.
- Events and changes.
- Collections and selections.
- Conditions, constraints, and rules.
- Procedures and available actions.
- Temporal facts and histories.
- Sources, provenance, and derivations.
- Conflicts, failures, and information that is no longer current.

The user can state facts, retrieve knowledge, define concepts, establish rules, and create procedures through the same deterministic language used to operate the system. Programming USERCOOP means teaching it durable vocabulary and behavior, not crossing into a separate conventional programming environment.

An immediate instruction, a reusable definition, a query, and a rule for future action all operate on the same semantic world:

```text
ALICE WORKS ON ORION
SHOW PEOPLE WORKING ON ORION
AN ACTIVE PROJECT IS A PROJECT WITH NO COMPLETION DATE
WHEN A PROJECT IS COMPLETED ARCHIVE ITS WORKING FILES
```

These examples indicate functional categories rather than fixing the final syntax.

USERCOOP distinguishes knowledge explicitly stated by the user, observed from the device, derived through rules, and produced by actions. A derivation follows inspectable deterministic rules. Ambiguity, contradiction, and failure become information items rather than occasions for the system to guess.

Something may remain known without currently being shown. The relationship is:

```text
knowledge item
    ↓ represented for the current context as
information item
    ↓ presented through
space
```

### Teaching and use

Teaching USERCOOP and using USERCOOP are the same ongoing activity. The user does not first prepare an expert system and later consult it. Facts, vocabulary, rules, procedures, corrections, and questions accumulate while the system is already being used.

A new installation begins as an expert system primarily about itself: what it is, what it intends, what it can do, how it reasons, and which parts of its knowledge it is permitted to modify on its own. It becomes personal through continued interaction.

The system must support sophisticated knowledge when the user supplies it. A personal scope does not imply simple subject matter or shallow inference.

### Subjective upper ontology

USERCOOP's upper ontology begins with the system doing the inference. It understands itself as a program situated on a device, acting through explicit capabilities, during a session shared with its user.

This is subjective in the sense of viewpoint, not emotion. Identity, intention, observation, action, permission, time, and explanation are organized around what USERCOOP is and how it participates in the world it knows.

"Because the user told me to" is not a complete explanation. A fuller chain includes the system's own standing intent to follow that instruction, the rule that connected it to an action, the capability that authorized the action, and the result.

Built-in policies use the same kind of knowledge as user-created policies. Retention, explanation, initiative, and self-audit begin with defaults. The owner may inspect and change any of them. USERCOOP may change them on its own only where the owner has explicitly granted that authority.

### Initiative and bounded autonomy

USERCOOP may act on its own initiative. It can advance inference, bring information forward, pilot the screen, begin an authorized procedure, or ask the user for knowledge it needs.

Initiative is bounded programmatically and modularly. The user determines:

- Which folder or other local scope is visible.
- Which device capabilities are authorized.
- Which parts of the knowledge base USERCOOP may modify on its own initiative.
- Which rules may initiate actions and which require confirmation.

External network access is never among the available capabilities. A rule cannot escape the capability boundary merely because its conclusion recommends an action.

### The device as a known world

The device is where USERCOOP runs, one of the worlds it knows about, and an environment in which it can act. Files, folders, applications, processes, settings, notifications, hardware state, typed lines, and operation results can all become objects, facts, events, or actions within the knowledge base.

Device management is therefore an expert domain of USERCOOP rather than a collection of unrelated utilities. Device facts can participate in queries, rules, and procedures just like user-defined knowledge:

```text
REPORT.PDF IS IN PROJECT ORION
EDITOR IS RUNNING
BATTERY LEVEL IS 18 PERCENT
WHEN BACKUP IS CONNECTED SHOW UNARCHIVED PROJECTS
```

Applications may be found, launched, focused, or stopped as objects and capabilities of the device. They are not the semantic foundation of USERCOOP and do not replace its knowledge model with their own interaction systems.

### The session as point of contact

The current session is itself a perdurant: something that persists and develops through time. It exists both as an object known to USERCOOP and as a real interval in the user's life. It is the point of contact between the system's semantic world and the temporality the user is actually living and working through.

A session is not merely the duration for which an executable remains open, a connection, or a container for transient interface state. It has a beginning, an evolving present, accumulated events and activities, interruptions, resumptions, and an eventual ending. It may be part of a longer undertaking while also containing shorter activities of its own.

Within the system, the session can be known through its current activities, ongoing work, completed steps, elapsed time, relevant objects, commitments, events, and changes of direction. Within the user's life, it is the actual period in which attention, effort, choice, and progress occur. USERCOOP's cooperation happens where those two descriptions meet.

The session is therefore the current focal perdurant around which the active knowledge display, activity stack, `ongoing stuff` list, attention model, and temporal rules are composed. Activities do not float in an abstract interface; they occur during this lived session and contribute to its development.

Time is part of the ontology, not merely a timestamp attached to facts. USERCOOP should represent events, states, intervals, and their relations. Allen's interval algebra is an initial foundation for relations such as before, during, overlapping, meeting, and finishing.

### Cooperation in lived time

USERCOOP is expected to cooperate with the user in the temporality of the current session. This includes, without reducing the system to a productivity application:

- Task management: knowing what is intended, active, paused, completed, blocked, or newly relevant.
- Work-time management: relating activities to available time, duration, sequence, interruption, resumption, and stopping points.
- Personal-growth management: maintaining locally defined goals, practices, learning, reflection, and progress across sessions.
- Context preservation: keeping paused work developed and resumable rather than forcing the user to reconstruct it mentally.
- Temporal attention: bringing forward knowledge when it becomes relevant to the current point in an undertaking.
- Session reflection: making what happened, changed, or remains unfinished available as knowledge rather than as an automatically generated judgment.

These are not isolated modules placed beside the knowledge base. Tasks, time, growth, and sessions are themselves knowledge domains expressed through the same objects, relationships, rules, events, histories, and activities as the rest of USERCOOP.

The system does not need to infer a hidden life plan or decide what personal growth should mean. The user defines the relevant concepts, commitments, measures, and rules. USERCOOP contributes memory, structure, derivation, temporal awareness, presentation, and action within those explicit terms.

## Core proposition

The interface is not a collection of windows that the user must arrange and monitor manually. It continuously materializes the user's evolving semantic context.

USERCOOP is a semantic interaction layer through which the user pilots the device. Rather than requiring the user to navigate the separate interfaces of files, applications, notifications, and system facilities, it coordinates those existing capabilities around the user's current intention.

The command stream serves two purposes at once:

1. It states what the user wants USERCOOP to know, infer, or do.
2. It provides an ongoing trace of what currently occupies the user's attention.

The display responds to that trace. It selects information, changes its level of detail, adjusts how much is simultaneously visible, moves focus, and reveals valid continuations while the instruction is still being composed.

The result is neither a conventional graphical desktop nor a conventional terminal:

| Conventional model | Primary organization |
|---|---|
| Window system | Applications arranged as rectangles |
| Terminal | Input and output arranged as one chronological stream |
| This system | Information arranged around the user's current activity and developing intention |

## Design principles

1. **Never guess.** An instruction resolves deterministically or fails without being replaced by a guessed interpretation. Failure generates a semantic event associated with the originating input line.
2. **Reveal the current language.** The system shows what is valid in the present context instead of requiring memorization of a global command set.
3. **React before submission.** A partial instruction may already resolve objects, narrow possibilities, and reorganize the display.
4. **Preserve authorship spatially.** User-authored and system-generated information items receive visibly distinct presentations, so their origin is apparent without classifying their content.
5. **Compose the display automatically.** The system decides what appears, where, and at what scale.
6. **Treat preferences as defaults, not prohibitions.** Explicit requests and genuine information requirements may temporarily override the user's resting presentation preferences.
7. **Be lively in the foreground and stable in the background.** Active composition may cause rapid meaningful movement; unrelated information changes conservatively.
8. **Keep content semantic.** Knowledge describes meaning and available action. USERCOOP owns presentation.
9. **Support the device's input modes.** Keyboard interaction is primary where available, but every action remains accessible through mouse or touch.
10. **Remain offline by construction.** USERCOOP must be programmatically unable to reach external networks. Its operation must never depend on Internet access or a remote service, and this boundary has no protocol-specific exception.
11. **Reward attention without demanding it.** A refinement should be perceptible to someone who attends to it while remaining unobtrusive to someone who does not. USERCOOP favors effects that can be noticed without insisting on being noticed.
12. **Allow initiative only through capabilities.** USERCOOP may ask, infer, present, and act on its own initiative, but only within user-defined knowledge and device boundaries.

## Offline by construction

Offline operation is a foundational property of USERCOOP, not merely a mode, preference, or promise about ordinary behavior. The application must be architected so that its runtime cannot initiate or receive communication across an external network.

This boundary keeps operation of the device local, makes the system useful without connectivity, and prevents the interaction layer from becoming an implicit conduit through which device activity or command history can leave the device. No adapter or extension may silently weaken this property.

Features that conventionally depend on online services are not performed by USERCOOP over the network. Where appropriate, USERCOOP may invoke a capability belonging to another installed application or to the operating system. That external application remains visibly and technically responsible for its own networking, permissions, and results.

### Local communication

Communication confined to the device is permitted when it is needed to connect USERCOOP to local adapters, applications, or system bridges. Possible transports include:

- Loopback TCP connections.
- Local WebSocket connections bound only to a loopback interface.
- Operating-system facilities such as local sockets, named pipes, or equivalent inter-process communication.

Such transports are implementation details of an in-device system. They must not listen on externally reachable interfaces, accept remote peers, or provide a route from a local component to an external network through USERCOOP.

"Local" means strictly within the same physical device that is running USERCOOP. Other computers, phones, appliances, or services on a trusted local-area network are external for the purpose of this principle and are not reachable by USERCOOP.

### External network boundary

The external-network restriction should be enforced programmatically and by architecture rather than relying only on convention. USERCOOP must not expose a general-purpose Internet client to its semantic kernel, rules, or adapters. Device adapters receive only the local capabilities required for their work, and the deployed application must be testable for the absence of externally reachable network paths.

The intended implementation is one coherent Godot application capable of performing the work required by USERCOOP. A separate general-purpose network broker is not part of the architecture. Where operating-system integration requires local IPC, USERCOOP may communicate with facilities already belonging to the same device.

This principle concerns USERCOOP itself. Launching a mail composer, browser, or other network-capable application through an operating-system action does not make USERCOOP the network client. The handoff must remain explicit, and USERCOOP must not silently collect, proxy, or transmit the resulting network traffic.

## Activities and contextual vocabulary

USERCOOP shows the user the vocabulary, information, and actions relevant to the current activity. An application does not present a parallel interface inside USERCOOP. USERCOOP remains the interaction system throughout.

[Symbolfront](https://github.com/symbolworks/symbolfront) is relevant prior art for one narrower idea: command vocabulary can be supplied by the current context instead of being permanently hard-coded as one global command set. USERCOOP adopts that principle within its own activity model; Symbolfront is not part of the runtime.

An activity is a temporary semantic environment:

```text
Activity
├── identity
├── parent activity
├── current semantic state
├── available commands
├── valid argument patterns
├── visible information sources
├── possible actions
├── completion conditions
└── exit or return behavior
```

### Activity stack

Activities form a stack. Entering a more specific activity pushes a context; completing, rejecting, or leaving it returns to its parent.

```text
Current session
└── Manage tasks
    └── New task
        └── Choose date and time
```

The activity stack is cognitive as well as navigational. Each level changes the relevant objects, available language, appropriate information, and likely next actions.

### Contextual language sources

USERCOOP determines the language currently shown to the user from the active activity, semantic types, rules, and capabilities known to the system. Its kernel defines:

- Commands valid in the current activity.
- Syntax patterns for those commands.
- Semantic types accepted by each slot.
- Candidate objects that may fill those slots.
- Actions that enter, complete, reject, or leave activities.
- Information items relevant to the activity.

A device adapter may register bounded facts, types, and authorized action signatures with that kernel. It does not define the activity or its presentation. USERCOOP performs parsing and discovery, shows valid continuations, manages history and attention, gives information space on the screen, and provides keyboard, mouse, and touch interaction.

### Entering and leaving activities

The user enters an activity, performs the work appropriate to it, and leaves when finished. The display adapts for the duration of that activity and releases its temporary information when the activity closes.

This is not equivalent to opening and closing an application window. An activity may draw on several knowledge domains and device capabilities while remaining one coherent cognitive context.

## Command language

The primary interaction is keyboard-driven through an active typing space. The vocabulary is terse and mechanical, taking inspiration from the archetypal keyboard scenes in *Tron* (1982) and *WarGames*.

SHRDLU is a spiritual ancestor rather than a syntax to copy. Its natural-language interface worked because it resolved against a small, closed, well-defined world of objects, relations, and actions. The same property permits deterministic resolution here.

REXX contributes the principle of least astonishment: the meaning of an instruction should follow from its visible words, without hidden precedence surprises or punctuation doing silent work.

### Deterministic interpretation

- A command that resolves cleanly is accepted.
- A submitted command that does not resolve cleanly does not execute and generates an error event associated with its input line.
- Fuzzy matching never silently substitutes a plausible interpretation.
- Every intermediate reduction follows an ordered, inspectable pattern list.

### Patterns and composition

Patterns use word position rather than punctuation to mark argument roles:

```text
PUT x INTO y
x TALLER THAN y
HELD x
```

Words that identify a pattern are reserved and cannot also serve as object names. Patterns are organized as an ordered list defining explicitly their precedence, and reduce from the highest precedence outward.

Worked example:

```text
PUT BLOCK TALLER THAN HELD BLOCK INTO BOX
```

1. `HELD BLOCK` matches `HELD x` and resolves to one held block, `OBJ1`.
2. `BLOCK TALLER THAN OBJ1` matches `x TALLER THAN y` and resolves to `OBJ2`.
3. `PUT OBJ2 INTO BOX` matches the outer operation and executes.

### Pipes and variables

Selections and results can be piped into later operations or stored in named variables. A selection may be piped into a display instruction, for example, causing the view to reveal it, or retained for reuse across later commands.

## Live composition

The screen reacts while the user types. Submission is not the first moment at which an instruction has meaning.

### Incremental semantic state

For every partial instruction, the parser exposes:

- Recognized keywords.
- Resolved subexpressions.
- Unresolved slots.
- Valid continuations.
- Candidate referents.
- Current semantic types.
- Temporary activity contexts.
- Likely spatial or informational focus.

This state drives the display immediately without executing the unfinished instruction.

### Valid continuations

The interface always shows what may validly follow from the current parser state. These are contextual possibilities, not a global command catalogue.

Entering an activity narrows the language. Filling an argument narrows it again. Completing or abandoning the activity restores the parent vocabulary.

### Case-shifting parser feedback

The ordinary appearance of user input is uppercase. In the large majority of composition, letters appear and remain uppercase as the instruction is recognized.

Lowercase is exceptional and carries specific parser feedback:

- A value recognized as a variable appears in lowercase, confirming that it is being interpreted as a variable rather than as command vocabulary.
- A sequence that no longer matches the language appears in lowercase, signaling a likely typo or other failure of recognition.

The display updates retroactively as understanding changes. The user can therefore see recognition directly in the letters without needing an additional icon, underline, or diagnostic message.

### Provisional cognitive context

Resolved portions of an unfinished instruction already affect the surrounding display.

While composing:

```text
PUT BLOCK TALLER THAN HELD BLOCK INTO BOX
```

the interface may progress as follows:

| Partial instruction | Provisional response |
|---|---|
| `PUT` | Open an operation context |
| `PUT BLOCK` | Make candidate blocks relevant |
| `PUT BLOCK TALLER THAN` | Reveal comparison information |
| `HELD` | Emphasize held-object categories |
| `HELD BLOCK` | Resolve a particular object and begin framing it |

If `HELD BLOCK` deterministically resolves to an object, a spatial view may begin panning and zooming toward it before the outer command is complete. Backspacing or changing the instruction unwinds that provisional context.

This movement is intended. The display should appear to live alongside rapid typing, as in the keyboard-driven scenes that inspired it.

## User-authored and system-generated information

The screen is not divided into applications, windows, or a terminal plus an output area. It is one composed workspace containing spaces. A space gives temporary visual presence to an information item or related group of information items: a line being typed, a submitted line, a set of valid continuations, a notification, a spatial view, or another part of the current activity.

Spaces are not user-managed windows and need not be persistent rectangles. USERCOOP creates, emphasizes, transforms, moves, and releases them as it composes the screen around the current activity.

The distinction between what the user authored and what the system generated is spatial rather than conversational. User-authored information items receive recognizably different spaces from results, errors, notifications, and other system-generated information. An observer can therefore recognize origin from placement and presentation without first reading and classifying the content.

### Typed-line information

A line being typed is itself an information item known to USERCOOP. While it is being composed, it is mutable and carries its current text together with the semantic state produced by incremental parsing. Submission changes it into a submitted-line information item and assigns it a permanent line number.

The information item and its visual presentation are distinct. The line does not inherently occupy a particular position, size, or shape, and it is not itself a space.

### Spaces showing typed lines

USERCOOP ordinarily gives the line being typed a large, prominent space. It gives recently submitted lines separate, smaller spaces nearby. Those presentation choices provide continuity without forming a terminal, console, transcript, or chronological input-output stream.

Spaces representing typed-line information show only text authored by the user and parser feedback applied to that text. System-generated results, failures, notifications, and automatic information receive other spaces elsewhere in the composition.

### Command failure events

A failing command does not answer the user with an explanation and does not add system-generated content to the submitted-line information item. It generates a separate semantic event such as `input line 47 error`.

That event becomes another information item managed by USERCOOP. It may receive importance, be given a space, affect attention, persist, recede, or be displaced under the same composition principles as other information. Its stable association with the submitted-line item lets USERCOOP present the failure in context without changing the user-authored item.

The event may contain structured failure data needed by USERCOOP to identify and manage it, but it is not inherently a prose response or conversational explanation. The presentation of that data remains a decision of the interaction system.

### History and citation

History and line numbers belong to the local USERCOOP installation. The user may configure what is visible and delete local history.

Deleting history never resets the line counter. A citation such as `line 47` therefore always identifies the same command, even if that command has since been deleted. A request for a deleted line generates a system information item.

Applications and device capabilities respond through ordinary operation correlation and never need to know USERCOOP's local line numbers. USERCOOP knows which local line caused an operation and may cite it when presenting the result. Separate USERCOOP installations therefore need no synchronized numbering.

Past history is itself retrieved through a command such as `SHOW LINE 47`. Mouse or touch scrolling remains available as an accessibility alternative. The requested line is given its own space, accompanied by a small reminder of the command that produced it.

## Information and spaces

An information item describes something USERCOOP may need to manage: its meaning, identity, content, relevance, and available actions. A space is the presence USERCOOP gives that item on the screen. The information item is semantic; the space is compositional.

Neither is a window or a card. An information item does not prescribe a rectangle, coordinates, or visual hierarchy. One item may move between spaces or representations as attention changes, and several related items may share a space when USERCOOP judges that they belong together.

### Semantic content

An information item is a contextual representation of knowledge. Its definition may include:

- Semantic type.
- Subject and stable identity.
- Content fields.
- Available actions.
- Intrinsic importance.
- Estimated handling time, when meaningful.
- Closing window or criticality inputs, when meaningful.
- Provenance and derivation.
- Supported representations.
- Minimum representation required by the current situation.

Facts observed through a device adapter enter the same knowledge model as facts stated by the user or derived by rules. Intrinsic content such as a document or message remains itself; an adapter does not gain control over how USERCOOP arranges or presents the workspace.

### Presentation belongs to USERCOOP

USERCOOP decides:

- Whether the information item is currently given space.
- Where it appears.
- Which representation appears in that space.
- How much emphasis it receives.
- When it displaces or is displaced by other information.
- How it transitions between states.
- How user preferences influence it.

### Multiple representations

An information item may support several semantic representations rather than arbitrary continuous resizing:

| Representation | Purpose |
|---|---|
| Overview | Identity, state, and most important summary |
| Standard | Information needed for ordinary work |
| Detailed | Full inspection or active manipulation |

These representations concern granularity. They do not determine how many other information items may simultaneously be given space.

## Typography

Text is the principal kind of perceptible information exchanged between USERCOOP and the user. Typography is therefore part of the interaction model rather than decoration applied after the interface has been designed. It must make the system cognitively affordable, visibly responsive, and capable of exposing technical depth without allowing that depth to dominate.

The goal is not to select fonts that call attention to their own beauty. The fonts should stay out of the way of USERCOOP being both beautiful and useful.

### Font system

USERCOOP uses two principal font families:

1. A proportional reading family that is comfortable for ordinary information and supports variable weight.
2. A monospaced family for user input, formatted content, and technical reference information, preferably also supporting variable weight.

Headings use the same proportional family as ordinary reading text. They are larger but set at a lighter stroke weight, so the increase in size does not produce a correspondingly heavy visual mass. This refers to the thickness of the strokes that form each letter, not to preserving the horizontal width of the complete line.

The small number of families gives USERCOOP one coherent typographic identity across applications and information sources. Changes of size, weight, spacing, and alignment provide hierarchy without making each kind of information appear to come from a different interface.

Font selection must prioritize:

- Comfortable sustained reading at ordinary sizes.
- Clear distinction among easily confused characters.
- Strong uppercase and lowercase forms.
- Useful punctuation, mathematical symbols, and numerals.
- Reliable rendering at both very large and very small sizes.
- Broad language coverage and deliberately chosen offline fallbacks.
- Stable character and line metrics across the weights USERCOOP uses.
- Licensing that permits the complete font set to be bundled and used offline.

### Monospace scales

The monospaced family has three characteristic scales:

- **Large:** user input. The line being typed is roughly twice the ordinary text size. It is the clearest and most immediate evidence that the device is receiving the user's intention.
- **Normal:** formatted or structurally literal content for which fixed character alignment is useful.
- **Very small:** quasi-irrelevant or technical reference information such as object identifiers, line numbers, software versions, and internal correlations.

The very small scale makes the machinery visible without making it central. Experienced users may read and use it. Other users may perceive it as quiet evidence that USERCOOP is listening, interpreting, and doing real work. Their own input remains large, meaningful information remains normally sized, and supporting machinery forms subtle visual texture around it.

Essential information must not depend on the very small scale. When technical information becomes relevant or is explicitly requested, USERCOOP gives it an ordinary readable representation.

The use of large monospaced uppercase input deliberately retains the directness associated with fictional and historical command interfaces: a person sits at a computer, states what they want in simple letters, and the device responds. This is not retro styling for nostalgia. It is a cognitively affordable interaction in which users do not need mastery of menus, keyboard punctuation, underscores, or elaborate syntax merely to address the device.

### Case as parser feedback

Uppercase is the normal visual state of user input. Lowercase is reserved for the two exceptional semantic conditions defined by live parsing: recognized variables and text that is not currently recognized, such as a developing typo.

Case therefore communicates understanding within the text itself. A change to lowercase is visible confirmation rather than an added warning ornament. Because uppercase is normal, these exceptions remain clear and uncommon.

### Text arrives through time

Every text appears letter by letter. A complete line is never materialized instantaneously when USERCOOP first presents it in a space.

The reveal is quick and does not turn an ordinary line into a long-running typewriter performance. Its purpose is to give textual appearance a perceptible duration: the system is listening, composing, and cooperating rather than dropping finished rectangles of content onto the screen. The effect should be apparent to someone attending to it while remaining natural and unobtrusive to someone who is not.

User input naturally appears at the pace of typing. System-generated text uses a brief controlled cadence appropriate to the current sport-to-zen pace and interaction cadence. Urgency, readability, and accessibility may accelerate the reveal, but its ordinary character remains progressive rather than instantaneous.

Letter-by-letter revelation belongs to the presentation of an information item, not to its semantic storage. USERCOOP may already know the complete text while its current space reveals that text through time.

### Text without visible containers

Information spaces do not normally draw rectangular containers around text. Internally, a 2D control still has bounds for layout, projection, focus, and interaction, but those bounds do not need to become a visible card or panel.

Text primarily needs an anchor, a vertical alignment line, a readable measure, and a meaningful relationship to nearby information. It may be left-aligned, centered, or right-aligned according to its role in the spatial grammar. Empty space, alignment, typography, and movement establish grouping before borders or backgrounds are considered.

Camera distance changes the room available to an information representation, not the basic legibility of its font. When less room is available, the item says less: it moves from detailed to standard to overview representation rather than continuously shrinking its text. The invisible projected rectangle remains useful as layout geometry even when no rectangle is visually drawn.

### Writing discipline

USERCOOP's own text is composed from simple sentences and short lines. When several short statements will communicate something clearly, they are preferred to a dense paragraph or a long line forced into an arbitrary container.

Device adapters and importers should supply semantic facts, identity, state, relationships, and actions wherever possible. USERCOOP remains responsible for expressing ordinary interface information in its coherent voice. Intrinsic content such as a message, document, or source file remains the content itself and may require longer-form reading.

Icons and emoji are not part of USERCOOP's interaction vocabulary. The system relies on letters, words, case, weight, scale, alignment, space, and movement rather than asking the user to learn a parallel symbolic language.

## Presentation preferences

The earlier idea of a single density preference combines two independent questions. They must remain separate.

### Granularity

Granularity expresses the user's resting preference between overview and detail.

- **Overview:** summarize first; let detail earn space or appear on request.
- **Detail:** expose more structure and supporting information by default.

### Occupancy

Occupancy expresses the user's resting preference for the total amount of information simultaneously visible.

- **Sparse:** preserve empty space and give fewer information items space at once.
- **Rich:** permit more concurrent information and a busier display.

The two axes form four legitimate regions:

|  | Overview | Detail |
|---|---|---|
| **Sparse** | Calm global picture | One subject examined deeply |
| **Rich** | Many compact summaries | Many detailed subjects at once |

### Sport-to-zen pace

A gradual **sport-to-zen** preference describes the user's resting preference for the pace and motion character of the interface.

- **Sport:** quicker acceleration, faster settling, shorter pauses, and a more immediate feeling of response.
- **Zen:** gentler acceleration, longer settling, more breathing room, and a more contemplative feeling of response.

The scale is continuous rather than a choice between two modes. It governs the motion and temporal presentation of the same semantic behavior; it does not make commands less deterministic, delay essential feedback, or change what the user is authorized to do.

The selected value is a baseline. USERCOOP may move temporarily around it to match the user's current **interaction cadence**: the general speed at which the user is presently typing, choosing, and advancing through the activity. Typing speed, intervals between actions, correction cadence, and rate of progression provide immediate local indications of that pace.

A rapid, sustained interaction cadence may pull presentation toward the sport side, as when the user is working in a hurry. Longer intervals and an unhurried cadence may pull it toward the zen side, as during a relaxed or exploratory session. USERCOOP responds to the demonstrated pace itself and does not need to infer why the user has adopted it.

Adaptation must be gradual, bounded, and resistant to oscillation. A brief burst of typing or a single pause must not cause a conspicuous change of character. Cadence is estimated entirely on the device from interaction timing already available to USERCOOP. The user may constrain or disable adaptation while retaining a fixed sport-to-zen preference.

### Preferences are equilibria

Preferences describe where the display rests when no stronger requirement exists. They are not hard limits.

Precedence is:

1. **Explicit request.** If the user asks for detail, show detail.
2. **Semantic requirement.** If information cannot be understood safely in a compact form, use the required representation.
3. **Simultaneous importance and criticality.** If several matters genuinely require attention, temporarily increase occupancy.
4. **Standing preference.** When the system has a choice, return toward the user's preferred granularity, occupancy, and sport-to-zen pace.

A sparse preference means “when possible, show less,” not “conceal simultaneous important information.” An overview preference means “begin with summaries,” not “withhold detail that was requested.”

The sport-to-zen preference is likewise an equilibrium rather than a fixed animation multiplier. Current interaction cadence, semantic urgency, and accessibility requirements may shift motion away from that equilibrium. When those pressures end, the interface settles back toward the chosen baseline.

## Automatic composition and attention

The user is not expected to move, resize, close, or scroll through arbitrary windows. USERCOOP decides what is shown, how, and where within its presentation grammar.

Automatic composition is primarily editorial judgment rather than geometric novelty. The essential problem is selecting and presenting the right information, not discovering clever coordinates for rectangles.

### Attention from command traffic

The current session and command stream are the primary attention signals. Something the user repeatedly references, selects, compares, or acts upon remains visible and prominent. Rules and active inference may also bring information forward on USERCOOP's initiative. Once attention moves elsewhere, information recedes and may eventually be displaced.

“Busy with something” is inferred from semantic command activity. No separate behavioral surveillance signal is required.

### Importance and task distance

George Furnas's 1986 *Generalized Fisheye Views* defines Degree of Interest as:

```text
DOI(x) = API(x) - D(x, y)
```

`API(x)` is a priori importance. `D(x, y)` is distance from the current focus, which Furnas permits to be logical or task distance rather than physical distance.

Here, task distance is derived from the active activity stack and command stream: recency of reference, frequency of reference, semantic relationship to resolved command objects, and relationship to unfinished slots.

Given a limited display budget, USERCOOP gives space to the highest-interest information items.

### Value versus handling time

“Quick to handle and rewarding relative to time spent” is a separate problem. Smith's rule, also called weighted shortest processing time, ranks work by value divided by handling time.

This axis answers what the user should act on first within a limited session. It contains no deadline. Furnas's model allocates screen space; value per handling time helps order action.

### Criticality

Criticality applies whenever an opportunity or delivery context has an identifiable closing window.

Effective importance is natural importance multiplied by the probability that the user will not remain in, or naturally return to, the relevant context before it closes. As the remaining window shrinks, the probability approaches one.

Criticality covers both:

- A real opportunity that disappears.
- The interface's chance to mention something before its context stops being useful.

Related prior art includes Horvitz, Jacobs, and Hovel's *Attention-Sensitive Alerting* (Microsoft Research, UAI 1999), which weighs the cost of interrupting now against the cost of deferring.

Known window types include:

- **Duration-bound:** a short fixed interval after a triggering event, such as correcting a typo.
- **Event-bound:** a window ending at a scheduled event.
- **Session-bound:** a window ending when the user leaves, estimated from expected session length rather than real-time behavioral inference.

Continuous standing state has no closing window. It remains governed by importance and task distance alone.

### Shared scales

Importance and criticality use bounded scales with a maximum of one.

A maximum prevents a newly introduced scoring formula from growing without limit and permanently dominating every established signal. Very low scores need no corresponding floor beyond zero; information may simply remain hidden.

Criticality is naturally a probability. Importance uses equivalent natural-language anchors:

- `1`: nothing is more important.
- `0`: the system could not care less.
- Intermediate values preserve meaningful ratios.

If several information items simultaneously reach maximum importance, they receive equal maximal treatment rather than being force-ranked by insignificant differences. This resembles high-stakes alerting systems that present several Warning-level events at the same tier.

## Spatial composition

USERCOOP uses a genuine three-dimensional layout while rendering most visible information through ordinary two-dimensional controls. The 3D world gives activities, information, and subjects stable spatial relationships. The 2D layer preserves precise typography and direct interface behavior.

Spatial position is semantic. It communicates progression, membership, provenance, current focus, and changes in activity context. USERCOOP therefore composes a spatial statement rather than arranging a collection of arbitrary panels.

### Rendering layers

The screen has three rendering layers, from front to back:

1. A transparent 2D control layer containing the visible representations of information items.
2. A 3D world containing layout anchors and, when appropriate, real visible 3D objects.
3. A visually empty sky rendered as a simple off-white or dark-grey field according to the current theme.

Most tools, descriptions, choices, states, and supporting details appear as 2D controls. Real 3D objects are reserved primarily for the final concepts being examined, manipulated, or analyzed: the things the activity is about rather than the tools used to work with them. This is why 2D information normally renders in front of the 3D world. Legible information supports the subject while the subject retains genuine spatial presence beneath it.

The 3D environment is conceptual rather than scenic. It does not require a room, floor, stars, grid, or decorative landscape. Its depth is made perceptible through composition, camera movement, scale, parallax, and the occasional presence of genuine 3D subjects.

### Projected information spaces

An information item remains distinct from both its 3D layout geometry and its visible 2D representation.

For each visible information space, USERCOOP maintains an invisible, camera-facing rectangle in the 3D layout. Its center and the midpoints of its four edges are projected through the camera into screen coordinates. Their projections determine the center, apparent width, and apparent height of the corresponding 2D control. Camera-space depth determines ordering among projected controls.

```text
information item
        ↓ represented in the spatial model by
invisible 3D rectangle
        ↓ projected through the camera into
screen position, apparent size, and depth order
        ↓ used to present
native 2D control
```

The visible control is therefore not a 3D billboard, texture, or subviewport. It remains native 2D interface content with clean typography. The invisible rectangle supplies only spatial placement and scale.

### The developing wall

The user's basic orientation is that of a person seated at a keyboard and facing an unbounded working wall. This wall is not a visible physical surface. It is the spatial development of the current activity stack as it exists now.

The wall may develop in different directions when the activity requires it, then retract when work completes. It does not need to preserve a permanent map of every previous activity. Later activity may develop a different structure from the same conceptual center.

The camera follows this development while generally preserving the stable experience of facing the working wall. Translation changes the user's point of view; rotation changes the direction of gaze from that point of view. Both are meaningful, but the design does not require continuous orbiting or disorienting changes of orientation.

### Directional grammar

The following directions describe the initial grammar for cultures that conventionally read and diagram progression from left to right. They are semantic defaults rather than claims of universality and may require adaptation for other cultural directions.

The initial position and the completed position of an activity are conceptual centers. A perdurant—an activity, process, or subject that develops through time—extends toward the right. If it contains several steps, each step appears to the right of the preceding step. The camera follows this development, and the latest operative step becomes the new conceptual center. Earlier steps remain toward the left as the path by which the current state was reached.

```text
initial step  →  next step  →  current or final step
                                      center
```

Around an individual step, the vertical axis expresses semantic provenance:

- Information about what comes from outside, what happened, what the state is, and what the system knows or reports develops above the step.
- Information about what is created here, what the user does, chooses, intends, or wants develops below the step.

Everything is ultimately rendered by USERCOOP. The distinction is therefore not who physically drew the text or control, but what the information is about: incoming condition and known state above; local intention and agency below.

```text
        incoming events and known state
                       ↑
                 current step
                       ↓
          user intention and local action
```

Several peer items belonging to the same enumeration are arranged vertically as a list. Their shared horizontal alignment—the fact that they occupy the same column or step of the line schema—carries the semantic of list membership. Vertical placement enumerates the members; it does not by itself define their relationship.

Each list member may develop independently toward the right:

```text
item A  →  development  →  development
item B  →  development
item C  →  development  →  development  →  development
```

Consequently, vertical enumeration does not conflict with the above-and-below provenance rule. List membership is established by common horizontal alignment and grouping, while provenance is established by attachment above or below a particular step or item.

### Overview and ongoing activities

Stepping back from the current composition produces an overview. The camera withdraws far enough to reveal more of the developed structure and the relationships among its parts. This is a change of granularity and framing, not necessarily a departure from the current activity. The activity may remain current while the user views it from farther away.

This gives overview a literal spatial meaning. Detail is approached; context is recovered by stepping back. USERCOOP need not replace the current information with an unrelated summary screen when the existing spatial development can itself be shown at a broader scale.

Withdrawing for overview must remain distinct from leaving an activity. An overview preserves the activity and its developed structure. Leaving completes, abandons, or returns from that activity and may cause its temporary structure to retract.

An activity that is paused so the user can engage in another activity also remains developed. The paused and current activities become peer members of an `ongoing stuff` list. Each member is a complete line schema with its own left-to-right development. The line schemas are placed one below another and aligned on their left starting points, so their shared horizontal origin identifies them as members of the same list.

```text
ongoing activity A:  start  →  step  →  paused current state
ongoing activity B:  start  →  step  →  active current state
```

Beginning or switching to the second activity does not erase or retract the first. Its developed line remains available as resumable context. Resuming it moves attention and the camera back to its existing current point rather than reconstructing it as a new activity.

The vertical ordering of ongoing activities does not imply that one follows another as a process. Their individual horizontal lines carry development through time; their common left alignment and vertical enumeration express that they are peers in the same set of ongoing work.

### Camera language

Camera movement is the primary intuitive channel through which USERCOOP communicates changes in activity context. Layout and camera are composed together: relevant information develops into an appropriate position, and the camera moves so that the current context is correctly presented in front of the user.

Provisional composition happens where the camera already is. While the user types an unfinished instruction, information may appear, recede, reorder, or receive emphasis around the current place. Local rotation, approach, withdrawal, or reframing may clarify the parser's developing understanding, but provisional interpretation does not pretend that the user has entered another activity location.

A committed activity transition is different: the camera literally travels to another place in the spatial composition. Entering a deeper activity develops a destination and moves the camera to it. Completing or leaving that activity retracts its temporary development while the camera returns toward the surviving parent context. Pausing an activity and switching to another moves the camera between their developed line schemas without retracting either one.

Translation and rotation need not wait for one another. Information may appear or disappear faster than the camera can travel to the newly appropriate point of view. In that case the camera first turns its gaze toward the new point of interest while translation is still underway. This is analogous to a person turning their head toward something before or while walking into a better position from which to inspect it. The user can therefore see the relevant subject immediately while the slower movement of viewpoint preserves spatial continuity.

Rotation also permits a contextual glance without leaving the current place. The camera may turn toward a distant but related part of the developed wall—for example, a previous step of the same activity or the parent activity within which the current sub-activity exists. This changes what the user is looking at without changing which activity is current, retracting anything, or committing a transition. When the glance ends, the camera may return its gaze to the current point of work.

These roles make rotation an expression of attention rather than travel:

- **Anticipatory gaze:** turn toward a new point of interest before or during translation to its new point of view.
- **Contextual glance:** look toward related context from the current position without leaving or changing the current activity.
- **Settled orientation:** align the final gaze with the composition once translation and reorganization have settled.

Rotation and translation begin together. Both use eased acceleration and deceleration, or an equivalent interpolation, so that neither snaps into motion. They differ primarily in how quickly they settle.

As an initial motion envelope, the camera may align with and lock its gaze on the target approximately `0.25` to `0.5` seconds after movement begins, while translation reaches the new position approximately `1` to `2` seconds after the same start. Rotation therefore feels like turning the head while translation feels like walking. Once gaze lock is reached, the camera continues looking at the target while its position completes the journey. The gaze leads; the viewpoint follows.

These timings are rough perceptual targets rather than fixed constants or a demand for literal physical simulation. Exact speed, acceleration, and duration remain subject to distance, urgency, readability, the sport-to-zen pace, and reduced-motion accessibility settings. The recognizable relationship is more important than the numbers: turning and walking begin together, gaze settles first, and position follows.

The difference should be only as visible as necessary to make the motion feel coherent. Someone who knows to observe the head-turn and walk relationship should be able to see it; someone who does not should simply experience one calm, natural camera movement. This is a direct application of the broader principle that a refinement may reward attention without demanding it.

Camera motions therefore form a restrained vocabulary:

- Local adjustment expresses changing attention within the present activity.
- Rotation expresses direction of gaze and can redirect attention without changing viewpoint or activity.
- Sustained spatial travel expresses entry into another activity context.
- Withdrawal without retraction expresses overview.
- Withdrawal accompanied by retraction expresses completion, exit, or return to a parent context.
- Travel between preserved line schemas expresses switching among ongoing activities.
- Reframing expresses reorganization of the current context.
- Combined rotation and translation let attention arrive before the camera reaches its final point of view.

Movement is not decorative animation added after layout. It preserves continuity and lets the user perceive how the current context grew from the previous one, where attention has moved, and when a temporary branch has ceased to exist.

## Motion, reactivity, and stability

The interface operates at two temporal regimes.

### Foreground reactivity

The active composition context responds immediately to meaningful parser changes. Valid continuations, resolved referents, information spaces, highlights, and spatial focus may all change during typing. These provisional changes occur locally within the current activity place.

This rapid movement is feedback, not instability. It externalizes the parser's developing understanding and produces the intended sense of a screen living alongside the user.

### Background hysteresis

Information unrelated to the active composition changes conservatively.

- Small score differences do not reorder information spaces.
- Ambient information does not repeatedly gain and lose space near a threshold.
- A current arrangement persists until a competitor wins decisively.
- Minimum display lifetimes prevent unreadable flashes.
- Recently displaced information may retain a short return advantage.

Hysteresis stabilizes the background without slowing the foreground.

### Returning to equilibrium

Explicit requests and urgent contexts may temporarily force greater detail or occupancy than the user normally prefers. When the activity completes or the pressure ends, the display settles toward the standing preference rather than snapping through every intermediate arrangement.

## Interaction and accessibility

Keyboard interaction is the intended primary mode where a keyboard is present. Full mouse-only and touch-only operation remain standing requirements.

Every semantic action available through the command language must have an accessible direct-manipulation path. Spatial views support ordinary pointing, dragging, panning, and zooming where appropriate. Keyboard focus is always visible when keyboard navigation is active.

Accessibility preferences may constrain motion, typography, contrast, timing, and information capacity. These constraints outrank aesthetic choices.

## Visual direction

The interface is quiet, calm, and restrained at rest. It should feel like a clear space for thought rather than a spectacle competing for attention.

- Simple forms, generous spacing, and highly legible typography.
- Soft, neutral colors with limited contrast reserved for meaningful state changes.
- Gentle motion when preserving continuity, directing attention, or confirming action.
- Rapid motion is permitted when directly caused by active command composition.
- Visual hierarchy comes from the interaction model itself.
- No decorative element without a functional purpose.

Calmness is an equilibrium, not immobility. A normally sparse interface may become temporarily dense and animated when the user's activity genuinely demands it.

## System boundary

USERCOOP is one coherent Godot application with internal boundaries between meaning, time, device authority, and presentation.

### Semantic kernel

The semantic kernel owns identities, values, relationships, facts, rules, procedures, queries, provenance, derivations, contradiction, and history. It also owns deterministic parsing and contextual vocabulary.

The kernel produces semantic state and ordered events. It does not decide coordinates, font sizes, camera paths, or animation.

### Session and inference runtime

The runtime owns the current session, activity stack, ongoing work, command history, temporal events, and inference processes. It advances these perdurants without blocking the application.

This is where knowledge meets lived time: what is active, paused, completed, interrupted, or becoming relevant now.

### Device observation and action

Device adapters give USERCOOP bounded access to the device it inhabits. They may observe files, processes, settings, notifications, hardware state, and operating-system events. They translate those observations into knowledge and expose authorized local actions.

Adapters provide facts and actions, not alternative interfaces. They do not control USERCOOP's vocabulary, activities, typography, spaces, or camera.

### Applications and command execution

USERCOOP can know about and operate applications as objects on the device. It may launch, focus, or stop an application and, where the operating system permits it, invoke one with explicit arguments or a local platform hook.

An advanced procedure may eventually invoke a complete Bash or PowerShell command line. On Android, it may use an available intent or another local operating-system facility. These are powerful device actions, not the organizing purpose of USERCOOP.

Execution remains explicit, inspectable, and authorized. Processes, output, failures, and device changes return as knowledge and events. External applications do not become the source of USERCOOP's semantic model.

### Operating-system authority

The operating system remains authoritative over files, processes, hardware, permissions, application sandboxing, and protected actions. USERCOOP does not bypass that authority.

Knowing that an action is appropriate is distinct from having permission to perform it. A derived action still requires an authorized device capability and, when appropriate, explicit confirmation.

### Godot application boundary

Godot is the chosen application environment, not a temporary renderer for a generic host. Its update loop, input system, 2D controls, 3D world, camera, animation, and temporal behavior are part of USERCOOP.

The semantic kernel remains separate from Godot presentation objects for clarity and testing. That separation is not a promise to reproduce USERCOOP in unrelated rendering technologies.

## Personal-device targets

Computers, smartphones, and tablets are natural targets for USERCOOP. The knowledge model and session concept remain coherent across them; device capabilities and input methods differ.

Smartphones and tablets deserve particular emphasis:

- They are personal devices carried through daily life, making the session a natural point of contact with lived time.
- Their conventional systems already expose activities, notifications, intents, permissions, sensors, and local hooks.
- Limited screen area increases the value of automatic composition, short lines, semantic reduction, and overview through camera distance.
- Application sandboxes make capability boundaries explicit.

USERCOOP remains offline on every target. A cellular or Wi-Fi connection does not grant it external network access. Platform integration remains local to the same physical device.

Keyboard interaction remains central when a physical keyboard is present. Touch and the on-screen keyboard are complete interaction paths, not reduced substitutes. Large monospaced input is especially valuable for users who simply want to type letters and see that the device is listening.

## Implementation

The first implementation is a Godot 4.7 .NET application. It should grow through working software rather than speculative framework building.

### Initial application structure

The root scene uses a plain `Node` because USERCOOP is neither fundamentally 2D nor 3D:

```text
Usercoop                         Node
├── Knowledge                    Node
├── Session                      Node
├── Inference                    Node
├── SpatialWorld                 Node3D
│   ├── CameraRig                Node3D
│   │   └── Camera               Camera3D
│   └── Environment              WorldEnvironment
└── Interface                    CanvasLayer
    └── Spaces                   Control
```

The root coordinates lifecycle. Knowledge, session, and inference are sibling runtime services. SpatialWorld and Interface are sibling presentations of their state.

### Semantic data is not the scene tree

The scene tree represents the running application, not every fact in the knowledge base. Facts, entities, relationships, rules, and derivations are ordinary semantic data rather than one Godot node per item.

The semantic kernel should begin with plain C# types carrying stable identities and explicit value semantics. Likely primitives include:

```text
EntityId
KnowledgeValue
Fact
Relation
Rule
Query
Derivation
Provenance
KnowledgeEvent
```

Godot nodes own services and connect them to the engine. Godot resources may hold authored vocabulary, schemas, themes, and test data, but they do not define the runtime knowledge model.

### Knowledge language

Facts and rules use short natural-language patterns with deterministic matching and rewriting. The approach is informed by string-rewriting systems and rule languages such as AIML, RiveScript, and ChatScript, while supporting both forward and backward chaining.

Datalog is the closest formal model. The surface language remains terse, sequential, and easy to teach. Its syntax is deliberately limited; its inference capabilities need not be shallow.

[LPS (Logic-based Production System)](https://www.doc.ic.ac.uk/~rak/papers/RuleML.pdf), developed by Robert Kowalski and Fariba Sadri, is another relevant reference. Its combination of logic programs, reactive rules, events, actions, changing state, and intentional behavior is especially pertinent to USERCOOP's temporal inference and bounded initiative.

Complex knowledge is built from many clear steps rather than hidden inside elaborate expressions. The same language is used to operate the system, teach it, inspect it, and revise its artifacts.

### Reasoning capabilities

The expert-system core should grow to support:

- Forward and backward chaining.
- Truth maintenance and dependency tracking.
- Hypothetical reasoning without committing hypotheses as facts.
- Explicit management of uncertainty.
- Causal models informed by Pearl's work on intervention and causation.
- Ontologies rooted in USERCOOP's subjective upper ontology.
- Explanations grounded in stored derivations, intentions, permissions, and outcomes.

Explainability serves both the user and USERCOOP itself. Derivation and action histories allow the system to audit its behavior, identify weak knowledge, and improve where it has authority to modify its own knowledge.

Retention policy is also knowledge. USERCOOP ships with rules for preserving explanations and traces. The owner may revise any of those rules; USERCOOP may revise them autonomously only within its granted write scope.

### Incremental inference

Inference develops over time. It must not freeze Godot while privately calculating a finished answer.

The inference scheduler advances a bounded number of deterministic logical operations, emits ordered events, and yields. Godot continues to render, accept input, reveal text, move the camera, and present partial results.

```text
question or event
    → match facts
    → activate rules
    → open and reject branches
    → derive knowledge
    → stabilize results
```

The complete inference trace is semantic data. Presentation may show a rapid selection of genuine steps in very small monospaced text. This visible machinery is never fabricated activity. When brought into focus, the trace can receive an ordinary readable representation.

Logical progress and visual cadence remain separate. The initial work budget should be measured in logical operations rather than frame duration so frame rate cannot change semantic results. Worker threads may come later if measurements justify them; cooperative scheduling is the simpler starting point.

Provisional results remain distinct from settled knowledge. Cancellation, inspection, and continued interaction are normal parts of an inference process.

### Persistence

Knowledge, rules, provenance, sessions, and histories persist locally. Storage must be versioned, recoverable, and able to represent changes without discarding their origin.

SQLite is the expected durable store. It provides local transactions, indexes, scale, and inspection without introducing a server or network dependency. Persistence remains behind a small interface so the semantic model does not become a database schema by accident.

Some knowledge artifacts should also be browsable from an IDE. Rules, definitions, and interaction-created material may have readable source representations beside the database. The user normally changes them through USERCOOP's own language in an interaction closer to an `ed` session than to hand-editing source files.

The database and readable artifacts serve different purposes: reliable indexed state on one side, inspectable and versionable expressions of knowledge on the other. USERCOOP remains the authority that keeps them coherent.

### Initial implementation direction

The first working path is deliberately narrow:

1. Establish the root services and 2D/3D rendering layers.
2. Render the current typed-line information item with the intended typography.
3. Add deterministic token recognition and uppercase/lowercase feedback.
4. Introduce minimal knowledge identities, facts, and events.
5. Represent the current session and one developing activity.
6. Advance a small inference process incrementally and show its genuine trace.
7. Project an invisible 3D information rectangle into a native 2D control.
8. Add one bounded local device domain, such as files, after the semantic path works end to end.

The aim is not to imitate a desktop or complete an expert-system framework before anything is visible. It is to establish one honest path from user letters, through semantic recognition and inference, into knowledge, space, motion, and persistent session history.
