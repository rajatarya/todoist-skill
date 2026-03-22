---
name: todoist
description: Use when the user asks about tasks, to-dos, what's due, productivity, or mentions Todoist. Also triggers when the user wants to add, complete, reschedule, or organize tasks. Accepts optional arguments like project names, task content, or date ranges.
---

# Todoist CLI (td)

Manage Todoist tasks, projects, labels, and more via the `td` CLI.

## Agent Rules

- Use `td task add` (NOT `td add`) for structured task creation with flags.
- Use `--json` or `--ndjson` for parseable output when processing results.
- Use `--dry-run` on destructive/mutating commands when unsure.
- Default JSON shows essential fields; use `--full` for all fields.

## Quick Reference

### Views
```bash
td today                                    # Due today + overdue
td upcoming 14                              # Next 14 days (default: 7)
td inbox                                    # Inbox tasks
td completed --since 2026-03-01             # Completed since date
td stats                                    # Karma and productivity
td activity --since 2026-03-20 --by me      # My recent activity
```

### Tasks
```bash
td task add "Deploy v2" --due tomorrow --priority p1 --project Work --labels "deploy,urgent"
td task add "Review PR" --due "next monday" --project Work --section "Code Review"
td task add "Sub-item" --parent "Deploy v2"
td task list --project Work --json
td task list --filter "overdue & #Work"     # Raw Todoist filter syntax
td task list --priority p1
td task view <ref>
td task complete <ref>
td task complete <ref> --forever            # Stop recurrence permanently
td task uncomplete id:xxx                   # Reopen (requires id:xxx)
td task update <ref> --due "next friday" --priority p2
td task reschedule <ref> "next week"        # Preserves recurrence
td task move <ref> --project "Work" --section "Done"
td task delete <ref> --yes
```

### Projects
```bash
td project list --json
td project view "Work"
td project create --name "Q2 Goals" --color blue
td section list "Work"
td section create --project "Work" --name "In Progress"
```

### Labels, Comments, Reminders
```bash
td label list
td label create --name "blocked"
td comment list <task-ref>
td comment add <task-ref> --content "Updated the spec"
td reminder list <task-ref>
td reminder add <task-ref> --at "2026-03-25 09:00"
```

### Filters
```bash
td filter list
td filter show "My Filter" --json          # Run a saved filter
td task list --filter "p1 & today"          # Inline filter query
```

### URLs
```bash
td view https://app.todoist.com/app/task/buy-milk-abc123
```

## Task References

Tasks can be referenced by:
- **Name** (fuzzy match): `td task view "Deploy v2"`
- **ID**: `td task view id:63jrMccP3CQrR426`
- Projects/labels by name or `id:xxx`

## Common Workflows

**Daily review:**
```bash
td today
td upcoming 3
```

**Create task with subtasks:**
```bash
td task add "Release checklist" --project Work --uncompletable
td task add "Run tests" --parent "Release checklist" --due tomorrow
td task add "Update changelog" --parent "Release checklist"
```

**Bulk status check (JSON for processing):**
```bash
td task list --project Work --json | jq '.[] | {content, due, priority}'
```
