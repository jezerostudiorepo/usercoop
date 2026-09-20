# USERCOOP Interaction System

## Contents

- [Purpose](#purpose)
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
  - [Content belongs to the provider](#content-belongs-to-the-provider)
  - [Presentation belongs to the host](#presentation-belongs-to-the-host)
  - [Multiple representations](#multiple-representations)
- [Presentation preferences](#presentation-preferences)
  - [Granularity](#granularity)
  - [Occupancy](#occupancy)
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
  - [Provider responsibilities](#provider-responsibilities)
  - [Host responsibilities](#host-responsibilities)
  - [Device capabilities and adapters](#device-capabilities-and-adapters)
  - [Rendering hosts](#rendering-hosts)
- [Beyond applications and windows](#beyond-applications-and-windows)
- [The Power as the first adapter](#the-power-as-the-first-adapter)
- [Research questions](#research-questions)

## Purpose

This document specifies an interaction system, command model and display model, independent of any one application.

The intended end product is a Godot application that provides a calm, quiet, and restrained alternative to both text-mode terminals and conventional windowing systems. It offers a different way to operate a computer, smartphone, individual application, or set of applications.

USERCOOP acts as a global interaction identity for the device. Here, identity refers to the coherent way the device presents itself and responds to its user, not to the identity of the user. By running USERCOOP, the device acquires a consistent activity model, command language, presentation logic, and interaction character across the capabilities it makes available.

The project is primarily about managing and operating the device. Access to services may be useful where it supports that purpose, but user accounts, personal identity, and service aggregation are not its organizing concern.

## Core proposition

The interface is not a collection of windows that the user must arrange and monitor manually. It continuously materializes the user's evolving semantic context.

USERCOOP is a semantic interaction layer through which the user pilots the device. Rather than requiring the user to navigate the separate interfaces of files, applications, notifications, and system facilities, it coordinates those existing capabilities around the user's current intention.

The command stream serves two purposes at once:

1. It tells applications what the user wants to do.
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
8. **Keep content semantic.** Applications describe meaning and available action. The host owns presentation.
9. **Retain full mouse operation.** Keyboard interaction is primary, not exclusive.
10. **Remain offline by construction.** USERCOOP must be programmatically unable to reach external networks. Its operation must never depend on Internet access or a remote service, and this boundary has no protocol-specific exception.

## Offline by construction

Offline operation is a foundational property of USERCOOP, not merely a mode, preference, or promise about ordinary behavior. The application should be architected so that its normal runtime cannot initiate or receive communication across an external network.

This boundary keeps operation of the device local, makes the system useful without connectivity, and prevents the interaction layer from becoming an implicit conduit through which device activity or command history can leave the device. No provider may silently weaken this property.

Features that conventionally depend on online services are not performed by USERCOOP over the network. Where appropriate, USERCOOP may invoke a capability belonging to another installed application or to the operating system. That external application remains visibly and technically responsible for its own networking, permissions, and results.

### Local communication

Communication confined to the device is permitted when it is needed to connect USERCOOP to local adapters, applications, or system bridges. Possible transports include:

- Loopback TCP connections.
- Local WebSocket connections bound only to a loopback interface.
- Operating-system facilities such as local sockets, named pipes, or equivalent inter-process communication.

Such transports are implementation details of an in-device system. They must not listen on externally reachable interfaces, accept remote peers, or provide a route from a local provider to an external network through USERCOOP.

"Local" means strictly within the same physical device that is running USERCOOP. Other computers, phones, appliances, or services on a trusted local-area network are external for the purpose of this principle and are not reachable by USERCOOP.

### External network boundary

The external-network restriction should be enforced programmatically and by architecture rather than relying only on convention. The Godot host and generic runtime should not expose general-purpose Internet clients to providers. Adapters should receive the minimum local capabilities required for their work, and the deployed application should be testable for the absence of externally reachable network paths.

The intended implementation is one Godot executable capable of performing the work required by USERCOOP. A separate privileged companion service or general-purpose network broker is not part of the default architecture. Where operating-system integration requires local IPC, USERCOOP may communicate with facilities already belonging to the same device, but the USERCOOP executable remains the coherent application and interaction host.

This principle concerns USERCOOP itself. Launching a mail composer, browser, or other network-capable application through an operating-system action does not make USERCOOP the network client. The handoff must remain explicit, and USERCOOP must not silently collect, proxy, or transmit the resulting network traffic.

## Activities and contextual vocabulary

USERCOOP shows the user the vocabulary, information, and actions relevant to the current activity. The user does not interact with a separate client, and an application does not present a parallel interface inside USERCOOP. USERCOOP remains the interaction host throughout.

[Symbolfront](https://github.com/symbolworks/symbolfront) is relevant prior art for one narrower idea: command vocabulary can be supplied by the current context instead of being permanently hard-coded as one global command set. USERCOOP adopts that principle within its own activity model; it does not adopt Symbolfront's client architecture or make Symbolfront part of the runtime.

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
Applications
└── Tasks
    └── New task
        └── Choose date and time
```

The activity stack is cognitive as well as navigational. Each level changes the relevant objects, available language, appropriate information, and likely next actions.

### Contextual language sources

USERCOOP determines the language currently shown to the user from the active activity and the capabilities available on the device. For built-in device functions, USERCOOP may define that language directly. For an integrated application, a local adapter may describe:

- Commands valid in the current activity.
- Syntax patterns for those commands.
- Semantic types accepted by each slot.
- Candidate objects that may fill those slots.
- Actions that enter, complete, reject, or leave activities.
- Information items relevant to the activity.

These descriptions supply meaning and capability, not presentation. USERCOOP performs parsing and discovery, shows valid continuations, manages history and attention, gives information space on the screen, and provides the keyboard, mouse, or touch interaction. The application or adapter cannot replace that interaction model with its own interface inside USERCOOP.

### Entering and leaving activities

The user enters an activity, performs the work appropriate to it, and leaves when finished. The display adapts for the duration of that activity and releases its temporary information when the activity closes.

This is not equivalent to opening and closing an application window. The activity may use information from several providers while remaining one coherent cognitive context.

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

As each letter is typed, a word that may still complete into a keyword is displayed in uppercase; otherwise it is lowercase.

The display updates retroactively. If later characters prove that an uppercase prefix can no longer form a keyword, the earlier letters fall back to lowercase immediately. The space showing the line being typed therefore reflects whether the parser still recognizes a possible instruction.

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

Past history is itself retrieved through a command such as `SHOW LINE 47`. Mouse scrolling remains available as an accessibility alternative. The requested line is given its own space, accompanied by a small reminder of the command that produced it.

## Information and spaces

An information item describes something USERCOOP may need to manage: its meaning, identity, content, relevance, and available actions. A space is the presence USERCOOP gives that item on the screen. The information item is semantic; the space is compositional.

Neither is a window or a card. An information item does not prescribe a rectangle, coordinates, or visual hierarchy, and a space is not an application-owned container. One item may move between spaces or representations as attention changes, and several related items may share a space when USERCOOP judges that they belong together.

The model resembles the semantic boundary used by [Microsoft Adaptive Cards](https://learn.microsoft.com/en-us/adaptive-cards/): an author owns the content while the host owns the look and feel. This system extends that boundary by adapting presentation not only to the host, but also to the user's inferred cognitive context.

### Content belongs to the provider

A provider defines an information item through:

- Semantic type.
- Subject and stable identity.
- Content fields.
- Available actions.
- Intrinsic importance.
- Estimated handling time, when meaningful.
- Closing window or criticality inputs, when meaningful.
- Supported semantic representations.
- Minimum representation required by the current situation.

### Presentation belongs to the host

The host decides:

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

### Preferences are equilibria

Preferences describe where the display rests when no stronger requirement exists. They are not hard limits.

Precedence is:

1. **Explicit request.** If the user asks for detail, show detail.
2. **Semantic requirement.** If information cannot be understood safely in a compact form, use the required representation.
3. **Simultaneous importance and criticality.** If several matters genuinely require attention, temporarily increase occupancy.
4. **Standing preference.** When the system has a choice, return toward the user's preferred granularity and occupancy.

A sparse preference means “when possible, show less,” not “conceal simultaneous important information.” An overview preference means “begin with summaries,” not “withhold detail that was requested.”

## Automatic composition and attention

The user is not expected to move, resize, close, or scroll through arbitrary windows. The system decides what is shown, how, and where within the host's presentation grammar.

Automatic composition is primarily editorial judgment rather than geometric novelty. The essential problem is selecting and presenting the right information, not discovering clever coordinates for rectangles.

### Attention from command traffic

The command stream is the primary attention signal. Something the user repeatedly references, selects, compares, or acts upon remains visible and prominent. Once attention moves elsewhere, it recedes and may eventually be displaced.

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

The camera follows this development while generally preserving the stable experience of looking forward. It may translate, approach, withdraw, pan, and reframe. Rotation remains restrained and meaningful; the design does not require the camera to orbit continuously or turn the user around without semantic cause.

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

Provisional composition happens where the camera already is. While the user types an unfinished instruction, information may appear, recede, reorder, or receive emphasis around the current place. Local pan, approach, withdrawal, or reframing may clarify the parser's developing understanding, but provisional interpretation does not pretend that the user has entered another activity location.

A committed activity transition is different: the camera literally travels to another place in the spatial composition. Entering a deeper activity develops a destination and moves the camera to it. Completing or leaving that activity retracts its temporary development while the camera returns toward the surviving parent context. Pausing an activity and switching to another moves the camera between their developed line schemas without retracting either one.

Camera motions therefore form a restrained vocabulary:

- Local adjustment expresses changing attention within the present activity.
- Sustained spatial travel expresses entry into another activity context.
- Withdrawal without retraction expresses overview.
- Withdrawal accompanied by retraction expresses completion, exit, or return to a parent context.
- Travel between preserved line schemas expresses switching among ongoing activities.
- Reframing expresses reorganization of the current context.
- Rotation is reserved for development whose changed direction genuinely carries meaning.

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

Keyboard interaction is the intended primary mode. Full mouse-only operation remains a standing requirement.

Every semantic action available through the command language must have an accessible graphical path. Spatial views support ordinary pointing, dragging, panning, and zooming where appropriate. Keyboard focus is always visible.

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

The interaction system should remain independent of both application domains and rendering technology.

### Provider responsibilities

An application provider supplies:

- Activities and their parent relationships.
- Contextual commands and syntax patterns.
- Semantic object types and stable identities.
- Candidate referents.
- Information items and supported representations.
- Available actions and completion behavior.
- Importance, handling-time, and criticality inputs when known.
- Authorization over domain mutations.

### Host responsibilities

The host supplies:

- Incremental deterministic parsing.
- Command discovery and valid continuations.
- Activity-stack management.
- Local history and citation.
- Attention inference from command traffic.
- Granularity and occupancy preferences.
- Automatic composition.
- Motion and hysteresis policy.
- Accessibility mechanisms.
- Rendering and input devices.

Providers do not control arbitrary pixels or inject executable interface code. The host does not invent domain mutations or bypass provider authorization.

### Device capabilities and adapters

USERCOOP does not need to absorb or reimplement every application and service on a device. It discovers or is connected to capabilities already exposed by the operating system and installed applications, then makes those capabilities available through its common activity and interaction model.

For example:

- If the device has a notification system, USERCOOP may receive or publish notifications through it and present them according to its attention and composition rules.
- If the device provides a way to compose mail, USERCOOP may launch that composition capability with relevant fields or context already supplied.
- If the operating system can browse or open files, launch applications, search, share content, or expose settings, adapters may represent those operations as semantic activities and actions.
- When an operation is better or more safely completed by a native application, USERCOOP may initiate it and hand control to that application rather than reproducing its complete interface.

The responsibility boundary is:

- USERCOOP owns the interaction model: activities, contextual language, intention, attention, semantic presentation, and transitions.
- The device and its applications own the underlying capabilities and domain behavior.
- Adapters translate between the two.
- Operating-system and application permissions remain authoritative.

This allows USERCOOP to change how a device is used without requiring it to replace the device's operating system, notification infrastructure, applications, or services.

### Rendering hosts

The semantic runtime and provider protocol must not depend on one renderer.

Possible hosts include:

- Godot, especially for spatial applications and The Power.
- A browser, especially for document-rich applications and broad portability.
- A native desktop host.
- A future shell or compositor.

Godot may be the first implementation without becoming part of the protocol.

## Beyond applications and windows

The system may ultimately serve as an activity-oriented shell or semantic environment.

Traditional graphical systems assign applications rectangles and ask the user to preserve context by arranging them. Traditional terminals combine commands and results into one stream. This system asks providers for semantic activities, then composes the computer around the user's current intention.

For example:

```text
Email
└── Search
    └── Conversation with Alice
        └── Compose reply
```

or:

```text
Project
└── Diagnose failing test
    ├── relevant source
    ├── failure event
    ├── recent changes
    └── corrective actions
```

These activities may cross conventional application boundaries. Their unity comes from the user's purpose, not from process ownership or a window frame.

Replacing a mature desktop environment is not an initial implementation requirement. The immediate goal is to prove that activity, contextual language, and automatic semantic composition form a useful third model of interaction.

## The Power as the first adapter

The Power is an unusually strong first application because it contains:

- A closed but rich object world.
- Spatial focus and camera movement.
- Long-lived and transient information.
- Delayed consequences.
- Simultaneous important events.
- Deep compositional commands.
- Real conflicts between overview and detail.
- Real conflicts between calm presentation and temporary occupancy.

The adapter provides stones, clans, cells, pledge trees, game actions, sensing, and authorization. The generic runtime provides activities, parsing, attention, composition, history, presentation preferences, and rendering policy.

Examples specific to The Power include:

- Selecting, viewing, and highlighting any legitimately perceived stone.
- Permitting mutations only for stones the player controls.
- Panning and zooming toward a stone resolved inside an unfinished command.
- Previewing a queued move during composition while leaving the board unchanged until the tick.
- Raising criticality as an event-bound opportunity approaches tick resolution.
- Publishing an aggregate session-duration baseline for session-bound estimates while keeping layout decisions within USERCOOP.

At least one small non-game provider, such as notes or tasks, should also be built early. This tests whether the runtime is genuinely general rather than merely game code with abstract names.

## Research questions

1. Can users learn a large system through contextual vocabulary without memorizing a global command language?
2. How much provisional screen movement helps comprehension before it becomes distracting?
3. Which parser states justify moving spatial focus, and which should only reveal possibilities?
4. How should a provisional context unwind when the user backspaces into ambiguity?
5. How strong must hysteresis be to stabilize ambient information without making the interface feel unresponsive?
6. Can granularity and occupancy be expressed as understandable preferences without exposing implementation complexity?
7. How should explicit requests, semantic minimums, criticality, and preferences be combined predictably?
8. What is the smallest information-item schema that remains expressive across unrelated providers?
9. Can application providers supply vocabulary and information safely without gaining control of USERCOOP's presentation?
10. Does the model remain usable without a spatial view, as in notes, tasks, mail, or programming?
11. Can the same semantic runtime support Godot, browser, and native hosts without collapsing to their lowest common denominator?
12. At what point does an activity-oriented environment become capable enough to replace part of a conventional desktop shell?
13. What technical boundary can make external network access impossible while preserving safe same-device communication with local applications and operating-system facilities?
