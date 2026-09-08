# Business Requirements Document (BRD)
## Zomato Business Intelligence Dashboard

**Prepared by:** [Your Name]
**Date:** [Date]
**Project Type:** Portfolio / Business Analyst Case Study
**Version:** 2.0 (Consolidated Single-Page Dashboard)

---

## 1. Project Overview

Zomato's Business Expansion & Strategy team needs a consolidated view of restaurant performance across global markets to guide decisions on market investment, pricing strategy, service feature adoption, and cuisine partnerships. Currently, this data exists as a flat, unprocessed dataset with no reporting layer — decisions are made without a clear, data-backed view of market health.

This project delivers a single-page, navigation-driven Power BI dashboard that transforms raw restaurant listing data into an actionable decision-support tool for the Strategy team, styled as a branded executive dashboard.

---

## 2. Business Objective

Enable Zomato's Business Expansion & Strategy team to answer four core questions:
1. Which countries/cities are strong markets, and which are underperforming despite high listing volume?
2. Does higher pricing correlate with higher quality, or is there a "value for money" segment being overlooked?
3. Do service features (online delivery, table booking) meaningfully improve customer engagement and ratings?
4. Which cuisines consistently perform best across markets, and where should new restaurant partnerships focus?

---

## 3. Current State (Before)

- Restaurant data exists as a raw CSV/JSON export with no cleaning, structure, or reporting layer
- No visibility into cross-market performance (all 15 countries' data sits unexamined together)
- No mechanism to compare price tier against rating
- No way to quantify the impact of delivery/booking features on engagement or quality
- Cuisine-level insights are not accessible since multiple cuisines are combined into single text fields per restaurant
- Business decisions on expansion and partnerships rely on assumption rather than evidence

---

## 4. Proposed State (After)

- A cleaned, modeled dataset with country lookup relationships and a dedicated cuisine-split table
- A single, branded dashboard page navigable via bookmark-driven buttons (Overview & Pricing, Market, Cuisines & Engagement, City Drill Down, Insights) — giving the feel of a multi-screen app without multiple physical pages
- A persistent Country slicer that remains active across every section (bookmark navigation configured to preserve filter state)
- A World Map visual for country-level performance, alongside data-bar/color-scale tables for precise figures
- Defined DAX measures for restaurant count, rating (adjusted for unrated listings), votes, cost, and feature-based rating gaps
- Top-10 filtering applied consistently across cuisine visuals, ranked by restaurant count, so comparisons are statistically meaningful
- A dedicated Insights screen summarizing the headline findings in plain business language

---

## 5. Scope

**In scope:**
- Data cleaning and transformation (Power Query), including encoding fixes and cuisine column splitting
- Data modeling (relationships, cuisine split table)
- DAX measure development
- Single-page dashboard with bookmark-based section navigation
- Custom red/black branded theme
- Insight documentation per section

**Out of scope:**
- Real-time data refresh / live API connection
- Predictive modeling or forecasting
- Currency conversion/normalization across countries
- Restaurant-level recommendation engine

---

## 6. Data Source

- **Dataset:** Zomato Restaurants Data (Kaggle, shrutimehta/zomato-restaurants-data)
- **Volume:** ~9,545 restaurants across 15 countries
- **Key fields:** Restaurant Name, Country Code, City, Cuisines, Average Cost for Two, Aggregate Rating, Votes, Has Online Delivery, Has Table Booking, Price Range
- **Supporting file:** Country-Code lookup table

---

## 7. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR1 | Dashboard must show total restaurants, countries, average rating, % online delivery, and average cost as headline KPIs, visible across all sections |
| FR2 | Dashboard must allow country-level (via map) and city-level (via drill-down table) performance comparison |
| FR3 | Dashboard must visualize cost vs. rating relationships, filterable by country |
| FR4 | Dashboard must quantify the rating and engagement difference between restaurants with/without delivery and table booking |
| FR5 | Dashboard must rank the Top 10 cuisines by frequency, and show their average rating using the same Top 10 set for consistency |
| FR6 | All ratings must exclude "Not rated" restaurants from average calculations to avoid skew |
| FR7 | Navigation between sections must occur via on-page buttons (bookmarks), not default page tabs |
| FR8 | The Country slicer selection must persist when navigating between sections |

---

## 8. Non-Functional Requirements

- Dashboard must remain performant with ~9,500+ rows and a ~20,000+ row cuisine-split table
- Visuals must be readable despite India representing ~90% of the dataset (volume skew handled via tables/treemaps with Top N filters, not distorted charts)
- Bookmark navigation must not reset slicer selections (Data capture disabled on all navigation bookmarks)
- Visual theme must remain consistent (red/black) across all sections

---

## 9. Assumptions & Constraints

- Currency values are not converted; cost comparisons are only valid within a single country
- Dataset skews heavily toward India (~90% of records), limiting the strength of "global" conclusions
- Map visual availability depends on tenant/organizational licensing settings

---

## 10. Success Criteria

- Single dashboard page functions with working section navigation, slicers, and measures
- Each section produces at least 2–3 clear, decision-oriented insights
- Cuisine comparisons are ranked consistently (same Top 10 set across all cuisine visuals)
- Dashboard is suitable for presentation as a Business Analyst portfolio artifact and LinkedIn showcase
