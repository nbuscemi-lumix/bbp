# BBP Editorial Calendar

A calendar page for the Black Bay Partners content program. Asana is the source of truth. This page only displays what is in Asana and holds no dates of its own.

## What it shows

- **Pipeline by week:** one row per content piece (the hub page and each insight article), with a marker for every task in its lifecycle.
- **By month:** the same tasks grouped by month, with counts of drafts, reviews, publishes, and LinkedIn posts.
- **Next up:** the next open tasks by due date, overdue first.

Marker types: D draft, R client review, P publish to the site and hub feed, L LinkedIn.

## How the data is read

The page runs as a Claude artifact and reads Asana through the viewer's own Asana connector. It makes read-only calls (`get_tasks` and `get_task`). Outside Claude there is no connector, so it shows a "not connected" message and no dates.

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
