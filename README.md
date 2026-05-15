# Analysis-of-Economic-Variables-and-Modeling-Economic-Growth
# Analysis of Macroeconomic Data and Modeling of Real GDP

Takahiro Hikida 

16 May 2026

## Introduction
### Motivation
When the Federal Reserve (US central bank) raises interest rates or unemployment spikes, the impact on Economic Growth (GDP) doesn’t happen overnight. Instead, economic variables act like falling dominoes, where a shock in one area creates a ripple effect that takes months or even years to fully materialize.

While simple correlations can show us what the economy looks like at a specific snapshot in time, they fail to capture these crucial time delays (lags) and chain reactions. I wanted to look beyond the surface and mathematically decode the hidden engine of the economy.

### Questions asked
1. How has the US economy evolved over time?
2. 2. How long does economic variables take to affect the Economic Growth?
3. Does “Consumer Sentiment” (how people feel about the economy) actually drive real Economic Growth, or is it merely statistical noise?
4. To what extent can we mathematically model and predict the structural portion of Economic Growth, separating it from unpredictable external shocks?
   
### The Approach
To answer the questions above, I had to learn and implement a new technique: the VAR (Vector AutoRegression) model and Impulse Response Function (IRF) analysis.

Unlike simple linear regression, a VAR model consists of a system of equations that allows multiple variables to influence each other over time. By combining this advanced time-series technique with interactive Plotly visualizations, I have built a data narrative that simulates how an initial “shock” (like a sudden rate hike) ripples through the US economy.

### Data Used
I used the data all from Federal Reserve Bank of St.Louis as csv files.

* University of Michigan: Consumer Sentiment (UMCSENT) from Federal Reserve Bank of St.Louis
* Federal Funds Effective Rate (FEDFUNDS) from Federal Reserve Bank of St.Louis
* Consumer Price Index for All Urban Consumers: All Items in U.S. City Average (CPIAUCSL) from Federal Reserve Bank of St.Louis
* Unemployment Rate (UNRATE) from Federal Reserve Bank of St.Louis
* Real Gross Domestic Product (GDPC1) from Federal Reserve Bank of St.Louis
  
## Procedure
### 1. Data Collection and Wrangling

### 2. Visualizing the Macroeconomic Landscape over Time
Before feeding the data into a complex mathematical model, it is crucial to visually inspect the historical trends of our variables. The time-series plots belowvariables.html illustrate the dynamic behavior of the U.S. economy over the past few decades. 

Key Observations:

Major Economic Shocks: We can clearly identify massive spikes and drops in the Economic Growth Rate and Unemployment Rate, particularly around the 2008 Financial Crisis and the 2020 COVID-19 pandemic. These are profound, unpredictable external shocks.

Inverse Relationships: Visually, there appears to be a natural friction between the Unemployment Rate and Economic Growth—when one spikes, the other plummets.

The “Lag” Intuition: If you look closely at the Federal Funds Rate and Inflation, their peaks and valleys do not always perfectly align with the dips in Economic Growth. They seem to trail behind or precede the growth curve, confirming our initial hypothesis: economic variables do not react instantly; they operate on a time delay.

### 3. The Ripple Effect: Impulse Response Analysis
Now that we have a valid structural model, we can finally answer our core questions by running an Impulse Response Function (IRF). An IRF allows us to simulate a hypothetical scenario: What exactly happens to Economic Growth over the next 10 quarters if we apply a sudden “shock” (a 1-standard-deviation increase) to one specific variable, while holding everything else constant?

The Unemployment Shock: When the Unemployment Rate spikes, the model shows an immediate and mathematically significant negative impact on Economic Growth. However, the graph reveals that the economy doesn’t recover instantly; the negative drag persists for several quarters before returning to the baseline, illustrating the “sticky” nature of job losses.

The Federal Funds Rate Shock: A sudden hike in interest rates by the Fed creates a delayed reaction. It doesn’t instantly crash the economy in Quarter 1. Instead, the model captures how the higher borrowing costs slowly seep into the system, steadily dragging down Economic Growth in the subsequent quarters (lags 2 and 3) before leveling out.

The “Consumer Sentiment” Revelation: One of the most surprising insights came from testing Consumer Sentiment. While it makes intuitive sense that a pessimistic public would spend less and slow down growth, the p-values in our VAR model suggested otherwise. Consumer Sentiment ultimately proved to be statistically insignificant when controlling for hard data like unemployment and interest rates. It turns out, how people feel about the economy does not independently drive growth; rather, their feelings are merely a reaction to the hard data.

### 4. Modeling the Engine: Actual vs. Predicted Growth
Given the information above, we are able to create an equation that best represents the present Economic Growth with the given parameters. The graph below plots the actual historical Economic Growth (Blue) against what our mathematical model predicted (Red).

Interpreting the Accuracy Metrics:

An $R^2$ of 0.253: In the context of physics, a 25% explanatory power might seem low. However, in macroeconomics, this is a profound finding. It mathematically proves that about 25% of the U.S. economic growth is strictly driven by the structural, delayed cycles of past unemployment, interest rates, and inflation.
The Remaining 75%: The moments where the actual data (Blue) drastically breaks away from our prediction (Red)—such as the massive 2020 spike—represent the remaining 75%. These are the unpredictable “black swan” events, like global pandemics or sudden geopolitical crises, which cannot be forecasted merely by looking at last quarter’s interest rates.
By filtering out that 75% of unpredictable noise, we now have a clean, mathematical baseline of the economy’s internal engine.

## Conclusion & Reflection
Our journey into the macroeconomic “domino effect” yielded powerful insights into how the U.S. economy actually operates beneath the surface. By moving beyond simple snapshots and building a time-delayed mathematical model, we answered our three core questions:

### 1. The Mathematical Memory of the Economy:
We confirmed that economic shocks do not happen overnight. The Federal Funds Rate and Unemployment Rate act as strong, delayed forces. Our optimized VAR model proved that about 25.3% of America’s Economic Growth is structurally determined by these past variables, leaving the rest to unpredictable, external “black swan” events.

### 2. The Biggest Surprise: A Mirror, Not a Motor
Perhaps the most surprising finding was the statistical insignificance of Consumer Sentiment. Going into this project, I hypothesized that how people feel about the economy would drive their spending and, consequently, GDP. However, the Impulse Response Function (IRF) proved otherwise. Consumer Sentiment turned out to be just statistical noise when controlling for hard data. It is a trailing indicator—a mirror reflecting the economy, not a motor driving it.

### Challenges & Learning a “New Technique”
The most challenging part of this project was stepping outside the standard CS-215 curriculum to learn and implement the Vector AutoRegression (VAR) model and Impulse Response Functions (IRF). Understanding how to make the data “stationary” (converting raw GDP into Growth Rates to avoid false correlations) was a steep learning curve. Furthermore, interpreting a system of equations where variables impact each other with varying time lags required a completely different way of thinking compared to standard linear regression. However, this challenge was incredibly rewarding, as it allowed me to simulate realistic, dynamic economic scenarios.

### Future Extensions
If I had more time and resources, I would extend this project by introducing variables that capture global supply chain metrics or energy prices (like crude oil). I would also be interested in applying this exact same VAR framework to other countries, such as Japan or the Eurozone, to see if their economies “remember” shocks for longer or shorter periods than the U.S.
