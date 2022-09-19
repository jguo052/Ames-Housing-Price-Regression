# Problem Statement

*In this project I am assuming the role of a Zillow employee*

**Zillow** is an American tech real-estate marketplace. **Our website advertises home and rental units** for property owners and managers. These advertisement services are one the company's primary source of income.

One feature that **Zillow** is known for is that it **provides free public estimates on the value of any home**. In this project, **we use data on home sales in Ames, Iowa** and create several linear regression models that **attempt to predict the sale price of a home** based on some of its information (size in square feet, number of bedrooms, neighborhood, etc). The value of having stronger price predictions is to improve public perception of Zillow and its reliability, ultimately increasing the number of users willing to purchase advertisement on our website.

We will deem our project successful if our model predicts sale prices of unseen data well. More precisely, **we will call our model succesful if the R squared score is above 0.75**.

---

# Process

We began by reading through the data descriptions and selecting a subset of 32 columns from the 81 total. These 32 felt like they would be the most informative for predicting `saleprice` or they appeared to columns that I wanted into somehow incorporate in the model. Many columns evaluated the quality or condition of some aspect of the home. I believed this would useful values but did not want them both, so I converted them into numerical values and took the product of the each quality-condition pair. The goal with this was to notice homes that scored high in both of these quality and condition columns. I also combined some columns in basic ways: summed full bath and half bath counts (scaling half bath counts by 1/2), and similarly summed finished basement area and unfinished basement area (again scaling unfinished basement area by 1/2). Some of the square foot related columns did not seem clear to me, so I made a more explicit column that came from the sum of the areas of the first and second floor areas. This was more or less the extent of my feature engineering.

Besides removing a few outliers, I moved on to picking a more specific set of features more carefully. I looked at which numeric columns had the highest correlation to the `saleprice` which were trying to predict. The most correlated column was the square foot column `sq_ft` (first and second floor combined). From these columns, I initially excluded any that produced variance inflation factor scores larger than 5 with `sq_ft`. My first numeric features were `sq_ft` and `bsmt_weighted_sf`.

I then examined the distributions within each categorical column to determine which were most diverse. My hope was that such columns would create separation between the sale prices and improve our predictions. These columns were `neighborhood` and `house_style`.

This allowed me to create the first model wich obtained an R squared score of 81%. From here, I was curious about incorporating more features. I started with the ones that produced the lowest VIF scores, but this hurt my model's scores. Then I chose to incorporate more features while being a bit more lax about VIF scores, since my main concern was prediction. This improved my models scores but I believed it also made my model more overfit. This did not appear in the scores of the train and validation sets, though. I tried to combat this with Ridge and Lasso, but the scores hardly changed. My final model was one where I drop a few features to decrease overfitting and gain interpretability.

---

# Conclusion

#### Prediction

Our goal was to build a linear regression model that accurately can predict the sale prices of homes in Ames, Iowa. Our metric for success was if our model exceeded an R squared score of 75%. Such a model would account for 75% of the variability in the sale price values.

Our production model above achieved an R squared value of 87.9% on unseen data. This demonstrates that it produces fairly reliable price predictions and can be pushed to the public.

Since this is one of the primary features Zillow offers, having stronger performing predictions is extremely relevant to our brand and credibility. Since our revenue stems from advertisement purchases, better public perception is directly related to the company's profitability.

#### Inference 

Beyond predicting home prices, our model also provides insight to how these different features influence the price of the home.

Before we say more her is the list of the features used in our model:
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

For example, from this list we can see that the least expensive neighborhoods Edwards, Brookside, Meadow Villag, Old Town (Excluding Iowa Department of Transportation and Railroad (IDOTRR)). This kind of information may be of interest to the public and it may be worthwhile to share on our website. This way people will have even more reasons to visit our site, increasing the value in creating ads on our site.


#### Next Steps

Our model is definitely has potential to generate stronger predictions. Also our y-value vs residuals plot show that there may be some minor sale price patterns in our data that we have not entirely captured into our model. These improvements would likely be fairly small and require a lot of time to gain with the current dataset.

If there is interest pursuing stronger predictions still, the main recommendations I would make would be to consider incorporating categorical features that I ruled out because they were quite homogenous (more than 75% of the values were identical). Some of these features may do a good job at predicting the highest value homes which is where the model seems to perform the weakest according to the residuals scatterplot.

Another option would be to look back through data I ruled out before beginning the project. The original dataset includes 80 features, and after some light exploratory data analysis performed outside of these notebooks, I settled on starting with 32 variables.