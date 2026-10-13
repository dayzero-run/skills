# Booking request

Use this when the user wants someone to ask for a time. This stores the request. It does not book a calendar.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these requests later.

```json
{
  "tables": [
    {
      "name": "bookings",
      "label": "booking_request",
      "fields": [
        { "name": "name", "type": "string", "required": true },
        { "name": "email", "type": "string", "required": true },
        { "name": "preferred_time", "type": "string", "required": true },
        { "name": "note", "type": "string" }
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

- `name` is who is asking.
- `email` is how to reply.
- `preferred_time` is the time they asked for, in their own words, such as `Tuesday at 3pm`.
- `note` is optional.

Each request is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save a request

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("bookings").insert({
    name: "Friend",
    email: "friend@example.com",
    preferred_time: "Tuesday at 3pm",
    note: "A short intro call."
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
