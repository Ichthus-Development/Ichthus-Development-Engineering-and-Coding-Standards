# Agentic Repository and Workspace Standards

*Companion document in the Agentic Development Standards family*

This document defines expectations for isolated agent work, source-control traceability, concurrent mutation, and protected change paths. It is authoritative for the detailed rules in its scope.

## 1. Isolated Workspaces

Agentic work SHOULD use task-specific branches, worktrees, containers, sandboxes, or equivalent isolated workspaces when practical.

Multiple agents MUST NOT unknowingly mutate the same working tree or equivalent mutable workspace concurrently.

When shared mutation is intentional, the workflow MUST define coordination and conflict handling sufficient to prevent one execution from silently overwriting, invalidating, or attributing another execution's work incorrectly.

Temporary workspaces SHOULD be reproducible or reconstructible from durable task state and repository history where practical.

## 2. Repository History and Change Attribution

Agents MUST preserve repository history and traceability appropriate to the project workflow.

Agentic work MUST NOT erase or rewrite relevant history merely to conceal failed attempts, prior authorship, review findings, or policy decisions.

Task output SHOULD identify, when applicable:

- Repository and workspace
- Branch or equivalent change set
- Relevant commit identifiers
- Files materially changed
- Validation performed and actual results
- Review or approval state
- Known unresolved issues

## 3. Protected Change Paths

Direct modification of protected or default branches SHOULD be prohibited for agentic implementation work unless project policy explicitly authorizes that workflow with equivalent controls.

Force-pushing protected branches MUST be prohibited unless an explicit exceptional policy defines who may authorize it, why it is necessary, and how traceability is preserved.

Merge, release, deployment, or publication authority MUST be separate from mere technical ability when project policy reserves those actions for review or approval.

An agent MUST NOT bypass branch protection, required checks, review gates, or equivalent repository controls to complete a task.

## 4. Workspace Scope

An agent SHOULD receive access only to repositories and paths needed for assigned work.

Unrelated local files, other project worktrees, user home directories, mounted shares, credentials, build caches containing sensitive material, and production artifacts SHOULD remain outside the agent workspace unless specifically required and authorized.

Generated files, downloaded artifacts, temporary patches, and research materials SHOULD have a defined disposition when they can affect reproducibility, licensing, security, or traceability.

---

[Return to the Agentic Development Standards](../agentic-development.md)
