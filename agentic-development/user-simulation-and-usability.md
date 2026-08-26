# Agentic End-User Simulation and Usability Standards

*Companion document in the Agentic Development Standards family*

This document defines end-user simulation, usability challenge, workflow discoverability, realistic misuse, and user-centered validation for agent-produced systems. It is authoritative for the detailed agentic rules in its scope.

These standards complement, but do not replace, the repository-wide [User Interface Standards](../ui-standards.md) and [Accessibility Standards](../accessibility.md).

## 1. Purpose

Functional correctness does not by itself establish that a product is usable, understandable, discoverable, or resilient to plausible human behavior.

For user-facing systems, an agentic workflow SHOULD consider validation from the perspective of a user who does not share the implementation team's assumptions, terminology, architecture knowledge, or expected interaction sequence.

An **End-User Simulation** or **Usability Challenge** role evaluates whether intended users can accomplish meaningful goals and whether plausible user behavior exposes defects, ambiguity, fragility, or unnecessary cognitive burden that ordinary implementation and deterministic testing may not reveal.

This role is not required for every change. Its use SHOULD be proportionate to the user impact, novelty, workflow complexity, consequence of error, and likelihood that implementation assumptions differ from actual user behavior.

## 2. Distinction from Other Validation Roles

End-user simulation is distinct from ordinary deterministic testing, code review, adversarial security testing, and independent challenge.

- **Testing / Validation** primarily asks whether defined behavior satisfies the specification and deterministic checks.
- **Reviewer** primarily asks whether the implementation is correct, maintainable, standards-compliant, and appropriately validated.
- **Adversarial Security Testing** asks whether the system can be exploited, abused, or made to violate trust boundaries within authorized scope.
- **Independent Challenge** asks whether the prevailing conclusion, framing, design choice, or shared assumption has a credible reason to be reconsidered.
- **End-User Simulation / Usability Challenge** asks whether a plausible user can understand and successfully use the system without relying on knowledge that exists only in the implementation team's mental model.

These responsibilities MAY overlap in findings, but one MUST NOT be treated automatically as satisfying another when the distinction is material to the risk being evaluated.

## 3. Goal-Oriented User Simulation

End-user simulation SHOULD begin from a user goal rather than a prescribed sequence of implementation-aware steps when workflow discoverability is being evaluated.

For example, prefer a task such as:

> You are a performer at a karaoke venue and want to request a particular song. Use the available application to accomplish that goal.

rather than:

> Open Venue, select Join, navigate to Search Catalog, locate the song, and choose Add to Rotation.

A test that supplies the exact intended workflow primarily validates instruction following. It does not establish that the workflow is discoverable by the intended user.

The simulation SHOULD receive enough context to represent the intended user accurately, but SHOULD NOT receive internal architecture, hidden implementation details, developer-only terminology, or prescribed interaction knowledge unless the real user would reasonably possess that information.

## 4. Plausible Human Behavior

End-user simulation SHOULD evaluate plausible behavior that may fall outside the ideal or expected path.

Relevant behaviors MAY include:

- Performing actions in an unexpected but reasonable order
- Attempting an action before completing a prerequisite
- Double-clicking or repeatedly activating an action when feedback is delayed
- Refreshing, navigating away, returning, or resuming after a delay
- Opening the same workflow in multiple tabs, windows, or devices when the product permits it
- Providing long, empty, malformed, differently cased, or otherwise unexpected but plausible input
- Using punctuation, international characters, whitespace, or values that developers may not have anticipated
- Losing connectivity, experiencing latency, or resuming after transient failure
- Misunderstanding domain terminology or labels
- Ignoring instructions that are visually secondary, unclear, or easy to miss
- Abandoning and later resuming partially completed work
- Repeating an operation because the interface does not clearly indicate progress or completion

The purpose is not to generate arbitrary chaos. Behavior SHOULD remain representative of plausible user actions, misunderstandings, environmental conditions, or interaction patterns relevant to the intended product.

Random fuzzing MAY complement this work, but arbitrary malformed-input generation alone does not satisfy end-user simulation.

## 5. Discoverability and Comprehension

A user-facing workflow SHOULD be evaluated for whether the intended user can reasonably determine:

- What can be done
- What information is required
- What action is expected next
- Whether an action succeeded, failed, or remains in progress
- What an error means and what the user can do about it
- Whether an operation can be retried safely
- Whether user-entered information will be preserved after a recoverable error
- Whether destructive or consequential actions are sufficiently clear
- Whether terminology reflects the user's domain rather than internal implementation language

A functionally available capability that intended users cannot reasonably discover or understand SHOULD be treated as a product-quality concern rather than dismissed solely because the underlying operation works when invoked correctly.

## 6. User Assumptions and Developer Knowledge

Agentic workflows MUST NOT assume that users possess knowledge merely because implementation, testing, or review agents possess it.

When successful use depends on undocumented implementation knowledge, hidden ordering assumptions, non-obvious terminology, or an interaction convention that the intended user is unlikely to understand, the workflow SHOULD identify the dependency as a usability or product-design concern.

An End-User Simulation role SHOULD distinguish between:

- documented or reasonably discoverable product behavior;
- domain knowledge expected of the intended user;
- training or onboarding explicitly required by the product;
- knowledge available only because the development team built the system.

The last category MUST NOT silently become a user requirement.

## 7. User Personas and Variation

Where materially useful, end-user simulation MAY use multiple bounded user perspectives such as:

- First-time or novice user
- Experienced returning user
- Infrequent user returning after a long absence
- Impatient user reacting to delayed feedback
- Mobile or constrained-device user
- User experiencing poor or intermittent connectivity
- User unfamiliar with internal terminology
- Keyboard-oriented or accessibility-relevant interaction patterns

Personas SHOULD represent meaningful differences in product interaction rather than decorative fictional biographies.

Accessibility-specific requirements remain governed by the [Accessibility Standards](../accessibility.md). End-user simulation MAY expose accessibility concerns but MUST NOT be treated as a substitute for required accessibility review or testing.

## 8. Findings and Evidence

A usability or end-user simulation finding SHOULD identify:

- User goal or scenario
- Relevant product state or environment
- Observed user path or attempted action
- Expected or reasonably inferred behavior
- Actual result
- User-facing consequence
- Reproducibility when applicable
- Suggested direction or question for resolution when useful

A finding SHOULD distinguish a material usability defect from personal preference.

For example, a failure to preserve entered data after a recoverable validation error may be a material defect. A preference for a different button color generally is not, absent an accessibility, consistency, discoverability, or other concrete engineering reason.

Findings SHOULD enter the durable finding and remediation lifecycle defined in [Task Lifecycle and Escalation](task-lifecycle-and-escalation.md) when their impact warrants tracking.

## 9. Relationship to Independent Challenge

Repeated difficulty observed during realistic user simulation MAY provide evidence that a development-team assumption should be challenged.

For example, if multiple plausible user simulations cannot discover a workflow that the implementation team considers intuitive, the [Independent Challenge](review-and-validation.md#5-independent-challenge) responsibility MAY examine whether the team's usability assumption remains justified.

End-user simulation itself SHOULD report observed behavior and consequences rather than invent disagreement solely to trigger redesign.

## 10. Pre-Production Use

For user-facing changes with material workflow, usability, safety, financial, privacy, or operational impact, pre-production review SHOULD consider whether realistic end-user simulation is warranted in addition to deterministic validation and ordinary review.

A successful result does not require discovering a defect. The purpose is to establish reasonable confidence that users can accomplish intended goals and that plausible deviations from the ideal path do not expose unacceptable behavior.

End-user simulation MUST NOT become an excuse for endless subjective redesign. Findings that recommend material redesign or refactoring SHOULD identify a concrete user-facing failure, risk, ambiguity, repeated friction, or product-quality consequence.

---

[Return to the Agentic Development Standards](../agentic-development.md)
