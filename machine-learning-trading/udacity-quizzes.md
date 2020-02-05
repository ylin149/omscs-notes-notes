---
id: machine-learning-trading-udacity-quizzes
title: Udacity Quizzes
course: machine-learning-trading
lecture: udacity-quizzes
---

# Udacity Quizzes - ML4T

## Reading and Plotting Stock Data
### Which Fields Should Be In A CSV File Quiz
![](https://assets.omscs.io/BED27ABE-D85D-4358-A2A3-FAE24EEDE5F6.png)

### Which Fields Should Be In A CSV File Quiz Solution
![](https://assets.omscs.io/EFB7C1BB-0A52-4357-83E9-D5BCCB262559.png)

We want to include data that changes frequently; otherwise, we are wasting space including redundant data. Of the options given, both “date/time” and “price of the stock” are good fits. The other data points are either static or change relatively infrequently.

### Compute Mean Volume Quiz
![](https://assets.omscs.io/9C27B65A-7816-42FF-880F-93D981E0A193.png)

Your task is to calculate the mean volume for each of the given symbols.

### Compute Mean Volume Quiz Solution
![](https://assets.omscs.io/99A66C8E-4B8E-413B-9713-22E7762069D9.png)

Given a DataFrame `df` containing a "Volume” column, the following code returns the mean of the values in that column.

```python
df[‘Values’].mean()
```

#### Documentation
- [pandas.DataFrame.mean](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mean.html)

### Plot High Prices for IBM Quiz
![](https://assets.omscs.io/6217684A-EBD2-4031-9155-E2306FB95161.png)

Your task is to plot the high prices for IBM.

### Plot High Prices for IBM Quiz Solution
![](https://assets.omscs.io/D4229E90-CE7E-4317-AC11-555F0D1701ED.png)

First, we need to make sure that we read in the right CSV, which we can accomplish with:

```python
df = pd.read_csv(‘data/IBM.csv’)
```

Next, we can retrieve the “High” column and plot it:

```python
df[‘High’].plot()
```

## Working With Multiple Stocks
### NYSE Trading Days Quiz
![](https://assets.omscs.io/5A7D6772-A997-4543-BFBF-5DC11F911F1F.png)

### NYSE Trading Days Quiz Solution
![](https://assets.omscs.io/1569B3C1-4D74-44D9-895F-57F66260BDCD.png)

See the breakdown [here](https://www.nyse.com/publicdocs/Trading_Days.pdf) (for 2018 and 2019).

### Types of Joins Quiz
![](https://assets.omscs.io/C6F35EA2-BEB7-44C2-914E-73C3F8A4414F.png)

We can avoid having to explicitly call `dropna` on line 22 by passing a certain value for the ‘how’ parameter of the `join` call on line 19. 

What is the value of that parameter?

### Types of Joins Quiz Solution
![](https://assets.omscs.io/24945379-86BC-488E-85FD-C9E88E049F00.png)

#### Documentation
- [pandas.DataFrame.join](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.join.html)

### Utility Functions for Reading Data Quiz
If we look at the code we have written so far, we see some duplication.

![](https://assets.omscs.io/B6F23728-810F-4698-8918-B0753B06C098.png)

Your task is to consolidate this code into one location: the utility function `get_data`.

![](https://assets.omscs.io/967D338A-969A-4343-A6BC-63A9269C4486.png)

### Utility Functions for Reading Data Quiz Solution
We have consolidated both the DataFrame initialization code and the joining code. 

![](https://assets.omscs.io/7BB55353-D82C-4369-AFFC-3CFB0A873D21.png)

Additionally, since we are using SPY as our baseline, we drop all rows from `df` where SPY has not traded - that is, where the SPY column has `NaN` values - with the following code:

```python
df = df.dropna(subset=[“SPY”])
```

#### Documentation
- [pandas.DataFrame.dropna](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html)
 
### How to Plot on “Equal Footing” Quiz
![](https://assets.omscs.io/533F01B4-36B8-4898-A860-8B735E1ADA08.png)

### How to Plot on “Equal Footing" Quiz Solution
![](https://assets.omscs.io/EF3D7A60-CF3B-4769-A3F8-D5157B461134.png)

While both of these are technically correct, the second approach leverages *vectorization* which is must faster than the iterative approach. Read more about vectorization [here](https://engineering.upside.com/a-beginners-guide-to-optimizing-pandas-code-for-speed-c09ef2c6a4d6).

### Slice and Plot Two Stocks Quiz
![](https://assets.omscs.io/5E5020D1-2E8C-422B-8867-733B8E88945C.png)

Your task is to write code that first slices `df` along the rows bounded by `start_index` and `end_index` and across `columns`, and then passes the slice to the `plot_selected` method.

### Slice and Plot Two Stocks Quiz Solution
![](https://assets.omscs.io/B76701D9-2822-4191-9B93-E49454905AD8.png)

We can create our slice using the following code, which we then pass to the `plot_data` method:

```python
df.ix[start_index:end_index, columns]
```

#### Documentation
- [pandas.DataFrame.ix - DEPRECATED](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ix.html)
- [pandas.DataFrame.loc](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html)
- [pandas.DataFrame.iloc](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.iloc.html)

## The Power of NumPy
### Replace a Slice Quiz
![](https://assets.omscs.io/1E2BC0CC-EADA-4431-ABDF-AE07857CF80D.png)

We need to move data from the last two rows and the last two columns of `nd2` to the first two rows and the first two columns of `nd1`. 

### Replace a Slice Quiz Solution
![](https://assets.omscs.io/60DEA1EE-99C0-4CC6-95F7-B01B9681CD59.png)

Let’s first look at how we can slice `nd2` to extract the data we want. We can slice the last two rows using negative indexing: `-2:`. We can slice the last two columns as `2:4`. Remember that NumPy indexing is upper-bound exclusive.

Now let’s see how we can transplant that data into `nd1`. We can select the first two rows of `nd1` as `0:2`, and we can select the first two columns as `0:2`.

The complete data transfer can be accomplished with the following code:

```python
nd1[0:2, 0:2] = nd2[-2:, 2:4]
```

#### Documentation
- [Indexing](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html)
 
### Specify the Data Type Quiz
![](https://assets.omscs.io/1A04EA50-3DE1-4BA2-85E6-B852F298AB7B.png)

We saw that the elements in an array created by `np.ones` are floats by default. Our task here is to update the call to `np.ones` and pass in a parameter that tells NumPy to give us integers instead of floats.

### Specify the Data Type Quiz Solution
![](https://assets.omscs.io/29CA699E-4950-4B22-948D-A38910E9A9EA.png)

We can accomplish this change with the following code:

```python
np.ones((5, 4), dtype=np.int_)
```

#### Documentation
- [numpy.ones](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ones.html)
- [Data types](https://docs.scipy.org/doc/numpy/user/basics.types.html#data-types)

### Locate Maximum Value Quiz
![](https://assets.omscs.io/55FC058B-8B31-4172-8F44-B44502611542.png)

Our task is to implement the function `get_max_index`, which takes a one-dimensional ndarray `a` and returns the index of the maximum value.

### Locate Maximum Value Quiz Solution
![](https://assets.omscs.io/480BE86C-66FF-452B-965F-AD9833D98574.png)

We can retrieve the index of the maximum value in `a` with the `argmax` method:

```python
def get_max_index(a):
	return a.argmax()
```

#### Documentation
- [numpy.argmax](https://docs.scipy.org/doc/numpy/reference/generated/numpy.argmax.html#numpy.argmax)

## Statistical Analysis of Time Series

### Which Statistic to Use Quiz

Assume we are using a rolling mean to track the movement of a stock. We are looking for an opportunity to find when the price has diverged significantly far from the rolling mean, as we can use this divergence to signal a buy or a sell.

Which statistic might we use to discover if the price has diverged significantly enough?

![](https://assets.omscs.io/2020-01-12-17-51-42.png)

### Which Statistic to Use Quiz Solution

![](https://assets.omscs.io/2020-01-12-17-52-03.png)

Standard deviation gives us a measure of divergence from the mean. Therefore, if the price breaches the standard deviation, we may conclude that the price has moved significantly enough for us to consider buying or selling the stock.

### Calculate Bollinger Bands Quiz

Computing Bollinger bands consists of three main steps: first, computing the rolling mean; second, computing the rolling standard deviation and; third, computing the upper and lower bands.

Our goal is to implement the three functions below to accomplish these tasks.

![](https://assets.omscs.io/2020-01-12-19-11-03.png)

### Calculate Bollinger Bands Quiz Solution

Given an ndarray `values` and a window `window`, we can calculate the rolling standard deviation as follows:

```python
# OLD
pd.rolling_std(values, window=window)

# NEW
values.rolling(window).std()
```

Given a rolling mean `rm` and a rolling standard deviation `rstd`, we can calculate the Bollinger bands as follows:

```python
rm + (2 * rstd), rm - (2 * rstd)
```

![](https://assets.omscs.io/2020-01-12-19-22-39.png)

#### Documentation
- [pandas.DataFrame.rolling](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rolling.html)

### Compute Daily Returns Quiz

![](https://assets.omscs.io/2020-01-12-22-45-10.png)

Our task is to implement a function `compute_daily_returns` that receives a DataFrame `df` and returns a DataFrame consisting of the daily return values. The returned DataFrame must have the same number of rows as `df`, and any rows with missing data must be filled with zeroes.

### Compute Daily Returns Solution

![](https://assets.omscs.io/2020-01-12-22-50-41.png)

Given a DataFrame `df` with `n` rows, we can create a new DataFrame with `n + m` rows where each row is shifted down `m` rows with the following code:

```python
df.shift(m)
```

Note that the newly created `m` rows at the top of the DataFrame will be filled with `NaN` values.

Therefore, we can divide every price in our DataFrame `df` by the price on the previous day like this:

```python
df / df.shift(1)
```

We can complete the daily return calculation, and generate a DataFrame `daily_returns` like so:

```python
df / df.shift(1) - 1
```

The only thing we have to consider now is the first row in `daily_returns`. Since the first row in the shifted DataFrame is filled with `NaN` values, any subsequent mathematical operations on those values yield `NaN`.

However, our task was to fill any rows with missing data with zeroes. We can fix `daily_returns` like this:

```python
# Deprecated
daily_returns.ix[0, :] = 0

# Use this
daily_returns.iloc[0] = 0
```

#### Documentation
- [pandas.DataFrame.shift](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shift.html)
- [pandas.DataFrame.ix - DEPRECATED](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ix.html)
- [pandas.DataFrame.loc](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html)
- [pandas.DataFrame.iloc](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.iloc.html)

## Incomplete Data

### Pandas fillna() Quiz

![](https://assets.omscs.io/2020-01-14-00-38-50.png)

Our task is to find the parameter that we need to pass to `fillna` to fill forward missing values.

### Pandas fillna() Quiz Solution

![](https://assets.omscs.io/2020-01-14-00-40-02.png)

#### Documentation
- [pandas.DataFrame.fillna](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.fillna.html)

### Fill Missing Values Quiz

If we look at the following plot of stock price data, we can see several gaps.

![](https://assets.omscs.io/2020-01-14-00-50-55.png)

Our task is to use the `fillna` method to fill these gaps.

### Fill Missing Values Solution

![](https://assets.omscs.io/2020-01-14-00-52-39.png)

We can use forward filling for gaps that have a definitive start date, and backward filling for gaps that have no beginning or begin before our date range.

#### Documentation
- [pandas.DataFrame.fillna](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.fillna.html)

## Histograms and Scatter Plots

### What Would it Look Like Quiz

Suppose that we've taken all of the SPY pricing data from over the years, generated an array of daily returns, and created a histogram from those returns.

Which of the following shapes would the histogram most likely have?

![](https://assets.omscs.io/2020-01-14-21-45-58.png)

### What Would it Look Like Quiz Solution

![](https://assets.omscs.io/2020-01-14-21-46-20.png)

### Compare Two Histograms Quiz

A common practice in finance is to plot histograms of the daily returns of different stocks together to assess how the stocks relate to each other.

Below are the daily returns histograms for SPY and XYZ, as well as three statements describing the relationship between the two.

![](https://assets.omscs.io/2020-01-14-22-30-14.png)

Which statement do you think is correct?

> Note that "vol" refers to volatility and not volume.

### Compare Two Histograms Quiz Solution

![](https://assets.omscs.io/2020-01-14-22-31-49.png)

We can see that the mean of SPY is slightly higher than the mean of XYZ, indicating that SPY outperforms XYZ.

Additionally, we can see that the XYZ curve is "flatter" than the SPY curve. This feature indicates that the daily returns of XYZ are more spread out than those of SPY, which are more centralized.

In summary, XYZ has both lower returns and higher volatility than SPY.

### Correlation vs. Slope Quiz

Given what we just learned about correlation and slope (beta), let's look at two scatterplots with their best-fit lines, and choose the most accurate statement.

![](https://assets.omscs.io/2020-01-15-22-13-09.png)

### Correlation vs. Slope Quiz Solution

![](https://assets.omscs.io/2020-01-15-22-15-24.png)

The best-fit line in the SPY vs. ABC scatterplot has a higher beta because that line has a larger slope than the corresponding line in the SPY vs. XYZ plot.

Additionally, the SPY and ABC daily returns are more highly correlated, which can be determined visually from examining how "tightly" they hug the best-fit line in the SPY vs. ABC plot.

## Sharpe Ratio and Other Portfolio Statistics

### Which Portfolio is Better Quiz

The Sharpe ratio allows us to consider our returns in the context of *risk*: the standard deviation, or volatility, of the returns. When we look at portfolio performance, we don't typically look at raw returns; instead, we adjust the returns received for the risk borne.

With this in mind, let's look at three comparisons of two stocks, ABC and XYZ, and decide which is better.

![](https://assets.omscs.io/2020-01-17-16-16-52.png)

### Which Portfolio is Better Quiz Solution

![](https://assets.omscs.io/2020-01-17-16-21-44.png)

For the first comparison, ABC is better. ABC and XYZ have similar amounts of volatility, but ABC has double the return of XYZ.

For the second comparison, XYZ is better. Both ABC and XYZ have the same return, but ABC is much more volatile than XYZ.

For the third comparison, we can't tell which is better, given the information provided. ABC has a higher return than XYZ, but that return is offset by higher volatility.

We need a qualitative measure to compare ABC and XYZ in this third example, and the Sharpe ratio is that measure.

### Form of the Sharpe Ratio Quiz

Consider the following three factors.

![](https://assets.omscs.io/2020-01-18-10-33-20.png)

How would you combine these three factors into a simple equation to create a metric that provides a measure of risk-adjusted return?

![](https://assets.omscs.io/2020-01-18-10-34-58.png)

### Form of the Sharpe Ratio Quiz Solution

![](https://assets.omscs.io/2020-01-18-10-35-43.png)

Only the third choice meets the two criteria we described earlier; all else being equal, higher returns increase our metric, and lower risk increases our metric. Additionally, a higher rate of risk-free return decreases our metric.

### What is the Sharpe Ratio Quiz

Assume we have been trading a strategy for 60 days now. On average, our strategy returns one-tenth of one percent per day. Our daily risk-free rate is two one-hundredths of a percent. The standard deviation of our daily return is one-tenth of one percent.

What is the Sharpe ratio of this strategy?

![](https://assets.omscs.io/2020-01-18-14-34-48.png)

> In financial terminology, one one-hundredth of one percent is known as a **basis point**, or "bip". Instead of saying, for example, that our strategy returns one-tenth of one percent per day, we could say it returns 10 bps per day.

### What is the Sharpe Ratio Quiz Solution

![](https://assets.omscs.io/2020-01-18-14-38-32.png)

Let's recall our formula for the Sharpe ratio:

$$
S = K * \frac{mean(R_p - R_f)}{\sigma_{R_p}}
$$

Given that $R_p = 0.001$ on average, $R_f = 0.0002$ on average, and $\sigma{R_p} = 0.001$, with a daily sample rate:

$$
S = \sqrt{252} * \frac{0.001 - 0.0002}{0.001}
$$

$$
S = \sqrt{252} * \frac{0.0008}{0.001}
$$

$$
S = \sqrt{252} * 0.8
$$

$$
S \approx 12.7
$$

## Optimizers: Building a Parameterized Model

### How to Defeat a Minimizer Quiz

Which of the following functions would be hard for the minimizer to solve?

![](https://assets.omscs.io/2020-01-20-00-40-15.png)

### How to Defeat a Minimizer Quiz Solution

![](https://assets.omscs.io/2020-01-20-00-40-46.png)

The first graph is hard because of the "flat" areas on either side of the parabola. A minimizer testing a point in the middle of this area wouldn't be able to find any gradient to follow, so it wouldn't know how to adjust the value it was currently testing.

The second graph is hard because it has several local minima that aren't necessarily the global minimum. A minimizer might "get stuck" in a local minimum, even though a more significant, global minimum exists.

The fourth graph is challenging  both because of the "flat" area and the discontinuity between the two halves.

### What is a Good Error Metric Quiz

Let's assume that a point $p_i$ has an error $e_i$, which is the vertical distance between $p_i$ and the best-fit line currently under consideration. Given a number of such errors $e_0, e_1, ..., e_n$, which of the following expressions describes the metric we want to minimize?

![](https://assets.omscs.io/2020-01-20-14-11-22.png)

### What is a Good Error Metric Quiz Solution

![](https://assets.omscs.io/2020-01-20-14-13-28.png)

We want to minimize the sum of the errors, but we want to ensure that errors above and below the line do not cancel out. To accomplish this, we need to make each error positive by either squaring it or taking its absolute value.

## Optimizers: How to Optimize a Portfolio

### Which Criteria is Easiest to Solve For Quiz

Let's assume we have a portfolio of four stocks, and we want to find the optimal allocations that maximize some performance metric. Which of the following metrics would be easiest to optimize for?

![](https://assets.omscs.io/2020-01-21-16-35-00.png)

### Which Criteria is Easiest to Solve For Quiz Solution

![](https://assets.omscs.io/2020-01-21-16-35-19.png)

It would be easiest to write an optimizer for cumulative return. To do so, all we need to do is allocate 100% of our portfolio into whichever stock had the highest cumulative return.

Optimizing for minimum volatility or Sharpe ratio involves evaluating various combinations of stocks, which is more complicated than simply putting all our eggs in one basket.

## How Machine Learning is Used at a Hedge Fund

### What's X and Y Quiz

Let's think about building a model to use in trading. Which of the following factors might be input values ($X$) to the model, and which might be output values ($Y$)?

![](https://assets.omscs.io/2020-01-22-17-57-46.png)

### What's X and Y Quiz Solution

![](https://assets.omscs.io/2020-01-22-17-58-20.png)

Since we often use models to predict values in the future, both future price and future return make sense as output values. Our model might make these predictions by considering price momentum, current price, and Bollinger values as input.

## Regression

### How to Predict Quiz

We've identified that, in KNN, for a particular query $Q$, we want to utilize the $K$ nearest data points to $Q$ to come up with a prediction. What should we do with those neighboring data points to find that prediction?

![](https://assets.omscs.io/2020-01-31-15-53-54.png)

### How to Predict Quiz Solution

![](https://assets.omscs.io/2020-01-31-15-58-08.png)

Remember that we want to predict a $y$-value for the queried $x$-value. As a result, it doesn't make sense to take the average of the $x$-values of the nearest neighbors. Additionally, we don't want to take the largest $y$-value; otherwise, the other neighbors have no influence on the prediction. The correct approach here is to take the mean of their $y$-values.

### Parametric vs Non-Parametric Quiz

Let's consider the relationship between variables in two different scenarios.

The first scenario involves firing a cannon. The independent variable is the value of the angle that the cannon makes with the ground, and the dependent variable is the horizontal distance the cannonball travels.

![](https://assets.omscs.io/2020-01-31-16-39-33.png)

The second scenario involves attracting bees to a food source. The independent variable is the richness of the food source, and the dependent variable is the number of bees attracted to that source.

![](https://assets.omscs.io/2020-01-31-16-42-14.png)

Note that this scenario is slightly different than the first because it's not clear that the number of bees always increases as richness increases.

Given these two scenarios, which, if any, is better modeled using a parametric model, and which, if any, is better modeled using a non-parametric model?

![](https://assets.omscs.io/2020-01-31-16-43-44.png)

### Parametric vs Non-Parametric Quiz Solution

![](https://assets.omscs.io/2020-01-31-16-48-54.png)

In the first scenario, we can start with an estimate of the underlying behavior of the system in terms of a mathematical equation that expresses how it behaves. This equation is just the equation of trajectory, which we can find online. We can then learn the parameters of this equation such that it describes the relationship between our variables.

In the second scenario, we have no initial estimate for the underlying mathematical equation, so it's better to use a non-parametric model, which can model any "shape" of relationship.

## Assessing a Learning Algorithm

### What Happens as K Varies Quiz

Consider the following three models, each generated using a different value for $K$.

![](https://assets.omscs.io/2020-01-27-16-18-46.png)

Our first task is to match the value of $K$ with the corresponding plot. Our second task is to decide whether we increase the chances of overfitting as we increase $K$. An **overfit** model matches the training set very well but fails to generalize to new examples.

### What Happens as K Varies Quiz Solution

![](https://assets.omscs.io/2020-01-27-16-36-13.png)

Let's consider the case where $K = 1$. In this case, the model passes through every point $P$ directly, since near $P$, the only point that has any influence is $P$.

Now consider the case where $K = N$. In this case, every point considers all of the neighbors. Thus, the generated model is a straight line passing through the mean of the $y$ values of all the points.

Of course, when $1 < K < N$, the graph lies between these two extremes. For $K = 3$, the graph roughly follows the points without passing through them directly.

As a result, we see that increases in $K$ decrease the probability of overfitting.

### What Happens as D Varies Quiz

Consider the following three polynomial models. The difference between each model is the [degree of the polynomial](https://en.wikipedia.org/wiki/Degree_of_a_polynomial) $d$.

![](https://assets.omscs.io/2020-01-27-17-08-58.png)

Our first task is to match the value of $d$ with the corresponding plot. Our second task is to decide whether we increase the chances of overfitting as we increase $d$.

### What Happens as D Varies Quiz Solution

![](https://assets.omscs.io/2020-01-27-17-23-47.png)

A polynomial of degree one matches the equation $y = m_1x + b$, which is the equation of a line and corresponds to the third plot.

A polynomial of degree two matches the equation $y = m_1x + m_2x^2 + b$, which is the equation of a parabola and corresponds to the first plot.

A third-order polynomial matches the equation $y = m_1x + m_2x^2 + m_3x^3 + b$, which corresponds to the second plot.

We see that as we increase $d$, our model begins to follow the points more closely. Indeed, it can be shown that for $N$ points, a parabola of degree $N$ exists that passes through each point.

Notice that for each of these models, we can extrapolate beyond the data given. This ability to extrapolate is a property of parametric models that instance-based models lack.

### Which is Worse Quiz

Suppose we just built a model. Which error would you expect to be larger: in-sample or out-of-sample?

![](https://assets.omscs.io/2020-01-28-23-28-25.png)

### Which is Worse Quiz Solution

In general, the out-of-sample error is worse than the in-sample error.

![](https://assets.omscs.io/2020-01-28-23-29-18.png)

### Correlation and RMS Error Quiz

Let's think about the relationship between RMS error and the correlation between $Y_{test}$ and $Y_{predict}$. Which of the following statements is true?

![](https://assets.omscs.io/2020-01-29-22-15-19.png)

### Correlation and RMS Error Quiz Solution

![](https://assets.omscs.io/2020-01-29-22-16-21.png)

In most cases, correlation decreases as RMS error increases. However, it is possible to construct examples where correlation increases as RMS error increases.

### Overfitting Quiz

Let's consider overfitting in KNN and how in-sample and out-of-sample error changes as $K$ increases from 1 to the number of items $N$ in a data set.

Which of the following plots correctly represents the shape of the error curves that we would expect for both types of error as we increase $K$?

![](https://assets.omscs.io/2020-01-30-20-56-43.png)

### Overfitting Quiz Solution

![](https://assets.omscs.io/2020-01-30-21-00-06.png)

Remember that KNN models are least generalized when $K = 1$. In other words, when $K = 1$, the model predicts each training point in the data set perfectly but fails to predict testing points accurately. As a result, KNN models overfit when $K$ is small.

### A Few Other Considerations Quiz

There are a few other factors worth considering when evaluating a learning algorithm. For each of the following factors, which of the two models has better performance?

![](https://assets.omscs.io/2020-01-30-21-11-49.png)

### A Few Other Considerations Quiz Solution

![](https://assets.omscs.io/2020-01-30-21-12-14.png)

Linear regression models require less space for persistence than KNN models. A linear regression model of degree four can be described in as few as four integers, while a KNN model must retain every single data point ever seen.

KNN models require less compute time to train than linear regression models. In fact, KNN models require zero time to train.

Linear regression models process queries more quickly than KNN models. The query time for a linear regression model is constant. The query time for KNN models grows with the number of queries, as previously queried data points are added to the data set and must be examined in subsequent queries.

Adding new data is quicker in KNN than in linear regression. Incorporating new data into a model requires retraining the model, but, as we just saw, the training time for a KNN model is zero.

## Ensemble Learners, Bagging, and Boosting

### How to Build an Ensemble Quiz

How might we go about building an ensemble of learners?

![](https://assets.omscs.io/2020-02-02-18-16-45.png)

### How to Build an Ensemble Quiz Solution

![](https://assets.omscs.io/2020-02-02-18-18-42.png)

We can create an ensemble by training several parameterized polynomials of differing degrees (A) or by training several KNN models using different subsets of data (B).

It doesn't make sense to train KNN models using randomized $Y$-values, because we want to train any model we plan to use on the actual data in our training set. As a result, neither (C) nor (E) is correct.

Instead of using just polynomial learners or KNN learners, we can combine the two into a super ensemble (D) for even better results.

### Overfitting Quiz

Which of these two models is least likely to overfit?

> Aside: the screenshot says "most likely to overfit", but he selects the model that is least likely to overfit.

![](https://assets.omscs.io/2020-02-02-20-19-46.png)

### Overfitting Quiz Solution

![](https://assets.omscs.io/2020-02-02-20-20-05.png)

### Overfitation Quiz

As we increase the number of models $m$ in our ensemble, which of the following strategies is more likely to overfit?

![](https://assets.omscs.io/2020-02-02-22-55-14.png)

### Overfitation Quiz Solution

![](https://assets.omscs.io/2020-02-02-22-55-46.png)

AdaBoost focuses primarily on improving the system for specific data points; in other words, it strives to fit. As a result, it is more susceptible to overfitting than is simple bagging.