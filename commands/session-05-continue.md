I want you to implement the next (or first if applicable) phase for the plan in
the current dev session.

We should have a plan.md and spec.md for the current dev session. Confirm that
we have these files.

Read the plan.md and spec.md files in full, as well as any other referenced
material needed for proper, full context. Do not rely on summaries for critical
context documents.

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

At the end of each phase, I will review the work and either ask for changes or
direct you to proceed with the next phase. Do not automatically proceed with
further phases.
