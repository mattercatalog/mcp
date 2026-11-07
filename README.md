# MatterCatalog MCP server

Ask an AI assistant whether a smart home device is **Matter certified**, which Matter devices to consider, and where to buy them, answered from [MatterCatalog](https://mattercatalog.com)'s catalog and its read of the CSA certification ledger.

- **Endpoint:** `https://mattercatalog.com/api/mcp` (remote MCP server, Streamable HTTP)
- **Read-only, no sign-in, no API key.**
- This repository holds documentation and client configuration only. The server is a hosted service run by MatterCatalog; there is no code to install.

## Tools

| Tool | What it answers |
|---|---|
| `check_matter_certification` | Is a product Matter certified? Searches MatterCatalog's published read of the CSA (Connectivity Standards Alliance) Distributed Compliance Ledger by product name, brand, model, part number or certificate ID: certificate IDs, certification dates, software and Matter versions, CSA device type and network, and the matching MatterCatalog page with that page's own certification answer. |
| `find_matter_devices` | Matter devices by category, platform (Apple Home, Google Home, Alexa, SmartThings; Home Assistant explained as a rule), network (Thread, Wi-Fi, Ethernet) and brand, each with its certificate, network, the platforms its page lists and the stores its page links, plus the matching MatterCatalog buying guide's picks. |
| `where_to_buy` | The stores a product's MatterCatalog page links, matched to the exact model, pack and region. Store names only. |
| `compare` | Two products side by side: certification, device type, Matter version, network, platforms and stores. |
| `catalog_stats` | Dated figures: Matter certified models and companies on the CSA ledger, new certifications, and what MatterCatalog lists. |

All tools are annotated `readOnlyHint: true`. Every answer states the date of the data it read and links mattercatalog.com pages. Answers contain **no prices and no store links**: the store buttons, prices with their check times and the affiliate disclosure are on the linked pages.

## Add it to your assistant

| Client | How |
|---|---|
| Claude (web, Desktop) | Customize → Connectors → Add custom connector → URL `https://mattercatalog.com/api/mcp`, no authentication |
| Claude Code | `claude mcp add --transport http mattercatalog https://mattercatalog.com/api/mcp --scope user` |
| ChatGPT | Plugins → Add custom MCP server → URL above, authentication none (on plans that offer custom MCP servers) |
| Perplexity | Connectors → Add custom → Add MCP connector → Remote → URL above, authentication None, Streamable HTTP (Pro, Max, Enterprise) |
| Grok | grok.com/connectors → New Connector → Custom → URL above |
| Gemini app | Settings → Connected Apps → Custom apps → Add a custom app → URL above (where available) |
| Gemini CLI | `gemini extensions install https://github.com/mattercatalog/mcp` or `gemini mcp add -s user --transport http mattercatalog https://mattercatalog.com/api/mcp` |
| Cursor | `~/.cursor/mcp.json`: `{"mcpServers":{"mattercatalog":{"url":"https://mattercatalog.com/api/mcp"}}}` |
| VS Code (Copilot) | `.vscode/mcp.json`: `{"servers":{"mattercatalog":{"type":"http","url":"https://mattercatalog.com/api/mcp"}}}` |
| LM Studio | Program → Install → Edit mcp.json: `{"mcpServers":{"mattercatalog":{"url":"https://mattercatalog.com/api/mcp"}}}` |
| Devin Desktop (Windsurf) | `devin mcp add -s user mattercatalog "https://mattercatalog.com/api/mcp"` |

Menu names change often; the URL and "no authentication" are what matter. Example questions: "Is the Aqara Smart Lock U200 Matter certified?", "Which Matter smart plugs work with Apple Home?", "Where can I buy the Eve Energy Smart Plug?", "Compare the Tapo P125M and the Eve Energy Smart Plug."

## Where the data comes from

The server reads the files mattercatalog.com publishes at every site build (the open-data catalog, the "Is it Matter certified?" lookup index and the dated figures), so its answers change when the site does. Certificate IDs and dates are the CSA's public records; MatterCatalog is independent and not affiliated with the CSA. Platforms are the ones each product page lists from the maker's own pages; supported features can vary by app.

## Privacy

No account and nothing stored about you. For each request the server logs the tool used, the name the assistant's software reports, the structured filters chosen, whether it failed and how long it took; never what was asked about (only its length). Logs are kept 30 days. Links in answers carry `utm_source` and `utm_medium=mcp` tags naming the assistant. Full policy: https://mattercatalog.com/privacy

## Links

- Documentation: https://mattercatalog.com/developers#mcp
- Open data (CSV and JSON, CC BY 4.0): https://mattercatalog.com/open-data and https://github.com/mattercatalog/matter-certified-devices
- Terms: https://mattercatalog.com/terms · Affiliate disclosure: https://mattercatalog.com/affiliate-disclosure
- Contact: team@mattercatalog.com

## License

The documentation and configuration files in this repository are licensed under [CC BY 4.0](LICENSE). The hosted service is provided by MatterCatalog under its [terms](https://mattercatalog.com/terms).
