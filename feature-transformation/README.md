# Feature Transformation

The featured transformation techniques are used to transform the data to normal distribution for better performance of the algorithm.
- FunctionTransformer
    - Log Transform
    - Square Transform
    - Square Root Transform
    - Reciprocal Transform
    - Custom Transform
- PowerTransformer
    - Box-Cox Transform
    - Yeo-Johnson Transform
- QuantileTransformer

## [FunctionTransformer](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.FunctionTransformer.html#sklearn.preprocessing.FunctionTransformer)

- Constructs a transformer from an arbitrary callable.

- A FunctionTransformer forwards its X (and optionally y) arguments to a user-defined function or function object and returns the result of this function. This is useful for stateless transformations such as taking the log of frequencies, doing custom scaling, etc.


## [PowerTransformer](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.PowerTransformer.html#sklearn.preprocessing.PowerTransformer)

- Apply a power transform featurewise to make data more Gaussian-like.
- Currently, PowerTransformer supports the Box-Cox transform and the Yeo-Johnson transform. The optimal parameter for stabilizing variance and minimizing skewness is estimated through maximum likelihood.
- Box-Cox requires input data to be strictly positive which return the transformed values between -5 to 5, while Yeo-Johnson supports both positive or negative data.
