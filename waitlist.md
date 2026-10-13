# Launch waitlist

Use this when the user wants a waitlist for one launch, one product, or one idea. This is not a newsletter. A newsletter uses the email subscription skill.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read this list later.

```json
{
  "tables": [
    {
      "name": "waitlist",
      "label": "waitlist",
      "fields": [
        { "name": "email", "type": "string", "required": true, "unique": true },
        { "name": "name", "type": "string" }
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

- `email` is the address. One row per address.
- `name` is optional.

Day Zero sets the row time. Do not add your own created-at field.

## Save a signup

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("waitlist").insert({
    email: "friend@example.com",
    name: "Friend"
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
