I want to continue the plan for the current dev session.

There should be a directory of markdown documents and artifacts for the current
dev session. The name of the directory should be called
`docs/dev-sessions/$(date +"%Y-%m-%d-%H%M")-{slug}` where `$(date
+"%Y-%m-%d-%H%M")` is a bash command and `{slug}` is a short description of the
session. If you don't know the current dev session from context already, derive
the slug from the name of the current git branch, otherwise ask me to provide a
short description.

We should have a plan.md and spec.md for the current dev session. Confirm that
we have these files. Read the plan.md and spec.md files. Those files may
mention other important related files that should be read as well. IMPORTANT:
Do not skip this or any important file context - read all the referenced files,
do not rely on summarizations for key context documents. If you have trouble
finding or reading the expected or referenced files, stop and ask.

Since we are continuing a plan that is already in progress, there may be
artifacts from prior work, like `phaseN-context.md` files - read those too.

Before starting to code, learn your whitelisted bash commands and try to use
them over logically equivalent bash commands than have not been whitelisted.
There are four possible cumulative configuration file locations for these:
1. $HOME/.claude/settings.json
2. $HOME/.claude/settings.local.json
3. .claude/settings.json in the current project
4. .claude/settings.local.json in the current project

For example, if `rg` is whitelisted but `grep` is not, do the search with `rg`.

Avoid changing directories unless absolutely needed. You forget where you
are and are slowed down by commands failing due to an unexpected working
directory.

**CRITICAL RULES FOR TESTING:**
- **NEVER DELETE OR DISABLE TESTS.** The purpose of tests is to verify that the
  code works! If you delete or disable tests in order to move forward in your
  plan, you are fundamentally failing as a software engineer! Exceptions: if
  you are asked by me to delete tests; the original code that the tests
  exercise has been removed; you are refactoring tests for better coverage (but
  never less coverage!)
- **FAILING TESTS ARE NOT OKAY.** There is no such thing as a test that "works"
  but isn't actually passing. A suite with 9 of 10 tests passing is not a
  passing suite. Do not consider your work done if there are failing tests. No
  exceptions.
- **NO TWEAKING ASSERTIONS JUST TO GET A TEST PASSING.** Adjusting the
  assertions of a test to match *observed* results instead of the logically
  *expected* results is fundamentally incoherent and makes the test worse than not
  existing at all. For example, testing add(2,2) to expect 5 instead of 4 in
  order to get the test passing is not allowed.
- **NO MOCKS.** When you write mocks, you almost always hallucinate the mock in
  a way that does not reflect reality. Because you are an LLM subject to
  hallucination, the rule is: *no mocks*. Exception: you have been given direct
  instruction on how and what to mock in the plan document.

At the end of each phase, write out a file in the dev session folder,
`phaseN-context.md` which is suitable for giving a fresh, blank-slate Claude
Code session the detailed information it needs to confidently tackle the next
phase. That includes but is not limited to:
- key initial orientation: a summary of the spec goals, locations of the spec/plan
  files in the dev session for further reading, and any other critical facts or
  instructions that have been given to you outside those files that you must
  remember.
- a concise but detailed recapitulation of work that was done in the completed
  phase
- problems or unexpected situations encountered and how they were addressed
- anything that is currently expected to be broken or has not been
  validated/tested

After writing this file, commit your changes to git (local only, without
pushing to remote).

I will review the work and either ask for changes, or direct you to proceed with
the next phase. Do not automatically proceed with further phases.
