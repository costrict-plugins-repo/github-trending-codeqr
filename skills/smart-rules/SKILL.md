---
name: smart-rules
description: Route a CodeQR short link to different destinations by device, country, city, region, continent, language, referrer or UTM parameter, or split its traffic between 2 to 4 destinations for an A/B test. Use when the person wants iPhone and Android visitors sent to different app stores, a page per country or language, a split test of landing pages, the results of a test, or to end a running test.
---

# Smart rules and A/B splits

Smart rules are the `rules` field of `create_link` and `update_link`. They are not enabled on every workspace, and where they are not, the API refuses the whole call: say so and offer the link without rules.

Every destination must be a real address from the person. Ask for any you do not have.

## How rules are read

- Rules are checked in order, and the first one that matches wins. A visitor who matches none goes to the link's own `url`.
- A condition is `attribute`, `operator` (`equals` or `not_equals`) and `value`, always all three together.
- Each rule sends its traffic either to one `url` or to a `split` of 2 to 4 `{ "url", "weight" }` variants whose weights add up to exactly 100, never both.
- A rule with no condition matches everyone, so it must be the last rule and it must split.

## Values that match

Values are compared whole and without regard to case. A value outside these sets is saved without an error and then never matches:

- `device` is the operating system: `iOS`, `Android`, `Windows`, `Mac OS` or `Linux`. "mobile" and "desktop" match nothing.
- `country` and `continent` are two-letter codes (`BR`, `US`; `SA`, `EU`, `NA`). `region` is the ISO 3166-2 short code (`SP`, `CA`), never the state's name. `city` is the city's name.
- `language` is one of `pt`, `en`, `es`, `fr`, `de`, `zh`, `ru`, `it`, `ja` or `ko`.
- `referrer` is the bare domain, such as `google.com`, never a full URL.
- `utm_source`, `utm_medium`, `utm_campaign`, `utm_term` and `utm_content` match the value on the incoming link.

## Patterns

App store by operating system, everyone else to the link's `url`:

```json
"rules": [
  { "attribute": "device", "operator": "equals", "value": "iOS", "url": "<App Store page>" },
  { "attribute": "device", "operator": "equals", "value": "Android", "url": "<Google Play page>" }
]
```

A/B test of two pages, half the traffic each:

```json
"rules": [
  { "split": [ { "url": "<page A>", "weight": 50 }, { "url": "<page B>", "weight": 50 } ] }
]
```

A visitor keeps the same variant for one hour, or for 30 days when the link has `trackConversion` on.

## Results and ending a test

- Each click is recorded with the variant it was sent to, so `get_analytics` with the `linkId`, `event: "clicks"` and `groupBy: "top_urls"` gives clicks per variant. With conversion tracking on, `event: "leads"` or `"sales"` compares what each variant produced.
- To end a test and send everyone to the winner, call `update_link` with the winner as `url` and `rules: null`.
