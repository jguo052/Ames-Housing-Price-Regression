# Problem Statement

*In this project I am assuming the role of a Zillow employee*

Zillow is an American tech real-estate marketplace. Our website advertises home and rental units for property owners and managers. These advertisement services are one the company's primary source of income.

One feature that **Zillow** is known for is that it **provides free public estimates on the value of any home**. In this project, **we use data on home sales in Ames, Iowa** and create several linear regression models that **attempt to predict the sale price of a home** based on some of its information (size in square feet, number of bedrooms, neighborhood, etc). The value of having stronger price predictions is to improve public perception of Zillow and its reliability, ultimately increasing the number of users willing to purchase advertisement on our website.

We will deem our project successful if our model predicts sale prices of unseen data well. More precisely, **we will call our model succesful if the R squared score is above 0.75**.

---
# Data

[Our data](https://www.kaggle.com/datasets/prevek18/ames-housing-dataset) consists of 2930 observations of residential home sales in Ames, Iowa between 2006 and 2010. Each observation has 82 variables describing various features and qualities of the home and property (for example land contour, neighborhood, number of half bathrooms, etc). A thorough description of the variables [can be found here](https://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

---

# Summary

Our goal is to preict the `saleprice` column of our dataset using linear regression for the sake of interpretability (we want to see as precisely as possible how much influence each variable has over the sales price). I found using 82 variables to be too noisy, so I selected a subset of 32 variables to initially explore. I generally opted to include variables that seemed remotely likely to influence sales price with the intention of removing more features throughout the analysis.

There were several variables that were closely related (e.g. finished and unfinished basement area). It seemed natural to to combine these features into a single one. For the example of finished and unfinished basement area, these two columns were combined through the computation $$1 \cdot (\text{finished area}) + \frac{1}{2} \cdot (\text{unfinished area})$$
A handful of other variables were combined in a similar way.

By looking at how much each numeric column correlated to our target, I identified the square footage of each home to be the numeric feature I most wanted to include in our model. Because we want the coefficients of our linear regression to be interpretable, it important to reduce any multicollinearity from our variables as possible. I accomplished this by looking at variance inflation factors (VIF) between the variables aside from `saleprice`. I excluded any variables that produced VIF scores larger than 5 with the square footage column. This resulted in including the columns `sq_ft` and `bsmt_weighted_sf` for our first attempt at a linear model.

To decide which categorical variables to include, I examined the distribution of the different categories within each variable. Some variables were highly imbalanced while others not so much. I chose to include `neighborhood` and `house_style` in the regression model because they seemed the most diverse and likely to demonstrate separation in sales price. With this choice of variables, my first regression model produced an R squared score of 81%.

From here, I was curious about how much of an impact incorporating additional features would have on our linear regression model (we were quite strict with our selection of variables in our initial model). The plan was to create several other linear models along with two that were regularized. After several iterations of being more lax about VIF scores, my model's R squared score improved but I got the impression that it was becoming overfit. I tried to combat this with Ridge and Lasso regularization, but the scores hardly changed.

![A bar graph of R squared scores for different linear models.](../images/iteration_scores.png)

The final model was produced by including a few additional features from our initial model, namely: garage area, kitchen quality, quality-condition, and exterior quality-condition. This improved the R squared score to 87% and did not feel like it tarnished the interpretability of the model too much.

---

# Conclusion

#### Prediction

Our goal was to build a linear regression model that accurately can predict the sale prices of homes in Ames, Iowa. Our metric for success was if our model exceeded an R squared score of 75%. Such a model would account for 75% of the variability in the sale price values.

Our production model achieved an R squared value of 87.9% on unseen data. This demonstrates that it produces fairly reliable price predictions and can be pushed to the public.

Since this is one of the primary features Zillow offers, having stronger performing predictions is extremely relevant to our brand and credibility. Since our revenue stems from advertisement purchases, better public perception is directly related to the company's profitability.

#### Inference 

Beyond predicting home prices, our model also provides insight to how these different features influence the price of the home.

Before we say more, here is the list of the features used in our model:
- square feet in the first and second floor
- basement square feet (unfinished basement are counted at half size)
- year the home was built
- neighborhood of the home
- number of finished stories in the home
- the quality of the kitchen (rated 1 through 5)
- the quality and condition of the home (rated 1 through 100)
- the exterior quality and condition of the home (rated 1 through 25)

One major take-away from our model is illustrated below. The list below shows how the price of a 1.5-story home (with a finished second floor) in different neighborhoods compare to Bloomington Heights. Of course this also allows you compare prices between the different neighborhoods outside of Bloomington Heights, too.

- GrnHill: 82623.69
- StoneBr: 41322.64
- Veenker: 27030.92
- NoRidge: 21249.94
- NridgHt: 18848.16
- Somerst: 10805.49
- Crawfor: 8042.97
- Timber: 7886.61
- Gilbert: 5868.0
- ClearCr: 3886.62
- CollgCr: 2751.02
- SawyerW: -3711.63
- Mitchel: -9249.54
- Landmrk: -11170.31
- Blueste: -12267.77
- NWAmes: -13529.22
- Sawyer: -14872.17
- NPkVill: -14928.61
- NAmes: -16464.14
- BrDale: -16796.03
- Greens: -19130.41
- SWISU: -19836.41
- Edwards: -20379.92
- BrkSide: -20652.11
- MeadowV: -26773.32
- IDOTRR: -28981.9
- OldTown: -34586.64

For example, from this list we can see that the least expensive neighborhoods are Edwards, Brookside, Meadow Villag, Old Town (Excluding Iowa Department of Transportation and Railroad (IDOTRR)). This kind of information may be of interest to the public and it may be worthwhile to share on our website. This will provide additional incentive to visit our website and increase ad revenue.

#### Next Steps

Our model definitely has potential to generate stronger predictions. Moreover, our y-value vs. residuals plot shows that there may be some minor sale price patterns in our data that we have not entirely captured into our model. Making such improvements to our model would likely require a fair bit of effort and may not be worth the performance improvements.

If there is interest pursuing stronger predictions still, the main recommendations I would make would be to consider incorporating categorical features that I ruled out because they were quite homogenous (more than 75% of the values were identical). Some of these features may do a good job at predicting the highest value homes which is where the model seems to perform the weakest according to the residuals scatterplot.

Another option would be to look back through data I ruled out before beginning the project. The original dataset includes 82 features, and after some light exploratory data analysis performed outside of these notebooks, I settled on starting with 32 variables. It may be the case that my intuition led me to ignore an informative variable.