# Link click

Use this when the user wants to count clicks on a specific outbound link, such as a button on a link-in-bio page. This is not the share button skill. The share button counts how someone shared this page.

This skill decides the table. You decide the links. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can count clicks later.

```json
{
  "tables": [
    {
      "name": "link_clicks",
      "label": "link_click",
      "fields": [
        { "name": "link", "type": "string", "required": true }
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

Insert one row every time someone clicks a link. The number of clicks is the number of rows. Day Zero sets the row time, so a later dashboard can count the last 7 days from that time.

`link` says which link they clicked. Use a short lowercase word such as `shop`, `calendar`, or `instagram`.

## Count a click

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  document.querySelector("#shop-link").addEventListener("click", function () {
    Dayzero.tables.from("link_clicks").insert({ link: "shop" });
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
