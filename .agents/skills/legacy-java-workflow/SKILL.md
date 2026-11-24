---
name: legacy-java-workflow
description: Use for read-only discovery and approved, minimal fixes in this Java, Spring Boot, JPA, Liquibase, and Ext JS legacy application.
---

# Legacy Java workflow

Apply this workflow whenever investigating or changing this repository. Read the root `AGENTS.md` first.

## Checkpoint 1: Explain (read-only)

- Review Git status, repository structure, README, `pom.xml`, `.editorconfig`, relevant application profiles, CI workflow, and the specific code paths involved.
- Confirm versions and behavior from checked-in build files; the README currently says Java 8 but `pom.xml` sets Java 17 and Spring Boot 2.7.18.
- Trace a request or feature across the Ext JS client, Spring web/configuration layer, service, repository/entity, and database migration when relevant.
- Do not edit files or run builds, tests, generators, database commands, or other state-changing commands during discovery.
- Report findings, questions, risk, and the exact proposed change. Stop and wait for the user's approval.

## Checkpoint 2: Map

- Describe only components and relationships supported by inspected source.
- For cross-layer behavior, map the sequence from client call through the Spring endpoint/service to persistence and back.
- Use a small Mermaid diagram in the report when it improves clarity. Do not add diagrams to the repository unless approved.

## Checkpoint 3: Establish a baseline

- Inspect existing tests and CI first. The current CI compiles with `-DskipTests`; do not infer that tests passed.
- Do not add or run tests unless the user asks. If testing is requested, propose commands and explain generated output or external dependencies before running them.
- Keep any requested characterization or regression coverage narrow and consistent with the repository's existing test conventions.

## Checkpoint 4: Fix (only after approval)

- Make the smallest change that addresses the confirmed behavior.
- Preserve API contracts, database semantics, authorization rules, and compatibility unless the approved scope says otherwise.
- Check Maven annotation processors before editing files under generated output paths such as `client/app` or `target/generated-sources/java`.
- Treat Liquibase changes and commands against any persistent database as high impact; require explicit approval and a clearly identified disposable/local target before execution.
- Do not upgrade dependencies, modernize frameworks, reformat unrelated files, or adjust CI as incidental cleanup.

## Checkpoint 5: Review and report

- Review the final diff for scope, generated files, secrets, configuration changes, and accidental behavior changes.
- Report exact files changed, requested verification performed, and anything not verified.
- Do not commit, push, open a pull request, merge, deploy, or alter GitHub settings without separate explicit user approval.