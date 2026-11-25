# Bidder concentration (Tier 2 order_book_detail)

Request: the order_book_detail shape in references/requests.md. Free, within the 20-per-report limit, and only after an authorised Tier 1 report. It reads the session's saved Tier 1 evidence, so it is not a fresh market read. Its as_of is the original Tier 1 as_of.

## Where it is
order_book_detail.observed_capacity.bid_side.maker_structure
Tier 1 reports never carry it. Read it at this exact path.

## Current fields (methodology_version 1.2-returned-offers-wallet-participation)
- status
- methodology_version
- venue: "opensea"
- order_scope: "eligible_collection_offers_returned_by_opensea"
- value_basis: "remaining_notional_in_offer_currency"
- chains, currency
- orders_counted, orders_with_maker, orders_without_maker
- distinct_makers_in_sample: distinct wallets in the returned offers
- largest_maker_share_of_value_in_sample_pct: share of total offer value held by the largest wallet by value
- top_3_makers_share_in_sample_pct: share held by the three largest wallets by value
- max_orders_by_any_maker_in_sample: most orders from any one wallet. It is NOT the order count of the largest wallet by value.
- trait_restricted_orders
- sample_complete: false when the response was paginated, otherwise null. It is never true.
- interpretation_boundary: carry it with any figure.

## status values
available; no_eligible_bids; bid_evidence_unavailable; maker_identity_incomplete; value_basis_incomplete; mixed_currency_shares_not_computed; mixed_chain_shares_not_computed.
Shares are filled in only when every eligible offer has a known chain, currency, positive value and maker, with one currency and one chain. Otherwise the shares are null. distinct_makers_in_sample and max_orders_by_any_maker_in_sample are null if any offer has no chain. Report the status. Do not fill gaps.
Where maker identities are incomplete (orders_without_maker above zero), wallet counts describe attributable wallets only. Compare orders_with_maker with orders_counted.

## How to read it
- Sample only. The figures cover up to 50 returned eligible OpenSea collection offers, not the full book. Do not assume they are the best-priced offers. Wallet counts and maximum orders may be well below full-book counts.
- All prices. Concentration covers every returned offer whatever its price. It is a different measure from the price-bounded capacity bands (within_2pct, within_5pct, within_10pct), which can contain very few orders. Do not combine or compare them as if they were one measure.
- Wallets are not people. One person can use several wallets.
- Distinguish observed bid participation and notional capacity from verified funded demand, executable liquidity or price support. Concentration alone does not establish any of these. MSM does not check whether a wallet holds the funds or whether an offer could be filled.
- Shares are of offer value in the offer currency, not of order count and not in USD.

## Missing or null maker_structure
- Key absent or null means concentration evidence is unavailable for that report. It is not zero concentration and not an error.
- Older sessions are a verified cause: a new Tier 2 request on a session created before this feature returns the block present but null. A null on its own does not establish the reason, so do not state one.
- A status other than available also means the figures are unavailable or partial. Report the status.

## Older reports (each is returned exactly as stored; check methodology_version)
- 1.0: distinct_makers, largest_maker_order_count, largest_maker_share_of_value_pct, top_3_makers_share_pct
- 1.1: distinct_makers_in_sample, max_orders_by_any_maker_in_sample, but the older share names (without _in_sample)
- 1.2: all four sample-scoped names (current)
- Reports saved before this feature existed have no maker_structure key.
- Never compare fields across versions by name alone. Read methodology_version first.
- History list and retrieve return the stored package unchanged. They create no new entry and cost nothing.
