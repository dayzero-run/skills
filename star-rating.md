# Star rating

Use this when the user wants a score from 1 to 5, with an optional comment.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these ratings later.

```json
{
  "tables": [
    {
      "name": "ratings",
      "label": "star_rating",
      "fields": [
        { "name": "score", "type": "number", "required": true },
        { "name": "comment", "type": "string" }
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

- `score` is the number of stars, from 1 to 5.
- `comment` is optional.

Each rating is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save a rating

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("ratings").insert({
    score: 5,
    comment: "Clear and fast."
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
