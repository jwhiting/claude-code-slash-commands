I want to recapitulate the work for the current dev session.

**FORMATTING REQUIREMENTS:**
Use only ASCII characters in all output, documentation, and code unless the content explicitly requires extended characters (e.g., user-provided strings, natural language content). Do not use Unicode emojis, fancy arrows, or decorative characters. CRITICAL: Never use curly/smart quotes (Unicode U+201C, U+201D, U+2018, U+2019) in any form - they prevent file editing and cause critical failures. Use plain ASCII alternatives:
- Use only straight ASCII quotes (U+0022) and apostrophes (U+0027)
- Use "->" instead of fancy arrows
- Use "*" or "-" for bullets instead of bullet characters
- Use "..." instead of ellipsis character
- No emojis (checkmark, X, celebration, etc.)

There should be a directory of markdown documents and artifacts for the current
dev session. The name of the directory should be called
`docs/dev-sessions/{slug}-$(date +"%Y-%m-%d-%H%M")` where `$(date
+"%Y-%m-%d-%H%M")` is a bash command and `{slug}` is a short description of the
session.

Read all the files in the dev session directory in full, especially the spec,
plan, and the phaseN-context docs. You might also want to look at git commit
history to be oriented on files changed, commit messages, and key diffs.

Then update these files:
- `recap.md` - a concise but thorough recap of what was done including problems
  encountered and their solutions (or lack thereof if applicable). This in
  essence combines all the phaseN-* documents into a single, compressed
  overview.
- `pr.md` - a concise, **humble** pull request description for this work,
  covering at least: the principle goal(s), new behaviors and key changes, new
  dependencies, breaking changes, concerns and remaining work to do,
  dependencies on other tasks, and anything else to help a developer quickly
  orient. avoid exaggeration and over-celebratory terms like 'comprehensive'
  and 'production ready' unless they are truly accurate and warranted from
  a critical review perspective. be neutral, accurate, concise, and helpful.

After writing these, commit your changes to git and push to remote.
