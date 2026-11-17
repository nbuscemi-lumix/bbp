# BBP Editorial Calendar

A calendar page for the Black Bay Partners content program. Asana is the source of truth. This page only displays what is in Asana and holds no dates of its own.

## What it shows

- **Pipeline by week:** one row per content piece (the hub page and each insight article), with a marker for every task in its lifecycle.
- **By month:** the same tasks grouped by month, with counts of drafts, reviews, publishes, and LinkedIn posts.
- **Next up:** the next open tasks by due date, overdue first.

Marker types: D draft, R client review, P publish to the site and hub feed, L LinkedIn.

## How the data is read

Two modes, same page:

- **Live (inside Claude):** the page runs as a Claude artifact and reads Asana through the viewer's own Asana connector, using read-only calls (`get_tasks` and `get_task`).
- **Snapshot (everywhere else, including GitHub Pages):** with no Asana connection, the page reads `data.json` from this repo. That file is a copy of the plan pulled from Asana at a point in time, and the page shows when. It contains task names, dates, and status only, with no Asana links or ids.

To refresh the snapshot, ask Claude to republish the BBP calendar. Claude pulls the current plan from Asana, rewrites `data.json`, commits, and pushes.

It reads one section of the Asana project and treats these as content pieces:

- Top-level tasks named `Hub: ...` or `Insight Article: ...`. The task due date is the publish date.
- Their subtasks. The task name prefix sets the marker type:
  - `[Web] Draft` or `[Web] Revise` for drafts
  - `[Review]` for client review
  - `[Web] Publish` for publishing
  - `[LinkedIn]` for social posts

To add a new article, create an `Insight Article: <topic>` task in that section, add subtasks with the same prefixes and due dates, then press Refresh on the page.

## Files

- `index.html`: the whole page (HTML, CSS, and JavaScript in one file).
- The `SECTION` constant near the top of the script is the Asana section id to read.
