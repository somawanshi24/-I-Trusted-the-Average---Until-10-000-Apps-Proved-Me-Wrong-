# Business Requirements Document (BRD)
## Project: Google Play Store Intelligence Dashboard

---

### 1. Document Control
| Field | Detail |
|---|---|
| Project Name | Google Play Store Intelligence Dashboard |
| Prepared By | [Neha Somawanshi] Aspiring Business Analyst |
| Stakeholder / Sponsor | Priya Menon, VP of App Ecosystem Growth, Google Play |
| Date | [20/08/2026] |
| Status | Draft v1.0 |

---

### 2. Business Background
Google Play's App Ecosystem Growth team advises third-party developers and internal partner teams on where growth opportunities exist on the Play Store. Currently, category selection, pricing strategy, and market-entry decisions are being made on anecdotal feedback and scattered spreadsheets rather than consolidated data. This has led to:

- Developer budgets being burned entering saturated categories with poor traction
- No clear evidence on whether paid vs. free monetization models perform better
- Uncertainty around whether app size / Android version requirements are suppressing installs in emerging markets
- No single decision-ready view leadership can hand to developer relations teams

### 3. Business Objective
Build a Power BI dashboard, backed by app catalog data, that gives the stakeholder a data-driven "opportunity map" of the Play Store — enabling faster, evidence-based guidance to developers and partner teams.

### 4. Stakeholders
| Stakeholder | Role | Interest |
|---|---|---|
| Priya Menon | VP, App Ecosystem Growth (Sponsor) | Needs decision-ready insights for developer relations guidance |
| Developer Relations Team | End user of insights | Needs category/pricing guidance to share with developers |
| Regional Partner Teams | Secondary stakeholder | Needs visibility into device/size constraints in emerging markets |
| Business Analyst (You) | Delivery owner | Translates data into insights and recommendations |

### 5. Business Questions to Answer
1. Which app categories are saturated (avoid) vs. underserved (opportunity) for new developers?
2. Does a paid vs. free pricing model change install volume or rating outcomes?
3. Is app size or minimum Android version quietly suppressing installs in any segment?
4. What are the top 3–4 recommendations to give developer relations teams this quarter?

### 6. Scope

**In Scope:**
- Analysis of Google Play Store app catalog data (category, installs, rating, price, size, content rating, Android version)
- Category saturation and opportunity analysis
- Free vs. paid monetization comparison
- App size / version vs. install correlation analysis
- Interactive Power BI dashboard with slicers for Category, Type, and Content Rating
- One-page insights & recommendations summary

**Out of Scope:**
- Real-time/live data refresh (static dataset snapshot only)
- User review sentiment analysis (unless a follow-on phase is scoped)
- Revenue/financial modeling beyond price-tier observations
- Country-level / geo-specific install data (dataset does not include this granularity)

### 7. Functional Requirements
| ID | Requirement |
|---|---|
| FR-01 | Dashboard shall display total apps, total installs, and average rating by category |
| FR-02 | Dashboard shall allow filtering by Category, Type (Free/Paid), and Content Rating |
| FR-03 | Dashboard shall show a saturation view: number of apps vs. average installs per category |
| FR-04 | Dashboard shall compare average rating and average installs for Free vs. Paid apps |
| FR-05 | Dashboard shall visualize app size distribution against install volume |
| FR-06 | Dashboard shall highlight top and bottom performing categories by install-to-rating ratio |
| FR-07 | Dashboard shall include a summary page with narrative insights and recommendations |

### 8. Non-Functional Requirements
| ID | Requirement |
|---|---|
| NFR-01 | Dashboard should load within a reasonable time for a ~10K row dataset |
| NFR-02 | Visuals should be clearly labeled and self-explanatory to a non-technical stakeholder |
| NFR-03 | Data cleaning steps must be documented and repeatable |

### 9. Data Requirements
| Field | Source | Notes |
|---|---|---|
| App, Category, Genres | Google Play Store Apps dataset (Kaggle) | Core dimensions |
| Rating, Reviews | Same dataset | Quality indicators |
| Installs | Same dataset | Requires cleaning (remove '+', ',') |
| Price, Type | Same dataset | Requires cleaning (remove '$') |
| Size | Same dataset | Requires unit standardization (M/k → MB) |
| Content Rating, Android Ver | Same dataset | Segmentation fields |

### 10. Assumptions
- The Kaggle dataset is a reasonable proxy for real Play Store catalog data
- Install counts (given as ranges, e.g., "10,000+") are treated as approximate, not exact
- Analysis reflects a point-in-time snapshot, not live trends

### 11. Constraints
- Dataset has no geographic/country field, limiting regional analysis to Android-version/size proxies only
- Some rows contain data quality issues (e.g., shifted columns) requiring cleanup before analysis

### 12. Deliverables
1. Cleaned dataset (Excel/Power Query output)
2. Power BI (.pbix) interactive dashboard
3. One-page insights & recommendations memo
4. GitHub-ready documentation (README, screenshots)

### 13. Success Criteria
- All 4 business questions are answered with a supporting visual
- Stakeholder can self-serve filter by category/type/content rating without analyst support
- Recommendations are specific and actionable, not generic observations
