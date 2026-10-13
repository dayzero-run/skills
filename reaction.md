# Reaction

Use this when the user wants to count likes, loves, or other reactions on a page.

This skill decides the table. You decide the button. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can count reactions later.

```json
{
  "tables": [
    {
      "name": "reactions",
      "label": "reaction",
      "fields": [
        { "name": "kind", "type": "string", "required": true }
      ]
    }
  ]
}
```

```bash
d0 tables apply
d0 site-key
```

## What the row is for

Insert one row every time someone reacts. The number of reactions is the number of rows. Day Zero sets the row time, so a later dashboard can count the last 7 days from that time.

`kind` says which reaction they used. Use a short lowercase word such as `like`, `love`, or `clap`.

## Count a reaction

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  document.querySelector("#like-button").addEventListener("click", function () {
    Dayzero.tables.from("reactions").insert({ kind: "like" });
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
