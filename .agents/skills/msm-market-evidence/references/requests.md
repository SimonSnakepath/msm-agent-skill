Endpoint: POST https://simoneastwood.app.n8n.cloud/webhook/msm-agent-v1
(If this ever differs from the live Developer Quickstart, https://mysellmate.digital/docs/developer-quickstart, follow the Quickstart.)
Headers: Content-Type: application/json ; x-msm-api-key: <value of MSM_API_KEY>
Missing or invalid key returns {"error":"AUTHENTICATION_REQUIRED", ...}
Shapes match the live Developer Quickstart (S435), except REJECT, labelled below. Anything in angle brackets is a placeholder.

LOOKUP by contract:
{"method":"get_market_evidence","session_id":"<unique>","action":"LOOKUP","lookup":{"contract_address":"0x...","chain":"ethereum","asset_type":"NFT"}}
LOOKUP by name: same, with "lookup":{"name":"PAX Gold"} (if both are sent, the contract address is used).
SELECT_ALTERNATIVE (ILLUSTRATIVE TEMPLATE, NOT EXECUTABLE JSON: replace the angle-bracket text with the whole "select" object of the chosen candidate, copied exactly as received):
{"method":"get_market_evidence","session_id":"<same>","action":"SELECT_ALTERNATIVE","selection":<the whole "select" object, unchanged>}
Tier 1 CONFIRM (no drill_down; spends credits):
{"method":"get_market_evidence","session_id":"<same>","action":"CONFIRM","request_id":"<new unique>"}
REJECT (free; declines the pending proposal; then send a new LOOKUP). CODE-DERIVED SHAPE, NOT YET INDEPENDENTLY VERIFIED against a captured live request body:
{"method":"get_market_evidence","session_id":"<same>","action":"REJECT","request_id":"<new unique>"}
Tier 2 package (CONFIRM with drill_down; free):
{"method":"get_market_evidence","session_id":"<same>","action":"CONFIRM","drill_down":"order_book_detail","request_id":"<new unique>"}
History list: {"method":"get_market_evidence","session_id":"<same>","action":"GET_HISTORY","history":{"limit":20}}
 (filters inside "history": cursor, asset, kind, package, from, to; follow next_cursor until it is null; "kind":"TIER1" lists paid reports)
History retrieve: "history":{"report_id":"<report_id>"} (inside the same request shape)
Example call:
  curl -s -X POST "<endpoint>" -H "Content-Type: application/json" -H "x-msm-api-key: $MSM_API_KEY" -d '{...}'
