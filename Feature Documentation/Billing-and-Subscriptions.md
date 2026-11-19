# Billing and Subscriptions

| Field | Details |
|---|---|
| User roles | Customer / advertiser and Host / screen owner |
| Application route | `/subscriptions` |
| Existing wiki/Jira mapping | Subscriptions and Plans [IA-262](https://insta-ad.atlassian.net/browse/IA-262), Plans and Pricing [IA-263](https://insta-ad.atlassian.net/browse/IA-263), plan selection [IA-264](https://insta-ad.atlassian.net/browse/IA-264), pricing decision [IA-272](https://insta-ad.atlassian.net/browse/IA-272), plan limits [IA-288](https://insta-ad.atlassian.net/browse/IA-288), subscription lifecycle [IA-275](https://insta-ad.atlassian.net/browse/IA-275), payments and billing [IA-213](https://insta-ad.atlassian.net/browse/IA-213), recurring billing/invoices [IA-292](https://insta-ad.atlassian.net/browse/IA-292), Host payouts [IA-250](https://insta-ad.atlassian.net/browse/IA-250); role context is in [Customer flow](./User-Account-Customer-Flow.md) and [Host flow](./User-Account-Host-Flow.md) |
| Application review | 2026-11-16 |
| Status | Current application UI documented; offers and payment workflows not verified |

## 1. Purpose

The Subscriptions page presents advertiser plans and screen-owner offers. The page copy describes campaign publishing plans and ways for screen owners to monetize display inventory. No plan was selected and no payment was made during review.

The advertiser Basic subscription lets the Customer select up to **10 devices/screens in one selected Ort** (locality/municipality), with a monthly per-screen price based on city-area tier. The supplied Kleinostheim low-tier example is **€60 per screen/month**, or **€600/month for 10 screens**. Aschaffenburg mid-tier and Berlin/Frankfurt high-tier amounts remain to be set. This is a Customer entitlement, not a limit on the number of screens a Host may own, register or list. Premium and other higher-plan geographic coverage and pricing (including Bavaria-wide and Germany-wide targeting) still need definition. See [Resource Management and Monetization](./Resource-Management-and-Monetization.md) for the targeting examples and unresolved rate card.

The rollout proposal waives Customer application-use/subscription fees for the first release and first-100 Customer cohort, with expansion from the first pilot to 10 Customers after successful process validation. The precise waived fees, duration, eligibility and payment treatment still require approval. This does not make campaign bookings free unless separately approved.

Host type 1 has a separate, not-yet-priced monetization choice: (1) a booking-fee route where InstaAd receives an agreed X% of each successful slot booking, or (2) a recurring application-use subscription paid regardless of booking volume, with no InstaAd booking fee. The Host chooses one route; the charges are not combined. The Host subscription fee is not curated yet and will be set after a trial with the first 100 eligible users. This Host pricing trial is distinct from the first-100 Customer application-fee waiver. See [Resource Management and Monetization](./Resource-Management-and-Monetization.md) for fee separation, cohort data and open decisions.

## 2. Subscription selection workflow

The app shows plans and actions to choose/manage a plan. The purchase and entitlement flow was not tested.

```mermaid
flowchart TD
    A[Activated account] --> B[Open Subscriptions]
    B --> C{Choose audience}
    C -->|Advertiser| D[Review campaign plan]
    C -->|Screen owner| E[Choose booking-fee route or application subscription]
    D --> F[Choose Plan]
    E --> G[View chosen Host fee route and applicable terms]
    F -. checkout and entitlement flow to verify .-> H[Plan active]
    G -. enrollment and payout flow to verify .-> H
```

```text
+------------------------------------------------------------------+
| Subscriptions & Offers                                           |
| Advertiser Plans             Screen Owner Offers       Growth Ready|
+------------------------------------------------------------------+
| Advertiser Basic                                                 |
| Up to 10 screens in one Ort · locality-tiered price/screen/month |
| Kleinostheim low tier: €60/screen/month; €600 for 10 screens     |
| Premium reach: categories/regions/countrywide - terms TBD         |
| 1 active campaign · 1 media asset · 1 play/hour                  |
| Daily 09:00-17:00 · basic targeting/reporting   [Choose Plan]    |
+------------------------------------------------------------------+
| Host type 1 fee routes (separate from advertiser plan)            |
| Booking fee: X% per successful booking OR application subscription|
| Subscription price TBD after first-100-user trial; not both fees  |
+------------------------------------------------------------------+
```

This is a schematic summary of the documented business model, not a verified current app rate card. An earlier app review showed a flat €50/month Starter Campaign card; that observed UI copy conflicts with the locality-tiered Basic pricing model documented here and must not be treated as the current approved rate card. Update/verify the application plan display before launch. The exact Aschaffenburg and Berlin/Frankfurt rates, other locality tiers, Premium entitlements and purchase/enforcement behavior remain unverified.

## 3. Advertiser plan shown

The advertiser Basic subscription is for campaign publishers and allows the Customer to select up to **10 screens in one selected Ort**. The per-screen monthly price is locality-tiered. The supplied low-tier Kleinostheim example is **€60 per screen/month**, so 10 screens cost **€600/month**. Aschaffenburg is a mid-tier example and Berlin/Frankfurt are high-tier examples, but their prices and the full locality mapping are TBD.

Customers may want broader plan-based audience coverage, such as all businesses in Kleinostheim, bakeries in Aschaffenburg, shoe shops and gyms across Bavaria or Germany, or all Germany. Do not promise that these are available under Basic: map each geographic reach/category option to Basic, Pro, Premium or other plans and confirm their screen caps and prices. The plan card also displayed the following campaign features/limits:

- Up to one active campaign
- Up to one uploaded media asset
- One play per hour
- Daily playback window 09:00–17:00
- Basic location targeting
- Standard time-slot scheduling
- Basic campaign reporting

The 10-screen/one-Ort cap and Kleinostheim example are the documented Basic proposal; the other plan details are displayed UI copy. Rate-card values outside the supplied example, geographic plan entitlements, enforcement and purchase flow are not independently verified.

## 4. Screen-owner offers shown

Screen-owner monetization is separate from the advertiser's Basic subscription. Basic's up-to-10-screen one-Ort limit is for the advertiser's selected ad-placement devices and does **not** establish a Host screen registration or ownership limit.

For Host type 1, the product model has two alternative fee routes:

- **Booking-fee route:** InstaAd receives X% of each successful slot booking. The Host does not also pay an application subscription on this route. The percentage is TBD.
- **Application-subscription route:** the Host pays a recurring application-use fee regardless of whether bookings occur. InstaAd does not charge a booking fee on this route. The subscription price is TBD until the first-100-user trial is evaluated.

The Host chooses one route, and the app must disclose which route is active. Do not present the Host application subscription as a booking fee or combine it with the booking percentage. The page also displayed these separate offer descriptions:

- **Screen Owner Pro:** priority campaign allocations, earnings dashboard, and payout insights
- **Network Partner:** intended for malls, co-working hubs, and transport networks with high-traffic screens

No complete pricing or enrollment workflow for the Pro and Network Partner offers was verified.

## 5. Relationship to other app workflows

- Advertiser plans relate to campaign and media use in [Advertiser Campaigns and Media](./Advertiser-Campaigns-and-Media.md).
- Screen-owner offers relate to screen registration in [Host Screen Management](./Host-Screen-Management.md).
- Host payout and tax requirements remain in the [Host flow](./User-Account-Host-Flow.md), including the planned Host verification gate.
- The shared proposed subscription, slot, booking-revenue and fixed-rent model is in [Resource Management and Monetization](./Resource-Management-and-Monetization.md).

The presence of plan cards does not establish that checkout, subscription entitlement enforcement, ad playback limits, earnings calculation, or payouts work end to end.

## 6. Existing Jira mapping and gaps

| Application feature | Existing related Jira reference | Scope note |
|---|---|---|
| Advertiser Basic: up to 10 devices in one Ort at locality-tiered monthly per-screen prices | [IA-263](https://insta-ad.atlassian.net/browse/IA-263), pricing decision [IA-272](https://insta-ad.atlassian.net/browse/IA-272), plan selection [IA-264](https://insta-ad.atlassian.net/browse/IA-264), and entitlement enforcement [IA-288](https://insta-ad.atlassian.net/browse/IA-288) | Kleinostheim low-tier example €60/device/month (€600/month for 10); Aschaffenburg mid-tier and Berlin/Frankfurt high-tier prices are TBD. This Customer limit is not a Host inventory cap. |
| Basic-to-Premium geographic and category targeting | Campaigns/media [IA-517](https://insta-ad.atlassian.net/browse/IA-517), plan catalog [IA-263](https://insta-ad.atlassian.net/browse/IA-263), pricing decision [IA-272](https://insta-ad.atlassian.net/browse/IA-272), plan selection [IA-264](https://insta-ad.atlassian.net/browse/IA-264) | Map locality, business-category, Bavaria-wide and Germany-wide coverage to plan tiers and prices; don't promise coverage until entitlement rules are approved. |
| Host type 1 fee route choice and trial pricing | Slot monetization [IA-520](https://insta-ad.atlassian.net/browse/IA-520), plan/pricing [IA-263](https://insta-ad.atlassian.net/browse/IA-263), decision [IA-272](https://insta-ad.atlassian.net/browse/IA-272), and payout [IA-250](https://insta-ad.atlassian.net/browse/IA-250) | Host chooses X% per successful booking or a fixed recurring application subscription with no booking fee; trial the first 100 eligible users before setting the subscription price. Never charge both routes together. |
| Plans and subscription catalog | [IA-262](https://insta-ad.atlassian.net/browse/IA-262), [IA-263](https://insta-ad.atlassian.net/browse/IA-263), [IA-264](https://insta-ad.atlassian.net/browse/IA-264), [IA-268](https://insta-ad.atlassian.net/browse/IA-268) | Existing plan/catalog scope. Purchase and entitlement enforcement have not been independently verified. |
| Subscribe, lifecycle, entitlement and recurring billing | [IA-275](https://insta-ad.atlassian.net/browse/IA-275), [IA-276](https://insta-ad.atlassian.net/browse/IA-276), [IA-287](https://insta-ad.atlassian.net/browse/IA-287), [IA-292](https://insta-ad.atlassian.net/browse/IA-292) | Existing implementation scope. No purchase, renewal, cancellation, entitlement, or invoice workflow was tested in the app. |
| Checkout and payment methods | [IA-213](https://insta-ad.atlassian.net/browse/IA-213), [IA-215](https://insta-ad.atlassian.net/browse/IA-215), [IA-226](https://insta-ad.atlassian.net/browse/IA-226) | Related existing payment and checkout issues; the visible Settings controls do not establish that these flows work end to end. |
| Host rental payments, earnings and payouts | [IA-255](https://insta-ad.atlassian.net/browse/IA-255), [IA-250](https://insta-ad.atlassian.net/browse/IA-250), [IA-251](https://insta-ad.atlassian.net/browse/IA-251) | Existing Host payment/payout requirements. Screen-owner offers and payout behavior were not verified. |

These are related existing Jira issues; their existence does not confirm that app plan selection, checkout, entitlements, invoices, or payouts work end to end. No additional billing feature was created.

## 7. Related documentation

- [Advertiser Campaigns and Media](./Advertiser-Campaigns-and-Media.md)
- [Host Screen Management](./Host-Screen-Management.md)
- [User Account Host Flow](./User-Account-Host-Flow.md)
- [User Account Customer Flow](./User-Account-Customer-Flow.md)
