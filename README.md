# 123offerte.it MCP: Italian offers for your AI assistant

Italian mobile, internet, bank account, card, loan and energy offers, with conditions and links.

A free, read-only [Model Context Protocol](https://modelcontextprotocol.io) server over the
[123offerte.it](https://123offerte.it) catalogue: mobile plans, home internet, current accounts,
credit cards, personal loans, electricity, gas and dual fuel in Italy. Prices come with their
conditions (duration, new customers only, commitments, upfront payments) and a link to each offer.
No account, no API key.

```text
https://123offerte.it/mcp
```

## Add it to your AI app

- **ChatGPT**: Plugins → + → Add custom MCP server → paste the URL above, _No authentication_.
  ([guide](https://developers.openai.com/api/docs/guides/custom-mcp-server))
- **Claude** (web or desktop): Customize → Connectors → Add custom connector → paste the URL, _No
  sign in_.
  ([guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp))
- **Other apps**: look for Connectors, Integrations or MCP in the settings and add the URL with no
  authentication.

## No connectors in your app? Copy this prompt

Works with assistants that can send web requests (agent modes) and with ones that can only open web
pages: both get the full search, with filters, conditions and links. Write your question at the end.

```text
Use the 123offerte.it catalogue of Italian offers (mobile plans, home internet, current accounts, credit cards, personal loans, electricity and gas) to answer my question.

How to read it:
- If you can send web requests (code, curl or a tool): POST JSON to https://123offerte.it/mcp with the headers "Content-Type: application/json" and "Accept: application/json, text/event-stream". First send {"jsonrpc":"2.0","id":1,"method":"tools/list"} to see the tools and their arguments. Then call one, for example {"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"search_mobile_plans","arguments":{"limit":5}}}. The JSON answer is on the "data:" line. No sign-in or session is needed.
- If you can only open web pages: open https://123offerte.it/api/ai and follow its search links (put your filters in the link).

Rules: null means unknown, not zero. Keep every price's conditions and how long it lasts. Link the 123offerte.it page of each offer you mention.

My question:
```

## Developers

Streamable HTTP, no authentication, no sessions. The same tools also answer plain GET links as
compact Markdown (or `?format=json`): start at
[https://123offerte.it/api/ai](https://123offerte.it/api/ai).

```sh
claude mcp add --transport http 123offerte https://123offerte.it/mcp
```

```json
{ "mcpServers": { "123offerte": { "url": "https://123offerte.it/mcp" } } }
```

| Tool                      | What it does                                                |
| ------------------------- | ----------------------------------------------------------- |
| `search_mobile_plans`     | Mobile plans by price, data, 5G, eSIM, network and provider |
| `search_home_internet`    | Home internet by technology, speed, modem and price         |
| `search_current_accounts` | Current accounts by fee, bank and services                  |
| `search_credit_cards`     | Credit cards by annual fee, network and repayment           |
| `search_personal_loans`   | Personal loans by amount and term, with APR and examples    |
| `search_energy`           | Electricity, gas or dual fuel with your yearly kWh and Smc  |
| `get_product`             | One offer's full details, conditions and link               |
| `compare_products`        | Compare 2–5 offers of the same kind                         |

`null` means unknown, never zero. A conditional price keeps its requirements; it does not mean you
qualify. Loan examples are not personal quotes; energy estimates use stated assumptions.

## Using the data

Free to use with attribution: credit **123offerte.it** with a link to the offer or category page.
See the [data terms](https://123offerte.it/en/data/terms). Data comes from providers' official
documents and, for energy, the Portale Offerte; always check the provider's current terms.

## In italiano

Collega il tuo assistente AI al catalogo di 123offerte.it: offerte mobile, internet casa, conti,
carte, prestiti, luce e gas, con condizioni e link. Gratis e di sola lettura. Istruzioni e prompt in
italiano: [123offerte.it/dati/ai](https://123offerte.it/dati/ai).

This repository holds documentation and the registry entry only; the server runs at
[123offerte.it](https://123offerte.it). The registry entry is
[`it.123offerte/mcp`](https://registry.modelcontextprotocol.io).
