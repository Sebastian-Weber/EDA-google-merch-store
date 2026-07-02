# Research Ideas, Constraints & Hypotheses

## Applicable to current approach (behavioral segmentation, no persona claims)

---

### 2 | Funnel — Add-to-Cart as Intent Signal
Is add-to-cart a reliable purchase intent signal, or do a significant share of users add items without converting?

**Why relevant:** add_to_cart is one of the 6 clustering features. If it is a weak conversion predictor, its weight in the feature matrix may distort cluster separation. Check: what share of users with add_to_cart > 0 never reach begin_checkout or purchase?

---

### 10 | Temporal — Pre/Post Holiday Cluster Composition
Does cluster composition shift between pre-holiday (Nov/Dec) and post-holiday (Jan)?

**Why relevant:** The dataset covers exactly one holiday season. If January produces a structurally different buyer profile, the clustering is seasonally skewed. This is the post-hoc seasonal analysis planned in 02_clustering.ipynb (currently a placeholder). Run: df.groupby(['cluster_name', 'month']).size(normalize=True)

---

### 12 | Segmentation — Browser Cluster as Collapsed Sub-Segments
Is the Browser cluster (81.1%) actually one homogeneous segment, or does it contain meaningful sub-segments that k-means at k=4 collapsed together?

**Why relevant:** A cluster covering 81% of users is analytically weak. It may contain at least two distinct sub-types: true single-session bouncers (1 page view, 0 items) and low-engagement multi-page browsers (several page views, 0 items). These would require k > 4 to separate. Reference: Dolnicar & Grun (2008) on the risk of over-compressed clusters masking behavioral heterogeneity.

---

### 15 | Constraint — Seasonal Skew, External Validity
The 3-month window (Nov 2020 to Jan 2021) covers only one holiday season. Purchasing behavior is seasonally skewed, threatening external validity of any derived segments.

**Why relevant:** Results cannot be generalized beyond this specific seasonal window. Any segment labeled by purchase frequency or conversion rate is measuring holiday-season behavior, not baseline user behavior. Reference: Campbell & Stanley (1963), Experimental and Quasi-Experimental Designs for Research — history threat to internal validity.

---

### 16 | Constraint — Obfuscated Item Names
Obfuscated item names limit product-level and category-level differentiation.

**Why relevant:** item_category and item_name fields contain placeholder values in parts of the dataset. Any category-level analysis is unreliable. This limits the interpretability of the Engaged Non-Converter segment specifically — we cannot say what they were browsing, only that they browsed extensively.

---

### 19 | Constraint — No Qualitative Layer
Behavioral clusters describe what users do, not why. Segment construction without motivational insight is an interpretive leap, not an empirical finding.

**Why relevant:** Already documented as Limitation 2 in capstone_documentation.html. Reinforce in notebook with explicit framing: cluster labels (Browser, Explorer, Engaged Non-Converter, Converter) are descriptive shorthand for behavioral patterns, not validated user types.

---

### 20 | Constraint — 81% Single-Cluster Dominance
81.1% of users in one cluster is a structural red flag. It is either genuine low purchase intent, or an artifact of obfuscation distortion. Cannot verify without ground truth.

**Why relevant:** Already documented as Limitation 1. The Silhouette Score peak at k=2 (0.82) confirms the data separates most cleanly into two groups, not four. The choice of k=4 is an interpretability decision, not a data-driven one. Document explicitly.

---

### 21 | Constraint — Gift-Purchase Context
Merchandising stores are gift-purchase contexts, especially during the holiday season. Buyer and end user are frequently different people. k-means cannot distinguish self-purchase intent from gift-purchase intent.

**Why relevant:** Not yet in capstone_documentation.html. The Converter segment (99.42% conversion rate) may not represent brand-loyal self-purchasers. It may represent task-completion buyers driven by social obligation (Secret Santa, Christmas gifts) rather than product affinity. This directly undermines the interpretability of the Converter label. Add as Limitation 6.

---

### 22 | Reframe — Seasonal Scope as Correct Scope
The dataset is not a flawed general study. It is a correctly scoped study of holiday season funnel behavior specifically.

**Why relevant:** Reframing the seasonal limitation as a scope definition strengthens the methodological position. Instead of "this study is limited by its seasonal window," the claim becomes "this study describes funnel behavior during a high-intent shopping period, which is a legitimate research object in its own right."

###

- A "no" implies someone considered buying and decided against it. A bounce means they never got that far — there was no decision to reject.

-> Concretely: the Browser cluster averages ~1.05 sessions and ~2 page views per user (profile table, cluster 0). 88.8% of them never viewed a single item. So this isn't "they looked at the product and passed" — it's "they loaded a page and left before the product was ever in front of them." That could be a bounce off the homepage, a mis-click, a bot/crawler, a referral link that didn't match intent, or someone checking one thing and leaving — you can't distinguish those from this data, but none of them represent a rejected purchase.

Why the distinction matters: if you treat Browser like Engaged Non-Converter ("they didn't convert, let's fix checkout friction"), you'd be solving the wrong problem — nothing about checkout affects someone who never viewed a product. Browser's fix (if any) would be top-of-funnel: landing page relevance, traffic quality, whether the right people are even arriving. Engaged Non-Converter's fix is bottom-of-funnel: checkout itself. Same "0% conversion" number, structurally different problem.