# RSVP

Use this when the user wants people to say whether they are coming to an event.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these replies later.

```json
{
  "tables": [
    {
      "name": "rsvps",
      "label": "rsvp",
      "fields": [
        { "name": "name", "type": "string", "required": true },
        { "name": "email", "type": "string", "required": true },
        { "name": "attending", "type": "boolean", "required": true },
        { "name": "guests", "type": "number" }
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

- `name` is who replied.
- `email` is how to reach them.
- `attending` is true when they are coming, and false when they are not.
- `guests` is how many extra people they are bringing. Use 0 when they come alone.

Each reply is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save a reply

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("rsvps").insert({
    name: "Friend",
    email: "friend@example.com",
    attending: true,
    guests: 1
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
