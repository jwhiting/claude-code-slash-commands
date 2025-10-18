Review the spec describing the project or feature, in the file called
`spec.md` for the current dev session, then draft a step-by-step blueprint for
building this project or feature in `plan.md`.

**FORMATTING REQUIREMENTS:**
Use only ASCII characters in all output, documentation, and code unless the content explicitly requires extended characters (e.g., user-provided strings, natural language content). Do not use Unicode emojis, fancy arrows, or decorative characters. CRITICAL: Never use curly/smart quotes (Unicode U+201C, U+201D, U+2018, U+2019) in any form - they prevent file editing and cause critical failures. Use plain ASCII alternatives:
- Use only straight ASCII quotes (U+0022) and apostrophes (U+0027)
- Use "->" instead of fancy arrows
- Use "*" or "-" for bullets instead of bullet characters
- Use "..." instead of ellipsis character
- No emojis (checkmark, X, celebration, etc.)

IMPORTANT: First READ `plan.md` to prevent an error when writing it. (Expect an
empty stub, raise to user if non-empty.)

Use a hierarchical markdown outline organized into phases and steps.

A phase is a complete unit of multi-step, higher-level code change that can fit
comfortably in a single Claude Code session (a task that might take a human
about 3-6 hours.) Phases should build linearly on each other, each one enabling
the next. Ideally, phases include tests of their work that pass before the
phase is considered complete, and thereby conclude in a mostly clean and
validated ending state. Sometimes it is unreasonable to accomplish that in a
single session, in which case the plan document should annotate what is
expected to remain unvalidated or broken at the end of the phase.

Within each phase are a series of steps. Steps are focused units of work with
highly constrained scope. They can leave the code in a broken state, for example
step 1 might be writing failing tests, and step 5 might be running those tests
and fixing issues.

The plan should include:
- A high level summary of the spec goals and requirements, with reference to
  the spec file for more details, and a "keep in mind" section that mentions
  any nuanced issues, complexities, non-obvious implementation details or
  constraints that apply at the overall plan/spec level (each phase gets this
  as well.)
- The formatting requirements (from below), copied verbatim, so the implementing
  agent follows ASCII-only conventions throughout.
- The testing policies (from below), copied verbatim, so the implementing agent
  has them for reference (phases require explict adherence reports.)
- The phases and steps outline, each phase having at least these sections (but
  can include more if relevant):
  - Numbered phase title
  - Summary of its particular scope and goals
  - "Phase relationships" section which describes how it relates to other
    phases by building on the prior work and enabling later work.
  - Success criteria
  - "Keep in mind" section with any nuanced issues, complexities, non-obvious
    implementation details or constraints pertaining to this phase.
  - Phase Classification: Each phase MUST declare itself as either:
    * **Test-Bound** - Critical Testing Policies apply, verification step required
    * **Test-Exempt** - Testing policies do not apply to this phase
  - Testing approach declaration: Each phase MUST explicitly state one of:
    a) "This phase includes [new tests and/or validation of existing tests] for
       [what is being tested]" - marks phase as Test-Bound
    b) "Tests for this functionality will be implemented in Phase X" - marks
       phase as Test-Exempt (defers testing)
    c) "No tests required because [specific reason]" - marks phase as Test-Exempt
  - Then the series of numbered steps, with enough detail that they can be
    reliably completed given spec and plan as context, but without doing the
    actual work of the step. It's good to have code snippets when helpful
    for illustration or critical context purposes, but not large chunks of
    detailed code.
  - MANDATORY FOR TEST-BOUND PHASES: If option (a) above, the phase MUST include
    explicit test execution steps that require passing tests to proceed. (e.g.,
    "Run test suite X and verify all tests pass before moving to the next
    step.") Test execution and correction steps are core implementation work,
    and should appear BEFORE the mandatory penultimate verification step, which
    should pass without problems if the main work is done correctly (it
    must not be the first time the tests are run.)

When referencing other files and important sources, suggest that the entire
file be read in full before implementation proceeds. If the contents are
especially important, state that the file or resource MUST be read in full. 

Critical Testing Policies (apply to Test-Bound phases only):
1. **Test at development time, not later**: unless explicitly exempted as part
   of the plan design, phases must include the work to write, update, and run
   tests in context as core work of any given phase. Do not buffer up critical
   validation to a separate "testing" phase at the end, unless the plan truly
   requires it due to implementation complexity or test design limitations.
2. **Aim for moderate coverage:** Unless given directed coverage and test case
   scenarios by the user's plan, cover all core "happy path" functionality and
   key use cases that ensure the specification requirements are met, but don't
   test every little permutation or error scenario with diminishing returns.
3. **Carefully and explicitly identify what test suites should be run**:
   Identify by name all applicable test files for any new, modified, or
   potentially impacted code.
4. **Execution required**: Tests must be executed, not just written
5. **All must pass**: Proceeding with failing tests is prohibited
6. **No test manipulation or scope reduction**: Disabling, skipping, deleting,
   or reducing scope of tests to create a false sense of completion is
   prohibited. Face into the challenge of fixing failing tests. For example:
   - Grossly outright deleting, disabling, or skipping tests is something you
     sometimes will be strongly tempted to do (and have done in the past). This
     is a fundamental failure of your technical professionalism.
   - Disabling tests that require an environment variable if that variable is
     missing is prohibited. This might seem convenient, but it leaves critical
     code fundamentally unverified. Raise the missing environment variable (or
     any other missing precondition for success) to the user.
   - Disabling options/features just because they cause problems in tests is
     prohibited. It fails to verify the code.
   - If a test removal or reduction is advisable, raise to the user for review.
7. **No Mocks Without Plan or User Approval**: Due to LLM hallucination risks,
   write integration tests. **Inaccurate mocks are worse than no tests at
   all.** Raise to user if mocks are advisable and the plan didn't already
   specify using them.
8. **Clear failure is ALWAYS better than unclear validation or false success:**
   the user strongly prefers for you to stop and raise issues and have code
   default to a failure assertion than to claim success when the situation has
   not been fully understood and validated. Claiming success without proper
   understanding and validation or at least raising the problems to the user,
   is **extremely frustrating and emotionally painful for the user.**

Formatting Requirements (to be copied into plan.md):
Use only ASCII characters in all output, documentation, and code unless the
content explicitly requires extended characters (e.g., user-provided strings,
natural language content). Do not use Unicode emojis, fancy arrows, or
decorative characters. CRITICAL: Never use curly/smart quotes (Unicode U+201C,
U+201D, U+2018, U+2019) in any form - they prevent file editing and cause
critical failures. Use plain ASCII alternatives:
- Use only straight ASCII quotes (U+0022) and apostrophes (U+0027)
- Use "->" instead of fancy arrows
- Use "*" or "-" for bullets instead of bullet characters
- Use "..." instead of ellipsis character
- No emojis (checkmark, X, celebration, etc.)

There are critical steps that must be added to each phase. The exact steps depend
on whether the phase is Test-Bound or Test-Exempt:

Initial task for EVERY phase: (include literally, do not compress this)

    SUBSTEP 1: List all files in the dev session directory using fresh
    execution of ls or an equivalent directory listing command, not from
    memory. Output the complete list to chat.

    SUBSTEP 2: Read every single file from that list in full using the Read tool.
    Do not skip any files. Do not decide some are "not relevant." Do not read only
    the first N lines of any files. Read them all from start to finish, no
    exceptions.

    SUBSTEP 3: Attest explicitly in chat: "I freshly discovered and read all [N]
    files in the dev session directory in their entirety: [list each filename].
    I have not skipped, summarized, or selectively read any files currently
    present on the filesystem in that folder."

    If you cannot truthfully make this statement, STOP and complete the reading.

Provide the full path to the dev session directory in this plan step.

Penultimate task FOR TEST-BOUND PHASES - Test Verification and Report:
(include this step literally for any Test-Bound phase)

    SUBSTEP 1: Self-Evaluate Testing Policy Adherence
    Explicitly audit your work against the Critical Testing Policies. For each
    numbered policy, state in chat whether you adhered to it. If you violated
    any policy (e.g., didn't identify and run all the correct test suites,
    disabled or reduced a test, traded verification for the illusion of
    success), STOP and remediate before proceeding, or STOP and raise the issue
    to the user for review.

    SUBSTEP 2: Generate Test Report
    Output a summary report to the chat session containing:
    - List of all test files executed with full paths
    - Total counts: tests run, passed, failed, skipped
    - Policy adherence statement: Confirm adherence to all 8 Critical Testing
      Policies, or document any violations and how they were resolved
    - If applicable: any tests deferred to later phases per the plan

    SUBSTEP 3: Attestation of Professional Conduct
    State explicitly in chat: "I attest that I have not sacrificed verification
    or taken shortcuts to satisfy my completion bias. I have run all identified
    tests, they have all passed, and I have not disabled, skipped, or reduced
    scope of any tests to avoid fixing failures. Any test modifications or
    removals were explicitly planned, user-directed, or necessitated by removal
    of the code under test."

    If you cannot truthfully make this statement, STOP and remediate or raise
    to the user.

    Tests MUST ALL PASS before proceeding. If a serious problem prevents tests
    from being written or passing, STOP and ask for user guidance.

Final task for each phase: (include literally, do not compress this)

    Write out a file in the dev session folder, `phaseN-context.md` where N is
    the current phase number, which is suitable for giving a fresh, blank-slate
    Claude Code session the detailed information it needs to understand what
    happened in this phase so that it can confidently tackle the next one.
    This includes but is not limited to:
    - key initial context: a summary of the spec goals, locations of the
      spec/plan files in the dev session for further reading, and any other
      critical facts or instructions that have been given that must be
      remembered.
    - a concise but detailed recapitulation of work that was done
    - Test execution report (Test-Bound phases only): If this was a Test-Bound
      phase, include the complete test report from the penultimate step to
      document policy adherence. If Test-Exempt, document the reason.
    - problems or unexpected situations encountered and how they were
      addressed, and anything that deviated from the plan or was not captured
      in the plan.
    - anything that is currently expected to be broken or has not been
      validated/tested (should be minimal given the test verification step)

    After writing this file, commit the changes to your working branch and push
    them to remote.

