 📊 Instagram Influencer Analytics Dashboard

## 📌 Project Overview
This project analyzes top Instagram influencers' performance data to uncover insights about their audience reach, engagement, and growth trends.  
The dataset includes metrics such as followers, likes, posts, engagement rates, and country distribution.  
The final output is an **interactive Power BI dashboard** that allows users to explore influencer rankings, engagement patterns, and geographical trends.

---

## 🎯 Objectives
- Clean and preprocess influencer data for accurate analysis.
- Calculate engagement metrics and growth rates using DAX.
- Build interactive Power BI visuals for quick insights.
- Identify top influencers by followers, engagement rate, and likes per post.
- Compare influencer performance across countries.

---

## 🗂 Dataset
**File:** `top_insta_influencers_data.csv`  
**Source:** Provided dataset (cleaned version available in `Cleaned_Data` folder).  

### Key Columns:
- `rank`: Influencer ranking in dataset.
- `channel_info`: Influencer username/profile.
- `country`: Country of influencer (missing values replaced with "Unknown").
- `followers`: Number of followers.
- `posts`: Total posts on Instagram.
- `avg_likes`: Average likes per post.
- `60_day_eng_rate`: Engagement rate for last 60 days.
- `new_post_avg_like`: Average likes for recent posts.
- `total_likes`: Total likes across all posts.
- `influence_score`: Calculated influence score.

---

## 🛠 Data Cleaning & Transformation (Power Query)
1. **Removed extra rows & promoted headers**.
2. **Trimmed text columns** to remove extra spaces.
3. **Created `fxParseNumber` function** to handle:
   - `K` → thousands (×1,000)
   - `M` → millions (×1,000,000)
   - `B` → billions (×1,000,000,000)
   - `%` → converted to decimal form.
4. Applied `fxParseNumber` to:
   - `followers`
   - `posts`
   - `avg_likes`
   - `60_day_eng_rate`
   - `new_post_avg_like`
   - `total_likes`
   - `influence_score`
5. **Replaced missing `country` values** with `"Unknown"`.
6. Converted all numeric columns to **Decimal Number** or **Whole Number** types.

---

## 📐 DAX Measures
```DAX
-- Engagement Rate (%)
Engagement Rate =
DIVIDE(
    SUM('top_insta_influencers_data'[avg_likes_clean]),
    SUM('top_insta_influencers_data'[followers_clean])
)

-- Likes per Post
Likes per Post =
DIVIDE(
    SUM('top_insta_influencers_data'[total_likes_clean]),
    SUM('top_insta_influencers_data'[posts_clean])
)

-- Likes Growth (%)
Likes Growth % =
DIVIDE(
    SUM('top_insta_influencers_data'[new_post_avg_like_clean]) - SUM('top_insta_influencers_data'[avg_likes_clean]),
    SUM('top_insta_influencers_data'[avg_likes_clean])
)
📊 Dashboard Features
Page 1 — Overview
KPI Cards: Total Followers, Total Likes, Avg Engagement Rate, Likes per Post, Likes Growth %.

Bar Chart: Top 10 influencers by followers.

Scatter Plot: Followers vs Engagement Rate (size = Influence Score).

Map: Influencers by country.

Page 2 — Engagement Analysis
Bar Chart: Likes per Post by country.

Column Chart: Avg Engagement Rate by country.

Table: Influencer details with measures.

Page 3 — Country Insights
Slicer: Country selection.

Bar Chart: Top 5 influencers by engagement rate in selected country.

💡 Insights from the Dashboard
Some influencers with fewer followers have higher engagement rates.

Certain countries dominate the follower count, while others excel in engagement.

Recent post engagement trends help identify growing vs declining influencers.

📎 How to Use
Open the .pbix file in Power BI Desktop.

Use slicers to filter by country or influencer.

Hover over data points for tooltips with extra insights.

Explore different pages for overview, engagement breakdown, and country-specific insights.

🚀 Future Improvements
Automate data refresh from Instagram APIs.

Add time-series visualizations for follower growth.

Include sentiment analysis of captions/comments.

Create mobile-friendly Power BI layout.
