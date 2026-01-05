# [KD-PL-001] - HLP Dynamic Pricing Algorithm

**DOCUMENT STATUS:** DRAFT

**IMPACT:** HIGH

**CONFIDENCE:** HIGH

**KNOWLEDGE DOMAIN(S):** Pricing, Revenue Management

**DATE:** 2026-01-05

**AUTHOR:** Manus AI

**REVIEWER(S):**

---

## 1. EXECUTIVE SUMMARY

The Hyper-Local Pulse (HLP) algorithm is PriceLabs' latest dynamic pricing engine, designed to provide more accurate and responsive pricing for short-term rentals (STRs). It represents a significant evolution from their previous model by leveraging hyper-local data sets, advanced demand forecasting, and a more nuanced approach to price elasticity. The core of HLP is its ability to define a unique competitive set for each property, analyzing 350 similar-sized listings within a dynamically determined radius of up to 15km. This allows the algorithm to capture micro-market trends, such as distinct seasonality and day-of-week patterns between neighborhoods just a few kilometers apart. The algorithm processes vast amounts of data, including scraped data from major OTAs (Airbnb, Vrbo, Booking.com) and direct data from partners like KeyData, to forecast demand and calculate the optimal price that maximizes expected revenue. While PriceLabs claims HLP can improve revenue by up to 9% over their old algorithm and new users see a 26% RevPAR boost, some user feedback on platforms like Reddit indicates mixed results, with some experiencing underpriced holidays and a need for more manual overrides. The system's strength lies in its data-driven, automated approach to capturing demand spikes and setting far-out and last-minute prices, but its effectiveness can vary by market and may still require active management and fine-tuning by the host.

## 2. HOW IT WORKS

The HLP algorithm is a multi-layered system that can be broken down into seven core components or "Unlocks":

1.  **Data Collection**: The process begins by gathering property-specific data (location, size, amenities, availability) from the connected PMS or OTA, and combining it with market-wide data scraped from over 10 million listings on Airbnb, Vrbo, and Booking.com. A key step here is a "block removal logic" that uses patterns and price anomalies to differentiate between actual bookings and owner-blocked dates on the scraped calendars [5].

2.  **Hyper-Local Compset**: This is the cornerstone of HLP. Instead of relying on broad city-level data, the algorithm defines a hyper-local market for each property. This compset consists of 350 similar-sized listings within a dynamically determined radius of up to 15km. This is achieved using Uber's H3 global grid system to efficiently query and analyze nearby properties in real-time, capturing unique neighborhood-level trends [10].

3.  **Demand Forecasting**: The algorithm forecasts future demand by analyzing historical booking curves. It selects relevant "reference dates" from the past based on seasonality, day-of-week, and event similarity. The forecast is then continuously refined using two key metrics: **Pacing** (current occupancy vs. historicals) and **Pickup** (the recent rate of new bookings) [10].

4.  **Demand Elasticity Modeling**: A crucial innovation is modeling demand as the "probability of getting booked" at various price points, rather than the number of units sold. The algorithm estimates a unique elasticity curve for each future date, considering the demand forecast and market price sensitivity. It recognizes that STR demand is complex, behaving as both elastic (for budget-friendly properties) and inelastic (for luxury properties) depending on the segment [9, 10].

5.  **Revenue Maximization**: The ultimate goal is to find the price that maximizes "Expected Revenue," calculated as `Price × Probability of Booking`. The algorithm identifies the optimal price point that balances the trade-off between a higher price and a lower booking probability [10].

6.  **Rate Evolution (Lead Time)**: Prices for a future date are not static; they evolve as the stay date approaches. The algorithm uses Dynamic Programming and the Bellman Equation to solve the complex problem of setting a sequence of optimal prices over time. This accounts for the changing probability of booking and the remaining booking opportunity, typically resulting in higher prices far out that discount as the date gets closer [3].

7.  **Market-Driven Defaults**: An industry-first feature exclusive to HLP, the system uses live market data (occupancy changes, pacing, booking velocity) to set dynamic, daily-updated defaults for last-minute and far-out pricing adjustments, reducing the need for manual configuration [1].

## 3. DATA INPUTS

The HLP algorithm is fueled by a combination of user-provided data and extensive market data.

| Data Category | Source | Details |
| :--- | :--- | :--- |
| **Listing Data** | User's PMS / OTA | Location, bedroom count, amenities, availability, base price, min/max price, customizations. [4] |
| **Market Data** | Scraped OTAs | Airbnb, Vrbo, Booking.com (over 10 million listings scanned). [10] |
| **Direct Data** | Partners | KeyData provides direct booking data. [5] |
| **Historical Data** | PriceLabs Internal | Historical booking curves, seasonality, and event data from all markets. [3] |
| **Competitor Data** | HLP Compset | Real-time pricing and availability of the 350-listing hyper-local compset. [10] |

## 4. PRICING GRANULARITY

The defining feature of the HLP algorithm is its granularity. It moves beyond city-level or even zip-code-level analysis to a truly hyper-local view.

-   **Compset Definition**: The algorithm identifies a compset of **350 similar-sized listings** for each property.
-   **Dynamic Radius**: This compset is found within a dynamically determined radius that can extend up to a **maximum of 15km**. The actual radius varies based on the density of similar properties in the area.
-   **Technology**: This is powered by **H3**, a geospatial indexing system developed by Uber, which allows for efficient and rapid querying of properties within specific hexagonal grid cells. This is a significant upgrade from their previous Ball Tree index system, enabling near real-time data updates [10].

This level of granularity allows the system to distinguish between micro-markets, such as the business-traveler-driven demand in Chicago's Loop versus the tourist-driven demand in nearby Lincoln Park (4km apart) [10].

## 5. ELASTICITY CALCULATION

PriceLabs has moved beyond a simple view of elasticity. Instead of a single elasticity value, the HLP algorithm acknowledges that price sensitivity varies significantly across the STR market.

-   **Probabilistic Approach**: Elasticity is not about how many units will sell, but the **probability of a single unit getting booked** at a certain price.
-   **Market Segmentation**: Through large-scale data analysis, PriceLabs has identified seven unique market segments, each with a different price elasticity. Some segments are highly elastic (a small price change causes a large drop in booking probability), while others are inelastic (price is less of a factor than quality or amenities) [9].
-   **Dynamic Assignment**: When a new property is onboarded, the system analyzes its attributes and its automatically assigned comp set to determine which of the seven elasticity segments it belongs to. This assigned elasticity profile then governs how the pricing model adjusts rates [9].
-   **Factors Influencing Elasticity**: The final elasticity curve for a given date is a function of the property's assigned segment, the overall demand forecast for that date, and the general price sensitivity of the market at that time (e.g., a ski town is less price-sensitive in winter than in summer) [10].

## 6. KEY STRENGTHS

-   **Hyper-Local Accuracy**: The use of a 350-listing, dynamically-sized compset (up to 15km) provides a level of market relevance that broader models lack, capturing unique neighborhood trends [10].
-   **Automated Event Detection**: The algorithm automatically detects demand spikes from known and unknown events by monitoring booking patterns, pacing, and competitor pricing, reducing the need for manual event pricing [6].
-   **Sophisticated Rate Evolution**: By using dynamic programming (Bellman Equation), the model optimizes the entire sequence of prices over a booking window, not just a single day's price, leading to reported revenue gains of ~9-11% [3].
-   **Data-Driven Defaults**: The "Market-Driven Defaults" for last-minute and far-out pricing are a unique feature that reduces host setup and adapts to live market conditions [1].
-   **Transparency**: PriceLabs provides significant documentation and technical deep dives into how their algorithm works, fostering user trust [10].

## 7. KEY WEAKNESSES

-   **Mixed User Feedback**: Despite company claims, real-world user feedback is mixed. Some hosts on Reddit report that the HLP algorithm underprices peak holidays and requires more manual overrides than the previous version [7].
-   **"Black Box" Risk**: While transparent in their documentation, the sheer complexity of the algorithm can make it difficult for the average user to understand why a specific price was recommended, leading to trust issues [7].
-   **Comp Set Dependency**: The accuracy of the pricing is highly dependent on the quality and relevance of the automatically generated 350-listing compset. If the compset is not truly representative, the pricing recommendations will be skewed.
-   **Cost**: Competitor analyses and user feedback note that PriceLabs is one of the more expensive tools on the market, which may be a barrier for smaller operators [8].

## 8. COMPETITIVE LANDSCAPE

The dynamic pricing space for STRs is competitive, with PriceLabs, Wheelhouse, and Beyond Pricing being the top three players.

| Feature | PriceLabs | Beyond Pricing | Wheelhouse |
| :--- | :--- | :--- | :--- |
| **Core Algorithm** | Hyper-local, elasticity segmentation, dynamic programming | Health Score based on seasonality, day of week, events | Externally validated model, 10B data points nightly |
| **Pricing Model** | Flat fee per listing (e.g., ~$19.99/mo in US) | Percentage of booking revenue (~1.25%) | Tiered, with % of revenue or flat fee options |
| **Key Differentiator** | Hyper-local compset, market-driven defaults, detailed analytics | Focus on a simple "Health Score" metric | Externally validated algorithm, strong UI/UX design |
| **Reported Weakness** | Can be complex, mixed user results on HLP | Most expensive, support is email-only | Limited PMS integrations and market coverage |

PriceLabs positions itself as the most data-intensive and customizable platform, appealing to professional revenue managers who want deep control. In contrast, Beyond focuses on simplicity with its "Health Score," and Wheelhouse emphasizes its externally validated model and user-friendly design [8].

## 9. UNANSWERED QUESTIONS & FURTHER RESEARCH

-   **HLP Granularity in Sparse Markets**: How does the HLP algorithm perform in rural or sparse markets where finding 350 similar listings within a 15km radius is impossible? How is the radius and compset size adjusted?
-   **Elasticity Segment Details**: What are the specific attributes of the seven price elasticity segments PriceLabs has identified? Understanding these would provide deeper insight into their model.
-   **"Market-Driven Defaults" Impact**: What is the quantifiable revenue impact of using the automated Market-Driven Defaults versus manually setting last-minute and far-out rules?
-   **User Override Rate**: What percentage of prices recommended by the HLP algorithm are manually overridden by users? This would be a key metric for algorithm confidence.

## 10. REFERENCES

[1] [PriceLabs Help: About Hyper Local Pulse (New Algorithm) and FAQ](https://help.pricelabs.co/portal/en/kb/articles/about-hyper-local-pulse-new-algorithm-and-faq)
[2] [PriceLabs Blog: Overview of PriceLabs' Dynamic Pricing Algorithm (Part 1)](https://hello.pricelabs.co/overview-of-pricelabs-dynamic-pricing-algorithm-part-1/)
[3] [PriceLabs Blog: Overview of PriceLabs' Dynamic Pricing Algorithm (Part 2)](https://hello.pricelabs.co/overview-of-pricelabs-dynamic-pricing-algorithm-part-2/)
[4] [PriceLabs Help: How Are the Price Recommendations Calculated?](https://help.pricelabs.co/portal/en/kb/articles/how-is-pricing-calculated)
[5] [PriceLabs Blog: Discover the science behind PriceLabs data and how it works](https://hello.pricelabs.co/science-behind-pricelabs-data/)
[6] [PriceLabs Help: How PriceLabs Handles Event Pricing?](https://help.pricelabs.co/portal/en/kb/articles/how-pricelabs-handles-event-pricing)
[7] [Reddit: r/airbnb_hosts - Pricelabs new hyperlocal algo much worse?](https://www.reddit.com/r/airbnb_hosts/comments/1i9f73p/pricelabs_new_hyperlocal_algo_much_worse/)
[8] [Wheelhouse Blog: Wheelhouse vs. Beyond Pricing vs. PriceLabs](https://www.usewheelhouse.com/blog/wheelhouse-vs-beyond-pricing-vs-pricelabs-a-pricing-tools-complete-comparison/)
[9] [Quibble Blog: Price Sensitivity for STRs](https://quibblerm.com/price-sensitivity-for-strs/)
[10] [PriceLabs Blog: Overview of PriceLabs' Dynamic Pricing Algorithm (Part 1)](https://hello.pricelabs.co/overview-of-pricelabs-dynamic-pricing-algorithm-part-1/)
