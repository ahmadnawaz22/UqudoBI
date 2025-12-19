Do this every time you make progress:
1-Before you change something, add 2–5 bullets in docs/01-scope-and-goals.md under:
-“Now”
-“Next”
-“Later”

2-When you decide something that you might revisit, write an ADR (2 minutes).
-Example decisions: “multi-user access model,” “schemas vs databases,” “backup approach,” “naming conventions.”

3-When you change the database, you only do it via:
-A new SQL file in db/migrations/
-And a one-line entry in docs/00-index.md (or a simple CHANGELOG section in README)

4-When you need to visualize, update:
-diagrams/er-diagram.excalidraw
-diagrams/mindmap.excalidraw
