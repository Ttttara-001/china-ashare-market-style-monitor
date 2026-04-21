# china-ashare-market-style-monitor
A Python-based market style monitor for the China A-share market using broad indices.

## 1. Problem & User
Most stock trading apps mainly show same-day market information, but they do not always help users understand the broader market environment. This project is designed for China A-share retail investors who want a clearer and more structured way to identify market style and possible style shifts.

## 2. Data
This project uses daily China A-share broad-index data collected through **Tushare** and stored locally in a CSV file.If the user has a valid Tushare account and token, the dataset can also be updated in real time.

- **Source:** Tushare
- **Access date:** 2026-04-20
- **Key fields:** `index`, `date`, `close`, `amount`, `volume`

The analysis includes 10 major broad indices:

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

## 3. Methods
The notebook follows three main steps:

1. **Data preparation**
   - load the local dataset
   - sort observations by index and date
   - remove rows with missing core fields
   - attach classification labels to each index

2. **Price-based analysis**
   - calculate past 12-month returns
   - calculate current-quarter returns
   - aggregate results into category-level summaries across:
     - size
     - elasticity
     - style orientation
   - compare past and current leaders to identify possible style shifts

3. **Activity confirmation**
   - calculate amount ratio = recent 5-day average trading amount / recent 20-day average trading amount
   - calculate volume ratio = recent 5-day average trading volume / recent 20-day average trading volume
   - check whether the current price-leading category is also supported by stronger market activity

## 4. Key Findings
- Over the **past 12 months**, the market style was **Mid** in size, **Medium** in elasticity, and **Growth-Active** in style orientation.
- In the **current quarter**, the market remained **Mid** in size and **Medium** in elasticity, but style orientation changed to **Balanced**.
- This suggests **no clear rotation** in the size and elasticity dimensions, but a **possible style shift** in the style-orientation dimension.
- Activity confirmation for **size** and **elasticity** was **limited**, because the current price-leading categories were above average in activity but not the strongest.
- In **style orientation**, the current price leader was **Balanced**, but activity was stronger in **Growth-Active**, which may suggest potential further rotation.

## 5. How to Run

### Default mode
By default, the notebook runs from the local CSV file, so a Tushare account is not required for normal use.

### Update mode
Tushare is only needed when the user wants to update the dataset. In that case, the user needs to prepare:
- a valid Tushare token
- the required Python package environment
- working access to the Tushare API

### Environment
The notebook mainly uses standard Python tools such as:
- pandas
- matplotlib
- datetime

If update mode is used, it also requires:
- tushare

## 6. Product Link / Demo
- **Demo video:** [insert demo link here]
- **Repository link:** [insert repository link here]

## 7. Limitations & Next Steps
This project has some limitations that should be acknowledged.

First, the classification framework is a practical proxy rather than a strict academic factor model. Second, the category-level results are based on simple equal-weight averages, which are easy to explain but may oversimplify the relative importance of different indices. Third, the activity confirmation analysis uses only trading amount and trading volume, so it does not capture all possible drivers of market style. Finally, the results depend on the selected time windows, and different settings may lead to slightly different interpretations.

If I were to improve the project further, I would add more indices such as style indices and sector indices, include a longer historical period with user-selected time ranges, and, if possible, develop the product into a more interactive webpage or mini application.
