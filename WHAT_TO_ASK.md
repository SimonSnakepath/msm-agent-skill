# Beyond the Price: What to Ask Your AI Agent

**Nine questions that go beyond a headline price.**

Already connected your AI Agent to [My Sell Mate (MSM)](https://www.mysellmate.digital)? These are reusable questions you can copy into your Agent. **No question names a particular asset:** replace `[asset]` or `[NFT collection]` with one you're interested in.

MSM provides dated, attributed market evidence. **MSM gives the evidence; your Agent interprets it.** A report is not a price prediction, guaranteed executable quote, proof of market manipulation or financial advice. Availability depends on the asset, the data sources and the report.

**Before starting:** Free LOOKUP identifies the proposed asset. Review that identity. A standard Tier 1 report costs **10 credits**; Tier 2 drill-downs are free once a Tier 1 report exists (subject to usage limits). Your Agent should ask for your authorisation before a chargeable Tier 1 request. Each asset requires its own session and Tier 1 report. Dates shown by MSM are observation timestamps, not a promise of live prices.

## Questions for any supported asset

### 1. What are the blind spots?

> For [asset], what can't MSM reliably tell me, and why? Show the report's as-of time, named sources, known unknowns and important caveats. Distinguish missing information from an observed zero.

**What MSM supplies:** Evidence-quality indicators, timestamps and explicit limitations, including `known_unknowns` and, where provided, `interpretation_boundary`.

**What your Agent adds:** A plain-English explanation of what those limits mean. It must not fill missing evidence with guesses.

### 2. Do the sources disagree?

> For [asset], which figures come from which providers? Where do the available sources disagree, and what can we *not* conclude from the comparison?

**What MSM supplies:** Named sources and, where overlapping provider evidence exists, reconciliation details or flagged conflicts.

**What your Agent adds:** An explanation of disagreements and their significance. **No reported conflict does not prove independent sources agree**; reconciliation may be unavailable or limited, and provider independence must not be assumed.

### 3. What changed between my saved reports?

> Using my saved MSM reports for [asset], compare fields that appear in both reports. State each as-of date, what changed, and which differences cannot be compared reliably.

**What MSM supplies:** The current Agent's own archived, dated reports through Research History (`GET_HISTORY`).

**What your Agent adds:** The comparison. MSM does not automatically compute a historical diff; reports may use overlapping samples or differ in coverage. Research History cannot retrieve reports your Agent never requested.

## Questions for NFT collections

### 4. How do asking prices compare with actual sales?

> For [NFT collection], are recent completed sales happening near the lowest observed asking price, or is there a gap between asks, collection-wide offers and sampled sale prices? State the observation time and sample limits.

**What MSM supplies:** Available ask and collection-wide bid references, recent completed sales samples and relevant Tier 2 execution detail.

**What your Agent adds:** A careful comparison, without treating an offer as a guaranteed fill or assuming that sampled sales represent floor-priced NFTs. Trait-specific and item-specific differences may matter.

### 5. Could I buy or sell near the floor price?

> If I wanted to buy or sell an NFT from [NFT collection], how close to the current floor price might a transaction be possible, based on observed listings, collection-wide offers and recent sales? Explain the buying and selling sides separately, and what the evidence cannot tell me.

**What MSM supplies:** The lowest observed asking price, nearby listings where available, the best observed collection-wide offer and relevant bid-side depth bands, spreads, and sampled completed sales, together with observation times and coverage cautions.

**What your Agent adds:** A cautious explanation of the price gaps and potential transaction friction, **not** a probability of execution, expected fill price or guarantee that any offer or listing remains available. An individual NFT's traits, item-specific offers, marketplace coverage and unverified funding can change what is actually possible.

### 6. How broad or concentrated is the buying interest behind the bids?

> For [NFT collection], how many distinct wallets are represented in the observed collection-wide offers, and how much of the bid value is concentrated among the largest one and three bidders? Compare this with observed liquidity near the best bid, and explain what the evidence cannot tell me about funding or execution.

**What MSM supplies:** Distinct wallet count, the largest wallet and top three wallets' shares of observed bid value, the maximum number of offers from any one wallet, price-bounded bid capacity and sample limitations.

**What your Agent adds:** Whether observed bid value is broadly distributed or concentrated, and how this relates to liquidity near prevailing market prices.

**Evidence boundary:** Concentration is measured across the returned sample of up to 50 eligible OpenSea collection offers, not specifically within the near-market price bands. Wallets do not necessarily represent separate people. Funding, execution capability, intent and complete market depth are not established.

This intelligence is included in the existing Tier 2 `order_book_detail` package at no additional charge following an authorised Tier 1 report (subject to usage limits). See the [bidder concentration reference](.agents/skills/msm-market-evidence/references/bidder-concentration.md) for interpretation and historical compatibility.

### 7. How broad is buying in the sampled sales?

> In the recent sales MSM sampled for [NFT collection], how many different buyer addresses appeared, and what share of observed buying came from the top one and top three? What can't that tell us?

**What MSM supplies:** NFT `execution_detail` participant-concentration figures, including `unique_buyers`, `top_buyer_share_pct` and `top_3_buyers_share_pct`, when available, from an observed sales sample of up to 50 transactions.

**What your Agent adds:** Interpretation of address-level concentration. One person may control several addresses; these numbers do not establish buyer identity, intent, demand quality or manipulation. MSM's concentration labels may be null by design.

## Questions for cryptocurrencies and tokenised assets

### 8. How deep and concentrated is the covered market?

> For [cryptocurrency or tokenised asset], how concentrated is provider-reported trading volume across covered venues, and what does the available per-venue order-book depth show? Include excluded markets and coverage limits.

**What MSM supplies:** Screened venue-level spread, volume-share and approximate ±2% depth evidence through the coin/RWA Tier 2 `order_book_detail`, where available.

**What your Agent adds:** A comparison of the reported markets. It must not present provider-reported volume as directly observed by MSM or treat per-venue depth as a consolidated, guaranteed executable order book.

### 9. How confidently was this token identified?

> For [tokenised asset or cryptocurrency], which asset did MSM match, on what basis and with what confidence? What does its available secondary-market evidence show, and what remains outside MSM's view?

**What MSM supplies:** Asset-resolution evidence such as `resolution_confidence`, plus available venue and liquidity observations.

**What your Agent adds:** Explanation of identity confidence and market limitations. A name-only match is not exact contract verification. For tokenised real-world assets, secondary-market data does **not** establish underlying reserves, custody, redemption rights or other off-chain backing.

## An extra question worth asking every time

> Which of these figures are provider-reported, what are their observation times, and which caveats should I carry into any conclusion?

**Remember:** Ask about an asset you care about, verify the proposed identity, and authorise any chargeable report before your Agent sends `CONFIRM`.

[Install the MSM Agent Skill](README.md) · [Developer Quickstart](https://www.mysellmate.digital/docs/developer-quickstart) · [MSM website](https://www.mysellmate.digital)
