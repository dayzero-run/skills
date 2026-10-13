# Scoreboard

Use this when the user wants to save a game score, a quiz result, or a leaderboard row.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these scores later.

```json
{
  "tables": [
    {
      "name": "scores",
      "label": "scoreboard",
      "fields": [
        { "name": "player", "type": "string", "required": true },
        { "name": "score", "type": "number", "required": true }
      ]
    }
  ]
}
```

```bash
d0 tables apply
d0 site-key
```

## What each field is for

- `player` is the name to show on the board.
- `score` is the number they earned.

Each result is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save a score

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("scores").insert({
    player: "Friend",
    score: 12
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
