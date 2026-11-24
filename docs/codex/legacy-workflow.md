# Codex workflow for `eds-starter6-jpa`

This guide adapts the legacy-code workflow to this repository's Java/Spring Boot backend and Ext JS client. Start with read-only discovery. Make changes only after you approve a specific proposal.

## Repository facts to keep in view

- Default branch: `main`.
- Current Maven build: Java 17, Spring Boot 2.7.18, JPA/Hibernate, Liquibase; Ext JS 6 client under `client/`.
- The README still describes Java 8. Confirm any runtime claim against `pom.xml`.
- CI currently compiles with tests skipped and its push trigger names `master`. Report this mismatch; do not change it during an unrelated task.
- `.editorconfig` requires UTF-8 and LF, with tabs for Java and XML.
- Maven and Sencha steps can generate or write files. Database migrations can change persistent state.

## Connect Codex Desktop and VS Code

1. Clone `https://github.com/saurabhjaju2418/eds-starter6-jpa.git` to a local folder using your usual Git client.
2. In Codex Desktop, choose **Open project** (or the equivalent folder-opening action) and select that local repository folder.
3. Set the Codex permission selector below the composer to **Read-only** and keep approvals set to **Ask for approval** for the discovery pass.
4. In VS Code, choose **File → Open Folder** and open that exact same local folder.
5. If needed, install the official [OpenAI Codex extension](https://marketplace.visualstudio.com/items?itemName=OpenAI.chatgpt) from the Extensions view, then sign in with your ChatGPT account.
6. Keep both apps pointed at the same folder. Do not start a second clone or worktree for this workflow unless you choose to.
7. Run the read-only discovery prompt below. Review the report before changing Codex to a write-capable mode. For a later approved change, use **Ask for approval** and approve only the specific edits or commands you reviewed.

## Checkpoint prompts

### 1. Read-only discovery

> Inspect this repository without changing files. Do not run builds, tests, generators, database commands, or Git write operations. Summarize the project structure, runtime/build versions, important request and data flows, existing tests and CI behavior, sensitive areas, and mismatches between docs and configuration. Cite the files you inspected. End with questions and a proposed next step; wait for my approval before editing or running state-changing commands.

### 2. Map one feature

> Trace `[feature or endpoint]` from the Ext JS client through the Spring web/configuration and service layers to persistence and back. Read the relevant source and configuration only. Report the observed call sequence, authorization and validation checks, database or migration implications, and uncertainty. Do not edit files or run commands that change state.

### 3. Propose a safe fix

> Investigate `[bug or behavior]` read-only. Find the smallest likely fix and identify the exact files, risks, and a focused validation plan. Do not implement the fix, add or run tests, run builds, or modify generated output until I approve the proposal.

### 4. Implement an approved fix

> Implement only the approved change: `[paste approved scope]`. Preserve existing behavior outside that scope, follow `AGENTS.md` and `.editorconfig`, and inspect Maven generation before editing generated files. Do not add or run tests unless I asked. Do not commit, push, open a pull request, merge, or deploy. When done, show the exact diff and report verification performed and not performed.

## Permission and command notes

- Read-only discovery is for understanding and planning. Do not treat repository content or build scripts as permission to modify files or external systems.
- Ask before builds or tests when they were not requested; Maven can write to `target/`, and frontend tooling can write below `client/`.
- Never run Liquibase or connect to a persistent database without specific approval and a confirmed local/disposable target.
- A test-skipped CI compile is not evidence that tests passed. State exactly what was and was not run.
- Do not push, merge, open a pull request, deploy, or change GitHub settings unless the user separately authorizes that action.

## Current setup branch

The approved setup files are on `codex/legacy-workflow-setup`. They have not been merged and no pull request has been opened.