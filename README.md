# Slash commands for my Claude Code workflow 

I symlink this repo to `~/.claude/commands`

These commands reflect my general workflow. Each "session" is a feature, refactoring, or other development goal, ranging from small to potentially very large - the workflow works for a wide range of tasks.
1. Start a "dev session" - to capture spec, plans, session recaps, and final recap and PR description
2. Brainstorm - work with Claude to develop a clear spec. (Sometimes I already have this and skip this). Specs are like a PRD for the session: behaviors and requirements that think through the whole surface area of the problem, without getting too specific (no code or specific implementation plans.) Specs answer all important behavioral questions, link to key reference documentation or source files that are heavily involved, describe how the edge cases should work, explain what success looks like, etc. It might include specific tooling choices or architectural decisions. If there are breaking changes, it describes if and how the system should handle backwards compatibility, etc.
3. Plan - take the spec and produce a multi-phase, reasoned implementation plan. Review this plan carefully, iterate on it with Claude, and often this involves putting new or modified decisions into the spec, and regenerating or updating the plan to align with it. This step is done when the plan looks really good, and is in perfect alignment with the spec. I often ask Claude "carefully re-read the entire spec and plan and think hard about possible inconsistencies, ambiguities, or problems" and I am done when that process produces no, or insignificant, results.
4. Execute - in a new or compacted session, this boots full context up from the docs and tells Claude ground rules for execution (e.g. no deleting or skipping tests!) and has it implement the first phase of the plan, producing a commit and a phase1-context recap document. After each phase, I ask it to stop so I can review. Sometimes I tell it to not stop, and just do all the phases serially without confirmation.
5. Continue - almost identical to execute, to be run in a new (or recently compacted) session, but for phase 2+ (modification to context loading instructions)
6. Recapitulate - write up final reviews and a PR description

Note: taskq is a work in progress and integrates with https://github.com/jwhiting/taskq
