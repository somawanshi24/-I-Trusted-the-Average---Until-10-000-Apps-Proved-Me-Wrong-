# Findings & Recommendations Report
## Project: Google Play Store Intelligence Dashboard

---

### Document Control
| Field | Detail |
|---|---|
| Prepared By | [Your Name] — Business Analyst |
| Stakeholder | Priya Menon, VP of App Ecosystem Growth, Google Play |
| Related Document | Business Requirements Document (BRD) — Google Play Store Intelligence |
| Status | Final v1.0 |

---

### Purpose

This report answers the four business questions defined in the BRD, using the cleaned Google Play Store app catalog dataset. Each finding includes the supporting KPI(s), the chart used, a key caveat where relevant, and a specific recommendation for Priya's developer relations team.

---

## Q1: Which app categories are saturated (avoid) vs. underserved (opportunity)?

**KPIs used:** App Count per Category, Avg/Median Installs per Category, Avg Rating per Category, Opportunity Score (`Avg Installs × Avg Rating ÷ Total Apps`)

**Chart:** Bubble/scatter (App Count vs. Avg Installs, sized by Rating), ranked bar chart of Opportunity Score

**Finding:**
Communication ranks #1 by raw Opportunity Score, but this is driven by a small number of dominant incumbent apps (WhatsApp/Gmail-type apps) rather than genuine white space — verified by checking that its app count (387) is close to the dataset average, while its installs (103M avg) are ~6x the overall average, confirming outlier skew rather than low competition.

**Genuine opportunity categories:** Video Players, Entertainment, and Social — high installs and ratings without being dominated by a handful of giants.

**Recommendation:**
Advise new developers to target Video Players, Entertainment, or Social rather than Communication. Communication should be flagged internally as a "false positive" opportunity category driven by incumbents.

---

## Q2: Does a paid vs. free pricing model change install or rating outcomes?

**KPIs used:** Avg Installs (Free/Paid), Avg Rating (Free/Paid), Free App %, Paid App %

**Chart:** KPI cards, category-level bar comparisons (Top 10 filtered)

**Finding:**
- Avg Rating: Free 3.55 vs. Paid 3.41 — a small, likely insignificant gap
- Avg Installs: Free 18.85M vs. Paid 96.89K — a large gap, explained by catalog composition (92.61% Free vs. 7.38% Paid) and the natural adoption barrier of paying upfront before trying an app

**Recommendation:**
Do not recommend one pricing model universally. Free suits developers optimizing for reach/scale (ad revenue, user base growth); Paid suits developers optimizing for direct revenue per user, since rating quality holds up even with a much smaller install base. The choice should depend on the developer's business model, not on which model "wins" on installs.

---

## Q3: Is app size or Android version suppressing installs?

**KPIs used:** Median Installs by Size Tier (Small/Medium/Large), Median Installs by Android Tier (Old/Mid/Newer)

**Chart:** Bar charts, Size Tier and Android Tier vs. Median Installs

**Method note:** Average was initially used but found to be heavily skewed by a small number of blockbuster apps (e.g., Subway Surfers, Candy Crush, Temple Run) present in every size tier. Median was used instead to get a result robust to these outliers.

**Finding — Size:**
Even using outlier-resistant Median, Large apps show dramatically higher installs (~1.00M) than Medium (~50K) and Small (~10K). App size does not suppress installs — if anything, the opposite pattern holds, though this may reflect that successful apps grow larger over time (adding features) rather than size directly causing installs.

**Finding — Android Version:**
Apps requiring outdated Android versions (pre-3.0, "Old") show meaningfully lower median installs (~20K) than apps requiring more modern versions (~50K, both "Mid" and "Newer" tiers) — despite older-version apps not being rare in the catalog. This suggests install performance tracks with how current/actively maintained an app is, rather than with how many apps target a given version.

**Recommendation:**
Regional partner teams' concern that app size or newer-version requirements may suppress installs on lower-end devices is not supported by this dataset. If anything, larger apps and apps targeting modern Android versions show stronger install performance. Recommend not treating size or modern-version requirements as install barriers. Note: this dataset has no geography field, so region-specific effects cannot be confirmed or ruled out.

---

## Q4: Executive Summary — Top Recommendations for Developer Relations

| # | Insight | Recommendation |
|---|---|---|
| 1 | Video Players, Entertainment, and Social offer genuine opportunity; Communication's top ranking is an outlier illusion driven by incumbents | Point new developers to Video Players, Entertainment, or Social |
| 2 | Free and Paid apps perform similarly on rating quality; the install gap reflects catalog composition and payment friction, not quality | Recommend pricing model based on developer goals (reach vs. revenue), not a blanket rule |
| 3 | Larger apps show dramatically higher median installs, even after removing outlier bias | Do not treat app size as a growth barrier |
| 4 | Apps targeting outdated Android versions underperform; modern-version apps do not underperform despite being a smaller group | Do not discourage developers from targeting newer Android versions only |

---

### Key Methodology Notes (for technical review)
- All "per-app" averages use `AVERAGEX`/`MEDIANX` over `VALUES(App)` to prevent duplicate-row inflation from apps appearing multiple times in the raw dataset.
- App counts use `DISTINCTCOUNT` rather than `COUNTROWS` for the same reason.
- Size and Android Version fields required custom Power Query cleaning (unit standardization, "Varies with device" exclusion, multi-part version parsing) before analysis.
- Size and Android Version tier thresholds were set using actual Min/Max/Average from the cleaned data, not arbitrary round numbers.
- Where Average was found to be outlier-sensitive (Q3), Median was used instead and both results are documented for transparency.

### Limitations
- No geographic/country-level data — regional claims (e.g., emerging market device constraints) cannot be tested with this dataset.
- Install counts are approximate ranges (e.g., "10,000+"), not exact figures.
- Analysis reflects a single point-in-time snapshot of the Play Store catalog.
