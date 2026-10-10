# Customer Market Segmentation with K-Means

An unsupervised machine learning project that groups customers into segments based on how **satisfied** and how **loyal** they are, using K-Means clustering from scikit-learn.

## The goal

Not every customer is the same. A business can only act on that if it knows which groups exist. This project finds natural customer groups in the data without any labels, so each group can be understood and treated differently.

## Dataset

30 customers, each with two features:

| Feature | Description |
|---------|-------------|
| `Satisfaction` | Satisfaction score from 1 (low) to 10 (high) |
| `Loyalty` | Loyalty score, roughly -1.7 (disloyal) to +1.4 (very loyal) |

## What I did

1. **Explored the data.** A scatter plot of satisfaction against loyalty showed that the customers form visible groups.
2. **First attempt: K-Means with 2 clusters on the raw data.** The result split customers almost entirely by satisfaction and ignored loyalty. Satisfaction ranges from 1 to 10 while loyalty only spans about 3 units, so satisfaction dominated the distance calculation.
3. **Standardized both features** so each has a mean of 0 and a standard deviation of 1. Both variables now count equally.
4. **Used the elbow method.** I ran K-Means for 1 to 9 clusters and plotted the within-cluster sum of squares (WCSS). The curve drops sharply up to about 4 clusters and flattens afterwards, so 4 clusters is the natural choice.
5. **Explored the final solution.** I fitted K-Means on the standardized data, assigned each customer to a cluster and plotted the result.

## Results

The data separates into four customer segments (values are approximate averages):

| Segment | Satisfaction | Loyalty | Meaning |
|---------|--------------|---------|---------|
| Champions | High (~8.6) | High (+1.0) | Happy and loyal. The most valuable group. |
| Happy but not committed | High (~8.1) | Low (-0.4) | Satisfied, but could still leave. |
| Loyal but unhappy | Low-mid (~4.3) | High (+0.8) | Stay despite low satisfaction. |
| Alienated | Low (~3.4) | Low (-1.4) | Unhappy and disloyal. Most likely to churn. |

## Conclusion

- **Scaling matters.** Without standardizing, K-Means ignored loyalty and gave a misleading result. Features on different scales must be standardized first.
- **The elbow method points to 4 segments**, and these are easy to interpret.
- **Satisfaction and loyalty are not the same thing.** Satisfied customers are not always loyal, and loyal customers are not always satisfied, so a business needs different actions for each segment:
  - *Champions*: reward and keep them
  - *Happy but not committed*: build loyalty with offers or a rewards programme
  - *Loyal but unhappy*: fix their pain points before a competitor does
  - *Alienated*: decide whether they are worth the cost of winning back

## How to run

1. Install the requirements:
   ```
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
2. Keep `3.12.+Example.csv` in the same folder as the notebook
3. Open `Market_Segmentation.ipynb` in Jupyter and run the cells from top to bottom

## Tech used

Python, pandas, NumPy, scikit-learn (KMeans), Matplotlib, Seaborn, Jupyter Notebook
