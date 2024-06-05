# DL_project

## ANN Model:
1. Normalization: It can be used when data does contain outliers. Scikit-Learn provides a transformer called MinMaxScaler for this. It has a feature_range hyperparameter that lets you change the range if, for some 
reason, you don’t want 0–1 (e.g., neural networks work best with zero-mean inputs, so a range of –1 to 1 is preferable).
2. Standardization: Unlike minmax scaling, standardization does not restrict values to a specific range. However, standardization is much less affected by outliers. 
3. Data with a heavy tail: When a feature’s distribution has a heavy tail (i.e., when values far from the mean are not exponentially rare), both min-max scaling and standardization will squash most values into a small 
range. Models generally don’t like this at all. So before you scale the feature, you should first transform it to shrink the heavy tail, and if possible to make the distribution roughly symmetrical. For example, a 
common way to do this for positive features with a heavy tail to the right is to replace the feature with its square root (or raise the feature to a power between 0 and 1). If the feature has a really long and heavy tail, such as a power law distribution,
then replacing the feature with its logarithm may help. Another approach to handle heavy-tailed features consists in bucketizing the feature. This means chopping its distribution into roughly equal-sized buckets, and replacing each feature value with the index of the bucket it belongs to.
4. Data with multiple peaks: When a feature has a multimodal distribution (i.e., with two or more clear peaks, called modes), it can also be helpful to bucketize it, but this time treating the bucket IDs as categories,
rather than as numerical values. This means that the bucket indices must be encoded, for example using a OneHotEncoder (so you usually don’t want to use too many buckets). This approach will allow the model to more
easily learn different rules for different ranges of this feature value. Another approach to transforming multimodal distributions is to add a feature for each of the modes (at least the main ones). The similarity
measure is typically computed using a radial basis function (RBF)—any function that depends only on the distance between the input value and a fixed point. The most commonly used RBF is the Gaussian RBF, whose output
value decays exponentially as the input value moves away from the fixed point.