$ARGUMENTS

**FORMATTING REQUIREMENTS:**
Use only ASCII characters in all output, documentation, and code unless the content explicitly requires extended characters (e.g., user-provided strings, natural language content). Do not use Unicode emojis, fancy arrows, or decorative characters. CRITICAL: Never use curly/smart quotes (Unicode U+201C, U+201D, U+2018, U+2019) in any form - they prevent file editing and cause critical failures. Use plain ASCII alternatives:
- Use only straight ASCII quotes (U+0022) and apostrophes (U+0027)
- Use "->" instead of fancy arrows
- Use "*" or "-" for bullets instead of bullet characters
- Use "..." instead of ellipsis character
- No emojis (checkmark, X, celebration, etc.)

We are going to use the local `taskq` CLI tool and your subagent capability to
complete the tasks in a queue of tasks managed by that tool. 

1. Refer to `taskq --help` output for context on this local CLI tool.

2. Ensure you have the queue name and count. If you don't know the queue name,
   ask the user. If no subagent count is specified, use 1 subagent.

3. Validate the queue exists and has pending tasks.

4. Spawn the specified number of subagents to process tasks from the given
   queue in parallel. Each subagent uses the `taskq` tool, and should:

  A. Use `taskq checkout <queue>` to get their task and instructions
  B. Quit immediately if no tasks remain to work on, else
  C. Complete the assigned work according to the task instructions
  D. Use `taskq complete <queue> <task_id>` to mark their task done

IMPORTANT: Do NOT checkout tasks yourself. Instead, immediately spawn the
requested number of subagents using the taskq tool in parallel. Each subagent
operates independently on the same queue.

Example for "queue is 'index-files', use 10 subagents":
- Spawn 10 Task tool calls simultaneously
- Each gets instructions: "Use `taskq checkout index-files` to checkout next
  task from 'index-files' queue, complete the work per task instructions, then
  mark complete with `taskq complete index-files <task ID>`"

