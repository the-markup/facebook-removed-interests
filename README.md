# Citizen Browser: Facebook Promised to Remove “Sensitive” Ads. Here’s What They Left Behind

This repository contains data from the story "[Facebook Promised to Remove “Sensitive” Ads. Here’s What They Left Behind](https://themarkup.org/)" from The Markup's [Citizen Browser](https://themarkup.org/citizen-browser/) series. For more information about how the Citizen Browser application was built and the Facebook data it collects, see "[How We Built a Facebook Inspector](https://themarkup.org/citizen-browser/2021/01/05/how-we-built-a-facebook-inspector)."

## Context
Facebook provides advertisers a targeting option called "[detailed targeting](https://www.facebook.com/business/help/182371508761821?id=176276233019487)" to refine groups of people by demographics, interests, and behaviors based on their activities through the platform. In a 2021 statement, Meta said that, starting in mid-January 2022, they would cut back on this detailed targeting and remove the ability for advertisers to target users based on certain interests that describe health, race or ethnicity, political affiliation, religion, or sexual orientation.

To better understand the results of this change, we analyzed the “interests” that advertisers used to target Facebook ads delivered to The Markup's Citizen Browser panel between March 16, 2021 and April 19, 2022., We also examined the interests that Meta's Facebook ad tool suggested alongside these collected interests prior to January 2022. 

From this collection, we queried the Facebook ad tool on April 14, 2022, after the removal took place, to determine which of the interests we collected are no longer available.

| <img width="600" alt="Facebook Ads Manager suggested interests for African-American culture" src="https://user-images.githubusercontent.com/821717/167515006-081f8392-dfe7-4dc2-b4ab-2590c4cadbd7.png"> | annotation here |


## Data
The `data/` directory contains two csv files with data from the story.

1. `fb_removed_interests.csv` fb_removed_interests.csv contains Facebook's ad interests we were able to identify are no longer available as of April 14, 2022.
2. `fb_audience_overlaps.csv` contains Facebook's audience size estimates for pairs of interests with strong overlaps in users. These counts were collected from Meta's ad tool on January 7, 2022. We calculate the overlaps as follows:
- We collected Facebook’s low-end estimate for the number of users with interest #1, using the company’s ad tool.
- We repeated that process for interest #2. 
- We queried the combination of interest #1 and interest #2 in Facebook's ad tool, which produces a high and low estimate of the number of users at the union of the two interests.
- We estimated the overlap by subtracting Facebook's low-end estimate for the union of the two interests from the sum of its low-end estimates for the two interests when queried separately.


-----

Data in fb_removed_interests.csv is arranged as follows:
| column           | description                                                                                |
|:-----------------|:------------------------------------------------------------------------------------------|
| removed_interest   | Facebook ad interest that was available prior to April 14, 2022.                         |
| related_still_avail   | Facebook ad interest that was suggested in the ad tool along with removed_interest before it was removed. As of April 14, 2022, this interest is still availble. |
| aud_low_est      | Low range of Facebook's estimated audience size.  |
| aud_high_est      | High range of Facebook's estimated audience size.  |
| date_aud_test      | Date the audience size estimate was collected from the Facebook ad tool.  |
| seen_in_CB      | Ad interest appeared in a targeted ad in The Markup's Citizen Browser panel.  |
| unique_posters      | Number of unique advertisers in Citizen Browser dataset who targeted Facebook ads with this interest between March 16, 2021 and April 19, 2022.*  |
| unique_user      | Number of unique Citizen Browser panelists who were shown ads with this targeted interest between March 16, 2021 and April 19, 2022.  |
/* These counts may undercount posters where the poster name was redacted due to privacy protections of the Citizen Browser parsers.

Data in fb_audience_overlaps.csv is arranged as follows:
| column           | description                                                                                  |
|:-----------------|:------------------------------------------------------------------------------------------|
| interest_1 | Interest removed from Facebook's detailed targeting options between January and April 2022 |                      
| interest_2 | Interest suggested by Facebook's ad tool in conjunction with interest_1 before it was removed  |
| int1_aud | Facebook's low audience estimate for interest_1 |
| int2_aud | Facebook's low audience estimate for interest_2  |
| combined_aud | Facebook's low audience estimate for interest_1 + interest_2  |
| aud_overlap  | Result of (interest_1 + interest_2) - combined_aud  |



