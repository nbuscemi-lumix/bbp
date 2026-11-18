# BBP Editorial Calendar

A Gantt-style calendar for the Black Bay Partners content program. Asana is the source of truth. This page only displays what is in Asana and holds no dates of its own.

## What it shows

- One collapsible row per content piece (the hub page, then the insight articles / spokes), with a bar from its first task to its last.
- Subtasks under each piece (web drafts, client review, publish, LinkedIn posts) as dots at their due dates. Publish dates are diamonds.
- Platform icons next to each piece (Website, LinkedIn), taken from the task prefixes.
- Dashed sub-subtasks are proposed and do not exist in Asana yet. They can be hidden with the toggle.
- A link at the top to the review content spreadsheet.

## How the data is read

The page reads `data.json` from this repo. That file is a copy of the plan pulled from Asana at a point in time, and the page shows the date as "Last update". It holds task names, dates, and status only, with no Asana links or ids.

To refresh it, ask Claude to republish the BBP calendar. Claude pulls the current plan from Asana, rewrites `data.json`, commits, and pushes.

Content pieces are top-level tasks named `Hub: ...` or `Insight Article: ...` (due date is the publish date). Their subtasks use a prefix that sets the platform and marker:

- `[Web] Draft`, `[Web] Revise`, `[Web] Publish`
- `[Review]` for client review
- `[LinkedIn]` for LinkedIn posts

## Files

- `index.html`: the page (HTML, CSS, and JavaScript in one file).
- `data.json`: the Asana snapshot.
