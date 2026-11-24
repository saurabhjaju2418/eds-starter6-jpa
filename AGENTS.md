# Repository guidance for Codex

## Project facts

- This repository combines a Java/Spring Boot application with an Ext JS 6 client.
- The Maven build in `pom.xml` currently targets Java 17 and Spring Boot 2.7.18. The README's Java 8 description is stale; treat the checked-in build as authoritative and do not change the runtime baseline without approval.
- Java source is under `src/main/java/ch/rasc/eds/starter`; resources, including Liquibase changelogs, are under `src/main/resources`; the client is under `client/`.
- Maven annotation processors generate Java and client-side artifacts. Inspect the relevant Maven plugin configuration before editing generated output; prefer changing its source inputs.
- Follow `.editorconfig`: UTF-8 and LF; Java, Groovy, Kotlin and XML use tabs.
- The current GitHub Actions workflow compiles with tests skipped and is configured for pushes to `master`, while the repository default branch is `main`. Report this mismatch; do not silently change the workflow.
- The build includes database and Liquibase configuration. Treat schema, migration, and persistent-data changes as high impact.

## Workflow and approval boundary

1. Start each task with read-only discovery. Inspect the relevant code, existing behavior, build configuration, and Git status before proposing a change.
2. Report findings, uncertainty, proposed files, and the exact validation steps before editing. Wait for the user's approval of that specific change.
3. After approval, make the smallest change that addresses the request. Preserve existing behavior, naming, formatting, and dependency versions unless the user approved a broader change.
4. Do not add or run tests unless the user asks. Do not run commands that modify source, generated files, build output, databases, or external state without approval.
5. Show the diff and explain what changed, what you verified, and any remaining uncertainty.
6. Do not push, merge, open a pull request, deploy, change GitHub settings, or modify remote data without separate explicit approval. The one-time approval to publish the workflow setup files on `codex/legacy-workflow-setup` applies only to those three files.

## Safety for this repository

- Never expose credentials, tokens, personal data, or local environment contents in output.
- Do not connect to production or a non-disposable database, run migrations, or alter persistent data without explicit approval.
- Avoid dependency upgrades, framework migrations, broad formatting, and unrelated cleanup during a targeted fix.
- Do not hand-edit generated client or Java sources until you have checked how they are produced and confirmed the user wants generated output changed.
- When build or test commands are requested, explain side effects first. Maven may write to `target/`; frontend build steps may write under `client/`.