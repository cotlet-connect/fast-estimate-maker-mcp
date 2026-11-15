# Fast Estimate Maker MCP server

Connect Fast Estimate Maker to ChatGPT, Claude and other AI agents through Cotlet.dev. Work with estimates, leads, change orders and job costs in your signed-in contractor account. Review changes before sending them.

## What you can ask

> Draft estimate line items from these job-site photos for my review.

> List estimates viewed at least three times so I can plan follow-ups.

> Read the margin for estimate 1042 and summarize its recorded costs.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Fast Estimate Maker tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

Run the included Python module with Python 3.10 or later:

```bash
python3 fast_estimate_maker_agent.py serve
```

Or with Docker:

```bash
docker build -t fast-estimate-maker-mcp .
docker run -i --rm -e COTLET_API_KEY fast-estimate-maker-mcp
```

Tools: `fast_estimate_maker_guide`, `fast_estimate_maker_status`, `fast_estimate_maker_open`, `fast_estimate_maker_read`, `fast_estimate_maker_click`, `fast_estimate_maker_type`, `fast_estimate_maker_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, with no third-party runtime dependencies. Clone this repository and run:

```bash
export COTLET_API_KEY="your-key"
python3 fast_estimate_maker_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 fast_estimate_maker_agent.py status    # is Fast Estimate Maker ready in your Cotlet.dev account
python3 fast_estimate_maker_agent.py guide     # Fast Estimate Maker screens and sign-in link
python3 fast_estimate_maker_agent.py read      # open Fast Estimate Maker, read the page, close the browser
python3 fast_estimate_maker_agent.py tools     # list Cotlet.dev tools
python3 fast_estimate_maker_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Fast Estimate Maker users

**How do I connect my account?**

Request access at https://cotlet.dev/signup?app=fast-estimate-maker, sign in to Fast Estimate Maker in your Cotlet.dev Cloud Browser and enable it for agents.

**Can I review changes before they are sent?**

The hosted integration asks for confirmation before write calls by default. Review the requested operation before approving it.

**Does Fast Estimate Maker provide a public API?**

The Cotlet.dev integration page reports no public Fast Estimate Maker API or official MCP server as checked on 13 November 2026.

**Is Cotlet.dev affiliated with Fast Estimate Maker?**

No. Cotlet.dev is independent and not affiliated with Fast Estimate Maker.

## Learn more

- [fast-estimate-maker integration and hosted tools](https://cotlet.dev/integrations/fast-estimate-maker-api-mcp-server)

---

More: https://cotlet.dev/integrations/fast-estimate-maker-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=fast-estimate-maker

Request access: https://cotlet.dev/signup?app=fast-estimate-maker&utm_source=github&utm_medium=readme&utm_campaign=fast-estimate-maker

## Workflows on the hosted integration

Examples documented on the live integration page:

- `create_photo_to_estimates`
- `track_estimate_views`
- `manage_crm_lead_management`
- `track_hail_alerts`
- `create_change_orders`
- `send_invoices_and_collect_payments`
- `track_job_costing_and_receipt_ocr`

The local stdio adapter exposes seven browser helpers listed above. These helpers forward to Cotlet.dev; the workflow operations are documented on the hosted integration page.
