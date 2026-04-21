Objective
This repository contains the submission for the Data Science/Analytics Intern assignment at Primetrade.ai.
The project analyzes the relationship between daily market sentiment (Bitcoin Fear/Greed Index) and trader behavior/performance on the Hyperliquid platform to uncover actionable trading strategies.

Setup & Installation
Clone this repository to your local machine:

Bash
git clone [https://github.com/yourusername/primetrade-assignment.git](https://github.com/yourusername/primetrade-assignment.git)
cd primetrade-assignment
Install the required dependencies:

Bash
pip install pandas numpy matplotlib seaborn scikit-learn
Ensure fear_greed_index.csv and historical_data.csv are in the root directory.

How to Run
Execute the main analysis script from your terminal:

Bash
python trader_sentiment_analysis.py
The script will output data shape validations, missing value counts, and the predictive model's classification report to the console. It will also generate two visual plots detailing trade frequency and PnL distributions.

 Project Write-Up
Part A: Methodology & Data Preparation
Timestamp Alignment: The trader dataset contained granular IST timestamps (%d-%m-%Y %H:%M). These were parsed and converted to a standard YYYY-MM-DD string format to align perfectly with the daily sentiment index.

Feature Engineering: Raw execution data was aggregated at the Date and Account level to generate key daily metrics: Total Daily PnL, Trade Frequency, Win Rate, and Long/Short Ratio.

Dataset Merging: A left join was utilized to map market sentiment to every active trading day for each account, dropping days where sentiment data was unavailable.

Part B: Key Insights
Insight 1 (Performance vs. Sentiment): Average daily PnL shifts significantly based on market sentiment. During Greed days, the average PnL was [Insert Greed PnL], compared to [Insert Fear PnL] during Fear days.

Insight 2 (Behavioral Shifts): Traders alter their trade frequency based on sentiment. The data indicates that during [Fear/Greed] days, overall trade volume [increases/decreases].

Insight 3 (Trader Segmentation): By segmenting traders into "High Frequency" and "Low Frequency" cohorts (based on the median daily trade count), the data reveals that [Insert observation from your bar chart, e.g., High Frequency traders suffer heavier drawdowns during Fear days compared to Low Frequency traders].

Part C: Actionable Strategy Output
Based on the behavioral archetypes and sentiment data, I propose the following rules of thumb for algorithmic trading strategies:

Dynamic Frequency Throttling: For accounts categorized in the "High Frequency" segment, throttle the maximum allowed daily trades by [X]% when the market transitions to "Fear" to preserve capital and prevent over-trading in volatile downtrends.

Directional Bias Filtering: If a trader's historical Long/Short ratio exceeds 1.5, reduce their position sizing automatically during "Fear" days, as heavily long-biased traders underperform when market sentiment flips negative.

 Bonus: Predictive Modeling
To push the analysis further, a Random Forest Classifier was trained to predict a trader's next-day profitability (1 = Profitable, 0 = Unprofitable).

Features Used: total_trades, win_rate, long_short_ratio, daily_pnl, and sentiment_numeric (Greed=1, Fear=0).

Performance: The model achieved an accuracy of [Insert accuracy %] on the test set.

Feature Importance: By extracting the Gini importance from the Random Forest, the model revealed that [Insert top feature from console output] is the strongest predictor of a trader being profitable the following day, followed closely by [Insert second top feature].
