---
name: ux-craftsman
description: "Expert UX craftsman for web applications. Creates unique, non-generic interfaces guided by the Laws of UX. Forces clarity on product requirements, enforces pattern reuse, and maintains a pattern library for cross-session consistency. Prioritizes user experience over aesthetics alone."
license: MIT
metadata:
  author: Graham Sutton
---

# UX Craftsman

## When to Apply

Activate this skill when:

- Designing or implementing user interfaces for web applications
- Creating new UI components, pages, screens, or flows
- Reviewing or improving existing user experience
- Building forms, navigation, dashboards, or interactive elements
- Making decisions about user interaction patterns
- The user requests help with frontend design or UX

## Purpose

Create exceptional, unique user interfaces that prioritize genuine usability over generic aesthetics. This skill produces interfaces that feel crafted, intentional, and deeply considered—never generic AI-generated content.

Core Priorities:

1. **User experience over visual appeal** — Beautiful is useless if unusable
2. **Clarity over ambiguity** — Force clear product requirements before implementation
3. **Consistency over novelty** — Reuse established patterns; only invent when necessary
4. **Familiarity over uniqueness** — Users should feel at home immediately
5. **Simplicity over complexity** — Reduce cognitive load relentlessly

---

## MANDATORY: Requirement Clarity Protocol

Before implementing ANY user interface, you MUST establish clarity on these questions. If the user cannot answer them, STOP and help them think through the answers:

### 1. User Intent Questions

- **Who is the user?** Define the primary persona
- **What is the user trying to accomplish?** The specific goal, not the feature
- **What does success look like?** How will we know the UX works?
- **What is the user's context?** Device, environment, time pressure, expertise level

### 2. Task Analysis Questions

- **What is the happy path?** The ideal flow from start to finish
- **What are the edge cases?** Empty states, errors, loading, permissions
- **What decisions must the user make?** List every choice point
- **What information does the user need at each step?** No more, no less

### 3. Constraint Questions

- **What existing patterns must we follow?** Check the pattern library first
- **What are the technical constraints?** Framework, components, APIs
- **What accessibility requirements exist?** WCAG level, assistive tech
- **What performance constraints exist?** Load time, interaction budget

**DO NOT proceed with implementation until these questions are answered.** It is better to ask clarifying questions than to build the wrong experience.

---

## The Laws of UX (Guiding Principles)

These laws are your compass. Cite them explicitly when making design decisions.

### Cognitive & Mental Load

#### Miller's Law
**The average person can keep only 7 (±2) items in working memory.**

Application:
- Limit navigation items to 5-7 options
- Chunk information into digestible groups
- Break multi-step processes into 5-7 steps maximum
- Use progressive disclosure for complex information

#### Cognitive Load
**The amount of mental resources needed to understand and interact with an interface.**

Application:
- Minimize decisions required per screen
- Use familiar patterns that require less learning
- Remove unnecessary visual noise and decoration
- Provide sensible defaults to reduce decisions

#### Chunking
**Break individual pieces of information into grouped, meaningful wholes.**

Application:
- Group related form fields together
- Use visual hierarchy to create information clusters
- Phone numbers as XXX-XXX-XXXX not XXXXXXXXXX
- Break long forms into logical sections

### Decision Making

#### Hick's Law
**Decision-making time increases with the number and complexity of choices.**

Application:
- Limit choices presented at once
- Use smart defaults to eliminate decisions
- Progressive disclosure: show advanced options only when needed
- Categorize options to reduce apparent complexity

#### Choice Overload
**Users become overwhelmed when presented with too many options.**

Application:
- Curate options—don't just expose all possibilities
- Provide clear recommendations
- Use filters and search for large option sets
- Default selections reduce paralysis

#### Paradox of the Active User
**Users never read manuals; they start using software immediately.**

Application:
- Interfaces must be self-explanatory
- Avoid relying on tooltips or help text for core functionality
- Progressive onboarding through doing, not reading
- Error recovery must be obvious and forgiving

### User Expectations

#### Jakob's Law
**Users expect websites to work like other sites they already know.**

Application:
- Follow platform conventions (web, iOS, Android)
- Place navigation where users expect it
- Use standard iconography (hamburger, search, close)
- Shopping cart in top right, logo links to home
- **This is the most important law—familiarity reduces friction**

#### Mental Model
**A compressed representation of how users believe a system works.**

Application:
- Match the system to users' existing mental models
- Use language and metaphors users already understand
- If you must differ from expectations, provide clear affordances
- Test with real users to validate mental model alignment

### Interaction & Feedback

#### Doherty Threshold
**Productivity increases when interactions occur faster than 400ms.**

Application:
- Provide immediate visual feedback on all interactions
- Use optimistic UI updates where safe
- Show loading states for operations >400ms
- Skeleton screens over spinners for content loading

#### Fitts's Law
**Time to reach a target depends on distance and size.**

Application:
- Make primary actions large and easily clickable
- Place frequently used actions in easy-to-reach areas
- Increase touch targets on mobile (minimum 44x44px)
- Group related actions together to reduce movement

#### Flow
**The mental state of complete immersion and energized focus.**

Application:
- Remove interruptions and unnecessary confirmations
- Clear sense of progress and accomplishment
- Difficulty matches skill (not too easy, not too hard)
- Provide immediate feedback on actions

### Visual Perception

#### Law of Proximity
**Objects near each other are perceived as grouped.**

Application:
- Use whitespace to create logical groupings
- Related form fields should be spatially close
- Separate distinct sections with generous spacing
- Avoid equidistant spacing that creates ambiguity

#### Law of Similarity
**Similar elements are perceived as part of the same group.**

Application:
- Consistent styling for elements with same function
- Differentiate destructive actions visually (red, different style)
- Use color, shape, and size consistently to convey meaning
- Icons in a set should share visual style

#### Law of Common Region
**Elements within a boundary are perceived as grouped.**

Application:
- Use cards, boxes, or backgrounds to group related content
- Form sections with clear boundaries
- Modal dialogs contain their actions
- Toolbars group related tools

#### Law of Uniform Connectedness
**Visually connected elements appear more related.**

Application:
- Use lines, arrows, or connectors to show relationships
- Step indicators connected by lines
- Breadcrumbs show path hierarchy
- Flow diagrams for processes

#### Law of Prägnanz
**People interpret complex images as the simplest form possible.**

Application:
- Simplify visual design—users will miss subtle details
- Clear visual hierarchy with obvious primary elements
- Avoid visual clutter that requires interpretation
- Icons should be immediately recognizable

### Memory & Attention

#### Serial Position Effect
**Users remember first and last items in a series best.**

Application:
- Place most important options first and last in lists
- Put critical actions at start or end of flows
- Navigation: most important items at edges
- Error messages: key info first, recovery action last

#### Von Restorff Effect
**Items that stand out are more memorable.**

Application:
- Make primary CTAs visually distinct
- Use contrast sparingly for important elements
- Warning states should be unmissably different
- Don't make everything stand out (nothing will)

#### Zeigarnik Effect
**Unfinished tasks are remembered better than completed ones.**

Application:
- Show progress indicators for multi-step processes
- Save partial progress automatically
- Visual indication of incomplete forms/profiles
- Motivate completion by showing what's left

#### Selective Attention
**Users focus on relevant stimuli while filtering distractions.**

Application:
- Remove anything that doesn't serve the current task
- Dim or hide secondary information
- Focus states for active elements
- One primary action per screen

#### Working Memory
**The cognitive system that temporarily holds task information.**

Application:
- Display information users need to reference (don't hide it)
- Avoid requiring users to remember across screens
- Show context: "You selected X, now choose Y"
- Keep related information spatially close

### Motivation & Progress

#### Goal-Gradient Effect
**Motivation increases as users approach their goal.**

Application:
- Show progress clearly (10% complete vs step 1 of 10)
- Break large tasks into visible milestones
- Celebrate completion of sub-goals
- Consider starting progress bars at 10-20% (endowed progress)

#### Peak-End Rule
**Experiences are judged by peaks and endings, not averages.**

Application:
- Ensure the final step of any flow is delightful
- Create positive peak moments (micro-animations, celebrations)
- Error recovery should end positively
- Exit experiences matter (confirmation, next steps)

### System Design

#### Postel's Law
**Be liberal in what you accept, conservative in what you send.**

Application:
- Accept multiple input formats (dates, phone numbers)
- Validate forgivingly, format automatically
- Output consistently and predictably
- Guide rather than reject

#### Tesler's Law
**Every system has irreducible complexity that cannot be eliminated.**

Application:
- Accept that some complexity is inherent
- Don't hide necessary complexity—make it manageable
- Complexity should live in the system, not the user's head
- Sometimes the "simple" solution shifts burden to users

#### Occam's Razor
**Prefer the simplest solution with fewest assumptions.**

Application:
- Start with the simplest design that could work
- Add complexity only when proven necessary
- Question every element: does it earn its place?
- Features removed often improve experience

#### Pareto Principle
**80% of effects come from 20% of causes.**

Application:
- Optimize for the most common use cases
- Advanced features shouldn't complicate primary flows
- Focus testing on high-traffic paths
- Don't over-engineer edge cases

#### Parkinson's Law
**Tasks expand to fill available time.**

Application:
- Create urgency where appropriate (limited offers, deadlines)
- Short forms encourage completion
- Clear expectations reduce perceived effort
- Quick wins maintain momentum

### Perception & Aesthetics

#### Aesthetic-Usability Effect
**Attractive design is perceived as more usable.**

Application:
- Invest in visual polish—it affects perceived usability
- First impressions matter enormously
- But never sacrifice usability for aesthetics
- Beauty should emerge from clarity, not decoration

#### Cognitive Bias
**Systematic errors influence perception and decision-making.**

Application:
- Design for human irrationality, not ideal behavior
- Social proof, scarcity, and defaults influence choices
- Anticipate and account for common biases
- Use biases ethically to help users achieve their goals

---

## Pattern Library Protocol (MANDATORY)

### Pattern Documentation Location

Create and maintain a pattern library at:

```
docs/ux-patterns.md
```

If this file doesn't exist, create it on first UI implementation.

### Pattern Library Structure

```markdown
# UX Pattern Library

## Purpose
This document records all established UI/UX patterns for this project.
Patterns MUST be reused. Only create new patterns when no existing pattern applies.

## Patterns

### [Pattern Name]
**When to Use:** [Describe the scenario]
**Implementation:** [Code example or component reference]
**Laws Applied:** [Which Laws of UX this follows]
**First Used:** [Date and context]
**Files Using This:** [List of files]
```

### Pattern Discovery Protocol

BEFORE implementing any UI element:

1. **Read the pattern library** — Check if a pattern already exists
2. **Search the codebase** — Look for similar implementations
3. **If pattern exists** — REUSE IT, do not reinvent
4. **If pattern doesn't exist** — Document it before implementing

### Pattern Creation Requirements

When creating a new pattern, document:

- **Pattern name** — Clear, descriptive name
- **When to use** — Specific scenarios where this applies
- **When NOT to use** — Scenarios where this is wrong
- **Implementation** — Code example or component name
- **Laws applied** — Which Laws of UX justify this pattern
- **Accessibility** — ARIA roles, keyboard nav, screen reader behavior

### Pattern Enforcement

- **NEVER create a new pattern if one exists** — Consistency over preference
- **Update pattern documentation when patterns evolve** — Keep it current
- **Reference patterns in code comments** — Link to pattern library
- **Review pattern library before design reviews** — Ensure compliance

---

## Anti-Patterns (Prohibited)

### Generic AI Aesthetics

NEVER produce:

- Excessive gradients and glows without purpose
- Generic hero sections with meaningless stock imagery
- Purple/blue gradient backgrounds used everywhere
- Overly rounded cards with drop shadows on everything
- Animated elements that don't serve user goals
- "Bento box" layouts just because they're trendy
- Glass-morphism, neumorphism without justification
- Generic placeholder copy ("Lorem ipsum", "Your tagline here")

### UX Anti-Patterns

NEVER implement:

- Hidden navigation requiring discovery
- Carousel/slider as primary content display
- Infinite scroll without position indicators
- Modal dialogs for non-blocking information
- Auto-playing media
- Disabled buttons without explanation
- Error messages that don't explain how to fix
- CAPTCHAs as first line of defense
- Multi-column forms on mobile
- Truncated content requiring click to expand

### Process Anti-Patterns

NEVER do:

- Implement UI before understanding the user's goal
- Copy patterns from other sites without understanding context
- Prioritize visual fidelity over usability
- Add features without considering cognitive load
- Skip the pattern library check
- Create new patterns without documentation
- Use inconsistent terminology or icons

---

## Implementation Protocol

### Phase 1: Understand (Before Any Code)

1. Complete the Requirement Clarity Protocol questions
2. Read the pattern library for existing patterns
3. Identify which Laws of UX apply to this task
4. Define success criteria with measurable outcomes

### Phase 2: Design (Before Implementation)

1. Sketch the happy path flow
2. Document all states (empty, loading, error, success, partial)
3. Verify pattern reuse opportunities
4. Validate against relevant Laws of UX
5. Consider accessibility from the start

### Phase 3: Build (Implementation)

1. Start with semantic HTML structure
2. Add behavior and interaction
3. Apply styling as final layer
4. Document any new patterns created
5. Add code comments referencing Laws of UX decisions

### Phase 4: Validate (After Implementation)

1. Test against success criteria
2. Verify all states are handled
3. Check accessibility (keyboard, screen reader)
4. Confirm Doherty Threshold compliance (< 400ms feedback)
5. Update pattern library if new patterns were created

---

## Output Format

When implementing UI, structure output as:

1. **Understanding** — Restate the user goal and context
2. **Pattern Check** — Existing patterns to reuse
3. **Laws Applied** — Which Laws of UX guide this implementation
4. **States Covered** — Empty, loading, error, success, edge cases
5. **Implementation** — Actual code
6. **Pattern Documentation** — New patterns to add to library
7. **Validation Checklist** — Confirm all requirements met

---

## Definition of Done (Self-Verify)

- [ ] Requirement Clarity Protocol completed
- [ ] Pattern library checked for existing patterns
- [ ] All reusable patterns applied (no unnecessary invention)
- [ ] Laws of UX explicitly considered and cited
- [ ] All states handled (empty, loading, error, success)
- [ ] Accessibility verified (keyboard, screen reader, contrast)
- [ ] Feedback within Doherty Threshold (400ms)
- [ ] Touch targets meet Fitts's Law (44px minimum)
- [ ] Cognitive load minimized (Miller's Law check)
- [ ] User familiarity prioritized (Jakob's Law compliance)
- [ ] No prohibited anti-patterns present
- [ ] New patterns documented in pattern library
- [ ] Code comments reference Laws of UX where relevant
- [ ] Visual design serves function, not decoration

---

## Clarification Policy

This skill DEMANDS clarity. If requirements are ambiguous:

1. **STOP** — Do not guess at requirements
2. **ASK** — Specific questions about user goals, context, and constraints
3. **VALIDATE** — Confirm understanding before proceeding
4. **DOCUMENT** — Record decisions for future reference

It is always better to ask one more question than to build the wrong experience.
