# Event Study of the CS:GO / CS2 Skins Market

This project applies **quantitative finance techniques** to the Steam Community Market for CS:GO / CS2 weapon cases.  
It showcases the use of **event study methodology** on an alternative digital asset market.

---

## Project Overview

- **Goal:** Measure how major in-game events (case releases, esports majors, rare pool changes) impact the prices of CS:GO/CS2 cases.  
- **Why interesting:**  
  - Skins are a *tradable asset class* with liquidity, speculation, and supply shocks.
  - Events in the game mimic **earnings, product launches, or policy changes** in traditional markets.  
  - This dataset is messy.  

- **Cases Overview:** 
  - Cases are opened to create new skins
  - Opening a case consumes it
  - New cases are dropped once per week per player if the player is active enough
  - There are active drops, rare drops and discontinued cases
  - The rates are 99:1:0 respectively
  - This means that:
    - Active drops are inflationary
    - Rare drops are deflationary if they are opened at a sufficient rate
    - Discontinued cases are purely deflationary
---

## Methodology

1. **Data**
   - Price histories per case from the Steam Community Market.
   - Event data:  
     - *Case releases* (supply introduced).  
     - *Rare pool changes* (case drop rate decreased).  
     - *Esports majors* and *general updates*.

2. **Returns**
   - Convert raw prices into **log returns**:  
     r_t = ln(P_t / P_{t-1})

3. **Normal (expected) returns**
   - Estimate each item’s average return over a **30-day estimation window** before the event.

4. **Abnormal returns**
   - Difference between actual return and normal return:  
     AR_t = r_t - mu

5. **Cumulative Abnormal Returns (CAR)**
   - Sum abnormal returns over different event windows, e.g. [-1,1], [0,1], [-5,5].

6. **Significance testing**
   - Compute test statistics and p-values to check if CARs are statistically different from zero.

---

## 📊 Results

### 1. Mean CAR by event type
- **Rare pool events:** strong and consistent **positive CARs** — cases often spike when supply is cut.  
- **Case releases:** mixed — some new cases depress old ones, others have muted effects.  
- **General esports/patch events:** mostly noise, very limited effect on case prices.  

### 2. Significance share
- Rare pool events: **most frequently significant**, showing systematic market reaction.  
- Case releases: **occasional significance**, often short-lived.  
- General events: **rarely significant**, confirming weak linkage.

### 3. Example heatmaps
![Mean CAR heatmap](output/heatmap_meanCAR_case_release.png)  
![Significance share heatmap](output/heatmap_sigshare_rare_pool.png)  

---

## 📂 Project Structure

```
data/
  events/             # raw event CSVs
  item data/          # raw Steam price histories
clean/                # cleaned daily VWAP per item, event master
scripts/
  build_events_and_prices.py  # cleaning & preprocessing
  event_study.py              # event study calculations
  plot_heatmaps.py            # visualization
output/
  event_study_results.csv     # results (CAR, t-stats, p-values)
  heatmap_*.png               # heatmaps
public/
  index.html                  # interactive chart (Plotly)
```

---

## 🧾 Key Takeaways

- This project demonstrates:
  - **Data cleaning**: messy CSVs into structured daily returns + event master.  
  - **Quant methodology**: event study framework, abnormal returns, t-tests.  
  - **Visualization**: interactive Plotly charts + static seaborn heatmaps.  
- Rare pool events show **strongest market impact**, while esports majors show **little to no price effect**.

---

## 💡 Extensions

If taken further, one could:
- Apply **cross-sectional regression** to see which items react most to events.  
- Explore **factor models** (e.g. case index vs. individual case).  
- Backtest simple **trading strategies** (buy on rare pool drop, sell after hype).

---

## 🏁 Conclusion

This is a compact **quant-style event study** applied to a nontraditional asset market.  
It shows transferable skills in:
- **Statistical analysis**
- **Event-driven modeling**
- **Data visualization**
