# china-ashare-market-style-monitor
A Python-based market style monitor for the China A-share market using broad indices.

## Project Overview
This project builds a small Python-based market style monitor for the China A-share market. Instead of only showing daily market movements, it focuses on a more structured question:

- What kind of market style dominated over the past 12 months?
- What kind of market style is leading in the current quarter?
- Has a style shift occurred?

The project is a simple data product. It uses broad-index data to summarise the market in a way that is easier to interpret for non-professional users.

## Analytical Problem
Most stock market apps mainly show short-term information such as daily gainers, daily losers, and sector heatmaps. These are useful, but they do not always help users understand the broader market environment.

In the China A-share market, different periods may be dominated by different styles, such as large-cap blue-chip leadership, more balanced market performance, or growth-active and high-elasticity leadership. However, they still find it difficult to build a clear understanding of the broader market environment, which means they often lack a basis for judging what types of stocks are aligned with the market’s medium- to long-term main direction when selecting stocks.

This project tries to solve that problem by offering a clearer summary of market style across meaningful time windows instead of only looking at daily moves.

## Product Need
In practice, predicting prices and forecasting the exact direction of the market is always difficult. A more realistic approach is to understand the current market environment as clearly as possible and respond to it, rather than trying to predict every move.

This is why a structured market style monitor can be useful: it helps users identify the broader market context, recognise the current leading style, and notice possible style shifts.


## Target Users
The main target users are China A-share retail investors who already follow the market but do not yet have a structured framework for market style analysis.

This product may also be useful for:
- finance or accounting students
- beginner analysts
- financial information platforms that want to provide a clearer market-style summary

## Product Idea
The product reads broad-index data and produces a simple market-style interpretation based on two parts:

### 1. Price-based style analysis
This part identifies:
- the dominant market style over the **past 12 months**
- the dominant market style in the **current quarter**
- whether a **style shift** may have occurred

### 2. Activity confirmation analysis
This part checks whether the current price-leading style is also supported by stronger market activity, using:
- trading amount
- trading volume

So the final output is not just “what is strongest now”, but also “whether that strength is supported by market participation”.

## Data Source
The project uses daily China A-share broad-index data collected through **Tushare** and stored locally as a CSV file.

Main fields used:
- `date`
- `index`
- `close`
- `amount`
- `volume`

### Included Indices
The following 10 broad indices are included:

- SSE 50
- CSI A50
- CSI 300
- SZSE 100
- CSI 500
- ChiNext
- STAR 50
- CSI 1000
- CSI 2000
- Beijing 50

These indices are used as proxy indicators of broader market style.

## Classification Framework
The included indices are grouped into three dimensions:

### 1. Size
- Large
- Mid
- Small

### 2. Elasticity
- Low
- Medium
- High

### 3. Style Orientation
- Blue-chip Core
- Balanced
- Growth-Active

This is a practical classification framework for interpreting market style. It is not intended to be a strict academic factor model.

## Methods

### A. Data Preparation
The notebook first:
- loads the dataset
- sorts the observations by index and date
- removes rows with missing core fields
- attaches classification labels to each index

### B. Price-Based Analysis
For each included index, the notebook calculates:
- past 12-month return
- current-3-month return

It then aggregates results into category-level summaries across:
- size
- elasticity
- style orientation

The notebook compares:
- the past 12-month leader
- current-3-month leader

If the leaders are different, it treats this as a possible **style shift**.

### C. Activity Confirmation
For each index, the notebook calculates:

- **amount ratio** = recent 5-day average trading amount / recent 20-day average trading amount  
- **volume ratio** = recent 5-day average trading volume / recent 20-day average trading volume  

These are then aggregated into the same three dimensions.

The notebook checks whether the current price-leading category:
- is also strongest in activity
- is above average in activity
- or is weaker than another category, which may suggest possible rotation

## Main Outputs
The notebook produces:

- a summary of the dominant style over the **past 12 months**
- a summary of the dominant style in the **current-3-month**
- a judgement on whether **style rotation** has occurred
- an **activity confirmation conclusion** for:
  - size
  - elasticity
  - style orientation
- top-performing indices by 12M return
- top-performing indices by current-3-month return

## Repository Structure
A simple structure for this repository is:

```text
.
├── README.md
├── china-ashare-market-style-monitor.ipynb
└── a_share_indices_daily.csv
```

## How to run
### Default mode
By default, the notebook runs from the local CSV file, so a Tushare account is not required for normal use.

### Update mode
Tushare is only needed when the user wants to update the dataset. In that case, the user needs to prepare:
- a valid Tushare token
- the required Python package environment
- working access to the Tushare API

## Environment
The notebook mainly uses standard Python tools such as:

- pandas
- matplotlib
- datetime

If update mode is used, it also requires:

- tushare

## Why This Product Matters

This project is useful because it moves beyond same-day market heatmaps and gives a more structured reading of the broader market environment.

Instead of trying to predict every short-term move, it focuses on a more practical idea:

- Understand the market over a meaningful time window
- Identify the current style clearly
- Respond to style changes rather than trying to guess everything in advance

## Limitations
This project has some limitations that should be acknowledged.

1. First, The classification framework is a product-oriented proxy, not strict academic factor classification.
2. Second, the category-level results are calculated using simple equal-weight averages. This approach is transparent and easy to understand, but it may oversimplify the relative importance of different indices.
3. Third, the activity confirmation analysis is based only on trading amount and trading volume. Although these indicators are useful for measuring short-term market participation, they do not represent all possible drivers of market style.
4. Finally, results depend on window settings (20/60/240, 5/20). However, different windows may lead to conclusions look slightly different.

## Demo Video
