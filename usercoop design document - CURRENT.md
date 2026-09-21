# USERCOOP Design Document

**Status:** design specification, revision 3.
**Scope:** an interaction system, a command model, and a display model, specified independently of any one application.
**Target:** one Godot 4.7 .NET application for personal computers, smartphones, and tablets.

## How to read this document

The document is organized as six parts, from intent to implementation and reference material. Each part can be read on its own, but the earlier parts constrain the later ones: intent decides boundaries, boundaries decide language, language decides presentation, and presentation decides implementation.

The document states design commitments directly. Platform-dependent commitments are accompanied by build or test requirements rather than left as editorial questions.

Example commands are written in the style USERCOOP will use, but they indicate functional categories rather than fixing the final syntax.

## Contents

**[Part I. Intent](#part-i-intent)**

- [1. Purpose](#1-purpose)
- [2. A personal programmable expert system](#2-a-personal-programmable-expert-system)
- [3. The session and lived time](#3-the-session-and-lived-time)
- [4. Core proposition](#4-core-proposition)
- [5. Design principles](#5-design-principles)

**[Part II. Boundaries](#part-ii-boundaries)**

- [6. Offline by construction](#6-offline-by-construction)
- [7. Capabilities and authority](#7-capabilities-and-authority)

**[Part III. Language](#part-iii-language)**

- [8. Activities and contextual vocabulary](#8-activities-and-contextual-vocabulary)
- [9. Command language](#9-command-language)
- [10. Live composition](#10-live-composition)

**[Part IV. Information and presentation](#part-iv-information-and-presentation)**

- [11. Information items and spaces](#11-information-items-and-spaces)
- [12. Authorship, typed entries, and history](#12-authorship-typed-entries-and-history)
- [13. Typography](#13-typography)
- [14. Presentation preferences](#14-presentation-preferences)
- [15. Attention and automatic composition](#15-attention-and-automatic-composition)
- [16. Spatial composition](#16-spatial-composition)
- [17. Motion, reactivity, and stability](#17-motion-reactivity-and-stability)
- [18. Accessibility](#18-accessibility)
- [19. Visual direction](#19-visual-direction)

**[Part V. Implementation](#part-v-implementation)**

- [20. System boundary](#20-system-boundary)
- [21. Personal-device targets](#21-personal-device-targets)
- [22. Building it](#22-building-it)

**[Part VI. Glossary and references](#part-vi-glossary-and-references)**

- [23. Glossary](#23-glossary)
- [24. References and prior art](#24-references-and-prior-art)

---

# Part I. Intent

## 1. Purpose

The intended end product is a Godot application that provides a calm, quiet, and restrained alternative to both text-mode terminals and conventional windowing systems. It offers a different way to operate a computer, smartphone, or tablet.

USERCOOP acts as a global interaction identity for the device. Here, identity refers to the coherent way the device presents itself and responds to its user, not to the identity of the user. By running USERCOOP, the device acquires a consistent activity model, command language, presentation logic, and interaction character across the capabilities it makes available.

The project is primarily about maintaining and applying personal knowledge through lived sessions, including knowledge of and action upon the device itself. User accounts, online identity, and service aggregation are not its organizing concern.

Smartphones and tablets are first-class targets, not ports. Their personal, continuous, touch-oriented use makes them especially appropriate devices for USERCOOP, and the constraints they impose are treated as design inputs rather than late compromises.

## 2. A personal programmable expert system

USERCOOP is an offline, personal, programmable expert system. It lets the user build, examine, extend, and apply knowledge about a locally defined world, and it can operate the device as part of that world.

It is not primarily an application launcher, conversational assistant, or integration layer. It may operate applications as objects on the device, but it is itself the persistent knowledge and action system whose role is to cooperate with the user.

"Personal" means that its concepts, vocabulary, classifications, rules, procedures, and stored knowledge belong to the user and remain on the device. It does not refer to an online identity, behavioral profile, or service account.

### 2.1 Knowledge and programming

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

An immediate instruction, a reusable definition, a query, and a rule for future action all operate on the same semantic world. They need not compress their whole interaction into one line. Context can be established first and then receive the kind of expression it expects:

```
usr:    NEW ENTRY
        CATEGORY PEOPLE
        FACTS
        ALICE WORKS ON orion
        PAUL TOO

sys:    2 FACTS SAVED
        WHAT IS ORION

usr:    ORION IS
        CATEGORY PROJECTS
        NEW PROJECT

sys:    PROJECT ORION SAVED

usr:    TODO THIS WEEK
        DEFINE ORION
        IMPORTANCE HIGH

sys:    1 TASK SAVED
```

Then later:

```
usr:    REQUEST
        WHO WORKS ON ORION

sys:    CATEGORY PROJECTS
        ALICE
        PAUL
        TOTAL 2 PEOPLE WORK ON ORION
```

Defining a deduction:

```
usr:    NEW ENTRY
        CONCEPT PROJECT
        DEDUCTIONS
        PROJECT p IS ACTIVE PROJECT
        IF NOT p HAS COMPLETION DATE

sys:    1 DEDUCTION SAVED
```

Creating a behavior:

```
usr:    NEW ENTRY
        PRODUCTIONS
        WHEN PROJECT p IS COMPLETE
        THEN ARCHIVE WORKING FILES OF p

sys:    1 PRODUCTION SAVED
```

These examples are scenes showing what it's like to work with USERCOOP. The language grammar and vocabulary are fully customizable, like everything else in the system.

USERCOOP distinguishes knowledge explicitly stated by the user, observed from the device, derived through rules, and produced by actions. A derivation follows inspectable deterministic rules. Ambiguity, contradiction, and failure become information items rather than occasions for the system to guess. When more than one valid reading remains, USERCOOP exposes the alternatives and asks the user to resolve them.

Something may remain known without currently being shown. The relationship is:

```text
knowledge item
    | represented for the current context as
information item
    | presented through
space
```

### 2.2 Teaching and use

Teaching USERCOOP and using USERCOOP are the same ongoing activity. The user does not first prepare an expert system and later consult it. Facts, vocabulary, rules, procedures, corrections, and questions accumulate while the system is already being used.

A new installation begins as an expert system primarily about itself: what it is, what it intends, what it can do, how it reasons, and which parts of its knowledge it is permitted to modify on its own. It becomes personal through continued interaction.

The system must support sophisticated knowledge when the user supplies it. A personal scope does not imply simple subject matter or shallow inference.

### 2.3 Subjective upper ontology

USERCOOP's upper ontology begins with the system doing the inference. It understands itself as a program situated on a device, acting through explicit capabilities, during a session shared with its user.

This is subjective in the sense of viewpoint, not emotion. Identity, intention, observation, action, permission, time, and explanation are organized around what USERCOOP is and how it participates in the world it knows.

"Because the user told me to" is not a complete explanation. A fuller chain includes the system's own standing intent to follow that instruction, the rule that connected it to an action, the capability that authorized the action, and the result.

Built-in policies use the same kind of knowledge as user-created policies. Retention, explanation, initiative, and self-audit begin with defaults. The owner may inspect and change any of them. USERCOOP may change them on its own only where the owner has explicitly granted that authority.

### 2.4 Initiative and bounded autonomy

USERCOOP may act on its own initiative. It can advance inference, bring information forward, pilot the screen, begin an authorized procedure, or ask the user for knowledge it needs.

Initiative is bounded programmatically and modularly. The user determines:

- Which folder or other local scope is visible.
- Which device capabilities are authorized.
- Which parts of the knowledge base USERCOOP may modify on its own initiative.
- Which rules may initiate actions and which require confirmation.

A rule cannot escape the capability boundary merely because its conclusion recommends an action. Capability classes, authorization, and the safety bounds on acting rules are specified in [section 7](#7-capabilities-and-authority).

### 2.5 The device as a known world

The device is where USERCOOP runs, one of the worlds it knows about, and an environment in which it can act. Files, folders, applications, processes, settings, notifications, hardware state, typed entries, and operation results can all become objects, facts, events, or actions within the knowledge base.

Device management is therefore an expert domain of USERCOOP rather than a collection of unrelated utilities. Device facts participate in requests, deductions, and productions just like user-defined knowledge. Using the same illustrative grammar as section 2.1, an exchange might look like this:

```
usr:    NEW ENTRY
        PRODUCTIONS
        WHEN BACKUP IS CONNECTED
        THEN SHOW PROJECTS WITH UNARCHIVED FILES

sys:    1 PRODUCTION SAVED
```

Later, USERCOOP senses the device event and applies the production without requiring the user to report the device state:

```
sys:    BACKUP CONNECTED
        PROJECTS WITH UNARCHIVED FILES
        ORION
        TOTAL 1
```

Applications may be found, launched, focused, or stopped as objects and capabilities of the device. They are not the semantic foundation of USERCOOP and do not replace its knowledge model with their own interaction systems.

## 3. The session and lived time

### 3.1 The session as point of contact

The current session is itself a perdurant: something that extends and develops through time rather than existing whole at each instant. It exists both as an object known to USERCOOP and as a real interval in the user's life. It is the point of contact between the system's semantic world and the temporality the user is actually living and working through.

A session is not merely the duration for which an executable remains open, a connection, or a container for transient interface state. It has a beginning, an evolving present, accumulated events and activities, interruptions, resumptions, and an eventual ending. It may be part of a longer undertaking while also containing shorter activities of its own.

Within the system, the session can be known through its current activities, ongoing work, completed steps, elapsed time, relevant objects, commitments, events, and changes of direction. Within the user's life, it is the actual period in which attention, effort, choice, and progress occur. USERCOOP's cooperation happens where those two descriptions meet.

The session is therefore the current focal perdurant around which the activity stack, the `ongoing stuff` list, attention, and temporal rules are composed. Activities do not float in an abstract interface; they occur during this lived session and contribute to its development.

Time is part of the ontology, not merely a timestamp attached to facts. USERCOOP represents events, states, intervals, and their relations. Allen's interval algebra is the initial foundation for relations such as before, during, overlapping, meeting, and finishing.

### 3.2 Cooperation in lived time

USERCOOP is expected to cooperate with the user in the temporality of the current session. This includes, without reducing the system to a productivity application:

- Task management: knowing what is intended, active, paused, completed, blocked, or newly relevant.
- Work-time management: relating activities to available time, duration, sequence, interruption, resumption, and stopping points.
- Personal-growth management: maintaining locally defined goals, practices, learning, reflection, and progress across sessions.
- Context preservation: keeping paused work developed and resumable rather than forcing the user to reconstruct it mentally.
- Temporal attention: bringing forward knowledge when it becomes relevant to the current point in an undertaking.
- Session reflection: making what happened, changed, or remains unfinished available as knowledge rather than as an automatically generated judgment.

These are not isolated modules placed beside the knowledge base. Tasks, time, growth, and sessions are themselves knowledge domains expressed through the same objects, relationships, rules, events, histories, and activities as the rest of USERCOOP.

The system does not need to infer a hidden life plan or decide what personal growth should mean. The user defines the relevant concepts, commitments, measures, and rules. USERCOOP contributes memory, structure, derivation, temporal awareness, presentation, and action within those explicit terms.

## 4. Core proposition

The interface is not a collection of windows that the user must arrange and monitor manually. It continuously materializes the user's evolving semantic context.

USERCOOP is a semantic interaction layer through which the user pilots the device. Rather than requiring the user to navigate the separate interfaces of files, applications, notifications, and system facilities, it coordinates those existing capabilities around the user's current intention.

The stream of user entries serves two purposes at once:

1. It states what the user wants USERCOOP to know, infer, or do.
2. It provides an ongoing trace of what currently occupies the user's attention.

The display responds to that trace. It selects information, changes its level of detail, adjusts how much is simultaneously visible, moves focus, and reveals valid continuations while the instruction is still being composed.

The result is neither a conventional graphical desktop nor a conventional terminal:

| Conventional model | Primary organization |
|---|---|
| Window system | Applications arranged as rectangles |
| Terminal | Input and output arranged as one chronological stream |
| USERCOOP | Information arranged around the user's current activity and developing intention |

## 5. Design principles

1. **Never guess.** An entry resolves deterministically, exposes its remaining ambiguity for the user to resolve, or fails when it has no valid reading. USERCOOP never silently chooses a merely plausible interpretation. Failure generates a semantic event associated with the originating entry.
2. **Reveal the current language.** The system shows what is valid in the present context instead of requiring memorization of a global command set.
3. **React before submission.** A partial entry may already resolve objects, narrow possibilities, and reorganize the display.
4. **Preserve authorship spatially.** User-authored and system-generated information items receive visibly distinct presentations, so their origin is apparent without classifying their content.
5. **Compose the display automatically.** The system decides what appears, where, and at what scale.
6. **Treat preferences as defaults, not prohibitions.** Explicit requests and genuine information requirements may temporarily override the user's resting presentation preferences.
7. **Be lively in the foreground and stable in the background.** Active composition may cause rapid meaningful movement; unrelated information changes conservatively.
8. **Keep content semantic.** Knowledge describes meaning and available action. USERCOOP owns presentation.
9. **Support every input mode completely.** Keyboard interaction is primary where a keyboard is present, and every semantic action remains available through mouse or touch alone.
10. **Remain offline by construction.** USERCOOP's own runtime must be programmatically unable to initiate or receive communication across an external network, and its operation must never depend on Internet access or a remote service. Section 6 states exactly what this covers.
11. **Reward attention without demanding it.** A refinement should be perceptible to someone who attends to it while remaining unobtrusive to someone who does not.
12. **Allow initiative only through capabilities.** USERCOOP may ask, infer, present, and act on its own initiative, but only within user-defined knowledge and device boundaries.
13. **Let accessibility bound everything else.** Accessibility requirements constrain motion, typography, contrast, timing, and information capacity, and they outrank both aesthetic choices and the user's ordinary presentation preferences.

---

# Part II. Boundaries

## 6. Offline by construction

Offline operation is a foundational property of USERCOOP, not a mode, a preference, or a promise about ordinary behavior.

### 6.1 What the guarantee covers

The guarantee is stated precisely so that it can be enforced and tested rather than merely asserted.

**Covered.** The USERCOOP process, its semantic kernel, its session and inference runtime, its device adapters, and any component that ships inside the application must be unable to initiate or receive communication across an external network. There is no protocol-specific exception, and no adapter or extension may silently weaken this property.

**Not covered.** Other programs on the device retain their own networking. USERCOOP may hand work to them under the rules in [section 6.4](#64-handoff-to-network-capable-programs) and [section 7.3](#73-command-execution). The operating system itself remains networked.

"Local" means strictly within the same physical device that is running USERCOOP. Other computers, phones, appliances, or services on a trusted local-area network are external for the purpose of this principle and are not reachable by USERCOOP.

This boundary keeps operation of the device local, makes the system useful without connectivity, and prevents the interaction layer from becoming an implicit conduit through which device activity or command history can leave the device.

### 6.2 Local communication

Communication confined to the device is permitted where it is needed to connect USERCOOP to local adapters, applications, or system bridges. Candidate transports, in order of preference:

1. Operating-system facilities such as Unix domain sockets, named pipes, or equivalent inter-process communication. These are preferred because they are not network sockets and therefore do not require network permissions.
2. Loopback TCP or loopback WebSocket connections, on platforms where option 1 is unavailable and where opening a loopback socket does not require granting the application general network permission.

Such transports are implementation details of an in-device system. They must not listen on externally reachable interfaces, accept remote peers, or provide a route from a local component to an external network through USERCOOP.

The transport is selected per platform. A loopback transport is admitted only where it can be granted without also granting external network access; otherwise USERCOOP uses a non-network operating-system IPC facility. Android packages do not request the `INTERNET` permission.

### 6.3 Enforcement and verification

The restriction is enforced by construction and confirmed by tests, not by convention.

| Layer | Mechanism |
|---|---|
| Source | No networking namespace or engine networking API may be referenced by kernel, runtime, or adapter code. Enforced by a static analysis rule that fails the build. |
| Dependencies | Third-party packages are audited for networking surface before adoption. A package that opens sockets is not admitted. |
| Engine and runtime | Release builds use a custom Godot build profile and export template with networking modules excluded. Runtime libraries with reachable networking surfaces are not admitted into the release artifact. |
| Platform | The application is packaged without network permissions wherever the platform expresses them, including the Android `INTERNET` permission. |
| Test | An automated test runs the packaged application under observation and asserts that it opens no external connection and listens on no externally reachable interface. |

The last row is the one that matters most: the offline property must be a passing test in the build, not a paragraph in this document.

Official editor builds may be used during development, but they do not satisfy the release guarantee. A release exists only when its custom artifact passes the static, packaging, and runtime tests above.

### 6.4 Handoff to network-capable programs

Features that conventionally depend on online services are not performed by USERCOOP over the network. Where appropriate, USERCOOP may invoke a capability belonging to another installed application or to the operating system. That external application remains visibly and technically responsible for its own networking, permissions, and results.

Launching a mail composer, a browser, or another network-capable application through an operating-system action does not make USERCOOP the network client. The handoff must remain explicit and visible to the user, and USERCOOP must not collect, proxy, or transmit the resulting network traffic.

## 7. Capabilities and authority

Everything USERCOOP can do to the device it inhabits is expressed as a capability. A capability is knowledge: it can be inspected, queried, explained, granted, and withdrawn through the same language as anything else.

### 7.1 Capability classes

| Class | What it permits | Default |
|---|---|---|
| Observation | Reading files, processes, settings, notifications, and hardware state within a declared scope | Granted for scopes the user has named |
| Local action | Changing state through a bounded, named operation, such as moving a file within an authorized folder | Granted per scope, confirmation configurable |
| Application operation | Launching, focusing, or stopping a known application, or invoking it with explicit arguments | Granted per application |
| Command execution | Running an arbitrary command line, shell invocation, or platform intent | Denied by default, see 7.3 |

Each class is scoped. A capability names what it may touch, not merely what it may do. A grant is recorded with its own provenance, so USERCOOP can always explain why an action was permitted.

### 7.2 Authorization and confirmation

Knowing that an action is appropriate is distinct from having permission to perform it. A derived action requires an authorized capability and, where the capability says so, explicit confirmation.

The operating system remains authoritative over files, processes, hardware, permissions, application sandboxing, and protected actions. USERCOOP does not attempt to bypass that authority, and an operating-system refusal returns as knowledge rather than being retried silently.

### 7.3 Command execution

An advanced procedure may eventually invoke a complete Bash or PowerShell command line, an Android intent, or another local operating-system facility. These are the most powerful actions USERCOOP can take, and they are the one place where the offline guarantee needs explicit care: an arbitrary command line can reach the network even though USERCOOP cannot.

Command execution is therefore treated as its own capability class with stricter rules than any other:

- It is denied by default and must be granted deliberately.
- A grant names either specific command forms or an allowlist of executables. A grant of "any command" is possible but is presented as what it is: a removal of the boundary that the rest of the design maintains.
- Every execution is recorded with its originating entry, the rule or procedure that produced it, the capability that authorized it, and its result.
- A command that a rule produced on USERCOOP's own initiative requires confirmation unless the user has granted that specific command form for unattended use.
- Execution never becomes implicit. USERCOOP shows what it is about to run in the same terms the user would have typed.

Processes, output, failures, and device changes return as knowledge and events. External applications do not become the source of USERCOOP's semantic model.

### 7.4 Safety bounds on acting rules

Rules may fire actions, actions produce events, and events may fire further rules. That loop is the point of the design, and it is also the obvious failure mode. Three bounds apply:

1. **Cycle detection.** A derivation chain that revisits the same rule and binding within one triggering event is stopped and reported as a failure event rather than continuing.
2. **Action rate bounds.** Each capability carries a maximum action rate. Exceeding it suspends the rule and produces a failure event rather than degrading silently.
3. **Depth bounds.** Action-producing rules have a bounded cascade depth from a single originating event.

When a bound is reached, USERCOOP reports what stopped, which rule reached the bound, and what it would have done next. Suspension is visible; a suspended rule is information, not an invisible policy.

The user may raise, lower, or remove these bounds. Such a change is an explicit modification of USERCOOP's operating knowledge and is recorded with its provenance and consequences. USERCOOP may propose a different bound, but it may apply that proposal autonomously only when the user has specifically granted it authority to modify that bound. The system's knowledge of what it may modify is distinct from the user's unrestricted ownership of their system.

---

# Part III. Language

## 8. Activities and contextual vocabulary

USERCOOP shows the user the vocabulary, information, and actions relevant to the current activity. An application does not present a parallel interface inside USERCOOP. USERCOOP remains the interaction system throughout.

An activity is a temporary semantic environment:

```text
Activity
|-- identity
|-- parent activity
|-- current semantic state
|-- available commands
|-- valid argument patterns
|-- visible information sources
|-- possible actions
|-- completion conditions
`-- exit or return behavior
```

### 8.1 Activity stack

Activities form a stack. Entering a more specific activity pushes a context; completing, rejecting, or leaving it returns to its parent.

```text
Current session
`-- Manage tasks
    `-- New task
        `-- Choose date and time
```

The activity stack is cognitive as well as navigational. Each level changes the relevant objects, available language, appropriate information, and likely next actions.

### 8.2 Where the current language comes from

USERCOOP determines the language currently shown to the user from the active activity, semantic types, rules, and capabilities known to the system. Its kernel defines:

- Commands valid in the current activity.
- Syntax patterns for those commands.
- Semantic types accepted by each slot.
- Candidate objects that may fill those slots.
- Actions that enter, complete, reject, or leave activities.
- Information items relevant to the activity.

A device adapter may register bounded facts, types, and authorized action signatures with that kernel. It does not define the activity or its presentation. USERCOOP performs parsing and discovery, shows valid continuations, manages history and attention, gives information space on the screen, and provides keyboard, mouse, and touch interaction.

### 8.3 Entering and leaving activities

The user enters an activity, performs the work appropriate to it, and leaves when finished. The display adapts for the duration of that activity and releases its temporary information when the activity closes.

This is not equivalent to opening and closing an application window. An activity may draw on several knowledge domains and device capabilities while remaining one coherent cognitive context.

The active activity contributes context to the current grammar. It may change the vocabulary, patterns, or continuations presently available, according to definitions the user can inspect and modify. Context therefore reduces repetition without imposing one universal syntax on every activity.

## 9. Command language

The primary interaction is keyboard-driven through an active typing space. The vocabulary is terse and mechanical, taking inspiration from the archetypal keyboard scenes in *Tron* (1982) and *WarGames* (1983).

SHRDLU is a spiritual ancestor rather than a syntax to copy. Its natural-language interface worked because it resolved against a small, closed, well-defined world of objects, relations, and actions. The same property permits deterministic resolution here.

REXX contributes the principle of least astonishment: the meaning of an instruction should follow from its visible words, without hidden precedence surprises or punctuation doing silent work.

### 9.1 Custom grammar and deterministic interpretation

The language is not an invariant of USERCOOP. Its grammar is part of the programmable knowledge base. USERCOOP begins with a usable grammar, but the owner may revise or replace it just as they may revise other knowledge.

A grammar may distinguish declarative, imperative, and interrogative modes; accept concise administrative forms such as those in the examples; provide synonyms or inflected forms such as `WORK` and `WORKS`; and define how constructs occupy slots inside larger constructs. These are facilities available to the grammar, not fixed words or mandatory categories built into the interaction system.

Context does not replace grammar. It supplies information to the active grammar, which may use the current activity and earlier parts of an entry to interpret what follows. This permits stepwise articulation without requiring every intention to be compressed into one elaborate command.

The supplied grammar follows the intended terse, punctuation-free direction, but it does not seek to imitate unrestricted prose. A customized grammar remains deterministic: customization changes the definitions by which entries are understood, not the requirement that USERCOOP know which definition it applied.

- An entry that resolves cleanly is accepted.
- A submitted entry with no valid reading does not execute and generates a failure event associated with that entry.
- A submitted entry with several valid readings does not execute yet. USERCOOP enters a clarification activity, presents the alternatives in the terms that distinguish them, and accepts a selection or further entry from the user.
- Fuzzy matching never silently substitutes a plausible interpretation.
- Every intermediate reduction follows an ordered, inspectable pattern list.

Clarification is a normal continuation of the activity, not an admission that natural-language guessing has taken place. The ambiguity itself is known precisely. If the user abandons clarification, no reading is committed.

### 9.2 Patterns and composition

#### Multiline entries

The unit of submission is an entry, not a physical line. USERCOOP treats the entry as unfinished until the user submits an empty line by pressing Enter twice after the last content line. A single Enter only adds another line to the same entry. An active grammar may define words such as `DONE` as explicit alternatives to the empty terminating line.

The grammar currently in force determines how the lines of an entry relate, what may be omitted or inferred from context, and what each construct means. The examples above intentionally leave those definitions unstated: they demonstrate pace and character rather than standardizing their syntax.

One possible grammar can use word position rather than punctuation to mark argument roles:

```text
PUT x INTO y
x TALLER THAN y
HELD x
```

In this example, patterns are organized as an ordered list that explicitly defines their precedence, and they reduce from the highest precedence outward.

Worked example:

```
usr:    PUT BLOCK TALLER THAN HELD BLOCK INTO BOX
```

1. `HELD BLOCK` matches `HELD x` and resolves to one held block, `OBJ1`.
2. `BLOCK TALLER THAN OBJ1` matches `x TALLER THAN y` and resolves to `OBJ2`.
3. `PUT OBJ2 INTO BOX` matches the outer operation and executes.

### 9.3 Names and reserved words

Words that identify a pattern are reserved and cannot also serve as object names. Because the user can define new vocabulary at any time, the two namespaces can collide, and the collision must fail rather than resolve by preference.

A definition that would make an existing reserved word into an object name, or that would reserve a word already used as an object name, is rejected at the moment it is stated. The rejection is a failure event that names the conflict and the existing definition. USERCOOP does not rename, shadow, or disambiguate by context.

The user may retire a reserved word. USERCOOP first shows the patterns and readable artifacts that depend on it. Retirement deactivates those patterns but does not delete facts: stored knowledge refers to stable identities, not to the current spelling of a name. Renaming, rebinding, and deletion are separate explicit operations.

### 9.4 Pipes and variables

Selections and results can be piped into later operations or stored in named variables. A selection may be piped into a display instruction (for example, to make the view reveal it) or retained for reuse across later commands.

## 10. Live composition

The screen reacts while the user composes a multiline entry. Submission is not the first moment at which the entry has meaning.

### 10.1 Incremental semantic state

For every partial entry, the parser exposes:

- Recognized keywords.
- Resolved subexpressions.
- Unresolved slots.
- Valid continuations.
- Candidate referents.
- Current semantic types.
- Temporary activity contexts.
- Likely spatial or informational focus.

This state drives the display immediately without executing the unfinished entry. Completed lines remain provisional until the terminating empty line, but they already constrain the interpretation of later lines and may affect the display.

### 10.2 Valid continuations

The interface always shows what may validly follow from the current parser state and the active grammar. These may include continuations of the current line or possible next lines. They are contextual possibilities, not a global command catalog or a list of mandatory fields.

Entering an activity narrows the language. Beginning an entry, filling an argument, or completing a line narrows it again. Submitting or abandoning the entry and completing or leaving the activity restore the appropriate parent vocabulary.

### 10.3 Case as parser feedback

The ordinary appearance of user input is uppercase. In the large majority of composition, letters appear and remain uppercase as the instruction is recognized.

Lowercase is exceptional and carries specific parser feedback:

- A value recognized as a variable appears in lowercase, confirming that it is being interpreted as a variable rather than as command vocabulary.
- A sequence that no longer matches the language appears in lowercase, signaling a likely typo or other failure of recognition.

The display updates retroactively as understanding changes. The user can therefore see recognition directly in the letters without needing an additional icon, underline, or diagnostic message. Because uppercase is normal, these exceptions remain clear and uncommon.

Case feedback is a channel of the Latin-script presentation, not a universal mechanism. Scripts without case distinction, and scripts whose case mapping is not reversible character by character, cannot carry it. Where case feedback is unavailable, the same two conditions are carried by an equivalent non-case channel, chosen once and used consistently: reduced stroke weight for a recognized variable, and reduced weight plus a subtle horizontal offset for unrecognized text. The semantic meaning is identical; only the visible channel differs.

The first implementation provides a Latin-script command vocabulary. Unicode text, including mixed-script text, is permitted in literal values and object names wherever it does not collide with reserved vocabulary. Additional command-language scripts are added as complete language presentations, with an appropriate parser-feedback channel and tested font coverage; they are not approximated by Latin case rules.

### 10.4 Provisional cognitive context

Resolved portions of an unfinished entry already affect the surrounding display.

Within one line of an entry using that example grammar, while composing:

```
usr:    PUT BLOCK TALLER THAN HELD BLOCK INTO BOX
```

the interface may progress as follows:

| Partial construct | Provisional response |
|---|---|
| `PUT` | Open an operation context |
| `PUT BLOCK` | Make candidate blocks relevant |
| `PUT BLOCK TALLER THAN` | Reveal comparison information |
| `PUT BLOCK TALLER THAN HELD` | Emphasize held-object categories |
| `PUT BLOCK TALLER THAN HELD BLOCK` | Resolve a particular object and begin framing it |
| `PUT BLOCK TALLER THAN HELD BLOCK INTO` | Make candidate destinations relevant |
| `PUT BLOCK TALLER THAN HELD BLOCK INTO BOX` | Resolve the destination and present the complete operation |

If `HELD BLOCK` deterministically resolves to an object, a spatial view may begin panning and zooming toward it before the outer construct or entry is complete. Backspacing, changing an earlier line, or abandoning the entry unwinds that provisional context.

This movement is intended. The display should appear to live alongside rapid typing, as in the keyboard-driven scenes that inspired it.

### 10.5 Response targets

"React before submission" is a timing claim, so it carries numbers. These are initial targets for a mid-range device of each class, to be measured rather than assumed:

| Event | Target | Ceiling |
|---|---|---|
| Keystroke to updated parser state and updated letter case | 16 ms | 50 ms |
| Keystroke to updated valid continuations | 50 ms | 100 ms |
| Resolution of a referent to the start of camera movement | 100 ms | 200 ms |

Parsing a partial entry must be incremental. Re-parsing the whole entry from its first character on every keystroke is acceptable only while it stays inside these targets, and the design should not assume it will.

Inference results are exempt. They arrive when they arrive, and [section 22.5](#225-incremental-inference) describes how they are presented while incomplete.

---

# Part IV. Information and presentation

## 11. Information items and spaces

An information item describes something USERCOOP may need to manage: its meaning, identity, content, relevance, and available actions. A space is the presence USERCOOP gives that item on the screen. The information item is semantic; the space is compositional.

Neither is a window or a card. An information item does not prescribe a rectangle, coordinates, or visual hierarchy. One item may move between spaces or representations as attention changes, and several related items may share a space when USERCOOP judges that they belong together.

The screen is not divided into applications, windows, or a terminal plus an output area. It is one composed workspace containing spaces. A space gives temporary visual presence to an information item or a related group of them: an entry being composed, a submitted entry, a set of valid continuations, a notification, a spatial view, or another part of the current activity. USERCOOP creates, emphasizes, transforms, moves, and releases spaces as it composes the screen around the current activity.

### 11.1 Semantic content

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

### 11.2 Presentation belongs to USERCOOP

USERCOOP decides:

- Whether the information item is currently given space.
- Where it appears.
- Which representation appears in that space.
- How much emphasis it receives.
- When it displaces or is displaced by other information.
- How it transitions between states.
- How user preferences influence it.

### 11.3 Multiple representations

An information item may support several semantic representations rather than arbitrary continuous resizing:

| Representation | Purpose |
|---|---|
| Overview | Identity, state, and most important summary |
| Standard | Information needed for ordinary work |
| Detailed | Full inspection or active manipulation |

These representations concern granularity. They do not determine how many other information items may simultaneously be given space.

## 12. Authorship, typed entries, and history

The distinction between what the user authored and what the system generated is spatial rather than conversational. User-authored information items receive recognizably different spaces from results, failures, notifications, and other system-generated information. An observer can therefore recognize origin from placement and presentation without first reading and classifying the content.

### 12.1 Typed-entry information

An entry being typed is itself an information item known to USERCOOP. The current line being typed is also known separately as the mutable part of that entry; it is not identical to the space that happens to show it. The unfinished entry contains that line, any preceding physical lines, and the semantic state produced by incremental parsing. A single Enter completes the current physical line and begins another within the same entry. An empty line submits the entry, changes it into a submitted-entry information item, and assigns it a permanent entry number.

The entry and its individual lines are known information. They do not inherently occupy a particular position, size, or shape, and they are not themselves spaces.

### 12.2 Spaces showing typed entries

USERCOOP ordinarily gives the current line of the entry a large, prominent space. Earlier lines of the same unfinished entry remain visibly associated with it, and recently submitted entries receive separate, smaller spaces nearby. Those choices provide continuity without forming a terminal, console, transcript, or chronological input-output stream.

Spaces representing typed-entry information show only text authored by the user and parser feedback applied to that text. System-generated results, questions, failures, notifications, and automatic information receive other spaces elsewhere in the composition.

### 12.3 Failure events

A failing entry does not answer the user with an explanation and does not add system-generated content to the submitted-entry information item. It generates a separate semantic event:

```text
input entry 47 failure
```

That event becomes another information item managed by USERCOOP. It may receive importance, be given a space, affect attention, persist, recede, or be displaced under the same composition principles as other information. Its stable association with the submitted-entry item lets USERCOOP present the failure in context without changing the user-authored item.

The event may contain structured fields needed by USERCOOP to identify and manage the failure, but it is not inherently a prose response or conversational explanation. The presentation of those fields remains a decision of the interaction system.

The term "failure event" is used throughout this document for this construct. Parse failures, unresolved references, refused authorizations, exceeded safety bounds, and failed device operations are all failure events, differing in their structured data rather than in kind.

### 12.4 History and citation

History and entry numbers belong to the local USERCOOP installation. The user may configure what is visible and delete local history.

Deleting history never resets the entry counter. A citation such as `entry 47` therefore always identifies the same submitted entry, even if it has since been deleted. A request for a deleted entry generates a system information item. When a particular physical line matters, it is addressed within its entry, as in `entry 47 line 3`.

The entry counter is part of persisted installation state, not of the history table. Restoring from a backup restores the counter, and a restore never reissues a number that was used before the backup was taken. If a restore would do so, USERCOOP advances the counter past the highest number ever recorded rather than reusing it. Stable citation is worth more than contiguous numbering.

Applications and device capabilities respond through ordinary operation correlation and never need to know USERCOOP's local entry numbers. USERCOOP knows which local entry caused an operation and may cite it when presenting the result. Separate USERCOOP installations therefore need no synchronized numbering.

Past history is retrieved through a request such as `SHOW ENTRY 47`. Mouse or touch scrolling remains available as an equivalent path. The requested entry is given its own space, accompanied by a small reminder of the request that retrieved it.

## 13. Typography

Text is the principal kind of perceptible information exchanged between USERCOOP and the user. Typography is therefore part of the interaction model rather than decoration applied after the interface has been designed. It must make the system cognitively affordable, visibly responsive, and capable of exposing technical depth without allowing that depth to dominate.

The goal is not to select fonts that call attention to their own beauty. The fonts should stay out of the way, so that USERCOOP can be both beautiful and useful.

### 13.1 Font system

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

### 13.2 Monospace scales

The monospaced family has three characteristic scales:

- **Large:** user input. The line being typed is roughly twice the ordinary text size. It is the clearest and most immediate evidence that the device is receiving the user's intention.
- **Normal:** formatted or structurally literal content for which fixed character alignment is useful.
- **Very small:** rarely needed or purely technical reference information such as object identifiers, line numbers, software versions, and internal correlations.

The very small scale makes the machinery visible without making it central. Experienced users may read and use it. Other users may perceive it as quiet evidence that USERCOOP is listening, interpreting, and doing real work. Their own input remains large, meaningful information remains normally sized, and supporting machinery forms subtle visual texture around it.

Essential information must never depend on the very small scale, and the very small scale is subject to the minimum sizes in [section 18](#18-accessibility). When technical information becomes relevant or is explicitly requested, USERCOOP gives it an ordinary readable representation.

The use of large monospaced uppercase input deliberately retains the directness associated with fictional and historical command interfaces: a person sits at a computer, states what they want in simple letters, and the device responds. This is not retro styling for nostalgia. It is a cognitively affordable interaction in which users do not need mastery of menus, keyboard punctuation, underscores, or elaborate syntax merely to address the device.

### 13.3 Text arrives through time

Every text appears letter by letter. A complete line is never materialized instantaneously when USERCOOP first presents it in a space.

The reveal is quick and does not turn an ordinary line into a long-running typewriter performance. Its purpose is to give textual appearance a perceptible duration: the system is listening, composing, and cooperating rather than dropping finished rectangles of content onto the screen. The effect should be apparent to someone attending to it while remaining natural and unobtrusive to someone who is not.

User input naturally appears at the pace of typing. System-generated text uses a brief controlled cadence appropriate to the current sport-to-zen pace and interaction cadence. Urgency, readability, and accessibility may accelerate the reveal, and a reduced-motion or assistive-technology setting removes it entirely, as specified in section 18.

Letter-by-letter revelation belongs to the presentation of an information item, not to its semantic storage. USERCOOP may already know the complete text while its current space reveals that text through time. Because the full text exists as knowledge from the first frame, selection, search, and assistive technology always operate on the whole text, never on the portion so far revealed.

### 13.4 Text without visible containers

Information spaces do not normally draw rectangular containers around text. Internally, a 2D control still has bounds for layout, projection, focus, and interaction, but those bounds do not need to become a visible card or panel.

Text primarily needs an anchor, a vertical alignment line, a readable measure, and a meaningful relationship to nearby information. It may be left-aligned, centered, or right-aligned according to its role in the spatial grammar. Empty space, alignment, typography, and movement establish grouping before borders or backgrounds are considered.

Camera distance changes the room available to an information representation, not the basic legibility of its font. When less room is available, the item says less: it moves from detailed to standard to overview representation rather than continuously shrinking its text. The invisible projected rectangle remains useful as layout geometry even when no rectangle is visually drawn.

### 13.5 Writing discipline

USERCOOP's own text is composed from simple sentences and short lines. When several short statements will communicate something clearly, they are preferred to a dense paragraph or a long line forced into an arbitrary container.

Device adapters and importers should supply semantic facts, identity, state, relationships, and actions wherever possible. USERCOOP remains responsible for expressing ordinary interface information in its coherent voice. Intrinsic content such as a message, document, or source file remains the content itself and may require longer-form reading.

Icons and emoji are not part of USERCOOP's interaction vocabulary. The system relies on letters, words, case, weight, scale, alignment, space, and movement rather than asking the user to learn a parallel symbolic language.

## 14. Presentation preferences

Presentation density is two independent preferences, not one, and pace is a third. They are specified separately because they answer different questions.

### 14.1 Granularity

Granularity expresses the user's resting preference between overview and detail.

- **Overview:** summarize first; let detail earn space or appear on request.
- **Detail:** expose more structure and supporting information by default.

### 14.2 Occupancy

Occupancy expresses the user's resting preference for the total amount of information simultaneously visible.

- **Sparse:** preserve empty space and give fewer information items space at once.
- **Rich:** permit more concurrent information and a busier display.

The two axes form four legitimate regions:

|  | Overview | Detail |
|---|---|---|
| **Sparse** | Calm global picture | One subject examined deeply |
| **Rich** | Many compact summaries | Many detailed subjects at once |

### 14.3 Sport-to-zen pace

A gradual **sport-to-zen** preference describes the user's resting preference for the pace and motion character of the interface.

- **Sport:** quicker acceleration, faster settling, shorter pauses, and a more immediate feeling of response.
- **Zen:** gentler acceleration, longer settling, more breathing room, and a more contemplative feeling of response.

The scale is continuous rather than a choice between two modes. It governs the motion and temporal presentation of the same semantic behavior; it does not make commands less deterministic, delay essential feedback, or change what the user is authorized to do.

The selected value is a baseline. USERCOOP may move temporarily around it to match the user's current **interaction cadence**: the general speed at which the user is presently typing, choosing, and advancing through the activity.

Interaction timing is the only behavioral signal USERCOOP collects, and it is used for one purpose: placing the presentation on the sport-to-zen scale. Specifically, it consists of typing speed, intervals between actions, correction cadence, and rate of progression. It is computed entirely on the device, it is not persisted beyond the current session, it is never a fact in the knowledge base, and it never influences what USERCOOP concludes, permits, or does. The user may constrain or disable the adaptation while retaining a fixed sport-to-zen preference.

A rapid, sustained cadence may pull presentation toward the sport side, as when the user is working in a hurry. Longer intervals and an unhurried cadence may pull it toward the zen side. USERCOOP responds to the demonstrated pace itself and does not infer why the user has adopted it.

Adaptation must be gradual, bounded, and resistant to oscillation. A brief burst of typing or a single pause must not cause a conspicuous change of character.

### 14.4 Preferences are equilibria

Preferences describe where the display rests when no stronger requirement exists. They are not hard limits.

Precedence, from strongest to weakest:

1. **Accessibility requirement.** Motion, contrast, timing, typography, and capacity constraints bound everything below. They are not overridden by an explicit request for something they forbid; instead, the request is satisfied in a form the constraint permits.
2. **Explicit request.** If the user asks for detail, show detail.
3. **Semantic requirement.** If information cannot be understood safely in a compact form, use the required representation.
4. **Simultaneous importance and criticality.** If several matters genuinely require attention, temporarily increase occupancy, within the capacity limit of section 18.
5. **Standing preference.** When the system has a choice, return toward the user's preferred granularity, occupancy, and sport-to-zen pace.

A sparse preference means "when possible, show less," not "conceal simultaneous important information." An overview preference means "begin with summaries," not "withhold detail that was requested."

The sport-to-zen preference is likewise an equilibrium rather than a fixed animation multiplier. Current interaction cadence, semantic urgency, and accessibility requirements may shift motion away from that equilibrium. When those pressures end, the interface settles back toward the chosen baseline rather than snapping through every intermediate arrangement.

## 15. Attention and automatic composition

The user is not expected to move, resize, close, or scroll through arbitrary windows. USERCOOP decides what is shown, how, and where within its presentation grammar.

Automatic composition is primarily editorial judgment rather than geometric novelty. The essential problem is selecting and presenting the right information, not discovering clever coordinates for rectangles.

### 15.1 Attention from command traffic

The current session and stream of user entries are the primary attention signals. Something the user repeatedly references, selects, compares, or acts upon remains visible and prominent. Rules and active inference may also bring information forward on USERCOOP's initiative. Once attention moves elsewhere, information recedes and may eventually be displaced.

"Busy with something" is inferred from semantic command activity: what the user is naming, resolving, and acting on. No surveillance signal beyond the interaction timing of section 14.3 is collected.

### 15.2 Three questions, three measures

The design uses three established ideas, each answering a different question. They are specified separately here and combined in section 15.6.

| Question | Measure |
|---|---|
| What deserves screen space now? | Degree of interest |
| What should the user act on first? | Value per handling time |
| What will be too late if not mentioned now? | Criticality |

### 15.3 Degree of interest

George Furnas's 1986 *Generalized Fisheye Views* defines Degree of Interest as:

```text
DOI(x) = API(x) - D(x, y)
```

`API(x)` is a priori importance. `D(x, y)` is distance from the current focus, which Furnas permits to be logical or task distance rather than physical distance.

Here, task distance is derived from the active activity stack and entry stream: recency of reference, frequency of reference, semantic relationship to resolved entry objects, and relationship to unfinished slots.

Both terms are normalized to the same `0` to `1` scale, so that the subtraction is meaningful. `D` is `0` for the current focus and approaches `1` for information with no discernible relationship to the current activity. Consequently `DOI` falls in the range `-1` to `1`, and only non-negative values compete for space.

### 15.4 Value per handling time

Smith's rule, also called weighted shortest processing time, ranks work by value divided by handling time. This axis answers what the user should act on first within a limited session. It contains no deadline.

This measure orders action; it does not allocate space. It affects the sequence in which items are offered, the ordering within a list, and which item is proposed as the next step. It never overrides degree of interest in the decision about what is visible.

### 15.5 Criticality

Criticality applies whenever an opportunity or delivery context has an identifiable closing window.

Effective importance is natural importance multiplied by the probability that the user will not remain in, or naturally return to, the relevant context before it closes. As the remaining window shrinks, that probability approaches one.

Criticality covers both:

- A real opportunity that disappears.
- The interface's chance to mention something before its context stops being useful.

Known window types:

- **Duration-bound:** a short fixed interval after a triggering event, such as correcting a typo.
- **Event-bound:** a window ending at a scheduled event.
- **Session-bound:** a window ending when the user leaves, estimated from expected session length rather than real-time behavioral inference.

Continuous standing state has no closing window. It remains governed by importance and task distance alone.

### 15.6 How the three combine

Criticality feeds degree of interest; value per handling time stands apart.

```text
effective importance  =  intrinsic importance * criticality factor
DOI(x)                =  effective importance(x) - D(x, focus)
space allocation      =  highest DOI first, within the display budget
action ordering       =  value / handling time, among items already offered
```

The criticality factor is `1` for information with no closing window, and rises toward the bound as the window closes. Effective importance is clamped to the shared maximum of `1`, so criticality can bring something forward but cannot make it outrank everything permanently.

### 15.7 Shared scales

Importance and criticality use bounded scales with a maximum of one.

A maximum prevents a newly introduced scoring formula from growing without limit and permanently dominating every established signal. Very low scores need no corresponding floor beyond zero; information may simply remain hidden.

Criticality is naturally a probability. Importance uses equivalent natural-language anchors:

- `1`: nothing is more important.
- `0`: the system could not care less.
- Intermediate values preserve meaningful ratios.

### 15.8 The display budget

Space is finite, and on a phone it is very finite. The budget is a property of the device and the current accessibility settings, not of the scoring.

USERCOOP computes a maximum number of simultaneous spaces from the available area, the current representation sizes, and the minimum text sizes required by section 18. Scoring selects which items fill that budget; scoring never enlarges it.

If several information items simultaneously reach maximum effective importance and together exceed the budget, they receive equal maximal treatment rather than being force-ranked by insignificant differences. This resembles high-stakes alerting systems that present several warning-level events at the same tier. When they cannot all be shown:

1. Each is given the overview representation rather than a larger one.
2. If they still exceed the budget, USERCOOP presents a single space enumerating them, at the same maximal emphasis, with the count visible.
3. USERCOOP never silently drops an item at maximum effective importance.

## 16. Spatial composition

USERCOOP uses a genuine three-dimensional layout while rendering most visible information through ordinary two-dimensional controls. The 3D world gives activities, information, and subjects stable spatial relationships. The 2D layer preserves precise typography and direct interface behavior.

Spatial position is semantic. It communicates progression, membership, provenance, current focus, and changes in activity context. USERCOOP therefore composes a spatial statement rather than arranging a collection of arbitrary panels.

### 16.1 Rendering layers

The screen has three rendering layers, from front to back:

1. A transparent 2D control layer containing the visible representations of information items.
2. A 3D world containing layout anchors and, when appropriate, real visible 3D objects.
3. A visually empty sky rendered as a simple off-white or dark-gray field according to the current theme.

Most tools, descriptions, choices, states, and supporting details appear as 2D controls. Real 3D objects are reserved primarily for the final concepts being examined, manipulated, or analyzed: the things the activity is about rather than the tools used to work with them. This is why 2D information normally renders in front of the 3D world. Legible information supports the subject while the subject retains genuine spatial presence beneath it.

The 3D environment is conceptual rather than scenic. It does not require a room, floor, stars, grid, or decorative landscape. Its depth is made perceptible through composition, camera movement, scale, parallax, and the occasional presence of genuine 3D subjects.

### 16.2 Projected information spaces

An information item remains distinct from both its 3D layout geometry and its visible 2D representation.

For each visible information space, USERCOOP maintains an invisible, camera-facing rectangle in the 3D layout. Its center and the midpoints of its four edges are projected through the camera into screen coordinates. Their projections determine the center, apparent width, and apparent height of the corresponding 2D control. Camera-space depth determines ordering among projected controls.

```text
information item
        | represented in the spatial model by
invisible 3D rectangle
        | projected through the camera into
screen position, apparent size, and depth order
        | used to present
native 2D control
```

The visible control is therefore not a 3D billboard, texture, or subviewport. It remains native 2D interface content with clean typography. The invisible rectangle supplies only spatial placement and scale.

### 16.3 The developing wall

The user's basic orientation is that of a person seated at a keyboard and facing an unbounded working wall. This wall is not a visible physical surface. It is the spatial development of the current activity stack as it exists now.

The wall may develop in different directions when the activity requires it, then retract when work completes. It does not need to preserve a permanent map of every previous activity. Later activity may develop a different structure from the same conceptual center.

The camera follows this development while generally preserving the stable experience of facing the working wall. Translation changes the user's point of view; rotation changes the direction of gaze from that point of view. Both are meaningful, but the design does not require continuous orbiting or disorienting changes of orientation.

### 16.4 Directional grammar

These directions describe the initial grammar for cultures that conventionally read and diagram progression from left to right. They are semantic defaults rather than claims of universality and may require adaptation for other cultural directions.

A **line schema** is the spatial form of one perdurant: a horizontal line of steps developing left to right, with its attached information arranged above and below. It is the basic unit of spatial composition, and every activity, process, or developing subject has one.

The starting position of an activity is its conceptual center. As the activity develops, each step appears to the right of the preceding step. The camera follows this development, and the latest operative step becomes the new conceptual center. Earlier steps remain toward the left as the path by which the current state was reached.

```text
initial step  ->  next step  ->  current step
                                    center
```

Around an individual step, the vertical axis expresses semantic provenance:

- Information about what comes from outside, what happened, what the state is, and what the system knows or reports develops above the step.
- Information about what is created here, what the user does, chooses, intends, or wants develops below the step.

Everything is ultimately rendered by USERCOOP. The distinction is therefore not who physically drew the text or control, but what the information is about: incoming condition and known state above; local intention and agency below.

```text
        incoming events and known state
                       ^
                 current step
                       v
          user intention and local action
```

Several peer items belonging to the same enumeration are arranged vertically as a list. Their shared horizontal alignment, the fact that they occupy the same column or step of the line schema, carries the semantic of list membership. Vertical placement enumerates the members; it does not by itself define their relationship.

Each list member may develop independently toward the right:

```text
item A  ->  development  ->  development
item B  ->  development
item C  ->  development  ->  development  ->  development
```

Consequently, vertical enumeration does not conflict with the above-and-below provenance rule. List membership is established by common horizontal alignment and grouping, while provenance is established by attachment above or below a particular step or item.

### 16.5 Overview and ongoing activities

Stepping back from the current composition produces an overview. The camera withdraws far enough to reveal more of the developed structure and the relationships among its parts. This is a change of granularity and framing, not a departure from the current activity. The activity may remain current while the user views it from farther away.

This gives overview a literal spatial meaning. Detail is approached; context is recovered by stepping back. USERCOOP need not replace the current information with an unrelated summary screen when the existing spatial development can itself be shown at a broader scale.

Withdrawing for overview must remain distinct from leaving an activity. An overview preserves the activity and its developed structure. Leaving completes, abandons, or returns from that activity and may cause its temporary structure to retract.

An activity that is paused so the user can engage in another activity also remains developed. The paused and current activities become peer members of an `ongoing stuff` list, which is the literal name of that list in USERCOOP's own vocabulary. Each member is a complete line schema with its own left-to-right development. The line schemas are placed one below another and aligned on their left starting points, so their shared horizontal origin identifies them as members of the same list.

```text
ongoing activity A:  start  ->  step  ->  paused current state
ongoing activity B:  start  ->  step  ->  active current state
```

Beginning or switching to the second activity does not erase or retract the first. Its developed line remains available as resumable context. Resuming it moves attention and the camera back to its existing current point rather than reconstructing it as a new activity.

The vertical ordering of ongoing activities does not imply that one follows another as a process. Their individual horizontal lines carry development through time; their common left alignment and vertical enumeration express that they are peers in the same set of ongoing work.

### 16.6 Camera language

Camera movement is the primary intuitive channel through which USERCOOP communicates changes in activity context. Layout and camera are composed together: relevant information develops into an appropriate position, and the camera moves so that the current context is correctly presented in front of the user.

Provisional composition happens where the camera already is. While the user types an unfinished entry, information may appear, recede, reorder, or receive emphasis around the current place. Local rotation, approach, withdrawal, or reframing may clarify the parser's developing understanding, but provisional interpretation does not pretend that the user has entered another activity location.

A committed activity transition is different: the camera literally travels to another place in the spatial composition. Entering a deeper activity develops a destination and moves the camera to it. Completing or leaving that activity retracts its temporary development while the camera returns toward the surviving parent context. Pausing an activity and switching to another moves the camera between their developed line schemas without retracting either one.

Translation and rotation need not wait for one another. Information may appear or disappear faster than the camera can travel to the newly appropriate point of view. In that case the camera first turns its gaze toward the new point of interest while translation is still underway, as a person turns their head toward something before or while walking into a better position from which to inspect it. The user can therefore see the relevant subject immediately while the slower movement of viewpoint preserves spatial continuity.

Rotation also permits a contextual glance without leaving the current place. The camera may turn toward a distant but related part of the developed wall (a previous step of the same activity, or the parent activity within which the current sub-activity exists). This changes what the user is looking at without changing which activity is current, retracting anything, or committing a transition. When the glance ends, the camera may return its gaze to the current point of work.

Three roles make rotation an expression of attention rather than travel:

- **Anticipatory gaze:** turn toward a new point of interest before or during translation to its new point of view.
- **Contextual glance:** look toward related context from the current position without leaving or changing the current activity.
- **Settled orientation:** align the final gaze with the composition once translation and reorganization have settled.

Rotation and translation begin together. Both use eased acceleration and deceleration, or an equivalent interpolation, so that neither snaps into motion. They differ primarily in how quickly they settle. As an initial motion envelope, the camera may lock its gaze on the target roughly `0.25` to `0.5` seconds after movement begins, while translation reaches the new position roughly `1` to `2` seconds after the same start. Rotation therefore feels like turning the head while translation feels like walking. The gaze leads; the viewpoint follows.

These timings are rough perceptual targets rather than fixed constants. Exact speed, acceleration, and duration remain subject to distance, urgency, readability, the sport-to-zen pace, and reduced-motion settings. The recognizable relationship matters more than the numbers: turning and walking begin together, gaze settles first, and position follows.

The difference should be only as visible as necessary to make the motion feel coherent. Someone who knows to observe the head-turn and walk relationship should be able to see it; someone who does not should simply experience one calm, natural camera movement.

Camera motions therefore form a restrained vocabulary:

| Motion | Meaning |
|---|---|
| Local adjustment | Changing attention within the present activity |
| Rotation alone | Redirected gaze without changing viewpoint or activity |
| Sustained travel | Entry into another activity context |
| Withdrawal without retraction | Overview |
| Withdrawal with retraction | Completion, exit, or return to a parent context |
| Travel between preserved line schemas | Switching among ongoing activities |
| Reframing | Reorganization of the current context |
| Combined rotation and translation | Attention arriving before the camera reaches its final point of view |

Movement is not decorative animation added after layout. It preserves continuity and lets the user perceive how the current context grew from the previous one, where attention has moved, and when a temporary branch has ceased to exist.

**Every camera motion in this vocabulary has a non-spatial equivalent.** See section 18.3.

## 17. Motion, reactivity, and stability

The interface operates at two temporal regimes.

### 17.1 Foreground reactivity

The active composition context responds immediately to meaningful parser changes. Valid continuations, resolved referents, information spaces, highlights, and spatial focus may all change during typing, within the targets of section 10.5. These provisional changes occur locally within the current activity place.

This rapid movement is feedback, not instability. It externalizes the parser's developing understanding and produces the intended sense of a screen living alongside the user.

### 17.2 Background hysteresis

Information unrelated to the active composition changes conservatively.

- Small score differences do not reorder information spaces.
- Ambient information does not repeatedly gain and lose space near a threshold.
- A current arrangement persists until a competitor wins decisively.
- Minimum display lifetimes prevent unreadable flashes.
- Recently displaced information may retain a short return advantage.

Hysteresis stabilizes the background without slowing the foreground.

### 17.3 Returning to equilibrium

Explicit requests and urgent contexts may temporarily force greater detail or occupancy than the user normally prefers. When the activity completes or the pressure ends, the display settles toward the standing preference rather than snapping through every intermediate arrangement.

## 18. Accessibility

Accessibility is specified here as a first-class part of the interaction model, because several of USERCOOP's most distinctive mechanisms (letter-by-letter reveal, case as feedback, camera motion, very small technical text, a 3D scene carrying 2D controls) are exactly the mechanisms that exclude people when they are designed carelessly.

Accessibility requirements bound every other presentation rule, as stated in principle 13 and in the precedence of section 14.4.

### 18.1 Complete input paths

Keyboard interaction is the intended primary mode where a keyboard is present. Full mouse-only and touch-only operation are standing requirements, not reduced substitutes.

Every semantic action available through the command language must have an accessible direct-manipulation path. Spatial views support ordinary pointing, dragging, panning, and zooming where appropriate. Keyboard focus is always visible when keyboard navigation is active, and focus order follows the spatial grammar: along a line schema left to right, then above and below each step.

### 18.2 Legibility floors

These are hard minimums, not preferences.

| Property | Requirement |
|---|---|
| Body text contrast | At least 4.5:1 against its background, in both themes |
| Large and very small monospace contrast | At least 4.5:1, with no exemption for the very small scale |
| Non-text state indication | At least 3:1, and never the only channel carrying meaning |
| Minimum rendered text size | No text is rendered below the platform's minimum readable size after camera projection |
| User text scaling | Honored up to at least 200 percent, with the display budget recomputed rather than the text clipped |

Camera distance reduces what an item says, never how legibly it says it. When projection would push a representation below the minimum size, the item changes representation or leaves the composition. It never shrinks below the floor.

The guidance to reserve strong contrast for meaningful state changes governs color relationships among quiet elements. It never licenses text below these floors.

### 18.3 Motion, timing, and their equivalents

A reduced-motion setting changes presentation without changing semantics:

| Mechanism | Reduced-motion equivalent |
|---|---|
| Letter-by-letter reveal | Text appears complete, with a brief single fade or no transition |
| Camera travel between activity contexts | Cut, with a persistent textual indication of the activity entered or left |
| Anticipatory gaze and contextual glance | The related context is presented in place, labeled as context |
| Overview withdrawal | Representation change to overview without camera movement |
| Provisional panning during composition | Emphasis change only, no movement |

No essential information is conveyed by movement alone. Every motion in the camera vocabulary of section 16.6 has a meaning, and every one of those meanings is also expressed by a change the user can read.

Nothing essential is conveyed only by timing. No interaction depends on responding within an interval, and any duration-bound criticality window is stated rather than merely felt.

### 18.4 Assistive technology

The composition is a semantic model before it is a picture, which is the property that makes this tractable: an accessibility tree can be generated from information items rather than reverse-engineered from a scene.

- Every information space exposes its semantic type, identity, content, provenance, and available actions to the platform accessibility layer.
- Authorship, which is carried spatially for sighted users, is exposed explicitly as a property, so that user-authored and system-generated items remain distinguishable without spatial perception.
- Parser feedback carried by case or weight is also exposed as a state, so that a recognized variable and an unrecognized sequence are reported as such.
- Failure events are announced as events associated with their line, not as silent visual changes.
- Text is exposed complete from the moment the item exists, never progressively.

Every projected space remains a native 2D `Control` and participates in an explicit logical accessibility order derived from the semantic composition rather than from screen coordinates. Platform accessibility support is an acceptance criterion for each target build. A target is not released until automated tree assertions and assistive-technology tests confirm that spaces, states, authorship, actions, and reading order are exposed correctly.

### 18.5 Capacity

Cognitive and perceptual accessibility settings may reduce the maximum number of simultaneous spaces, force overview representations, or disable adaptive pace. These reductions apply to the display budget of section 15.8 and therefore bound rule 4 of the precedence order: simultaneous importance may increase occupancy only up to the capacity the user's settings allow. Above that, USERCOOP enumerates rather than expands.

## 19. Visual direction

The interface is quiet, calm, and restrained at rest. It should feel like a clear space for thought rather than a spectacle competing for attention.

- Simple forms, generous spacing, and highly legible typography.
- Soft, neutral colors, with saturated or high-contrast treatments reserved for meaningful state changes, always within the contrast floors of section 18.2.
- Gentle motion when preserving continuity, directing attention, or confirming action.
- Rapid motion is permitted when directly caused by active command composition.
- Visual hierarchy comes from the interaction model itself.
- No decorative element without a functional purpose.

Calmness is an equilibrium, not immobility. A normally sparse interface may become temporarily dense and animated when the user's activity genuinely demands it.

---

# Part V. Implementation

## 20. System boundary

USERCOOP is one coherent Godot application with internal boundaries between meaning, time, device authority, and presentation.

### 20.1 Semantic kernel

The semantic kernel owns identities, values, relationships, facts, rules, procedures, queries, provenance, derivations, contradiction, and history. It also owns deterministic parsing and contextual vocabulary.

The kernel produces semantic state and ordered events. It does not decide coordinates, font sizes, camera paths, or animation.

### 20.2 Session and inference runtime

The runtime owns the current session, activity stack, ongoing work, command history, temporal events, and inference processes. It advances these perdurants without blocking the application.

This is where knowledge meets lived time: what is active, paused, completed, interrupted, or becoming relevant now.

### 20.3 Device adapters

Device adapters give USERCOOP bounded access to the device it inhabits. They may observe files, processes, settings, notifications, hardware state, and operating-system events, within the capability scopes of section 7. They translate those observations into knowledge and expose authorized local actions.

Adapters provide facts and actions, not alternative interfaces. They do not control USERCOOP's vocabulary, activities, typography, spaces, or camera.

Adapters are in-process modules of the single Godot application, not separate processes. They are therefore inside the offline boundary of section 6.1 and are covered by its enforcement and tests. Local IPC, where it is needed, connects USERCOOP to facilities that already belong to the operating system or to other installed applications; it is not the mechanism by which USERCOOP's own adapters talk to their host.

There is no out-of-process or dynamically downloaded adapter model. An adapter becomes part of USERCOOP only by being reviewed, compiled into the application, and subjected to the same offline and capability tests as the rest of the release. Other installed programs remain external applications reached through explicit handoff or bounded local IPC; they do not become trusted adapters.

### 20.4 Applications and command execution

USERCOOP can know about and operate applications as objects on the device. It may launch, focus, or stop an application and, where the operating system permits it, invoke one with explicit arguments or a local platform hook. Arbitrary command execution follows the stricter rules of section 7.3.

### 20.5 Godot application boundary

Godot is the chosen application environment, not a temporary renderer for a generic host. Its update loop, input system, 2D controls, 3D world, camera, animation, and temporal behavior are part of USERCOOP.

The semantic kernel remains separate from Godot presentation objects for clarity and testing. That separation exists so the kernel can be tested without a running scene, not as a promise to reproduce USERCOOP in unrelated rendering technologies.

## 21. Personal-device targets

Computers, smartphones, and tablets are natural targets. The knowledge model and session concept remain coherent across them; device capabilities and input methods differ.

Smartphones and tablets deserve particular emphasis:

- They are personal devices carried through daily life, making the session a natural point of contact with lived time.
- Their conventional systems already expose activities, notifications, intents, permissions, sensors, and local hooks.
- Limited screen area increases the value of automatic composition, short lines, semantic reduction, and overview through camera distance.
- Application sandboxes make capability boundaries explicit.

USERCOOP remains offline on every target. A cellular or Wi-Fi connection does not grant it external network access, and platform integration remains local to the same physical device.

Keyboard interaction remains central when a physical keyboard is present. Touch and the on-screen keyboard are complete interaction paths. Large monospaced input is especially valuable for users who simply want to type letters and see that the device is listening.

Android is the first mobile implementation target; iOS follows through the same semantic and presentation architecture. The project uses the mobile export support of the selected Godot .NET release and native Godot platform plugins where operating-system bridges require them. A phone build is established at the beginning of implementation, so mobile remains an architectural constraint rather than a later port. Web export is not a target.

## 22. Building it

The first implementation is a Godot 4.7 .NET application. It should grow through working software rather than speculative framework building.

### 22.1 Initial application structure

The root scene uses a plain `Node` because USERCOOP is neither fundamentally 2D nor 3D:

```text
Usercoop                         Node
|-- Knowledge                    Node
|-- Session                      Node
|-- Inference                    Node
|-- SpatialWorld                 Node3D
|   |-- CameraRig                Node3D
|   |   `-- Camera               Camera3D
|   `-- Environment              WorldEnvironment
`-- Interface                    CanvasLayer
    `-- Spaces                   Control
```

The root coordinates lifecycle. Knowledge, session, and inference are sibling runtime services. SpatialWorld and Interface are sibling presentations of their state.

### 22.2 Semantic data is not the scene tree

The scene tree represents the running application, not every fact in the knowledge base. Facts, entities, relationships, deductions, productions, and derivations are ordinary semantic data rather than one Godot node per item.

The semantic kernel begins with plain C# types carrying stable identities and explicit value semantics. Likely primitives:

```text
EntityId
KnowledgeValue
Fact
Relation
Deduction
Production
Query
Derivation
Provenance
KnowledgeEvent
```

Godot nodes own services and connect them to the engine. Godot resources may hold authored vocabulary, schemas, themes, and test data, but they do not define the runtime knowledge model.

### 22.3 Knowledge language

The grammar is a user-modifiable part of the knowledge system. It maps entries to facts, requests, deductions, productions, and other semantic objects through deterministic matching and rewriting. The implementation is informed by string-rewriting systems and rule languages such as AIML, RiveScript, and ChatScript. Deductions support both forward and backward chaining; productions connect conditions and events to intentional action.

Datalog is the closest formal model for the inference beneath the customizable surface grammar. USERCOOP ships with a terse, sequential grammar that is easy to teach, but that grammar is a starting point rather than a permanent system syntax. A user may make it smaller, extend it, or replace its vocabulary and constructions without reducing the inference capabilities beneath it.

LPS (Logic-based Production System), developed by Robert Kowalski and Fariba Sadri, is another relevant reference. Its combination of logic programs, reactive rules, events, actions, changing state, and intentional behavior is especially pertinent to USERCOOP's temporal inference and bounded initiative.

The supplied grammar favors building complex knowledge from many clear steps rather than hiding it inside elaborate expressions. Whatever grammar is active is used to operate the system, teach it, inspect it, and revise its artifacts, including the grammar itself.

### 22.4 Reasoning capabilities

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

### 22.5 Incremental inference

Inference develops over time. It must not freeze the application while privately calculating a finished answer.

The inference scheduler advances a bounded number of deterministic logical operations, emits ordered events, and yields. The application continues to render, accept input, reveal text, move the camera, and present partial results.

```text
question or event
    -> match facts
    -> activate rules
    -> open and reject branches
    -> derive knowledge
    -> stabilize results
```

The complete inference trace is semantic data. Presentation may show a rapid selection of genuine steps in very small monospaced text. This visible machinery is never fabricated activity. When brought into focus, the trace receives an ordinary readable representation.

Logical progress and visual cadence remain separate. The initial work budget is measured in logical operations rather than frame duration, so frame rate cannot change semantic results. Worker threads may come later if measurements justify them; cooperative scheduling is the simpler starting point.

Provisional results remain distinct from settled knowledge. Cancellation, inspection, and continued interaction are normal parts of an inference process.

### 22.6 Persistence, portability, and recovery

Knowledge, rules, provenance, sessions, and histories persist locally. Storage must be versioned, recoverable, and able to represent changes without discarding their origin.

SQLite is the expected durable store. It provides local transactions, indexes, scale, and inspection without introducing a server or network dependency. Persistence remains behind a small interface so the semantic model does not become a database schema by accident.

Some knowledge artifacts should also be browsable from an IDE. Rules, definitions, and interaction-created material may have readable source representations beside the database. The user normally changes them through USERCOOP's own language, in an interaction closer to an `ed` session than to hand-editing source files.

The database and readable artifacts serve different purposes: reliable indexed state on one side, inspectable and versionable expressions of knowledge on the other. USERCOOP remains the authority that keeps them coherent.

**Moving between devices.** A person with a laptop and a phone will want their knowledge in both places, and USERCOOP cannot synchronize over a network. The design therefore treats portability as a file problem, not a service problem:

- A complete export is a single local file containing knowledge, rules, provenance, capability grants, history, and the entry counter.
- Export and import are ordinary authorized local actions. Moving the file between devices is the user's business and happens outside USERCOOP, by whatever means they already use.
- Import is explicit and inspectable. It reports what it will add, what conflicts with existing knowledge, and what it will not carry over. Capability grants never transfer silently, because a grant refers to a scope on one particular device.
- Restoring from an export follows the entry-counter rule of section 12.4.

Diverged installations are merged explicitly, never by silent synchronization. When a common ancestry exists, import performs a three-way semantic comparison using stable identities and provenance. Compatible additions are proposed together; contradictory facts, rule changes, deletions, and competing names become conflict information items for the user to resolve. Without common ancestry, the imported material first enters as a named knowledge source and remains distinct until the user accepts particular additions or reconciliations. Capability grants never merge or transfer between devices.

### 22.7 Testing

The distinctive claims of this design are testable, and the ones that are not tested will not survive contact with a real implementation.

| Claim | How it is tested |
|---|---|
| Never guess | Property tests over generated entries: every entry resolves to one reading, enters clarification with every remaining valid reading exposed, or produces a failure event when no reading exists. No entry silently commits a second-choice interpretation. |
| Offline by construction | Build-time static analysis plus the runtime observation test of section 6.3. |
| Deterministic parsing | Golden tests generated from the grammar currently under test, including multiline entries, contextual patterns, synonyms where defined, precedence cases, and reserved-word collisions. |
| Frame rate cannot change results | The same inference run at different operation budgets and frame rates produces identical derivations in the same order. |
| Response targets | Measured per keystroke on each device class, reported as a distribution rather than an average. |
| Accessibility floors | Automated contrast and minimum-size checks over rendered compositions, plus accessibility-tree assertions for every space type. |
| Composition stability | Replay of recorded entry streams, asserting that background spaces do not oscillate and that minimum display lifetimes hold. |
| Capability enforcement | Every capability class has a test that an ungranted action fails, is reported, and does not partially execute. |

### 22.8 Initial implementation direction

The first working path is deliberately narrow:

1. Establish the root services and the 2D and 3D rendering layers.
2. Render the current typed-entry information item with the intended typography and multiline submission behavior.
3. Build and run steps 1 and 2 on one Android phone before the stack is entrenched.
4. Add deterministic token recognition and the case or weight feedback channel.
5. Introduce minimal knowledge identities, facts, and events.
6. Represent the current session and one developing activity.
7. Advance a small inference process incrementally and show its genuine trace.
8. Project an invisible 3D information rectangle into a native 2D control.
9. Put the offline enforcement test and the accessibility floor checks into the build, before there is much to fix.
10. Add one bounded local device domain, such as files, after the semantic path works end to end.

The aim is not to imitate a desktop or complete an expert-system framework before anything is visible. It is to establish one honest path from user letters, through semantic recognition and inference, into knowledge, space, motion, and persistent session history.

---

# Part VI. Glossary and references

## 23. Glossary

| Term | Meaning |
|---|---|
| Activity | A temporary semantic environment with its own vocabulary, information, and exits |
| Capability | An authorized, scoped ability to observe or act on the device |
| Criticality | The probability that a closing window will pass before the user returns to the relevant context |
| Display budget | The maximum number of simultaneous spaces, computed from device area and accessibility settings |
| Effective importance | Intrinsic importance multiplied by the criticality factor, clamped to one |
| Entry | The multiline unit of user submission, terminated by an empty line and assigned one permanent history number |
| Failure event | A semantic event generated when something does not resolve, is not permitted, or does not succeed |
| Information item | A contextual representation of knowledge, with type, content, provenance, and available actions |
| Interaction cadence | The user's present typing and progression speed, used only to place presentation on the sport-to-zen scale |
| Knowledge item | A durable fact, rule, entity, or relation in the knowledge base |
| Line schema | The spatial form of one perdurant: a horizontal line of steps with information above and below |
| `ongoing stuff` | The literal name of the list whose members are the currently developed activities |
| Perdurant | Something that extends and develops through time, such as a session or an activity |
| Space | The visual presence USERCOOP gives to one or more information items |
| Task distance | Normalized distance from the current focus, derived from the activity stack and entry stream |

## 24. References and prior art

| Reference | Used for |
|---|---|
| Furnas, *Generalized Fisheye Views* (1986) | Degree of interest, and logical rather than physical distance |
| Smith's rule, weighted shortest processing time | Ordering action by value per handling time |
| Horvitz, Jacobs, and Hovel, *Attention-Sensitive Alerting* (UAI 1999) | Weighing the cost of interrupting now against the cost of deferring |
| Allen's interval algebra | Temporal relations among events, states, and intervals |
| Kowalski and Sadri, LPS (Logic-based Production System) | Reactive rules, events, actions, and intentional behavior over changing state |
| Datalog | The closest formal model for the knowledge language |
| AIML, RiveScript, ChatScript | Deterministic pattern matching and rewriting over short natural-language forms |
| SHRDLU | Deterministic resolution against a small, closed, well-defined world |
| REXX | The principle of least astonishment in command syntax |
| Pearl on intervention and causation | Causal models in the reasoning core |
| *Tron* (1982), *WarGames* (1983) | The directness of the keyboard scenes that inform the input model |
