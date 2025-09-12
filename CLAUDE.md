# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a collection of slash commands designed to streamline a structured development workflow using Claude Code. The commands are meant to be symlinked to `~/.claude/commands` for use across development sessions.

## Development Workflow Architecture

The workflow is built around "dev sessions" - structured development cycles that can handle features, refactoring, or other development goals of varying complexity. Each session follows these phases:

### Session Structure
Sessions create a directory at `docs/dev-sessions/$(date +"%Y-%m-%d-%H%M")-{slug}` containing:
- `spec.md` - behavioral requirements and specifications (like a PRD)
- `plan.md` - multi-phase implementation plan with detailed steps
- `pr.md` - pull request description (populated at session end)
- `phaseN-context.md` - context files for each completed phase

### Workflow Commands

1. **session-01-start.md** - Initialize or resume a dev session
   - Creates session directory structure if needed
   - Reads existing session documents for context

2. **session-02-brainstorm.md** - Develop specifications
   - Interactive spec development through iterative questioning
   - Focuses on behavioral requirements, edge cases, testing approach
   - Saves final spec to `spec.md`

3. **session-03-plan.md** - Create implementation plan
   - Generates hierarchical markdown outline organized into phases and steps
   - Each phase should fit comfortably in a single Claude Code session (3-6 hours equivalent)
   - Phases build linearly, concluding in validated states
   - Testing integrated into each phase, not deferred to final phase

4. **session-04-execute.md** - Execute first phase of plan
   - Reads spec and plan for full context
   - Implements first phase with strict testing requirements
   - Creates `phase1-context.md` for handoff to next session
   - Commits changes locally (never pushes automatically)

5. **session-05-continue.md** - Execute subsequent phases
   - Similar to execute but for phase 2+
   - Reads all previous phase context files
   - Creates `phaseN-context.md` after completion

6. **session-06-recap.md** - Finalize session
   - Creates comprehensive `recap.md` combining all phase contexts
   - Generates humble, accurate pull request description in `pr.md`
   - Commits final documentation

### Critical Testing Rules

- **NEVER DELETE OR DISABLE TESTS** except when removing exercised code or refactoring for better coverage
- **FAILING TESTS ARE NOT OKAY** - all tests must pass before phase completion
- **NO TWEAKING ASSERTIONS** to match observed vs expected results
- **NO MOCKS** due to LLM hallucination risks - prefer integration tests

## Additional Tools

### TaskQ Integration
The `taskq.md` command integrates with https://github.com/jwhiting/taskq for parallel task processing using subagents.

## Session Management Best Practices

- Phases should conclude in clean, validated states
- Always read full context documents, never rely on summaries
- Use whitelisted bash commands when available (check ~/.claude/settings.json and project .claude/ configs)
- Avoid changing directories - use absolute paths instead
- Create phase context files suitable for fresh Claude Code sessions
- Only commit locally unless explicitly instructed to push

## Key Principles

- Specifications focus on behavior and requirements without implementation details
- Plans break work into manageable, linear phases
- Testing is integrated throughout, not deferred
- Context preservation enables seamless handoffs between sessions
- Documentation captures both successes and problems encountered