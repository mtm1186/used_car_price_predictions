# Price Prediction Model For Used Automobiles 

###### Matthew Malone https://git.generalassemb.ly/mtm1186

## Problem Statement
In the United States used cars represent almost half of the U.S. auto retail market and is the largest retail segment of the economy. There has been a shift by consumers to purchase more affordable previously owned vechinces as automobile debt has surpassed 1 trillion dollars and now makes up 9.5% of American consumer debt. The market for used vehicles is challenging to navigate for many consumers as prices can vary widely as many formulas fail to take into the many nuances of a car.

Consumers can use online valuation calculators to get an estimate on a car but these sites tend to only factor in a few features like make, model and miles driven. They also value the car on a straight line depreciation formula which can be overly simplistic, especially for cars that were well maintained by the previous owner. Buyers may look to third party appraisals to price a second hand car, but often these appraisals are costly and time consuming. 

In the current used car market landscape there is a need by both buyers and sellers for a price prediciton method to better determine the fair market value of a car. Individual sellers can use this price prediciton model to better price their cars before putting them on the market. Buyers can use additional predictions to reference them against popular online valuators to get a better idea of the fair market value of a car. In the often times overwhelming used car market a price predicition model that accounts for the nuances of an automobiles many features will benefit both buyers and sellers to help determine the actual worth of a used car. 

A series of regression models will be utilized to predict the price of the cars in our dataset. These include; Linear Regression, Ridge, Lasso, Decision Trees, Random Forest, Extra Trees and Gradient Boost. The model will be evaluated using the metric Root Mean Squared Error (RMSE). This metric was chosen because it provides us with a number that is more easily interpreted for our parameter of interst, whic is price. In this case the metric will show the difference in monetary units (Euros) the predicted price was from the actual price. A benchmark RMSE score within 10% of the mean value of the cars in our dataset is how we will determine if we have a successful model. This would mean if the cars in the data set had a mean value of 5,000 a succesful RMSE score would be <= 500. A score like this would be helpful as a secondary appraisal to help consumers confirm they are paying a fair value for a used car. 

## Data Dictionary

|Column|Type|Description|
|:---|---|:---|
|Date Crawled|string|When this ad was first scraped from the website 
|Name|string|Name of the Car (Ex. VW Golf 1.87)
|Seller|string|Seller Type, Private or Dealer 
|Offer Type|string|The average sat Math score
|Price|int|Listed price of car
|AB Test|string|Offer is a test or control 
|Vehicle Type|string|Type of vehcile (SUV, Coupe, Van, etc.)
|Year of Registration|int|When the vehicle was first registered
|Gearbox|string|Transmission type (Manual or Automatic)
|Power Ps|int|Power of the car is PS
|Model|string|Model of the vehicle (VW Golf, Audi A4, BMW M3)
|Kilometer|int|Number of ilometers driven
|Month of Registraion|string|Which month the car was first registered
|Fuel Type|string|What type of fuel the car uses (Diesel, Gasoline, Electric)
|Brand|string|The Vehicle Manufactuer (Toyota, Volkwagen, Honda)
|Not Repaired Damage|string|If the car has damage that is unrepaired
|Date Created|string|The date for which the ad at ebay was created
|Postal Code|int|Postal Code of Seller/Cars location
|Last Seen|string|When the web scraper last saw the ad online


## Executive Summary
Predicting the price of used cars is an important problem that has great value in real world applications. As more consumers shift away from leasing or financing cars, more people are looking toward the used car market. Navigating the used car market can be challenging and it is unclear to many buyers and sellers as what the fair market value of a car is.  Intuition tells us that the older the car and the more miles it has on the odometer the cheaper it will be. However, in the data that was collected for this project we observed prices varying greatly in both the age and miles driven categories. This led us to believe that there are many additional features that are affecting the price of a used car. 

Given the extreme range in our target variable price we knew we would have to remove outliers on both ends of the price range. There were cars listed at over 150,000 euros and cars listed under 500 euros. For a used car prediction model we didn’t want to have cars priced extremely high as these vehicles are likely exotics or collectors items and did not represent what we believed to be the average used car. Addtionally we wanted to remove cars below 500 euros as these could be considered “junkers” and may be bought just for parts or scrap metal. During the modelling phase we kept scaling back on the max price as the scores of the model were very poor. The high price cars were making it very difficult for the model to learn. When going back to look at the distribution of prices the majority of the cars were in the 500 – 20,000 euro range. We ended up settling on this price range for our target variable. We believed this was a true representation on what a normal person would spend on a used car. Prices above this threshold were equivalent of the price of some new cars and we wanted to focus on a realistic price range for the average consumer. 

We wanted to use a number of different models in attempt to get the best score. We started with a simplified approach dropping the null values from our data set and running a linear regression model. We then went back and imputed the mode values for our categorical variables with missing values and re-ran the linear regression model where we observed an improvement in our score. We began to observe training scores that were much better than testing scores on many of the models. We removed the feature "car models" becuase we believed this was making it challenging for the models to train because of how many car model types were in the dataset. This was likely creating too much noise and was causing the models to overfit. When introducing tree based models we observed better scores and our Random Forest Model was our best performing model. 

Overall, the scores our models produced were poor. There were only a few features that had any impactful correlation on our models. The additional features created too much noise and it made it challenging for the models to learn.  When we scaled back to just a few features the noise was reduced and the models were less overfit but they still performed poorly. Due to the wide range in price amongst every feature, especially model and brand of car it made it extremely difficult for the models to make accurate price predictions. These results reinforce the idea that setting the actual price of a used automobile is extremely challenging and is most likely why straight line depreciation is used for this problem. 



Our approach was to create simple models and increase the complexity as we went while tuning the parameters. This resulted in us observing an inscrease in model performance. However, we also started to observe higher variance in our models which caused us to scale back on complexity to find an ideal bias variance tradeoff.

# Conclusion
Ones intuition regarding the sale price of a used car was reinforced through our predictions. We were able to identify age of a vehicle and the distance that it has been driven as being the most important factors related to the resale value of a car. Kilowatts the european equivalent of horsepower was also one of the most important features related to our target variable. We can infer from this that it is probably due to the size of the engine which is one of the most important components of an automobile. However, this may come as no surprise as the average person would probably assume engine size/power is an important factor in the price of a car. The reality of our predictive model demonstrates that cars have many nuanced features that affect the resale value of a car. The information that was provided in our dataset was not enough to make accurate predicitons even with what we would consider the most important features of a car. Also, a lot of noise was introduced with the model and brands of the cars for sale. A BMW 5 series had a mean price of 7,000 Euros but the prices ranged from just below 60,000 Euro down to 1,000 Euro. Based off of this information the model of the car introduces a lot of additional noise that may make it more challenging for the model to learn from. We observed this with the majority of makes and models with prices ranging from just below retail value to junk status. 

Based on our models performance it would not be effective in assisting buyers and sellers who are looking for additional appraisals on pre-owned vehicles. The predictions were too far off the acutal price for this to be an effective model. The best performing model was the random forest model (Training RMSE 1636.557, Testing RMSE 1697.326), which is approximately 20% of the mean value of the prices of cars in our dataset. If this model was put into use buyers and sellers would run the risk of overpaying or selling below the fair market value by a considerable amount. Straight line depreciation is most likely the industry standard becuase it provides a catch all solution to pricing pre-owned vehicles. No advanced analysis is required and prices can be set with consistency. The fact that a car is a depreciating asset makes it a challenging item to predict. Besides miles driven and age cars experience a lot of wear and tear and some owners maintain their cars well and others don't, but this is an extremely nuanced variable that is difficult to quantify. Used cars prices are also subject to market fluctuations and negotiations. If someone really needs cash they may be willing to part with their car for a thousand or more less. The combination of these variables show how difficult it is to predict the re-sale price of a car. 

The majority of features in the dataset did not have a strong linear relationship with our target variable of sales price. This most likey introduced a considerable amount of noise into our model and is a key contributing factor into our models poor performance. Additional outside research shows that many used car buyers want to know "how the car runs". How the car runs is a variable that is made up with a number of factors and is extremely difficult to quantify and introduce as a feature into our model. Cars are complex pieces of machinary that have so many components, it is very difficult to take a handful of features and make an accurate prediction of that cars value. 

# Recommendations 
The car model feature should have been divided up in to subgroups. BMW could have had three different tiers of cars based off of mean price. One hot encoding the feature "car model" created a considerable amount of noise in the model, so much that it was removed completely to avoid overfitting. When analyzing the feature importance of the model many of scores were 0.0, which means it had no importance relative to our target variable. Intuitively we think certain car models are associated with certain prices so initially it made sense to include this in our features. 

We believe if we had focused on a specific type of vehicle brand our predictions could have been more accurate. The most popular make in our dataset was Volkswagen. If we only tried to predict Volkswagen prices there would have been less noise from other makes and models of cars. This then could have been used on other brands and could be used by buyers and sellers of those specific types of vehicles. This could then be more focused on specific vehicle types to get more accurate predictions. We would only take Volkswagen sedans into our model and exclude the other vehicle types like SUVs or vans. This would take a more targeted approach for the buyer or the seller, narrowing down the data to their specifications of used car they are looking to buy or sell.  

The minimum price of vehicles introduced in our dataset could be increased. The floor was set too low which allowed for the inclusion of many cars that could be considered "junk status" and are purchased for parts or scrap. These cars did not represent vehicles someone would be looking to purchase as their primary use of transportation. These low prices represent cars at the end of their lifecycle or could have been in a major accident, requiring a lot of repairs. These types of vehicles should be excluded and more additional research should be completed to set the minimum sale price for cars that should be included in our data. 

Industry standards for appraising the value of vehicles rely on comparable sales prices of similar makes and models. If we could introduce comprable sale prices in some way this could improve the accuracy of our predictions. This would be challenging to do but this is an important variable in used car prices. Date ranges would have to be included to assess the current market demand for certain makes and models 


# References 
Consumer Reports, May, 2014, https://www.consumerreports.org/cro/2012/12/how-much-is-the-used-car-really-worth/

Nerd Wallet, Jeanne Lee Oct, 2015, https://www.nerdwallet.com/blog/loans/dealers-set-car-prices/

InCharge Debt Solutions, Sept, 2017, https://www.incharge.org/understanding-debt/auto/the-truth-about-used-car-prices/


..