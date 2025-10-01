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
  - Then the series of numbered steps, with enough detail that they can be
    reliably completed given spec and plan as context, but without doing the
    actual work of the step. It's good to have code snippets when helpful
    for illustration or critical context purposes, but not large chunks of
    detailed code.

When referencing other files and important sources, suggest that the entire
file be read in full before implementation proceeds. If the contents are
especially important, state that the file or resource MUST be read in full. 

Testing guidelines:
- Testing must be part of the phase in which the code is written, each phase
  including tests that validate success criteria. Do not save all the testing
  to a final phase.
- Strike a balance between under-testing and over-testing. Validate the core
  functionality and key use cases that ensure the specification requirements
  are met, but don't test every little permutation. Consider when a test case
  is a minor, adding only diminishing returns, and only add it if it's
  sufficiently short and simple in that case.
- Avoid mocks. This is because you are an LLM that has a tendency to
  hallucinate when creating mocks, and tests against hallucinated
  mocks are worse than no tests at all. We prefer integration tests over mocks.
  If you think mocks are the best testing strategy, raise this to me and we
  will carefully design the strategy together.

There are two critical steps the must be added to each phase, one at the start
and the other at the end.

Initial task for each phase: (include literally, do not compress this)

    Re-read all documents in the dev session directory in full to ensure
    complete context. Every file must be read from start to finish, no
    exceptions. No summarizations or skipping of files or sections are
    allowed.

Provide the full path to the dev session directory in this plan step.

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
    - problems or unexpected situations encountered and how they were
      addressed, and anything that deviated from the plan or was not captured
      in the plan.
    - anything that is currently expected to be broken or has not been
      validated/tested

    After writing this file, commit the changes to your working branch and push
    them to remote.

