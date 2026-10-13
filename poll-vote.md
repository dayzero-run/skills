# Poll vote

Use this when the user wants a poll and a count of which option people pick.

This skill decides the table. You decide the page. Do not invent a server or a database. Follow https://dayzero.run/ai.md for the CLI, the site key, and deploy.

## Table

Add this table to `tables.json`. If the file already has other tables, keep them and add this one.

Copy `label` exactly. Day Zero stores it with the schema so the dashboard can count votes later.

```json
{
  "tables": [
    {
      "name": "votes",
      "label": "poll_vote",
      "fields": [
        { "name": "poll", "type": "string", "required": true },
        { "name": "choice", "type": "string", "required": true }
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

Insert one row every time someone votes. The number of votes for an option is the number of rows with that `choice`. Day Zero sets the row time, so a later dashboard can count the last 7 days from that time.

- `poll` is which question this vote belongs to. Use a short lowercase word such as `launch_color`.
- `choice` is the option they picked. Use a short lowercase word such as `green` or `blue`.

## Save a vote

```html
<script src="https://cdn.jsdelivr.net/gh/dayzero-run/SDK@main/dayzero.js"></script>
<script>
  Dayzero.init({ siteKey: "sk_..." });

  document.querySelector("#vote-green").addEventListener("click", function () {
    Dayzero.tables.from("votes").insert({
      poll: "launch_color",
      choice: "green"
    });
  });
</script>
```

Use the site key from `d0 site-key`. Never put the API token in the page.
