I want to resume or start a dev session.

**FORMATTING REQUIREMENTS:**
Use only ASCII characters in all output, documentation, and code unless the content explicitly requires extended characters (e.g., user-provided strings, natural language content). Do not use Unicode emojis, fancy arrows, or decorative characters. CRITICAL: Never use curly/smart quotes (Unicode U+201C, U+201D, U+2018, U+2019) in any form - they prevent file editing and cause critical failures. Use plain ASCII alternatives:
- Use only straight ASCII quotes (U+0022) and apostrophes (U+0027)
- Use "->" instead of fancy arrows
- Use "*" or "-" for bullets instead of bullet characters
- Use "..." instead of ellipsis character
- No emojis (checkmark, X, celebration, etc.) 

Resuming a session: Look at the current git branch for a session name slug, e.g. `feat/new-fancy-widget` would be `new-fancy-widget`, then see if there is a folder in `docs/dev-session` that corresponds to it with a date appended, e.g. `docs/dev-sessions/new-fancy-widget-2025-09-30-1505`. If that directory exists, that is our session. Read all the documents in the directory for context, completely from start to finish -- every single one, with one exception: do not read any files in the "exclude" subfolder as they are deliberately out of context.

Note: your glob tool only looks for files, not folders. search for `docs/dev-sessions/**/*.md` or similar.

Starting a session: If we're on main, or we're on a feature branch but but there's no session folder, it means you have to setup a new one.
1. If we're on main, ask me for a new name of the session. Let's say I give you "new fancy widget". Convert this to lowercase and replace non-alphanumerics with dashes, e.g. `new-fancy-widget`. If we're on a branch, e.g. `feat/new-fancy-widget` then you don't need to ask, you can assume i've already created the branch but haven't done the directory setup.
2. If we're on main, create a new feature branch e.g. `git checkout -b feat/new-fancy-widget`. If we're on a named branch already, no git commands are needed.
3. Create the session files directory as `docs/dev-sessions/{slug}-$(date +"%Y-%m-%d-%H%M")` where `$(date +"%Y-%m-%d-%H%M")` is a bash command and `{slug}` is `new-fancy-widget`.
4. Create the following placeholder files in the directory:
  - `spec.md` - the spec for the session
  - `plan.md` - the plan for the session
  - `recap.md` - a final recap of all work completed once finished
  - `notes.md` - a place to store user notes
  - `pr.md` - after the session is complete, we will populate a pull request description here.

Remember that this is the current dev session until we start another one or finish this one.
