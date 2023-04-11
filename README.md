## Will the Customer Accept the Coupon

Suppose a coupon is delivered to a person's cell phone for a restaraunt near where he or she is driving. How likely is the driver to accept the coupon and drive to the restaurant? What are the factors that would most influence whether this individual accepts the coupon? I analyzed these questions in the associated Notebook [Coupon_Application.ipynb](https://github.com/chellykearney/BerkeleyAI_ML_Practical_Application_1/blob/main/Coupon_Application.ipynb). This is a summary of my findings.

### Data Description

The dataset for this study comes from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios and then asks the person whether he or she will accept the coupon if he or she is the driver. There are five different types of coupons -- inexpensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and expensive restaurants (\\$20 - \\$50), with two different expiration times for the coupons - 2 hours and 1 day.

The survey collected demographic information for the driver - gender, age, marital status, children/no children, education, occupation, and annual income. It also included the number of times a driver goes to a bar, carry out venue, coffee house, inexpensive restaurant and expensive restaurant. The survey collected variables describing the driving context such as type of car, driving destination (home, work or no urgent destination), weather, temperature, time of day, whether the driver is driving in the same or opposite direction of the coupon venue, if there is a passenger in the vehicle and the driving distance to the coupon venue (5 min, 15 min or 25 min).

All variables from the survey are categorical. Temperature was classified as one of three separate temperatures - 30, 55 or 80 degrees Fahrenheit. Income and age are classified into different range categories. The direction of the driver with respect to the coupon venue, in the same direction or in the opposite direction, was recorded in two columns. These were combined to make one variable called 'direction.' The distance to the coupon venue was recorded in three columns (toCoupon_GEQ5min, toCoupon_GEQ15min, toCoupon_GEQ25min). These were combined to create one variable called 'distance.'

Less than 10\% of observations for car type were recorded, so this variable was not included in this analysis. After removing any null values in the data, there were 22 columns and 12,079 rows. The variable of interest is the Accept Rate. Figure 1 shows the distribution of drivers who accepted the coupon and those who did not. The relationship of the acceptance rate was analyzed with respect to the other 21 variables to identify the features that most influence this rate.

![coup_accept.png](attachment:coup_accept.png)

**Figure 1.** Distribution of coupon acceptance. In 57% of the driving scenarios, the driver accepted the coupon.


### Chi-Square Test of Association

All variables were categorical so I used the Chi-Square Test Statistic to determine if there was an association between each variable with the acceptance rate. This test utilizes a contingency table to analyze the data. Table 1 is a contingency table between the types of coupons and the acceptance rate. The categories for the type of coupon appear in columns, the categories for coupon acceptance appear in rows. Each cell reflects the total count for a specific pair of categories.

![cont_table.PNG](attachment:cont_table.PNG)

**Table 1.** Contingency table for type of coupon and acceptance.

If there is an association between the two variables, we would expect to see pairs of categories show different results. Figure 2 is a clustered bar chart of these two variables. The acceptance rate is 71% for inexpensive restaurants. The acceptance rate is 41% for bars. The variation in these results indicates an association between these variables.

![coupon-2.png](attachment:coupon-2.png)

**Figure 2.** Clustered bar chart showing acceptance rate among various types of coupons.

In contrast, figure 3 shows coupon acceptance by gender. The acceptance rate among male drivers is 59% and among female drivers is 55%. There is less variability among category pairs and thus a weaker association between these two variables. If gender played no role in whether a driver accepts a coupon, we would expect the proportions to be equal.

![gender.png](attachment:gender.png)

**Figure 3.** Clustered bar chart showing acceptance rate by gender.

The Chi-Square Statistic is a measure of the variability among categories. The larger the Chi-Square Statistic, the greater the probability that there is an effect between the two variables, i.e. there is an association. A contingency table was created for every variable with coupon acceptance. A Chi-Square Statistic was calculated on each contingency table. Table 2 summarizes these results and ranks each variable from highest Chi-Square Statistic to lowest.

![ChiSquare.PNG](attachment:ChiSquare.PNG)

**Table 2.** Summary of Chi-Square Statistics for each variable versus coupon acceptance.

These statistics were used to identify and rank the most significant factors on whether a driver would accept a coupon. The type of coupon ('coupon') was by far the most significant factor. The variables labelled CoffeeHouse, passenger, expiration and destination also had strong effects. The education level of the driver, whether the driver has children, the driver's gender, how many time as driver visits an inexpensive restaurant (< \$20), and which direction the driver is travelling have the least impact  on acceptance rate.

### Key Factors in Coupon Acceptance

In this section, I will discuss the top nine variables that influence whether a driver will accept the coupon. These are based on rankings in Table 2.

#### 1. Type of Coupon ('coupon')

They type of coupon had the strongest effect of all the variables on whether a driver accepted the coupon. Figure 2 above is a clustered bar graph showing coupon acceptance per the type of coupon. 

* Coupons issued for a bar were accepted 41% of the time.
* Coupons issued for Carry Away were accepted 74% of the time.
* Coupons issued for a Coffee House were accepted 49.6% of the time.
* Coupons issued for an expensive restaurant (\\$20 - \\$50) were accepted 45% of the time.
* Coupons issued for an inexpensive restaurant (<\$20) were accepted 71% of the time.

Coupons are more likely to be accepted if they are issued for Carry Away venues or inexpensive restaurants. Coupons are less likely to be accepted if they are issued for bars or expensive restaurants. Coupons are equally likely to be accepted or declined if the coupon is issued for a coffee house.

#### 2. How many times a driver visits a coffee house ('CoffeeHouse')

Figure 4 shows coupon acceptance versus how often a driver visits a coffee house. 

* Drivers who never visit a coffee house accepted the coupon 46% of the time.
* Drivers who visit a coffee house < 1 time accepted the coupon 55% of the time.
* Drivers who visit a coffee house 1-3 times accepted the coupon 65% of the time.
* Drivers who visit a coffee house 4-8 times accepted the coupon 63% of the time.
* Drivers who visit a coffee house > 8 times accepted the coupon 58% of the time.

Drivers who visit coffee houses, even if it is < 1 time, are more likely to accept the coupon. In particular, drivers who visit coffee houses 1-8 times are most likely to accept the coupon.

![coffehouse-2.png](attachment:coffehouse-2.png)

**Figure 4.** Clustered bar chart showing coupon acceptance versus how often a driver visits a coffee house.

#### 3. Passenger in the car ('passenger')

Figure 5 shows coupon acceptance when the driver is alone or has a passenger and what the relationship of the passenger is to the driver. 

* A driver who is alone accepted the coupon 53% of the time.
* A driver who has a friend in the car accepted the coupon 68% of the time.
* A driver with a kid in the car accepted the coupon 50% of the time.
* A driver with his or her partner in the car accepted the coupon 59% of the time.

Drivers with a friend or partner in the car are more likely to accept the coupon. In particular, drivers with a friend are most likely to accept the coupon.

![passenger.png](attachment:passenger.png)

**Figure 5.** Clustered bar chart showing coupon acceptance when a passenger is in the vehicle.

#### 4. Expiration Time for the Coupon ('expiration')

Figure 6 shows the coupon acceptance rate for coupons that expired after 1 day and those that expired after 2 hours.
* Coupons that expired in 1 day were accepted 63% of the time.
* Coupons that expired in 2 hours were accepted 50% of the time.

Coupons with expiration times of 1 day are more likely to be accepted.

![expiration.png](attachment:expiration.png)

**Figure 6.** Clustered bar chart showing coupon acceptance for each expiration time - 1 day and 2 hours.

#### 5. Destination ('destination')

Figure 7 shows coupon acceptance for each category of driver destination.
* Drivers with no urgent destination accepted the coupon 63% of the time.
* Drivers going home accepted the coupon 51% of the time.
* Drivers going to work accepted the coupon 50% of the time.

Drivers with no urgent destination are more likely to accept the coupon. Drivers headed home or to work are equally likely to accept or decline the coupon.

![destination.png](attachment:destination.png)

**Figure 7.** Clustered bar chart showing coupon acceptance for each driver destination category.

#### 6. Time of Day ('time')

Figure 8 shows the coupon acceptance rate at various times during the day.

* Coupons issued at 7AM are accepted 50% of the time.
* Coupons issued at 10AM are accepted 61% of the time.
* Coupons issued at 2PM are accepted 66% of the time.
* Coupons issued at 6PM are accepted 58% of the time.
* Coupons issued at 10PM are accepted 52% of the time.

Coupons issued between 10AM to 6PM are more likely to be accepted. Coupons issued at 7AM and 10PM are equally likely to be accepted or declined.

![time.png](attachment:time.png)

**Figure 8.** Clustered bar chart showing coupon acceptance by time of day.

#### 7. Distance of the Driver from the Coupon Venue ('distance')

Figure 9 shows coupon acceptance for categories of driver distance from the coupon venue - 5 minutes, 15 minutes or 25 minutes.

* A driver who is 5 minutes from the venue accepts the coupon 62% of the time.
* A driver who is 15 minutes from the venue accepts the coupon 56% of the time.
* A driver who is 25 minutes from the venue accepts the coupon 43% of the time.

A driver who is 15 minutes or less from the venue is more likely to accept the coupon. In particular, drivers who are 5 minutes from the venue accept are most likely to accept the coupon. Drivers who are 25 minutes from the venue are less likely to accept the coupon.

![distance.png](attachment:distance.png)

**Figure 9.** Clustered bar chart showing coupon acceptance for categories of driver distance from the coupon venue.

#### 8. Occupation of the Driver ('occupation')

Figure 10 shows the coupon acceptance rate for various professions. Percentages were not calculated for each category, but visually from the graph, we can make the following assessments.
* Drivers whose occupations are Students, Unemployed, Healthcare Support, Healthcare Practitioners, Sales, Management, Computer and Math, Office & Administration, Construction, Transportation or Business are more likely to accept the coupon.
* Drivers whose occupations are legal or retired are less likely to accept the coupon.

![occupation-2.png](attachment:occupation-2.png)

**Figure 10.** Clustered bar chart showing coupon acceptance by various occupations.

#### 9. Weather ('weather')

Figure 11 shows coupon acceptance rate during different types of weather.

* On sunny days, drivers accepted the coupon 60% of the time.
* On rainy days, drivers accepted the coupon 46% of the time.
* On snowy days, drivers accepted the coupon 48% of the time.

Drivers are more likely to accept the coupon on sunny days. Drivers are less likely to accept the coupon on rainy or snowy days.

![weather.png](attachment:weather.png)

**Figure 11.** Clustered bar chart showing coupon acceptance by different types of weather.

### Recommendations

Based on the findings from this analysis, the following are recommendations to increase the proportion of coupons accepted by drivers.

1. Coupons should be for inexpensive restaurants (<\$20) or carry away/takeout venues. **Avoid** issuing coupons for bars or expensive restaurants (\\$20-\\$50).

2. Coupons should target drivers who visit coffee houses.

3. Coupons should target drivers who have a friend or their partner in the vehicle.

4. Coupons should have an expiration time of 1 day.

5. Coupons should target drivers with no urgent destination.

6. Coupons should be issued between 10AM and 6PM.

7. Coupons should be issued when drivers are 15 minutes or less from the venue. 

8. Coupons should be targeted to drivers whose occupations are Student, Unemployed, Healthcare Support, Healthcare Practitioners, Sales, Management, Computer and Math, Office & Administration, Construction, Transportation or Business are more likely to accept the coupon. **Avoid** drivers whose occupations are legal or retired.

9. Coupons should be issued on sunny days. **Avoid** rainy or snowy days.
