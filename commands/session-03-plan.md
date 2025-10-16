Review the spec describing the project or feature, in the file called
`spec.md` for the current dev session, then draft a step-by-step blueprint for
building this project or feature in `plan.md`.

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
1. **Execution Required**: Tests must be executed, not just written
2. **All Must Pass**: Proceeding with failing tests is prohibited
3. **No Test Manipulation**: Disabling, skipping, or deleting tests to achieve
   passing status is prohibited
4. **No Scope Reduction**: Reducing functionality to avoid test failures is prohibited
5. **No Mocks Without Plan or User Approval**: Due to LLM hallucination risks,
   write integration tests; raise to user if mocks are necessary and the plan
   didn't already specify using them.
6. **Validate Existing Tests**: When modifying code, existing test coverage must pass

Testing guidelines:
- Testing must be part of the phase in which the code is written when testable
  functionality is created. Each phase should clearly state its testing approach:
  either it includes tests, defers them to a specific later phase, or explains
  why testing doesn't apply.
- Strike a balance between under-testing and over-testing. Validate the core
  functionality and key use cases that ensure the specification requirements
  are met, but don't test every little permutation.

There are critical steps that must be added to each phase. The exact steps depend
on whether the phase is Test-Bound or Test-Exempt:

Initial task for EVERY phase: (include literally, do not compress this)

    Re-read all documents in the dev session directory in full to ensure
    complete context. Every file must be read from start to finish, no
    exceptions. No summarizations or skipping of files or sections are
    allowed.

Provide the full path to the dev session directory in this plan step.

Penultimate task FOR TEST-BOUND PHASES - Test Verification and Report:
(include this step literally for any Test-Bound phase)

    SUBSTEP 1: Self-Evaluate Testing Policy Adherence
    Before executing tests, explicitly audit your work against the Critical
    Testing Policies. For each policy, state whether you adhered to it. If you
    violated any policy (e.g., disabled a test, reduced scope to avoid failures,
    skipped test execution), STOP and remediate before proceeding.

    SUBSTEP 2: Execute Tests
    1. Identify all test files that should be run for this phase
    2. Execute each test suite and capture full output in bash tool (do not
       pipe to tail or grep)
    3. If ANY tests fail: debug and fix issues, then repeat from step 2

    SUBSTEP 3: Generate Test Report
    Output a summary report to the chat session containing:
    - List of all test files executed with full paths
    - Total counts: tests run, passed, failed, skipped
    - Policy adherence statement: Confirm adherence to all 6 Critical Testing
      Policies, or document any violations and how they were resolved
    - If applicable: any tests deferred to later phases per the plan

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

