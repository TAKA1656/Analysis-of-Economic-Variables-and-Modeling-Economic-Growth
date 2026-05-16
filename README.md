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
I collected five different economic indicators from public databases. However, real-world data is rarely perfect, each dataset covered different time periods and frequencies. To ensure an accurate analysis, I merged these distinct sources by matching their observation dates, keeping only the timeframe where all five indicators perfectly overlapped. This gave me a clean, unified dataset to base my mathematical models on.

### 2. Visualizing the Macroeconomic Landscape over Time
Before feeding the data into a complex mathematical model, it is crucial to visually inspect the historical trends of our variables. The time-series plots below illustrate the dynamic behavior of the US economy over the past few decades. 

#### Key Observations:

* **Major Economic Shocks** <br>
We can clearly identify massive spikes and drops in the Real GDP and Unemployment Rate, particularly around the 2008 Financial Crisis and the 2020 COVID-19 pandemic. These are profound, unpredictable external shocks.

* **Inverse Relationships** <br>
Visually, there appears to be a natural friction between the Unemployment Rate and Economic Growth, when one spikes, the other reacts in the opposite direction.

### 3. Impulse Response Analysis
Here, we will run the Impulse Response Function (IRF). An IRF allows us to simulate a hypothetical scenario: What exactly happens to Economic Growth over the next 10 quarters if we apply a sudden “shock” (a 1-standard-deviation increase) to one specific variable, while holding everything else constant? Below is the resulting plot from the analysis.
<img width="1248" height="1200" alt="newplot" src="https://github.com/user-attachments/assets/ef586334-70d0-4000-a6fd-307c6aa3303b" />


#### How to Read the Impulse Response Graphs
Before diving into the results, here is a quick guide on how to interpret the Impulse Response Function (IRF) charts below.

* **The Horizontal Zero Line (The Baseline):** This line represents "no change" or "normal conditions."

* **The Solid Colored Line:** This represents our model's main prediction of how Economic Growth will react over the next 10 quarters after a sudden shock.

* **The Green Shaded Area (The Margin of Error):** This is the 95% Confidence Interval. Because predicting the economy is never 100% certain, this grey zone shows the range of possible outcomes.

* **Crossing Zero:** If the grey shaded area crosses or touches the zero line, it means the effect is not statistically significant. In this case, the impact is so uncertain that the true effect might just be zero. We can only confidently say a shock has a real impact when the entire grey area is clearly above or below the zero line.

#### Results
* **The Unemployment Shock**<br>
When the Unemployment Rate spikes, the model shows an immediate and mathematically significant negative impact on Economic Growth. However, the graph reveals that the economy doesn’t recover instantly; the negative drag persists for several quarters before returning to the baseline, illustrating the stickiness of job losses.　

* **The Federal Funds Rate Shock**<br>
A sudden hike in interest rates by the Fed creates a delayed reaction. It doesn’t instantly crash the economy in Quarter 1. Instead, the model captures how the higher borrowing costs, i.e., higher interest rates, slowly seep into the system, steadily dragging down Economic Growth in the subsequent quarters (lags 2 and 3) before leveling out.

* **The “Consumer Sentiment” Revelation**<br>
From the plot, human feelings aren't just statistical noise. The green confidence interval rises clearly above the zero line for the first few quarters. This provides mathematical proof that an optimistic public actually drives real economic growth, likely because confident consumers spend more money, creating a positive ripple effect throughout the economy.

### 4. Actual vs. Predicted Growth
Given the information above, we are able to create an equation that best represents the present Economic Growth with given parameters. The graph below plots the actual historical Economic Growth (Blue) against what our mathematical model predicted (Red).
<img width="1264" height="569" alt="newplot (1)" src="https://github.com/user-attachments/assets/00fcd7c3-a3ed-4d47-a8ce-83fc4f7d1d4d" />

#### The Equation

By filtering out the statistical noise and keeping only the highly significant variables, we built a structural equation. It reveals that today's Economic Growth is fundamentally driven by:
* The growth rates from the past 1 to 2 quarters.
* The unemployment rate from the past 1 to 2 quarters.
* The interest rate (Federal Funds Rate) set by the Fed exactly 2 quarters ago.

It might seem wierd that Consumer Sentiment is missing from the derived equation above, even though our earlier IRF graphs proved it has a significant impact. The equation only shows direct impacts on GDP. This means that consumer Sentiment doesn't directly increase GDP; instead, it triggers a ripple effect (e.g., confident consumers spend more, which lowers unemployment), and those other variables then boost GDP two quarters later. The equation shows the last variable that causally affects economic growth, but the IRF simulation proves that Consumer Sentiment does indirectly affect economic growth. 

#### Interpreting the Accuracy Metrics:

* **An $R^2$ of 0.253** <br>
A 25% explanatory power might seem low. However, in macroeconomics, this is a profound finding. It mathematically proves that about 25% of the U.S. economic growth is strictly driven by the structural, delayed cycles of past unemployment, interest rates, and inflation.
* **The Remaining 75%** <br>
The moments where the actual data (Blue) drastically breaks away from our prediction (Red), such as the massive 2020 spike—represent the remaining 75%. These are the unpredictable events, like global pandemics or sudden geopolitical crises, which cannot be forecasted merely by looking at last quarter’s interest rates.


## Conclusion
This analysis yielded some insights into how the US economy actually operates beneath the surface. By moving beyond simple snapshots and building a time-delayed mathematical model, we answered our three (or four) core questions:

### 1. How has the US economy evolved over time?
Through our initial time-series analysis, we observed that the U.S. economy is highly cyclical but constantly disrupted by unpredictable external shocks, most notably the 2008 Financial Crisis and the 2020 COVID-19 pandemic. We also visually confirmed an inherent friction between indicators; for example, unemployment and economic growth consistently mirror each other in an inverse relationship.
### 2. How long do economic variables take to affect Economic Growth?
Our mathematical model proved that economic shocks do not happen overnight. The Vector AutoRegression (VAR) analysis revealed that variables like the Federal Funds Rate and Unemployment Rate act as strong, delayed forces. It takes several quarters for a hike in interest rates or a spike in job losses to fully seep into the system and drag down the overall Economic Growth Rate.
### 3. Does “Consumer Sentiment” actually drive real Economic Growth, or is it merely statistical noise?
It is absolutely **NOT** just noise! If we only looked at direct mathematical equations, we might mistakenly conclude that human emotions don't matter. However, our VAR simulation (IRF) proved that an optimistic public creates a powerful domino effect. An increase in Consumer Sentiment indirectly drives real Economic Growth exactly two quarters (6 months) later. This mathematically proves that how people feel about the economy eventually translates into real-world economic activity.
### 4. To what extent can we mathematically model and predict the structural portion of Economic Growth?
By stripping away the statistical noise and focusing only on structurally significant variables with optimal lags, we successfully built a predictive equation. Our model achieved an $R^2$ score of 0.253. This mathematically proves that about 25.3% of America's Economic Growth is strictly determined by the delayed cycles of past economic indicators. The remaining 75% represents the unpredictable events (like global pandemics) that cannot be forecasted by structural models.

## Reflection
### Challenges & Learning a New Technique
The most challenging part of this project was the implementation of the Vector AutoRegression (VAR) model and Impulse Response Functions (IRF). Understanding why we need to convert raw GDP into Growth Rates was a steep learning curve. Furthermore, interpreting a system of equations where variables impact each other with varying time lags required a completely different way of thinking compared to standard linear regression. However, this challenge was very interesting, that I now feel that I have discovered completely different from what I have been learning before.

### What surprised me the most
The biggest surprise was the difference between direct mathematical equations and VAR simulations (IRF). I initially thought Consumer Sentiment was just statistical noise because its p-values were not significant in the direct equation for GDP. However, by looking closely at the IRF graphs, I discovered it actually has a significant indirect impact on the economy exactly two quarters later. This realization taught me that the interpretation can be different across analyses, and we cannot fully rely on one of them, as we will find ourselves missing some intuition otherwise.

### Future Extensions
If I had more time and resources, I would extend this project by introducing. variables that capture global supply chain metrics or energy prices (like crude. oil). I would also be interested in applying this exact same VAR framework to other countries, such as Japan or the Eurozone, to see if their economies remember shocks for longer or shorter periods than the U.S.

## References & Resources
**Data Sources**
* University of Michigan: Consumer Sentiment (UMCSENT) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UMCSENT)
* Federal Funds Effective Rate (FEDFUNDS) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/FEDFUNDS)
* Consumer Price Index for All Urban Consumers: All Items in U.S. City Average (CPIAUCSL) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/CPIAUCSL)
* Unemployment Rate (UNRATE) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/UNRATE)
* Real Gross Domestic Product (GDPC1) from Federal Reserve Bank of St.Louis (https://fred.stlouisfed.org/series/GDPC1)

**Resources for Coding**
* Plotly Dropdown Button: https://plotly.com/python/dropdowns/
* Stationarity of Data: https://otexts.com/fpp3/stationarity.html
* VAR Model Implementation: [Official statsmodels VAR documentation](https://www.statsmodels.org/stable/vector_ar.html)
* IRF(Impulse Response Function): https://www.statsmodels.org/stable/generated/statsmodels.tsa.vector_ar.irf.IRAnalysis.html
* Plotting Error Bands: [Plotly Continuous Error Bands](https://plotly.com/python/continuous-error-bars/)
* AI Assistance: Gemini (for code debugging, optimization)
