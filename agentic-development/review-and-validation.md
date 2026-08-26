# Agentic Review and Validation Standards

*Companion document in the Agentic Development Standards family*

This document defines independent review, deterministic verification, independent challenge, correlated-failure guardrails, pre-production challenge, validation evidence, and truthful reporting for agent-produced work. It is authoritative for the detailed rules in its scope.

## 1. Engineering Standards Remain Applicable

Agent-generated code and artifacts MUST satisfy the same applicable engineering standards as human-generated work.

Use of an agent MUST NOT be treated as evidence that a change has been reviewed, tested, secured, documented, challenged, or otherwise validated.

## 2. Deterministic Validation

When available and applicable, deterministic tooling SHOULD be used to execute validation such as:

- Builds and compiler diagnostics
- Unit tests
- Integration tests
- Static analysis
- Linters and format validation
- Schema and data-contract validation
- Database migration validation
- Security or dependency policy checks
- Packaging or deployment validation

An agent MAY interpret failures, design tests, identify missing coverage, or recommend additional validation. It MUST NOT replace required deterministic execution with a statement that the code appears correct.

Validation evidence MUST distinguish executed checks from checks that were unavailable, skipped, inferred, or merely recommended.

An agent MUST NOT fabricate, infer, or report successful test execution when the relevant command or tool did not actually complete successfully.

Required or materially applicable validation MUST NOT be omitted merely to reduce tokens, inference time, compute use, model cost, or elapsed workflow time. Resource optimization MAY change how validation is scheduled or scoped only when the resulting validation remains sufficient for the actual risk and applicable requirements.

## 3. Failure Reporting

Failed, incomplete, unavailable, flaky, or inconclusive validation MUST be reported accurately.

A task MUST NOT be represented as fully validated when required checks remain unresolved.

An agent attempting to correct a failure MUST NOT silently delete tests, weaken assertions, disable analyzers, suppress diagnostics, change acceptance criteria, or bypass policy solely to make validation pass.

Changes to validation rules or test expectations MAY be appropriate when the existing rule is incorrect, but such changes MUST be justified and reviewed as changes to the specification or control rather than disguised as implementation fixes.

## 4. Independent Review

Where independent review is required, the producing implementation execution MUST NOT treat its own review as satisfying that requirement.

A Reviewer SHOULD receive sufficient authoritative context to evaluate the change independently, including the applicable task and acceptance criteria, exact artifact or revision, applicable standards, validation evidence, and known material concerns.

A Reviewer SHOULD examine the relevant change, requirements, evidence, tests, risks, and applicable standards rather than merely summarize the implementer's explanation.

A Reviewer SHOULD NOT require the Implementation Agent's complete conversation or reasoning history when the authoritative task, change, evidence, and material rationale are sufficient for independent evaluation.

Implementation rationale SHOULD remain available when the rationale itself is a material design artifact, explains a non-obvious decision, records an accepted tradeoff, or is otherwise necessary to judge correctness.

Review findings SHOULD identify disposition clearly, such as accepted, rejected, changes required, questions requiring resolution, or risks requiring approval.

A reviewer MAY use agent-produced analysis, but independent review MUST preserve the reviewer's ability to disagree and form a separate judgment. Review independence MAY benefit from examining authoritative artifacts and evidence before receiving persuasive implementation narrative that is not necessary to understand the change.

## 5. Independent Challenge

For sufficiently consequential work, a workflow SHOULD consider an Independent Challenge responsibility that asks whether there is a credible evidence-based reason to reconsider the prevailing conclusion, problem framing, design choice, or shared assumption.

Independent Challenge differs from ordinary implementation review. Ordinary review primarily evaluates whether the selected solution was implemented correctly and conforms to requirements. Independent Challenge evaluates whether the selected solution or underlying interpretation is itself adequately justified.

The challenger MUST NOT be considered unsuccessful merely because no material defect or credible alternative is found. A valid challenge result MAY explicitly conclude that the prevailing conclusion remains the strongest available conclusion.

A challenge SHOULD:

- Identify the prevailing question or assumption being tested
- Examine relevant underlying evidence and authoritative constraints
- Identify a plausible alternative explanation, interpretation, or design only when one is materially supportable
- State the evidence supporting reconsideration
- Identify additional evidence or focused validation that could distinguish competing explanations when practical
- State a clear disposition

A challenge disposition SHOULD distinguish at least the following meanings, using project-defined terminology if desired:

- **Uphold** — the prevailing conclusion remains best supported by available evidence
- **Reconsider** — credible evidence or an alternative interpretation warrants further examination before relying on the prevailing conclusion
- **Insufficient Evidence** — available evidence does not support a confident conclusion

A challenger MUST NOT demand redesign, refactoring, or further work solely because another possible design, explanation, or abstraction can be imagined.

A challenger SHOULD explicitly uphold the prevailing conclusion when identified alternatives are materially weaker or unsupported.

Repeatedly reopening the same resolved question without materially new evidence SHOULD NOT occur. When repeated reopening becomes material, the workflow SHOULD require escalation or an explicit decision to resume investigation.

## 6. Challenge Independence and Anchoring

When independence materially affects confidence, an Independent Challenge execution SHOULD perform an initial analysis from the original problem, authoritative requirements, relevant raw or primary evidence, applicable constraints, architecture, and standards before being exposed to persuasive conclusions from prior agents where practical.

This requirement MUST NOT be used to conceal relevant facts, known failures, applicable decisions, safety constraints, or other information necessary for correct analysis.

The goal is controlled independence rather than artificial ignorance.

After the independent first-pass analysis is durably recorded, collaborative comparison and resolution MAY occur. The workflow MAY then compare the prevailing analysis, independent challenge, security findings, deterministic evidence, and other material records.

The same controlled-independence technique MAY be applied to ordinary review or security review when anchoring risk is material.

## 7. Correlated Failure, Consensus, and Minority Findings

Agreement among multiple agents MUST NOT automatically be treated as independent corroboration.

Agents may share correlated failure modes because they use the same model or model family, similar training, identical prompts, the same retrieved context, the same initial framing, another agent's conclusions, or shared architecture assumptions.

Where independent corroboration materially affects a decision, workflow design SHOULD consider diversity in one or more of:

- Model or provider
- Execution context
- Initial framing
- Evidence order
- Role instructions
- Analysis path

Different models or providers are not required in every case. Diversity is a means of reducing correlated failure, not an end in itself.

Findings and recommendations SHOULD be evaluated by evidence, reproducibility, authoritative requirements, risk, and technical merit rather than model size, role prestige, historical success, coordinator preference, or majority vote.

A materially supported minority finding SHOULD NOT be discarded merely because most agents disagree. Security-, safety-, compliance-, or correctness-relevant dissent capable of invalidating a shared assumption SHOULD be preserved and evaluated explicitly.

Consensus is evidence of agreement. It is not proof of correctness.

## 8. Risk-Proportionate Review and Challenge

Validation, review, security testing, and independent challenge depth SHOULD be proportionate to the impact, uncertainty, irreversibility, and failure modes of the change.

Additional independent challenge SHOULD be considered for work such as:

- High-impact architecture decisions
- Authentication, authorization, identity, or security-sensitive changes
- Destructive operations or difficult-to-reverse changes
- Database or data migrations with material failure consequences
- High financial, regulatory, privacy, or contractual impact
- Repeated unexplained failures
- Novel or poorly understood technology
- Broad consensus resting on weak or indirect evidence
- Decisions where several agents may share strongly correlated assumptions
- Major public API, schema, or external contract changes

Trivial documentation, routine mechanical changes, or low-risk implementation details MAY use lighter review when project policy permits it. Independent challenge MUST NOT become ceremonial work whose cost exceeds the risk it mitigates.

Choice of model, tool, or review mechanism MAY consider cost and throughput, but the selected mechanism MUST be capable enough for the assigned validation or review responsibility. A cheaper, smaller, or faster model MUST NOT be selected solely for economy when its demonstrated capability is insufficient for the required work.

## 9. Pre-Production Challenge

Higher-risk changes SHOULD have a defined pre-production decision boundary at which applicable evidence is assessed before release, deployment, or irreversible adoption.

The pre-production challenge MAY combine ordinary review, deterministic validation, adversarial security testing, independent challenge, architecture review, compliance review, or other controls appropriate to the risk. It does not require every logical role for every change.

The pre-production challenge SHOULD determine whether material issues remain such as:

- Unresolved correctness defects or failed required validation
- Credible security weaknesses or incompletely remediated security findings
- Important assumptions that have not received adequate independent examination
- Unresolved minority findings or dissent requiring disposition
- Unnecessary or harmful complexity with a concrete engineering consequence
- Architecture, coupling, or abstraction problems that create material maintainability or operational risk
- Unhandled failure modes
- Required human decisions, approvals, or accepted risks that remain outstanding

Passing this stage does not require that every challenger find a defect. A valid outcome MAY be that the current implementation remains justified and is ready to proceed.

## 10. Refactoring Guardrails

Refactoring SHOULD have a concrete engineering rationale such as duplicated logic, unclear responsibility, violation of established architecture, fragile coupling, security exposure, testability problems, maintainability issues, unnecessary complexity, a demonstrable performance concern, an incorrect abstraction, or a repeated defect pattern.

Refactoring SHOULD NOT be required merely because a reviewer would personally write the code differently, another abstraction is fashionable, a different library could perform the same task, the implementation is not aesthetically preferred, or an agent can imagine a theoretically cleaner design.

A review or challenge finding that recommends refactoring SHOULD identify the material engineering problem the refactoring is intended to resolve.

Review cycles SHOULD converge when required standards are satisfied and no material defect, risk, unresolved evidence question, or justified maintainability concern remains. Repeated stylistic improvement requests MUST NOT create an unbounded barrier to completion.

---

[Return to the Agentic Development Standards](../agentic-development.md)
