# Building the Foundation: How I Mapped the Data Landscape of MyOnlineShop
As a data analytics intern stepping into the fast-paced world of e-commerce, the first week can feel overwhelming. At MyOnlineShop, a burgeoning multi-category platform targeting urban Nigerians with fashion, fresh food, and electronics, Week 1 is designed to build a solid foundation. This isn't just about learning SQL or crunching numbers; it's about weaving data into compelling stories that drive business decisions. Drawing from real internship experiences (inspired by actual program briefs and data schemas), this guide breaks down the Week 1 tasks step by step. I'll explain the "what," "how," and crucially, the "why" behind each, showing how these activities transform raw data into narratives revealing customer behaviors, operational efficiencies, and growth opportunities.

As an expert in data storytelling, I'll frame this as the crucial foundation for a successful internship, turning novices into strategic analysts.


<h2>Executive Summary</h2>
The Week 1 brief requires you to: 
<ul>
<li>understand the business and product</li>

<li>define ten high-value metrics</li>

<li>design an Entity-Relationship Diagram (ERD) mapping customers, products, orders, and transactions.</li>
</ul>
This step-by-step playbook not only details what to do but why each step matters, with ties to the provided SQL schema for computability.


<h2>Step 1: Reviewing Product Documentation – Building Business Context</h2>
Start by immersing yourself in MyOnlineShop's core documentation, which outlines the platform's mission, problems solved, and goals. For example, urban Lagos dwellers face fragmented shopping, unreliable deliveries, and authenticity issues. MyOnlineShop addresses this with a unified platform, personalized recommendations, next-day Lagos delivery, secure payments (including a wallet system), and easy returns.

To review effectively:
<ul>
<li>Read Actively: Skim key sections like "Product Overview," "Problems," "Solutions," and "Goals." Note pain points (e.g., vendor searches) and solutions (e.g., personalization).</li>

<li>Map to Competitors: Compare with Jumia or Konga. MyOnlineShop stands out via local sourcing for fresh food and mobile-first UX.</li>

<li>Extract Metrics and KPIs: Highlight goals like 95% customer satisfaction (CSAT), 15% AOV increase, and 60% retention rate.</li>

<li>Take Notes and Visualize: Use a mind map linking user demographics (urban professionals) to features (proactive support) and outcomes (hassle-free shopping).</li>
</ul>
This might take 12 hours, with good decisions and tools like Notion for notes. Dissect key terms:
<ul>
<li>Target User: Urban dwellers in Lagos, focus analysis on urban patterns, logistics, and mobile behaviors.</li>

<li>Core Problems: Fragmented stores, unreliable vendors, unpredictable delivery, measure Vendor Reliability Score, On-Time Delivery Rate, Order Completion Rate.</li>

<li>Solution Differentiators: Personalized recommendations, fast delivery, secure escrow—link to tables like BUYER_PROFILES (preferences), SELLER_ORDERS (logistics), and ESCROW_WALLETS (trust).</li>

<li>Business Goals: 95% CSAT, +15% AOV in 6 months, 60% retention in 1 year, these are North Star Metrics for all analyses.</li>
</ul>
What to Extract as a Data Storyteller:
<ul>
<li>Business Goals: CSAT, AOV growth, retention.</li>

<li>Product Goals: Remove frictions (faster discovery, high order completion), highlight features (wallet, recommendations).</li>
</ul>
<h4>Why This Step Matters</h4>
Data storytelling requires context; without it, data is noise. This grounds you in the "why" behind numbers e.g., retention matters in a low-trust market. It aligns work with goals, preventing irrelevant metrics and enabling resonant stories like "Personalization solves urban frustrations, boosting sales." It transforms analysts into business strategists, ensuring analyses drive outcomes.


<h2>Step 2: Identifying Ten Key Metrics – Quantifying Success</h2>
Informed by documentation, select ten metrics spanning customer behavior, operations, satisfaction, and growth. Brainstorm 20+, prioritize by goals, and define clearly with relevance. Use the SQL schema for computability.

Here's a consolidated list of ten metrics, each with definition, schema sources, and importance:
<ul>
<li>Average Order Value (AOV) Definition: Total revenue ÷ number of orders (for delivered orders in a period). Columns: SELLER_ORDERS.TOTAL_AMOUNT, SELLER_ORDERS.ORDER_DATE, STATUS IN ('DELIVERED'). Why: Tied to +15% AOV goal; evaluates pricing, bundling, and recommendations for upselling.</li>

<li>Conversion Rate Definition: Orders placed ÷ sessions (proxy with unique buyers placing ≥1 order). Columns: BUYERS.BUYER_ID, BUYER_ORDERS.ORDER_ID, BUYER_ORDERS.STATUS. Why: Targets 90% order completion; measures UX effectiveness in reducing abandonment.</li>

<li>Order Completion Rate Definition: Delivered orders ÷ all placed orders. Columns: SELLER_ORDERS.STATUS = 'DELIVERED'. Why: Builds trust by addressing delivery reliability; reduces churn.</li>

<li>Refund/Dispute Rate Definition: Orders with REFUNDED_TO_BUYER or DISPUTED ÷ total orders. Columns: ESCROW_WALLETS.STATUS. Why: KPI for trust; highlights vendor or logistics issues.</li>

<li>Recommendation Uplift Definition: % lift in conversion for recommended users vs. control (proxy until flags exist). Columns: Event data flags; link to BUYER_ORDERS.STATUS. Why: Tied to 10% conversion increase from recommendations.</li>

<li>Customer Retention Rate (12-month) Definition: Active buyers now who were active 12 months ago ÷ buyers 12 months ago. Columns: BUYERS.BUYER_ID, BUYER_ORDERS.ORDER_DATE. Why: Core goal (60% retention); justifies loyalty programs.</li>

<li>Repeat Purchase Rate Definition: Buyers with ≥2 orders ÷ all buyers. Columns: BUYER_ORDERS by BUYER_ID. Why: Early loyalty signal; drives engagement via tiers.</li>

<li>On-Time Delivery Rate Definition: Orders delivered within SLA (proxy: time from ORDER_DATE to DELIVERED). Columns: SELLER_ORDERS.ORDER_DATE, STATUS. Why: Differentiator for next-day Lagos delivery; measures promises.</li>

<li>Net Revenue (Post-Refunds) Definition: Sum of delivered TOTAL_AMOUNT minus refunds. Columns: SELLER_ORDERS.TOTAL_AMOUNT, ESCROW_WALLETS.STATUS IN ('REFUNDED_TO_BUYER'). Why: True top-line metric; accounts for disputes.</li>

<li>Seller Quality Index (SQI) Definition: Weighted composite of ratings, return rates, and delivery success. Columns: SELLER_REVIEWS.RATING, ESCROW_WALLETS.STATUS, SELLER_ORDERS.STATUS. Why: Ensures curated marketplace; informs merchandising and payouts.</li>
</ul>
Tip for Two Slides: Slide 1: Names + definitions. Slide 2: Why + schema sources. Research benchmarks (e.g., 2-3% average conversion) for credibility.

<h4>Why This Step Matters</h4>
Metrics turn goals into narratives, providing plot points like "AOV rose 12% post-recommendations." Clear definitions avoid ambiguity, linking data to impact. They create a shared language, moving from vague "success" to specific insights, fostering focus on high-value areas like retention.


<h2>Step 3: Constructing an Entity-Relationship Diagram (ERD) – Mapping Data Relationships</h2>
Use the SQL schema to visualize connections. Tools: Draw.io (as in the .drawio file).
<ul>
<li>Identify Entities: Tables like SELLERS (SELLER_ID), BUYERS (BUYER_ID), PRODUCTS (PRODUCT_ID), BUYER_ORDERS, SELLER_ORDERS, ESCROW_WALLETS.</li>

<li>Define Attributes: Key fields, e.g., SELLERS.EMAIL (unique), PRODUCTS.STOCK_QTY, ESCROW_WALLETS.STATUS (e.g., HELD, RELEASED_TO_SELLER).</li>

<li>Map Relationships: One-to-Many: SELLER → PRODUCTS (via SELLER_ID FK). Many-to-Many: BUYERS → ORDERS → PRODUCTS (via ORDER_ITEMS). One-to-One: ESCROW_WALLETS ties to ORDERS. Cross: EMPLOYEES link to disputes via EMPLOYEE_ID in ESCROW_WALLETS.</li>

<li>Visualize: Rectangles for entities, crows-foot for cardinalities (1—∞). Include PK/FK, constraints (e.g., CHECK on ratings 1-5).</li>

<li>Iterate: Sketch, digitize, validate against schema (3-5 hours).</li>
</ul>
Core highlights: ESCROW_WALLETS as trust hub; separate buyer/seller order views; employee ops for governance.

<h4>Why This Step Matters</h4>
The ERD is the "map" for stories—e.g., joining BUYERS and ORDERS reveals retention tales. It prevents silos, enables holistic queries, and ensures integrity. It's essential for accurate queries, onboarding, and scaling analyses.


<h2>Conclusion: The Story Ahead</h2>
Week 1 task was a brilliantly designed introduction to the world of data analytics. It forced a methodical process:
<ul>
<li>First, understand the "Why" (The Business).</li>

<li>Then, define "What" to measure (The Metrics).</li>

<li>Finally, learn "Where" the data lives (The ERD).</li>
</ul>
