# Analysis of Macroeconomic Data and Modeling of Economic Growth

Takahiro Hikida 

16 May 2026

## Introduction
### Motivation
When the Federal Reserve (US central bank) raises interest rates or unemployment spikes, the impact on Economic Growth (Real GDP) doesn’t happen overnight. Instead, economic variables act like falling dominoes, where a shock in one area creates a ripple effect that takes months or even years to fully materialize.

While simple correlations can show us what the economy looks like at a specific snapshot in time, they fail to capture these crucial time delays (lags) and chained reactions. In this project, I attempted to create a mathematical model of economic growth, taking these time delays into account.

### Questions asked
1. How has the US economy evolved over time?
2. How long do economic variables take to affect the Economic Growth?
3. Does “Consumer Sentiment” (how people feel about the economy) actually drive real Economic Growth, or is it merely statistical noise?
4. To what extent can we mathematically model and predict the structural portion of Economic Growth, separating it from unpredictable external shocks?
   
### The Approach
To answer the questions above, I had to learn and implement a new technique: the VAR (Vector AutoRegression) model and Impulse Response Function (IRF) analysis.

Unlike simple linear regressions, a VAR model consists of a system of equations that allows multiple variables to influence each other over time. By combining this advanced time-series technique with interactive Plotly visualizations, I have built a data narrative that simulates how an initial “shock” (like a sudden rate hike) ripples through the US economy.

### Data Used
I used the data all from Federal Reserve Bank of St.Louis as csv files.

* University of Michigan: Consumer Sentiment (UMCSENT) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UMCSENT)
* Federal Funds Effective Rate (FEDFUNDS) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/FEDFUNDS)
* Consumer Price Index for All Urban Consumers: All Items in U.S. City Average (CPIAUCSL) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/CPIAUCSL)
* Unemployment Rate (UNRATE) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UNRATE)
* Real Gross Domestic Product (GDPC1) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/GDPC1)
  
## Procedure
### 1. Data Collection and Wrangling
I collected five different economic indicators from public databases. However, real-world data is rarely perfect—each dataset covered different time periods and frequencies. To ensure an accurate analysis, I merged these distinct sources by matching their observation dates, keeping only the timeframe where all five indicators perfectly overlapped. This gave me a clean, unified dataset to base my mathematical models on.

### 2. Visualizing the Macroeconomic Landscape over Time
Before feeding the data into a complex mathematical model, it is crucial to visually inspect the historical trends of our variables. The time-series plots belowvariables.html illustrate the dynamic behavior of the U.S. economy over the past few decades. 

#### Key Observations:

* **Major Economic Shocks** <br>
We can clearly identify massive spikes and drops in the Real GDP and Unemployment Rate, particularly around the 2008 Financial Crisis and the 2020 COVID-19 pandemic. These are profound, unpredictable external shocks.

* **Inverse Relationships** <br>
Visually, there appears to be a natural friction between the Unemployment Rate and Economic Growth, when one spikes, the other reacts in the opposite direction.

### 3. Impulse Response Analysis
Here, we will run the Impulse Response Function (IRF). An IRF allows us to simulate a hypothetical scenario: What exactly happens to Economic Growth over the next 10 quarters if we apply a sudden “shock” (a 1-standard-deviation increase) to one specific variable, while holding everything else constant? Below is the resulting plot from the analysis.

#### How to Read the Impulse Response Graphs
Before diving into the results, here is a quick guide on how to interpret the Impulse Response Function (IRF) charts below.

* **The Horizontal Zero Line (The Baseline):** This line represents "no change" or "normal conditions."

* **The Solid Colored Line:** This represents our model's main prediction of how Economic Growth will react over the next 10 quarters after a sudden shock.

* **The Grey Shaded Area (The Margin of Error):** This is the 95% Confidence Interval. Because predicting the economy is never 100% certain, this grey zone shows the range of possible outcomes.

* **Crossing Zero:** If the grey shaded area crosses or touches the zero line, it means the effect is not statistically significant. In this case, the impact is so uncertain that the true effect might just be zero. We can only confidently say a shock has a real impact when the entire grey area is clearly above or below the zero line.

#### Results
* **The Unemployment Shock**<br>
When the Unemployment Rate spikes, the model shows an immediate and mathematically significant negative impact on Economic Growth. However, the graph reveals that the economy doesn’t recover instantly; the negative drag persists for several quarters before returning to the baseline, illustrating the stickiness of job losses.　

* **The Federal Funds Rate Shock**<br>
A sudden hike in interest rates by the Fed creates a delayed reaction. It doesn’t instantly crash the economy in Quarter 1. Instead, the model captures how the higher borrowing costs, i.e., higher interest rates, slowly seep into the system, steadily dragging down Economic Growth in the subsequent quarters (lags 2 and 3) before leveling out.

* **The “Consumer Sentiment” Revelation**<br>
One of the most surprising insights came from testing Consumer Sentiment. While it makes intuitive sense that a pessimistic public would spend less and slow down growth, the p-values in our VAR model suggested it wrong. Consumer Sentiment ultimately proved to be statistically insignificant when controlling for hard data like unemployment and interest rates. It turns out, how people feel about the economy does not independently drive growth; rather, their feelings are merely a reaction to the hard data.

### 4. Actual vs. Predicted Growth
Given the information above, we are able to create an equation that best represents the present Economic Growth with given parameters. The graph below plots the actual historical Economic Growth (Blue) against what our mathematical model predicted (Red).

#### Interpreting the Accuracy Metrics:

* **An $R^2$ of 0.253** <br>
A 25% explanatory power might seem low. However, in macroeconomics, this is a profound finding. It mathematically proves that about 25% of the U.S. economic growth is strictly driven by the structural, delayed cycles of past unemployment, interest rates, and inflation.
* **The Remaining 75%** <br>
The moments where the actual data (Blue) drastically breaks away from our prediction (Red)—such as the massive 2020 spike—represent the remaining 75%. These are the unpredictable events, like global pandemics or sudden geopolitical crises, which cannot be forecasted merely by looking at last quarter’s interest rates.


## Conclusion
This analysis yielded some insights into how the US economy actually operates beneath the surface. By moving beyond simple snapshots and building a time-delayed mathematical model, we answered our three (or four) core questions:

### 1. How has the US economy evolved over time?
Through our initial time-series analysis, we observed that the U.S. economy is highly cyclical but constantly disrupted by unpredictable external shocks, most notably the 2008 Financial Crisis and the 2020 COVID-19 pandemic. We also visually confirmed an inherent friction between indicators; for example, unemployment and economic growth consistently mirror each other in an inverse relationship.
### 2. How long do economic variables take to affect Economic Growth?
Our mathematical model proved that economic shocks do not happen overnight. The Vector AutoRegression (VAR) analysis revealed that variables like the Federal Funds Rate and Unemployment Rate act as strong, delayed forces. It takes several quarters for a hike in interest rates or a spike in job losses to fully seep into the system and drag down the overall Economic Growth Rate.
### 3. Does “Consumer Sentiment” actually drive real Economic Growth, or is it merely statistical noise?
Perhaps the most surprising finding was the statistical insignificance of Consumer Sentiment. The Impulse Response Function (IRF) visualizations showed that when a shock is applied to Consumer Sentiment, the 95% confidence interval (the grey shaded area) completely crosses the zero line. This means that when controlling for hard, and concrete data, like unemployment and interest rates, how people feel about the economy is just statistical noise. It is a trailing indicator; a mirror reflecting the economy, not a motor driving it.
### 4. To what extent can we mathematically model and predict the structural portion of Economic Growth?
By stripping away the statistical noise and focusing only on structurally significant variables with optimal lags, we successfully built a predictive equation. Our model achieved an $R^2$ score of 0.253. This mathematically proves that about 25.3% of America's Economic Growth is strictly determined by the delayed cycles of past economic indicators. The remaining 75% represents the unpredictable events (like global pandemics) that cannot be forecasted by structural models.

## Reflection
### Challenges & Learning a New Technique
The most challenging part of this project was the implementation of the Vector AutoRegression (VAR) model and Impulse Response Functions (IRF). Understanding why we need to convert raw GDP into Growth Rates was a steep learning curve. Furthermore, interpreting a system of equations where variables impact each other with varying time lags required a completely different way of thinking compared to standard linear regression. However, this challenge was very interesting, that I now feel that I have discovered completely different from what I have been learning before.

### Future Extensions
If I had more time and resources, I would extend this project by introducing variables that capture global supply chain metrics or energy prices (like crude oil). I would also be interested in applying this exact same VAR framework to other countries, such as Japan or the Eurozone, to see if their economies remember shocks for longer or shorter periods than the U.S.

## References & Resources
**Data Sources**
* University of Michigan: Consumer Sentiment (UMCSENT) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UMCSENT)
* Federal Funds Effective Rate (FEDFUNDS) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/FEDFUNDS)
* Consumer Price Index for All Urban Consumers: All Items in U.S. City Average (CPIAUCSL) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/CPIAUCSL)
* Unemployment Rate (UNRATE) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UNRATE)
* Real Gross Domestic Product (GDPC1) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/GDPC1)
* Plotly Dropdown Button: https://plotly.com/python/dropdowns/
* Stationarity of Data: https://otexts.com/fpp3/stationarity.html
* VAR Model Implementation: [Official statsmodels VAR documentation](https://www.statsmodels.org/stable/vector_ar.html)
* IRF(Impulse Response Function): https://www.statsmodels.org/stable/generated/statsmodels.tsa.vector_ar.irf.IRAnalysis.html
* Plotting Error Bands: [Plotly Continuous Error Bands](https://plotly.com/python/continuous-error-bars/)
* **AI Assistance:** Gemini (for code debugging, optimization)
