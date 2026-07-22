# Amazon-Best-Sellers-Kitchen-Dining-Web-Scraping-EDA-Visualization
A data analytics internship project covering the full pipeline: scraping live e-commerce data, cleaning it, exploring it, and visualizing key patterns.
---

# Overview
This project scrapes Amazon Best Sellers data from the Kitchen & Dining category, cleans and structures the raw output, then explores relationships between price, star rating, and review count to answer three business questions about what drives bestseller status.
---

# Tools Used
- Octoparse = no-code web scraping (custom-built task, auto-detect workflow)
- Python = pandas for cleaning/analysis, matplotlib & seaborn for visualization
- Jupyter Notebook = analysis environment
---

# Methodology
### Scraping: 
Built a custom Octoparse task (rather than a paywalled template) targeting Amazon's Best Sellers page for Kitchen & Dining. Configured auto-detected fields for title, price, star rating, review count, and product rank, with pagination enabled to capture multiple pages.

### Data Cleaning: 
- The raw export contained duplicate field sets from repeated auto-detect passes (e.g. Title and Title1 columns).
- Resolved by identifying which column in each pair held valid data, dropping the empty duplicate, and renaming to clean labels.
- Converted Stars and Price from text (e.g. "4.7 out of 5 stars", "NGN 38,629.84") into numeric types for analysis.
- Removed 39 exact-duplicate rows (likely caused by scraper pagination overlap) and one incomplete row, leaving 67 clean records.
  
### Exploratory Data Analysis: 
Examined distributions and computed a correlation matrix across Price, Stars, and Review_Count.

### Visualization: 
Built a price distribution histogram, a Price vs. Review Count regression scatterplot, and a star rating boxplot.

---

# Business Questions & Key Findings
1. What does the price distribution look like among Best Sellers? Prices range from NGN 4,678 to NGN 109,016 (mean ≈ NGN 27,496).
Most products cluster between NGN 10,000–30,000, with a long right-hand tail of premium priced outliers above NGN 80,000.
A visible gap between NGN 60,000–80,000 suggests two distinct pricing segments rather than one continuous range.

2. Does price relate to popularity (review count) or rating? Correlations were weak across the board:
Price vs. Stars: r = 0.148
Price vs. Review Count: r = -0.115
Stars vs. Review Count: r = 0.072
The scatterplot (with regression line) confirms this visually, review counts are scattered broadly across all price points with no clear rising or falling trend. Being a bestseller does not require being cheap, highly rated, or heavily reviewed.

3. Which subcategory has the widest price range? Scope note: the original plan compared multiple subcategories, but the final dataset covers only Kitchen & Dining due to a tooling limitation during scraping (see Limitations). Within this single category, prices still span a wide range (NGN 4,678–109,016), indicating Kitchen & Dining alone spans both budget and premium price tiers.
---

# Visualizations
See notebooks/eda.ipynb for the full charts:
- Price distribution histogram
- Price vs. Review Count scatterplot with regression line
- Star rating boxplot
---

# Limitations
- Single category scope: Data covers only Kitchen & Dining, not a cross-category comparison as originally intended.
- Currency: Prices are in NGN (Nigerian Naira), reflecting Amazon's geo-based pricing at scrape time not USD.
- Sample size: 67 rows after cleaning is a modest sample; findings describe this snapshot, not the full Amazon catalog.
- Snapshot in time: Best Sellers rankings and prices change frequently; this reflects a single scrape date.
- Duplicate rows: 39 duplicate rows (of 106 originally scraped) were removed, likely due to scraper pagination/scroll overlap worth noting as a data quality artifact of the collection method.
---
