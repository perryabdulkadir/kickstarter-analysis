# Kickstarting with Excel

## Overview of Project
This is an analysis and visualization of Kickstarter campaigns for plays.

### Purpose
Louise has started a Kickstarter campaign to raise funds to produce a play entitled, “Fever.” The play’s Kickstarter campaign has come close to its goal just a short time after going live. Louise has tasked me with analyzing Kickstarter campaigns for plays based on their launch dates and funding goals and produce visualizations.

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date

#### Preparing the data

The first part of the analysis was to visualize campaign outcomes based on launch date. Using the data in Kickstarter_Challenge.xlsx, I added a column entitled “Years” in column U. Using the “Years” function, I populated the column with the year of the campaign’s creation. So, for example, cell U2 contained the code “=YEAR(S2)”, which turned the campaign creation date of 2/12/2014 into the year of 2014. 

#### Creating the pivot table
After this, I created a new pivot table in a new sheet, titled “Theater Outcomes by Launch Date.” I placed “Parent Category” and “Years” in the filter category. In the columns category I placed “Outcomes,” in the rows category I placed “Date Created Conversion,” and in the values category I placed “Count of Outcomes.”

After this, I filtered “Parent Category” so only theater campaigns were included in the pivot table below. Because I was not interested in campaigns where the “Outcome” column listed “live” or null, I filtered the outcomes in the pivot table to only display successful, failed, or canceled campaigns. From there, I sorted column labels Z->A so “successful”, “failed,” and “canceled” displayed in the proper order in the pivot table. This left me with a pivot table that looked like this: 


#### Creating the visualization

From there, I clicked the pivot table and added a pivot chart from underneath the Analyze ribbon in Excel. I selected the option for a line with markers. This resulted in the following graph: 


The chart correctly portrayed the data in the pivot table. From there, I simply added a title to the pivot chart to conclude my analysis of outcomes based on launch date. 

### Analysis of Outcomes Based on Goals

#### Preparing the data
To begin, I created a new sheet and labeled it “Outcome Based on Goals.” I created columns titled, “Goal,” “Number Successful,” “Number Failed,” “Number Canceled,” “Total Projects,” “Percentage Successful,” “Percentage Failed,” and “Percentage Canceled.” I created rows for “Less than 1000,” “1000-4999,” “5000-9999,” “10000-14999,” “15000 to 19999,” “20000-24999,” “25000-29999,” “30000-34999,” “35000-39999,”40000-44999,” “45000-49999,” and “Greater than 50000.”

#### Using the COUNTIFS function to populate the table

For this step, I started by writing the function for cell B2. This functions is:

```
 =COUNTIFS(Kickstarter!$D:$D, "<1000", Kickstarter!$R:$R, "plays", Kickstarter!$F:$F, "successful")
```

The COUNTIFS function counts data in a given range if it meets specified criteria. This row is for campaigns with goals less than $1000, so I specified 

```
Kickstarter!$D:$D, “<1000”
```

The “Kickstarter!$D:$D” code tells Excel to go into the “Kickstarter” sheet and analyze all cells in column D, Goal, to see if they meet my specified criterion. In this case, the criterion is “<1000” because I only want to include campaigns with goals under $1000 for this row. 

The next section of the code is:

```
Kickstarter!$R:$R, "plays"
```

This tells Excel to further restrict the criteria of its count to only include those campaigns where the Subcategory, column R, is “plays.” This is because I want to compare Louise’s campaign to similar campaigns for plays rather than other irrelevant subcategories, such as animation and children’s books. 

The final section of this code is: 

```
Kickstarter!$F:$F, "successful"
```
This tells Excel to look into the F column of the Kickstarter sheet, outcomes, and only include campaigns in its count if they were successful. We want this because column B in the Outcomes Based on Goals sheet is for successful campaigns.

Taken together, this entire piece of code is telling Excel to count the number of campaigns for plays that had goals of less than $1000 and were successful in reaching their fundraising goals. 

I based the formulas for all of the remaining cells on this first function. For example, in cell B3, I used the function

```
=COUNTIFS(Kickstarter!$D:$D, ">=1000", Kickstarter!$R:$R, "plays", Kickstarter!$F:$F, "successful", Kickstarter!$D:$D, "<=4999")
```

In this function, I only had to make a few tweaks from the previous function. I was still looking for “plays” as the subcategory and “successful” as the outcome, so those parts of the function remained unchanged. The only elements that changed relate to the goal amount: in row 3, I am only including campaigns with goals between $1000 and $4999. This bit of code tells Excel to only include campaigns with goals greater than or equal to $1000: 

```
Kickstarter!$D:$D, ">=1000"
```

And this bit of code tells Excel to only include campaigns with goals less than or equal to $4999. 

```
Kickstarter!$D:$D, "<=4999"
```

I repeated this process for all of column B, copying and pasting the function from the cell above and only changing the range of values to count from Column D of the Kickstarter sheet. 

Next, I used the COUNTIFS function to count the number of play Kickstarter campaigns that failed in a given goal range. For cell C2, I used this function:

```
=COUNTIFS(Kickstarter!$D:$D, "<1000", Kickstarter!$R:$R, "plays", Kickstarter!$F:$F, "failed")
```

I copied and pasted the function from B2 and changed only one element. 

```
Kickstarter!$F:$F, "failed"
```

Because column C is also counting only those campaigns in the play subcategory and also shares the same goal bins as column B, the only element that needed to be changed was that I was no longer looking for successes, but failures. I repeated the came process for all of column C, copying and pasting the code from the cell to its left and changing “success” to “failed.”

Finally, I repeated the same process for column D, copying and pasting the function from the cell to its left and changing “failed” to “canceled.” This left me with a table that looked like this: 

#### Additional calculations
In the next column, “Total Projects,” I simply used the SUM function to add the successful, failed, and canceled campaigns for each goal range. This left me with all play campaigns (excluding those with the category “Live” or null) for each range of goal amount. 

Next, I used simple formulas to calculate the percentage successful, percentage of failed, and percentage canceled for each goal range. For column F, percentage successful, I used the function

```
=B2/E2
```

I applied this to the rest of the column. For Percentage Failed, I used the function C2/E2 and applied it to the whole column. For the Percentage Canceled column, I used the function D2/E2. At this point, my table looked like this: 



#### Creating the visualization

From here, I simply selected columns F, G, and H in the Outcomes Based on Goals sheet and inserted a line chart and gave it a title.



### Challenges and Difficulties Encountered

#### Writing functions

Although I have used Excel functions before, this analysis included some of the longest functions I have used. In the Outcomes Based on Goals sheet, I ran into some issues with syntax at the beginning. My first COUNTIFS function kept returning errors – when I watched the video under “hint” in the module, I realized I had forgotten to include $ in the range. For example, I changed Kickstarter!D:D to Kickstarter!$D:$D. As I built my functions and occasionally got confused where things were, I learned that I could hover over sections of the function and Excel would tell me that section’s role in the function – for example, criteria_range1.

#### Checking results that seemed incorrect

The other concern I had was the fact that there were 0 campaigns in the Number Canceled column for every row. This seemed suspicious at first glance, so I investigated. First, I turned to the analysis I had already done in Theater Outcomes by Launch Date. This analysis showed that the theater parent category data set contained 839 successful campaigns, 493 failed campaigns, and 37 canceled campaigns. Immediately, this information showed that it was plausible for canceled campaigns to be much, much less common than successful or failed ones. Intuitively, it also makes sense that few campaigns would be canceled – even if a campaign is not performing well, from the perspective of the organizer, there is no harm in letting the campaign continue to run in the off chance that it succeeds. 

However, I wanted to do further analysis to ensure there were not any errors in my code. In the Kickstarter sheet, I filtered the subcategory column to show only the 1066 campaigns for plays. I then filtered by outcome: this showed 694 successful play campaigns, identical to the sum of the Number Successful column in the Outcomes Based on Goals sheet. The filter showed 353 failed play campaigns, which matched the sum of the Number Failed column. Finally, the filter showed no canceled play campaigns. This satisfied me that my conclusion 0 canceled play campaigns for every goal amount was correct. 




## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

One can look at the chart and conclude that there does seem to be a trend in terms of successful campaigns. While the number of failed and canceled campaigns remains relatively flat throughout the year, the number of successful theater campaigns tends to peak in May and decline steadily until September. Campaigns launched in December have fewer successes than those launched in any other month. 

The relative flatness of failed/canceled campaigns and the strong trend in successful campaign allows for a second conclusion: the percentage of successful theater campaigns, as a part of total theater campaigns, is highest in May, decreases steadily through the summer until September, and reaches a nadir in December. Based on this, someone considering launching a theater campaign might reconsider their plans to launch in December or might especially consider launching a campaign in May.  


- What can you conclude about the Outcomes based on Goals?

Play campaigns that have smaller goals (>$1000 or $1000-$4999) tend to be successful (75.8% and 72.7% successful, respectively. The success rate declines to around 50% for campaigns with goals in the range of $5000-$9999, $10000-$14999, $15000-$19999, and $20000-$24999. The success rate declines markedly for the next few ranges: $25000-$29999 has a success rate of 20.0% and $30000-$34999 has a success rate of 27.3%. The success rate climbs for the next two brackets – 66.7% of campaigns with goals in the range of $35000-$39999 and $40000-$44999. The success rate craters to 0% for the range of $45000-$49999 and 12.5% for $50000+. I will discuss the limitations of the data more in depth below: for now, however, it suffices to say that the number of observations is high for the lower goal ranges and very small for the highest goal ranges. Because of this scarcity of data, I am only comfortable drawing conclusions about the lower ranges of goals – generally speaking, chance of success is inversely proportional to goal amount. That is, those with more realistic goals are more likely to achieve them. This makes intuitive sense – it is easier to raise smaller amounts of money than larger amounts.  


- What are some limitations of this dataset?
There are some limitations to this dataset. As mentioned above, the number of observations is limited for campaigns with larger goals. Out of 1047 total play campaigns that succeeded, failed, or were canceled, there are only 42 that had goals of $25000 or larger. This means that 95.9% of all campaigns had goals lower than $25000. The number of campaigns is even more concentrated at the bottom of the goal ranges – 84.9% of campaigns had goals below $10000. This means that we can draw fewer inferences about higher campaign levels because there is a lack of data. For example, the goal range $45000-49999 has just 1 campaign – we cannot possibly draw strong conclusions with an n of 1. Looking at the percentage successful without the context of the sample size could lead to incorrect conclusions. Looking at just the percentage of successful campaigns, it would be foolish not to start a campaign with a goal of $45000-$49999 - after all, the success rate is 100%! Of course, when you learn that this 100% success rate is based on 1 out 1 campaign succeeding, it should temper your reliance on that data. 

Another limiting factor, this time for predicting theater outcomes by launch date, is that past performance is not necessarily indicative of future performance. It may be true that historically, May tends to be a good month for theater campaigns. However, the world is unpredictable – theater Kickstarter campaigns launched in May 2020 were almost certainly less successful than historical averages because the novel Coronavirus has shut down all large public gatherings in many parts of the world. Someone blindly relying on historical data without considering context might have been sorely disappointed if they tried to launch a theater campaign in May of this year.  


- What are some other possible tables and/or graphs that we could create?
It could be illuminating to explore success rate of play Kickstarter campaigns broken down by size of average donation. There would be columns for “Number Successful,” “Number Failed,” and “Number Canceled.” The rows would be bins of average donation size: for example, less than $5, $5-$20, $21-$50 … more than $1,000. This could provide Louise insight into how to market her campaign. For example, it might show that campaigns succeed more often when the average donations are very large. If that is the case, Louise would be better served spending her time courting wealthy philanthropists and patrons of the arts. On the other hand, if the data reveal that campaigns with small average donations succeed more frequently, she might consider a grass roots fundraising campaign. 

