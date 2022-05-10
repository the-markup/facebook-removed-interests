# Citizen Browser: Facebook Promised to Remove “Sensitive” Ads. Here’s What It Left Behind

This repository contains data from the story "[Facebook Promised to Remove “Sensitive” Ads. Here’s What It Left Behind](https://themarkup.org/)" from The Markup's [Citizen Browser](https://themarkup.org/citizen-browser/) series. For more information about how the Citizen Browser application was built and the Facebook data it collects, see "[How We Built a Facebook Inspector](https://themarkup.org/citizen-browser/2021/01/05/how-we-built-a-facebook-inspector)."

## Context
Facebook provides advertisers an ad-targeting option called "detailed targeting" to refine groups of people by demographics, interests, and behaviors based on their activities through the platform. **In a 2021 statement, Meta said that it would cut back on this detailed targeting and remove the ability for advertisers to target users based on certain interests that describe health, race or ethnicity, political affiliation, religion, or sexual orientation.** These changes took effect from mid-January 2022 to March 17, 2022.


## Data

In March 2021 we began collecting detailed targeting information from ads shown to our Citizen Browser panel. From March 16, 2021, through April 30, 2022, we collected more than 21 thousand interests from more than 270 thousand ads shown to more than 2,000 participants.

In late October 2021, before Facebook removed any interest-targeting options, we started compiling a list of potentially sensitive terms in our dataset, such as “Diabetes mellitus awareness” and “Adult Children of Alcoholics.” We also collected a list of terms that Facebook’s tools recommended to advertisers when they entered one of these potentially sensitive terms—for example, the company suggested “BET” and “Essence (magazine)” when advertisers searched for “African-American culture” (screen capture below).

![AfricanAmericanCulture-suggestions2x](https://user-images.githubusercontent.com/821717/167681695-76554405-2fc4-48ac-a9d9-7677cfd472dc.png)


### Collecting Audience Size:

Between late October 2021 and early January 2022, we found the audience size of each interest identified through the methods above using Facebook’s Ad Manager tool. 
* We collected Facebook’s low-end and high-end estimate for the number of users with interest #1, using the company’s ad tool.
* We repeated that process for interest #2. 
* We queried the combination of interest #1 and interest #2 in Facebook's ad tool, which produces a high and low estimate of the number of users at the union of the two interests.


<table>
  <tr>
    <td width="50%"><img src="https://user-images.githubusercontent.com/821717/167702953-5918fc29-7b7b-4eb1-8515-6e63872d8ab4.png" height="500"><br/>
    <small>Audience size range for “Diabetes melitus awareness” is 19,400,000 to 22,800,000. The midpoint of this range is 21,100,000.</small></td>
    <td width="50%"><img src="https://user-images.githubusercontent.com/821717/167702972-b7657f44-382c-4180-895c-9e7bda18bdf2.png" height="500"><br/>
    <small>Audience size range for “Diabetes melitus type 2 awareness” is 12,500,000 to 14,700,000. The midpoint of this range is 13,600,000.</small></td>
  </tr>
  <tr>
    <td width="50%"><img src="https://user-images.githubusercontent.com/821717/167702985-6b70737b-826a-4fd0-9a75-e26298ae3726.png" height="500"><br/>
    <figure>Audience size range for union of “Diabetes melitus awareness” and “Diabetes melitus type 2 awareness” is 23,300,000 to 27,100,000. The midpoint of this range is 25,200,000.</figure></td>
    
  </tr>
  </table>



<p>&nbsp;</p>


### Calculating Overlaps:

To measure the similarity between an interest and its suggested interest, we calculated the overlaps as follows:
* We calculated the midpoint between the high and low audience estimate of each of these audience estimates. 
* We estimated the intersection by subtracting audiences for the union of the two interests from the sum of the two interests when queried separately.
  - **Sum** of interest #1 + interest #2 = 34,700,000
  - **Union** of interest #1 and interest #2 = 25,200,000
  - **Intersection** = Sum - Union = 9,500,000
  - **Overlap with interest #1** = intersection/interest #1. The audience for interest 1 overlaps 45% with interest 2
  - **Overlap with interest #2** = intersection/interest #2. The audience for interest 2 overlaps 70% with interest 1

<p>&nbsp;</p>

### Identifying Removed Interests

We queried the Facebook ad tool in April 2022, after Facebook’s changes took effect, to determine which of the interests we collected are no longer available.

The data/ directory contains two CSV files with data from the story.

1. `fb_removed_interests.csv` contains all the Facebook ad interests we were able to identify as no longer available for targeting as of April 2022.
2. `fb_audience_overlaps.csv` contains Facebook's audience size estimates for selected pairs of interests with strong overlaps in users. 


<p>&nbsp;</p>
    

**Data in 'fb_removed_interests.csv' is arranged as follows:**
| column           | description                                                                                |
|:-----------------|:------------------------------------------------------------------------------------------|
| removed_interest   | A Facebook ad interest that was available for targeting at some point between March 2021 and March 2022, but not afterward.|
| aud_low_est      | Low range of Facebook's estimated audience size. Missing values reflect interests that were not queried in Facebook’s Ad Manager.  |
| aud_high_est      | High range of Facebook's estimated audience size. Missing values reflect interests that were not queried in Facebook’s Ad Manager. |
| date_aud_test      | Date the audience size estimate was collected for interests that were queried in the Facebook Ad Manager.|
| seen_in_CB      | A yes/no flag indicating whether advertisers used the interest to target  ads shown to users in The Markup's Citizen Browser panel between March 16, 2021, and April 30, 2022.  |
| unique_advertiser      | Number of unique advertisers in the Citizen Browser dataset who used this interest to target Facebook ads between March 16, 2021, and April 30, 2022. |
| unique_user      | Number of unique Citizen Browser panelists who were shown ads with this targeted interest between March 16, 2021, and April 30, 2022. |


    
<p>&nbsp;</p>  


**Data in 'fb_audience_overlaps.csv' is arranged as follows:**
| column           | description                                                                                  |
|:-----------------|:------------------------------------------------------------------------------------------|
| interest_1 | Interest removed from Facebook's detailed targeting options between January and April 2022 |                      
| interest_2 | Interest suggested by Facebook's ad tool in conjunction with interest_1 before it was removed  |
| int1_aud_low | Facebook's low audience estimate for interest_1 |
| int1_aud_mid | Calculated midpoint of the low and high audience counts of interest 1 |
| int1_aud_high | Facebook's high audience estimate for interest_1 |
| int2_aud_low | Facebook's low audience estimate for interest_2 |
| int2_aud_mid | Calculated midpoint of the low and high audience counts of interest 2 |
| int2_aud_high | Facebook's high audience estimate for interest_2 |
| union_aud_low | Facebook's low audience estimate for the union of interest_1 and interest_2|
| union_aud_high | Facebook's high audience estimate for the union of interest_1 and interest_2 |
| aud_intersect | Result of subtracting the midpoint of audience estimates for the union of interest 1 and interest 2 from the independent sums of the midpoint for the audience estimates of interest_1 and interest_2  |


