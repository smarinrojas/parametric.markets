# Parametric markets

## *abstract*

Parametric is a marketplace for fully collateralized parametric insurance alternative, where risk is priced by market forces, funded by liquidity providers, and settled automatically on-chain. Instead of relying on centralized insurers that privately maintain actuarial models, liquidity reserves, and claims control, Parametric replaces them with open market dynamics governed by smart contracts.

Each event or market represents a shared risk pool where two forces interact directly: users seeking protection and liquidity providers (LPs) competing to underwrite risk in exchange for yield. This competition is not purely financial—LPs bring their own probabilistic beliefs about the underlying event, contributing to a collective, on-chain intelligence that continuously updates prices through supply and demand.

Premiums evolve dynamically as a direct reflection of market sentiment. When demand for coverage rises faster than available collateral, premiums increase to attract new liquidity. Conversely, when LPs perceive the event as less likely and deploy more capital, premiums fall. Every policy is fully collateralized, ensuring solvency and eliminating counterparty risk by design.

Parametric transforms insurance from a trust-based, opaque system into an open, data-driven market where risk is priced transparently, executed automatically, and optimized collectively by the participants themselves.

## **What Is Traditional Insurance?**

At its core, insurance is a simple trade: you pay a small, predictable amount (Premium) today to avoid a potentially large, unpredictable loss in the future. It’s a mechanism for transferring risk.

Think of it like this:
You own a car. Every year, you pay an insurance company $500. In return, they promise that if your car is damaged in an accident, they’ll pay to repair it—maybe $10,000 or more.

You’re not paying because you expect the accident to happen; you’re paying to remove the uncertainty from your life. The insurer, on the other hand, collects premiums from thousands of drivers and uses statistical models (called actuarial models) to predict how many of them will crash. They profit when reality turns out slightly better than their predictions.

## **What Is a Parametric Insurance?**

Think of it as a weather trigger: if the gauge shows 100 mm of rain, you get paid - no adjusters needed.
Parametric insurance is a type of insurance that provides coverage for potential financial losses associated with a specific event, such as a natural disaster, a terrorist attack, or a political event. The coverage is based on a specific parameter, such as the amount of rainfall, the temperature, or the number of casualties, and the insurer compensates the insured based on the occurrence of the event and the value of the parameter.

## **Why Traditional Insurance Fails**

Misaligned incentives: Large incumbent insurers often have financial motives opposed to their policyholders; their profits frequently depend on avoiding claim payouts, leaving the insured at a disadvantage.

High overhead and bureaucracy: Heavy regulation and layered corporate processes create substantial administrative drag, inflating premiums.

Opacity and power imbalance: Centralization brings lack of transparency. Policies and payout criteria are often unclear; users face a "David vs. Goliath" scenario.


## **What are the advantages of blockchain in insurance?**

Blockchain-based insurance systems replace opacity with transparency, and centralized risk management with collective resilience.
Because policies, funds, and claims are all on-chain, anyone can verify solvency, terms, and historical behavior in real time.

Moreover, decentralized models can:

Ensure full collateralization, so every policy is backed by real, verifiable funds.

Enable instant, automated payouts through smart contracts.

Distribute exposure dynamically, allowing LPs to enter or exit markets freely.

Create risk-sharing ecosystems that adapt to real-world data, not rigid actuarial tables.

Even in extreme conditions — when traditional insurers freeze — blockchain systems continue to operate as long as the network runs. That’s resilience by design.

## **Black Swan Resilience**

In a black swan scenario, the difference between centralized and decentralized systems becomes clear.

Traditional insurers depend on trust and liquidity reserves that vanish under stress. Blockchain insurance, on the other hand, depends on mathematical guarantees and on-chain collateral, not corporate promises.

Every policy is fully backed, not leveraged.

Every payout is programmatically executed, not “reviewed.”

Every participant shares risk transparently, making the system antifragile — it learns and rebalances as new data emerges.

Where traditional insurance collapses under uncertainty, blockchain-based systems can absorb shocks and evolve, turning volatility into a mechanism for long-term stability.



## **Flight Delay/Cancel Insurance Markets**




### **Definition of cancellation/delay**




## **Why Full Collateralization?**




## **Baseline Probability (`P_hist`): A High-Granularity Actuarial Model**

The initial pricing for any market/event is determined by its baseline probability, `P_hist`. A core principle of Parametric is that risk pricing must be precise. Using a broad, generic average for flight delays would be simple but highly inaccurate. Instead, the protocol employs a high-granularity actuarial model that segments historical data across four key vectors: **route, airline, month, and day of the week.**

This methodology is standard in predictive modeling, where identifying the most influential variables is crucial for forecasting accuracy. Research in aviation analytics consistently confirms that these factors are among the most significant predictors of flight performance. The justification for each criterion is as follows:

*   **Route (Origin-Destination):** Different airports have vastly different operational complexities, traffic volumes, and susceptibility to weather. A route between two major, congested hubs like Newark (EWR) and San Francisco (SFO) carries an inherently different risk profile than a route between two smaller, regional airports. This makes the specific route the most fundamental data segment.

*   **Month (Seasonality):** Aviation performance is deeply affected by seasonality. Industry data consistently shows that summer months like June, July, and August have the highest rates of delays, driven by increased holiday travel volume and a higher frequency of convective weather events like thunderstorms. Conversely, winter months can be impacted by snowstorms and de-icing procedures, while autumn months like September and October often see the best on-time performance due to milder weather and lower travel demand.

*   **Day of the Week:** Air traffic volume is not uniform throughout the week. Peak travel days, typically Thursdays and Fridays, experience higher congestion. This creates a fragile operational environment where an initial delay can trigger a "ripple effect," causing a cascade of subsequent delays throughout the day. In contrast, mid-week days like Tuesdays and Wednesdays generally see lighter traffic and, consequently, better on-time performance.

*   **Airline:** Each airline maintains unique operational models, hub locations, fleet types, and maintenance schedules. An airline's policies regarding crew scheduling and its operational footprint at delay-prone hubs significantly influence its performance statistics. Therefore, segmenting by carrier is essential to capture these operator-specific risk profiles.

By tracking data at this granular level, the protocol avoids the pitfalls of generalized averages and establishes a baseline probability (`P_hist`) that accurately reflects the specific, recurring risk patterns associated with a given flight. This precise foundation is critical before the market dynamics of `P_dyn` are introduced.

## **Historic Probability Based on Regions**

When a route–month–weekday combination is first encountered, the system lacks live data. In this case, the initial event probability is derived solely from historical delay/cancellation records using a **Bayesian Beta-Bernoulli model**:


Each region maintains a historical delay probability, stored in a detailed record that considers both the month and the day of the week for each route, airport, and airline. This high-granularity approach is deliberately chosen, as industry data confirms that delay patterns are not only seasonal but also vary significantly depending on the day of the week.

https://norma.ncirl.ie/7521/1/aniketguru.pdf

https://upgradedpoints.com/news/airports-most-summer-flight-delays/

https://www.hrpub.org/download/20171130/UJM3-12110417.pdf

https://norma.ncirl.ie/7521/1/aniketguru.pdf

Tracking data at this level allows the system to capture specific, recurring patterns with greater accuracy. For example, summer months like June, July, and August consistently show the highest average delays due to increased holiday travel volume and more frequent convective weather events like thunderstorms. In contrast, autumn months such as September and October tend to have better on-time performance. Furthermore, data indicates that midweek days like Tuesday and Wednesday generally experience fewer delays compared to high-traffic days like Friday, which are popular for weekend travel. This methodology is standard in predictive modeling, where variables like month and day of the week are crucial for forecasting accuracy.

The contract tracks this history of delays and cancellations, adjusting the internal probability parameter  𝑝  for each segment (month and day of the week) based on new observations. As flights are resolved, the system updates these probabilities using a Bayesian Beta-Bernoulli model, ensuring that estimates evolve with the real-world performance of each specific time segment.

In line with the law of large numbers, as more flight outcomes are observed for a specific segment, its estimated probability  𝑝  will converge toward the true underlying delay probability for that period. However, since each new market segment starts with an initial prior of 50%, the early premiums will be relatively expensive until sufficient data accumulates.

### Bayesian Update

$$
P_{hist} = \frac{\alpha + D}{\alpha + \beta + N}
$$

Where:

* **D** = Number of delayed flights observed for that segment
* **N** = Total number of flights observed for that segment
* **α, β** = Prior parameters representing delayed/on-time weights (initialized to 1:1 → prior of 50%)

The contract maintains a historical record broken down by month and day of the week for each route and airline. This record is updated with the Beta-Bernoulli model so that:

Each market segment (e.g., "Mondays in January," "Saturdays in August") starts at  𝑝=50 .
Initial premiums for each segment are therefore more expensive.
Over time, probabilities adjust with high precision to the real-world market behavior for each specific day and season.

### **Information Decay & Temporal Relevance**

While historical probability (`P_hist`) provides a strong statistical foundation, its predictive power naturally declines as time passes without new data. Infrequently traded markets—or those representing rare or seasonal events—can experience **information staleness**, where the underlying probability no longer reflects current real-world conditions. For example, if no new flight data has been observed for a specific *route–month–weekday* segment in several months, operational changes, new airline schedules, or shifts in weather patterns may render older statistics less reliable.

To mitigate this degradation, the protocol introduces a **time-based decay factor**, ensuring that outdated data gradually loses influence unless refreshed by new observations or market activity. The adjusted historical probability evolves as:

$$
P_{adj} = P_{hist} \times e^{-\lambda \cdot \Delta t}
$$

Where:

* **Δt** = elapsed time (in days or weeks) since the last observed data update for that market segment.
* **λ** = decay constant controlling how quickly older information loses weight.

* Higher λ → faster decay (short-lived relevance).
* Lower λ → slower decay (long-term stability).

This mechanism models the **natural erosion of statistical confidence** over time, producing smooth and continuous decay rather than abrupt resets. It also encourages ongoing participation: active markets (with new trades or flight outcomes) automatically maintain data freshness, while inactive ones gradually lose predictive influence until revalidated by new data.

In practical terms:

* Markets with **frequent observations** (e.g., major routes or daily flights) retain high informational accuracy.
* Markets with **low liquidity or rare events** slowly decay, prompting Liquidity Providers (LPs) to re-evaluate their risk exposure.

This dynamic allows the system to self-regulate informational quality, balancing **historical accuracy** with **temporal relevance** — a key requirement for decentralized actuarial modeling.


## Dynamic Premium Adjustment via Market Sentiment

While historical data (P_hist) provides a robust baseline for establishing insurance markets based on past cancellation and delay records, the real world is significantly more dynamic. This inherent dynamism means that P_hist alone is often insufficient to adapt to rapidly evolving market conditions. Events such as adverse weather forecasts, unforeseen air traffic control issues, or critical airline-specific news can significantly alter the real-world probability of a delay, necessitating a more responsive pricing mechanism. Crucially, this real-time information, accessible to both travelers (policy purchasers) and Liquidity Providers (LPs), can profoundly influence their behavior, prompting increased demand for policies or adjustments in the supplied liquidity, respectively.

To capture this market sentiment and enable efficient prime price discovery, we introduce a Dynamic Premium Model. This model adjusts the probability an therefore the premium, based on the real-time supply and demand for insurance coverage on the platform, drawing inspiration from the Logarithmic Market Scoring Rule (LSMR) utilized in decentralized prediction markets like Polymarket. The core principle is that the premium for a new policy should rise when demand from travelers outpaces the supply of capital from Liquidity Providers (LPs), and fall as the market stabilizes, reflecting the collective market belief about the likelihood of the insured event.


### **Dynamic Price Discovery via a Logarithmic Market Scoring Rule (LMSR)**

While historical data (`P_hist`) provides a robust actuarial baseline, it is inherently backward-looking and incapable of reacting to immediate, real-world variables, such as adverse weather forecasts, air traffic congestion, or critical airline-specific news. To address this, Parametric transforms each per-event insurance market into a live prediction market, powered by a Logarithmic Market Scoring Rule (LMSR) engine.

This transforms passive capital provision into an active risk assessment mechanism. Liquidity Providers (LPs), motivated by yield, incorporate their own research into their decision to provide collateral. Their collective actions, balanced against the demand from travelers, create a dynamic price (`P_dyn`) that reflects the market's real-time, capital-weighted sentiment.

#### **The Mechanism: Logarithmic Market Scoring Rule (LMSR)**

Borrowed from the architecture of successful prediction markets, the LMSR is an automated market maker designed for information aggregation. Its core function is to maintain a cost function that makes it progressively more expensive to move the probability of an outcome as it approaches the extremes of 0% or 100%. This ensures that a strong market consensus requires significant capital to shift, reflecting high conviction.

The cost of purchasing a set of outcome shares is determined by the formula:

$$
C(q_1, q_2) = b \cdot \ln(e^{q_1/b} + e^{q_2/b})
$$

Where:
*   `q₁` and `q₂` are the quantities of shares outstanding for each outcome (e.g., "Delay" and "On-Time").
*   `b` is a liquidity parameter that controls the market's depth. A higher `b` value results in lower price sensitivity to trades.

From this cost function, the instantaneous price for an outcome—which represents the market's current probability—is derived:

$$
P_{dyn}(\text{Delay}) = \frac{e^{q_{\text{Delay}}/b}}{\sum_{j} e^{q_j/b}}
$$

This price, `P_dyn`, is what determines the premium.

#### **Market Dynamics: How Supply and Demand Shape the Price**

The brilliance of the LMSR is in how it interprets market actions. In our ecosystem, the two primary forces are travelers seeking coverage and LPs providing collateral.

1.  **Demand (Policy Requests → Price Increases):**
    When a traveler purchases a policy, they are effectively buying shares in the "Delay" outcome. This action increases the outstanding quantity of `q_Delay`. According to the price formula, increasing `q_Delay` while `q_On-Time` remains constant will **increase the price (`P_dyn`)**. This elegantly models the economic principle that rising demand, with supply held constant, leads to a higher price. The protocol correctly interprets this activity as a signal that the market believes the event is becoming more likely.

2.  **Supply (Liquidity Provision → Price Decreases):**
    When an LP provides collateral to underwrite a policy, they are expressing confidence that the event will *not* occur in order to earn the premium. This action is equivalent to buying shares in the "On-Time" outcome. This increases the quantity of `q_On-Time`. According to the price formula, increasing `q_On-Time` while `q_Delay` remains constant will **decrease the price (`P_dyn`)**. This models the principle that rising supply leads to a lower price. The protocol interprets this as a signal of growing market confidence that the event is less probable.

In essence, `P_dyn` is the live equilibrium between the capital flowing in to purchase protection and the capital flowing in to underwrite that protection. This transforms the premium from a static, predetermined number into a dynamic indicator of collective intelligence, continuously updated with every market action.


### **Initializing the LMSR with Historical Probability (`P_hist`)**

Before a market can operate dynamically, it requires an initial probability anchor. This anchor, `P_hist`, derived from the Bayesian historical model, represents the protocol’s prior belief about the likelihood of the event (e.g., a flight delay). The Logarithmic Market Scoring Rule (LMSR) then initializes its internal state based on this baseline, ensuring price continuity between actuarial estimation and live market trading.

### **Mathematical Initialization**

The LMSR operates on *quantities of shares* (`q_i`) representing each outcome. To align the initial LMSR prices with the pre-existing `P_hist`, the initial share quantities are set such that the implied LMSR price equals `P_hist`.

From the LMSR price equation:

$$
P(\text{Delay}) = \frac{e^{q_{\text{Delay}}/b}}{e^{q_{\text{Delay}}/b} + e^{q_{\text{On-Time}}/b}}
$$

Solving for the share quantities that reproduce `P_hist`, we set a symmetric baseline centered around 0:

$$
q_{\text{Delay}} = b \cdot \ln(P_{hist})
$$
$$
q_{\text{On-Time}} = b \cdot \ln(1 - P_{hist})
$$

This initialization ensures that:

$$
P_{dyn}(\text{Delay}) = P_{hist}
$$

### **Interpretation**

1. **Smooth Transition:**
   The LMSR starts at the same probability estimated by the actuarial model. This avoids discontinuities between the “data-driven” phase and the “market-driven” phase.

2. **Calibrated Liquidity Depth:**
   The liquidity parameter `b` determines how resistant the price is to early trades. A higher `b` makes the initial probability harder to move, appropriate for mature markets with strong historical data. A lower `b` makes the market more responsive, suitable for emerging or low-data segments.

3. **Unified Probability Evolution:**
   Once initialized, the LMSR continuously updates the market price `P_dyn` as traders interact. Over time, `P_dyn` reflects both the long-term statistical baseline (`P_hist`) and the short-term sentiment signals encoded in market activity.

In essence, this mechanism fuses actuarial modeling with decentralized market dynamics. The Bayesian `P_hist` defines where the story begins — the LMSR defines how it evolves.

## **Architecture: Per-Event Liquidity Markets vs. Aggregated Pools**

Parametric's architecture is defined by a foundational decision: the use of **per-event liquidity markets** instead of aggregated liquidity pools. Each insurable event, such as a specific flight, operates as a self-contained, fully-collateralized micro-market. This design is not an incremental improvement but a structural shift that offers the following strategic advantages:

1.  **Guaranteed Solvency and Absolute Risk Isolation.**
    In an aggregated pool, a single catastrophic event can drain the entire system, rendering it insolvent (socialized risk). Our model isolates risk: capital required to cover a specific flight is locked within its own smart contract. The outcome of one market has no financial impact on any other, eliminating systemic risk and cryptographically guaranteeing every payout.

2.  **Efficient, Real-Time Price Discovery.**
    Aggregated pools use static, averaged pricing. Our per-event markets function as live prediction markets. Traveler demand for coverage increases the premium (`P_dyn`), signaling higher risk. Capital from LPs supplying coverage decreases it, signaling confidence. This mechanism ensures the price reflects not only historical data (`P_hist`) but all available real-time information.

3.  **Incentive Alignment and Capital Efficiency.**
    This model transforms passive LPs into active **risk underwriters**. Profitability is directly tied to the accuracy of their risk assessment on each individual market. This is inherently more capital-efficient: funds are deployed and locked only to underwrite a specific, active risk, rather than sitting idle in a large pool to cover uncorrelated potential events.



### Incentive Alignment and Capital Efficiency

This model creates a powerful incentive alignment between the protocol and its LPs. They are not passive yield farmers; they are active underwriters whose profitability is directly tied to the accuracy of their risk assessments. This fosters a competitive environment where capital is allocated with diligence and precision, rewarding participants who best model the probability of events.
Furthermore, this approach is inherently more capital-efficient. Instead of maintaining a large pool of idle capital to cover tail-risk scenarios, capital is deployed and locked only when it is needed to underwrite a specific risk. This allows LPs to earn higher returns on active capital and maintains the overall health of the ecosystem by disincentivizing the funding of mispriced risks.
In conclusion, the decision to build Parametric around per-policy underwriting markets is fundamental to our vision. It moves beyond the simple automation of insurance to create a truly decentralized, market-driven system where risk is intelligently priced in real-time, capital is deployed efficiently, and the solvency of every contract is guaranteed.

### **Premium Calculation and Economic Model**

The premium is the price a traveler pays for protection. The architecture of this premium is designed to achieve two critical goals simultaneously:
1.  Reflect the true, market-assessed risk of the event in real time.
2.  Provide a built-in, positive expected value for Liquidity Providers (LPs) to compensate them for providing capital and assuming risk.

The process begins with determining the market's probability of the event, `p`.

$$
p =
\begin{cases}
P_{hist}, & \text{if the market is new}\\
P_{dyn}, & \text{if the market is active}
\end{cases}
$$

#### **Premium Structure: The Three Components**

The final price paid by the traveler is composed of the pure risk cost plus a margin, from which the protocol then takes its fee. This structure ensures transparency and aligns all incentives.

**1. Base Risk Premium:**
This represents the actuarially fair price of the risk transfer, based on the market's probability `p`. It is the expected loss for the underwriter.

$$
\text{Premium}_{\text{Base Risk}} = p \times \text{Payout}
$$

**2. LP Margin & Total Traveler Premium:**
To ensure LPs are incentivized to provide liquidity, a fixed percentage margin (`LP Margin`) is added to the Base Risk Premium. This margin is the LP's built-in compensation for their service—the opportunity cost of their capital and their willingness to assume risk. The sum of these components constitutes the total, all-in premium paid by the traveler.

$$
\text{Premium}_{\text{Traveler}} = \text{Premium}_{\text{Base Risk}} \times (1 + \text{LP Margin})
$$

**3. Distribution: LP Pool vs. Protocol Revenue:**
This `Premium_Traveler` is then distributed between the LPs and the protocol treasury. The protocol takes its fee as a percentage of this total, and the remainder is deposited into the market's premium pool to reward the LPs.

$$
\text{Premium}_{\text{LP Pool}} = \text{Premium}_{\text{Traveler}} \times (1 - \text{Protocol Fee})
$$

$$
\text{Protocol Revenue} = \text{Premium}_{\text{Traveler}} \times \text{Protocol Fee}
$$

#### **Ensuring a Positive Expected Value for LPs**

This economic model is designed to be fundamentally attractive to capital providers. The Expected Value (EV) for an LP is no longer a zero-sum game but is structurally positive.

The EV for an LP underwriting a portion of the risk is:

$$
\text{EV}_{\text{LP}} = \text{Premium}_{\text{LP Pool}} - (p_{\text{real}} \times \text{Payout})
$$

Where `p_real` is the LP's private, expert assessment of the event's true probability.

Crucially, due to the `LP Margin` embedded in the premium, an LP's EV is positive **even if they believe the market is perfectly priced** (i.e., `p_real = p`). This built-in profit ensures there is always a baseline incentive to provide collateral.

This creates a dual-alpha opportunity for sophisticated LPs:
1.  **Baseline Alpha:** Earning the non-speculative, guaranteed `LP Margin` for providing the essential service of liquidity.
2.  **Speculative Alpha:** Generating additional returns by identifying markets where they believe the dynamic price is an overestimation of the true risk (`p_dyn > p_real`).

This model ensures the traveler pays a transparent market price, the protocol earns a sustainable fee, and the LPs—the engine of the protocol—are properly and structurally compensated for their critical role.