# Share button

Use this when the user wants to count clicks on a share button, a copy-link button, or a share action.

This skill decides the table. You decide the button. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can count shares later.

```json
{
  "tables": [
    {
      "name": "shares",
      "label": "share_button",
      "fields": [
        { "name": "channel", "type": "string", "required": true }
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

Insert one row every time someone clicks or shares. The number of shares is the number of rows. Day Zero sets the row time, so a later dashboard can count the last 7 days from that time.

`channel` says what they did. Use a short lowercase word such as `click`, `copy_link`, `native_share`, or the place they shared to.

## Count a click

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  document.querySelector("#share-button").addEventListener("click", function () {
    Dayzero.tables.from("shares").insert({ channel: "click" });
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
