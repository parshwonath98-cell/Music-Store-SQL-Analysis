# Music-Store-SQL-Analysis
# 🎵 Music Store SQL Analysis: Retail Music Business Insights

A structured SQL-based business analysis project built to derive actionable insights from a relational music store database — focusing on customer spending behavior, artist and genre popularity, employee hierarchy, and country-level sales performance.

---

## 📌 Short Description

The Music Store SQL Analysis is a query-driven case study designed to answer 9 real-world business questions across three difficulty levels — Easy, Moderate, and Advanced — using a normalized relational database of 11 tables. This project is intended for data analysts, SQL practitioners, and hiring managers seeking evidence of practical query-writing skills across JOINs, subqueries, CTEs, and Window Functions.

---

## 🛠️ Tech Stack

The project was built using the following tools and technologies:

- 🗄️ **MySQL** – Relational database management system used to run and test all queries
- 🧠 **SQL (Structured Query Language)** – Core language used for all data extraction and analysis
- 📊 **CTEs (Common Table Expressions)** – Used in advanced queries for multi-step logic and readability
- 🪟 **Window Functions** – `ROW_NUMBER() OVER(PARTITION BY ...)` used for country-level ranking
- 🔗 **Multi-table JOINs** – Queries span up to 6 tables using INNER JOINs across a normalized schema
- 📁 **File Format** – `.sql` for query scripts and `.png` for database schema diagrams

---

## 📂 Data Source

**Source:** Sample Music Store Database (based on the open-source Chinook Database structure)

The database contains 11 interrelated tables covering the full retail music store ecosystem:

| Table | Description |
|-------|-------------|
| `employee` | Staff hierarchy and personal details |
| `customer` | Customer demographics and contact info |
| `invoice` | Transaction-level billing records |
| `invoice_line` | Line-item detail per invoice (track, price, quantity) |
| `track` | Song-level data including duration and unit price |
| `album` | Album metadata linked to artists |
| `artist` | Artist name and ID |
| `genre` | Music genre classification |
| `media_type` | Audio format type |
| `playlist` | Playlist names |
| `playlist_track` | Track-to-playlist mapping |

---

## ✨ Features / Highlights

### 🔴 Business Problem
Music retail businesses generate multi-dimensional transactional data across customers, artists, genres, and geographies. Without structured querying, key business questions remain unanswered:
- Who are the highest-value customers and where are they located?
- Which artists and genres dominate purchases globally?
- Which cities and countries generate the most revenue?
- How do customer spending patterns differ across countries?

### 🎯 Goal of the Project
To write structured, progressively complex SQL queries that:
- Answer concrete business questions at three difficulty levels
- Demonstrate proficiency in core and advanced SQL concepts
- Surface customer, artist, and geography-level insights from a normalized relational schema

### 🖥️ Walkthrough of Key Questions & Queries

---

**Question Set 1 — Easy**

**Q1: Senior Most Employee**
Identifies the most senior employee by job level using `ORDER BY levels DESC LIMIT 1`.

**Q2: Countries with Most Invoices**
Aggregates invoice counts by billing country using `GROUP BY` and `COUNT(*)` to rank countries by transaction volume.

**Q3: Top 3 Invoice Values**
Retrieves the three highest invoice totals using `ORDER BY total DESC`.

**Q4: Best Customer City**
Uses `SUM(total)` grouped by `billing_city` to find the city generating the highest cumulative revenue — useful for deciding where to host a promotional music festival.

**Q5: Best Customer by Spending**
Joins `customer` and `invoice` tables, aggregates total spend per customer, and returns the top spender.

---

**Question Set 2 — Moderate**

**Q1: Rock Music Listeners**
Uses a subquery to filter tracks by genre, then joins across `customer`, `invoice`, and `invoice_line` to return all Rock listeners ordered alphabetically by email.

**Q2: Top 10 Rock Artists by Track Count**
Joins `track`, `album`, `artist`, and `genre` to count Rock tracks per artist and return the top 10 bands by volume.

**Q3: Tracks Longer Than Average Duration**
Uses a scalar subquery (`AVG(milliseconds)`) inside a `WHERE` clause to filter and rank tracks above average song length.

---

**Question Set 3 — Advanced**

**Q1: Customer Spend by Artist**
Uses a CTE (`best_selling_artist`) to first identify the highest-earning artist, then joins across 6 tables to calculate how much each customer spent specifically on that artist.

**Q2: Most Popular Genre by Country**
Uses a CTE with `ROW_NUMBER() OVER(PARTITION BY customer.country ORDER BY COUNT(...) DESC)` to rank genres per country and return only the top genre per country, handling ties where applicable.

**Q3: Top Spending Customer by Country**
Uses a CTE with `ROW_NUMBER() OVER(PARTITION BY billing_country ORDER BY SUM(total) DESC)` to identify the highest-spending customer in each country, returning all tied customers where the top amount is shared.

---

### 💡 Business Impact & Insights
- **Customer Targeting:** Identifying top spenders and best-performing cities enables precision marketing and event planning (e.g., music festival location)
- **Artist Strategy:** Top Rock artist and track count analysis supports artist partnership and playlist curation decisions
- **Genre Localization:** Country-level genre popularity allows regional catalog optimization and targeted promotions
- **Global Sales View:** Country-level customer spend ranking supports territory management and international expansion planning


---

## 🚀 How to Use

1. Clone or download this repository
2. Import the music store database into **MySQL Workbench** or any MySQL-compatible client
3. Open `Music_Store_Query.sql`
4. Run queries individually or as a full script
5. Questions are organized into **3 sections** — Easy, Moderate, and Advanced — with comments marking each question clearly
