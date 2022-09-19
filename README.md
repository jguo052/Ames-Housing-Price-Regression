# Problem Statement

*In this project I am assuming the role of a Zillow employee*

**Zillow** is an American tech real-estate marketplace. **Our website advertises home and rental units** for property owners and managers. These advertisement services are one the company's primary source of income.

One feature that **Zillow** is known for is that it **provides free public estimates on the value of any home**. In this project, **we use data on home sales in Ames, Iowa** and create several linear regression models that **attempt to predict the sale price of a home** based on some of its information (size in square feet, number of bedrooms, neighborhood, etc). The value of having stronger price predictions is to improve public perception of Zillow and its reliability, ultimately increasing the number of users willing to purchase advertisement on our website.

We will deem our project successful if our model predicts sale prices of unseen data well. More precisely, **we will call our model succesful if the R squared score is above 0.75**.

---

# Summary



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


---


## Submission

Materials must be submitted by the beginning of class on **Monday, Sept. 19**.

The last day for the Kaggle competition will be **Monday, Sept. 19**.

Your technical report will be hosted on Github Enterprise. Make sure it includes:

- A README.md (that isn't this file)
- Data files
- Presentation slides
- Any other necessary files (images, etc.)

**Check with your instructors for how they would like you to submit your repo.**

---

## Presentation Structure

- **Must be within time limit of 8 minutes.**
- Use Google Slides or some other visual aid (Keynote, Powerpoint, etc).
- Consider the audience.
- Start with the **data science problem**.
- Use visuals that are appropriately scaled and interpretable.
- Talk about your procedure/methodology (high level).
- Talk about your primary findings.
- Make sure you provide **clear recommendations** that follow logically from your analyses and narrative and answer your data science problem.

Be sure to rehearse and time your presentation before class.

---

## Rubric

Your local instructor will evaluate your project (for the most part) using the following criteria.  You should make sure that you consider and/or follow most if not all of the considerations/recommendations outlined below **while** working through your project.

**Scores will be out of 27 points based on the 9 items in the rubric.** 
*3 points per section*

| Score | Interpretation |
| --- | --- |
| **0** | *Project fails to meet the minimum requirements for this item.* |
| **1** | *Project meets the minimum requirements for this item, but falls significantly short of portfolio-ready expectations.* |
| **2** | *Project exceeds the minimum requirements for this item, but falls short of portfolio-ready expectations.* |
| **3** | *Project meets or exceeds portfolio-ready expectations; demonstrates a thorough understanding of every outlined consideration.* |

### The Data Science Process

**Problem Statement**
- Is it clear what the student plans to do?
- What type of model will be developed?
- How will success be evaluated?
- Is the scope of the project appropriate?
- Is it clear who cares about this or why this is important to investigate?
- Does the student consider the audience and the primary and secondary stakeholders?

**Data Cleaning and EDA**
- Are missing values imputed appropriately?
- Are distributions examined and described?
- Are outliers identified and addressed?
- Are appropriate summary statistics provided?
- Are steps taken during data cleaning and EDA framed appropriately?
- Does the student address whether or not they are likely to be able to answer their problem statement with the provided data given what they've discovered during EDA?

**Preprocessing and Modeling**
- Are categorical variables one-hot encoded?
- Does the student investigate or manufacture features with linear relationships to the target?
- Have the data been scaled appropriately?
- Does the student properly split and/or sample the data for validation/training purposes?
- Does the student utilize feature selection to remove noisy or multi-collinear features?
- Does the student test and evaluate a variety of models to identify a production algorithm (**AT MINIMUM:** linear regression, lasso, and ridge)?
- Does the student defend their choice of production model relevant to the data at hand and the problem?
- Does the student explain how the model works and evaluate its performance successes/downfalls?

**Evaluation and Conceptual Understanding**
- Does the student accurately identify and explain the baseline score?
- Does the student select and use metrics relevant to the problem objective?
- Is more than one metric utilized in order to better assess performance?
- Does the student interpret the results of their model for purposes of inference?
- Is domain knowledge demonstrated when interpreting results?
- Does the student provide appropriate interpretation with regards to descriptive and inferential statistics?

**Conclusion and Recommendations**
- Does the student provide appropriate context to connect individual steps back to the overall project?
- Is it clear how the final recommendations were reached?
- Are the conclusions/recommendations clearly stated?
- Does the conclusion answer the original problem statement?
- Does the student address how findings of this research can be applied for the benefit of stakeholders?
- Are future steps to move the project forward identified?

### Organization and Professionalism

**Project Organization**
- Are modules imported correctly (using appropriate aliases)?
- Are data imported/saved using relative paths?
- Does the README provide a good executive summary of the project?
- Is markdown formatting used appropriately to structure notebooks?
- Are there an appropriate amount of comments to support the code?
- Are files & directories organized correctly?
- Are there unnecessary files included?
- Do files and directories have well-structured, appropriate, consistent names?

**Visualizations**
- Are sufficient visualizations provided?
- Do plots accurately demonstrate valid relationships?
- Are plots labeled properly?
- Are plots interpreted appropriately?
- Are plots formatted and scaled appropriately for inclusion in a notebook-based technical report?

**Python Syntax and Control Flow**
- Is care taken to write human readable code?
- Is the code syntactically correct (no runtime errors)?
- Does the code generate desired results (logically correct)?
- Does the code follows general best practices and style guidelines?
- Are Pandas functions used appropriately?
- Are `sklearn` methods used appropriately?

**Presentation**
- Is the problem statement clearly presented?
- Does a strong narrative run through the presentation building toward a final conclusion?
- Are the conclusions/recommendations clearly stated?
- Is the level of technicality appropriate for the intended audience?
- Is the student substantially over or under time?
- Does the student appropriately pace their presentation?
- Does the student deliver their message with clarity and volume?
- Are appropriate visualizations generated for the intended audience?
- Are visualizations necessary and useful for supporting conclusions/explaining findings?

In order to pass the project, students must earn a minimum score of 1 for each category.
- Earning below a 1 in one or more of the above categories would result in a failing project.
- While a minimum of 1 in each category is the required threshold for graduation, students should aim to earn at least an average of 1.5 across each category. An average score below 1.5, while it may be passing, means students may want to solicit specific feedback in order to significantly improve the project before showcasing it as part of a portfolio or the job search.

### REMEMBER:

This is a learning environment and you are encouraged to try new things, even if they don't work out as well as you planned! While this rubric outlines what we look for in a _good_ project, it is up to you to go above and beyond to create a _great_ project. **Learn from your failures and you'll be prepared to succeed in the workforce**.
