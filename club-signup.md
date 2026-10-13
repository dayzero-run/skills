# Club signup

Use this when the user wants people to join a club, a class, or a group.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read this list later.

```json
{
  "tables": [
    {
      "name": "signups",
      "label": "club_signup",
      "fields": [
        { "name": "name", "type": "string", "required": true },
        { "name": "email", "type": "string", "required": true, "unique": true },
        { "name": "group_name", "type": "string", "required": true }
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

- `name` is who is joining.
- `email` is the address. One row per address.
- `group_name` is the club, class, or group they joined.

Day Zero sets the row time. Do not add your own created-at field.

## Save a signup

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("signups").insert({
    name: "Friend",
    email: "friend@example.com",
    group_name: "Thursday study group"
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
