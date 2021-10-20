# group_project_A15
# Executive Summary 

> Simply put, what we have done here is taken a rough data set, cleaned it, and run some analysis to communicate some interesting observations and predictions regarding AirBnB's presence in Brussels. We started by converting variables to formats that would be of use to us. Then, we selected certain variables from the raw data set on the basis of their usefulness in conducting regressions, data visualisations, correlation tests, etc. Using these variables, we plotted bar charts, distribution charts, and more. Lastly, we ran regressions and made some predictions. 

## Data Visualisation 

> We approached the data visualisation with the objective of challenging pre-concieved notions we had regarding relationships between a cusomter and seller in the AirBnB context. Through some qualitative analysis, we answered questions such as "What is the relationship between the quality of a host (seller) and the price they charge" and compared results to our hypotheses. 

## Regression Analysis

### Creating the explained variable

> For the regression part, we started by creating a new variable called **Price_4_nights** to calculate the cost of staying 4 nights at an Airbnb. Given we were looking specifically at the cost for 2 people, we filtered the data to calculate the cost for only Airbnb’s which could accommodate at least 2 people. However, for the regression model, we have instead decided to create and use **log_Price_4_nights** as the explained variable since its distribution is close to a normal distribution. Before, starting with the different regression models, we split total dataset into trained and tested the data set.

#### Models Results

> **Model 1**     
For Model 1, we have tested the significance of **property type**, the **number of reviews** and **review score rating** on the price of an airBnB. At first glance, there is a negative relationship between review score rating and the price for 4 nights at an Airbnb, which seems strange given that normally we would expect properties having higher ratings will have higher prices. However, the negative relationship is very small and is nearly zero and it is not statistically significant. Other variables are significant.`Prop_type_simplified` is a categorical variable, so the first thing we should understand is this regression is choosing `entire condo` as a base line. The intercept can be interpreted as an entire condominium (condo) will command a log price_4_nights of 5.883. If another property type is chosen such as a private room in rental unit or a private room in residential home, then the log price will be decreased by 0.563 and 0.430 respectively. This make sense as the price of renting a room will be lower than that of an entire condo. In general, property type is a significant predictor of price of an AirBnb. Checking for collinearity, we can see that this is not an issue here in this model due to VIF being lower than 5.  Then we run model 1 on our tested dataset, and RMSE = 0.518    
**Model 2**      
In model 2, we find `review_score_rating` is insignificant, so we drop it in our following regression. For model 2, we want to determine if room type is a significant predictor of the cost for 4 nights and we find out that every room type, except for a hotel room, is a significant predictor of price. Again, checking for collinearity, we can see that this is not an issue here in this model due to VIF being lower than 5. Checking for overfitting, we find the RMSE = 0.504 on tested data set.       
**Model 3**          
For model 3, we want to determine if number of *bathrooms*, *bedrooms*, *bed* and *size of the house* are significant predictors of the cost for 4 nights. The number of beds is not significant predictors of `log_price_4_nights`. However, the number of bedrooms, bathrooms and size of the house are significant predictors. Given VIF is less than 5, it doesn't seem that there is any issue of multi-collinearity. Checking for overfitting, we find the RMSE = 0.441 on tested data set.      
**Model 4**   
For model 4, we want to understand if superhosts (`host_is_superhost`) command a pricing premium, after controlling for other variables.  At first glance, being a superhost seems command a pricing premium compared to being not. However, it is not statistically significant. So we have 95% confidence to say being a superhost doesn't command a pricing premium. Given VIF is less than 5, it doesn't seem that there is any issue of multi-collinearity. We find the RMSE = 0.418 on tested data set.   
**Model 5**  
`host_is_superhost` is not significant, so we don’t include it in our regression. For model 5, we want to see if the fact that some hosts allows you to immediately book their listing may command a price premium compared to those who don’t. We find out that being able to instantly book an Airbnb is a significant predictor of price. Given VIF is less than 5, it doesn't seem that there is any issue of multi-collinearity. Checking RMSE on tested data set, we find RMSE = 0.441.  
**Model 6**    
For model 6, we have created a new variable called `neightbourhood_simplified`, where we broke down the 19 neighbourhoods in Brussels into 5 neighbourhood based on where they are located in the city of Brussels. We separed the different neighbourhoods into neighbourhoods located in the North West, North East, East/Centre, West/Centre and South/Centre.  Location is a good significant predictor of `log_price_4_nights` as seen by t-statistics. Rooms located in the East won't have a significant effect on price, however, rooms located in North East, North West, South have significant postive effect on `price_4_night`. Again, given VIF is less than 5, it doesn't seem that there is any issue of multi-collinearity. Checking RMSE on tested data set, we find RMSE = 0.441.       
**Model 7**       
For model 7, we try to find the effect of the variable `avalability_30` or `reviews_per_month` on `log_price_4_nights`, after we control for other variables. For this model, we find `number_of_reviews` is not significant, then we try to replace it with `review_scores_rating`, then this is significant. This might because `reviews_per_month` could represent much information of `number_of_review`, so this variable become insignificant. We also find that `availability_30` and `reviews_per_month` have significant positive effect on `price_4_nights`. Again, given VIF is less than 5, it doesn't seem that there is any issue of multi-collinearity. Checking RMSE on tested data set, we find RMSE = 0.3703.

##### Prediction

>**Choosing a model**   
Model 7 has the highest adjusted R^2, and also the lowest RMSE in testing set, which means model7 has the best explaining ability with no overfitting. So we use model7 for prediction.\
**Prediction**  
Suppose I want to order a private room in rental unit, located in North West. We want this room to have more than 10 reviews with an average score rating higher than 4.5. Based on the existing dataset, our point estimation for the price I should pay for 4 nights is 123.4 Euros, and 95% upper price is 131.6 Euros, 95% lower price is 115.7 Euros.
