# Guestbook

Use this when the user wants visitors to leave a public note, a guestbook entry, or a short comment on the page.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these notes later.

```json
{
  "tables": [
    {
      "name": "notes",
      "label": "guestbook",
      "fields": [
        { "name": "name", "type": "string", "required": true },
        { "name": "message", "type": "string", "required": true }
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

- `name` is who wrote the note.
- `message` is the note itself.

Each note is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save a note

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("notes").insert({
    name: "Friend",
    message: "Glad this exists."
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
