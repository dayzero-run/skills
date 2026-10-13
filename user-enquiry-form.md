# User enquiry form

Use this when the user wants a contact form, a question form, or a way for someone to send a message.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can read these messages later.

```json
{
  "tables": [
    {
      "name": "enquiries",
      "label": "user_enquiry",
      "fields": [
        { "name": "name", "type": "string", "required": true },
        { "name": "email", "type": "string", "required": true },
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

- `name` is who wrote.
- `email` is how to reply.
- `message` is what they asked.

Each submit is a new row. Day Zero sets the row time. Do not add your own created-at field.

## Save an enquiry

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  Dayzero.tables.from("enquiries").insert({
    name: "Friend",
    email: "friend@example.com",
    message: "I would like to know more."
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
