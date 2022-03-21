### Background

One of New York City's goals for combating climate change is to increase the refuse to organics diversion rate, and one of the ways to do this is through expanding the city's curbside composting program, which is operated by the Department of Sanitation. The program was suspended for approximately 16 months during the pandemic and now that it's rolling out service again in eligible districts, it needs an improved plan for expansion. Currently, it’s only expanding into eligible districts based on the number of sign-ups in a district and sign-up rates vary greatly based on the district. In the district with the highest sign-up rate, approximately 3/4 of households (approximately 33K) have signed up for the service; in the district with the lowest sign-up rate, only 3% (approximately 1K) have signed up.

The scoping for this project can be found in [this document](https://docs.google.com/document/d/11p08Gr9mXwlCwe0h_wq35OQC0ZYXTVRxv0pXbe1qQWM/edit?usp=sharing).

### Data Science Solution

#### Opportunity
    
The curbside composting program is a way to reduce the amount of trash bags on a sidewalk and it’s more convenient than going to a composting drop-off site, both of which may appeal to households with greater amounts of trash and more limited access to alternative forms of composting in their districts.

#### Impact Hypothesis

Outreach by the DSNY about the curbside composting program in eligible districts with low sign-up rates that have large amounts of trash and limited alternative options for composting will lead to more sign-ups and, thus, more expansion.

#### Solution Path  

- Visualize eligible districts by household sign-up rates, amounts of trash, and other composting options
- Create an index to prioritize eligible districts for outreach based on these factors
- Conduct outreach in districts with the highest index scores

#### Measures of Success

- Index accurately ranks districts based on their need for outreach, according to the inputs (i.e., sign-up rates, amounts of trash and access to alternative options for composting)
- Sign-up rates in districts where outreach is conducted will be higher than they were before outreach was conducted

### Data

I used the following data sources for this project:

- [DSNY Monthly Tonnage Collection data](https://data.cityofnewyork.us/City-Government/DSNY-Monthly-Tonnage-Data/ebb7-mvp5) from NYC OpenData
- [Food Scrap Drop-off Locations in NYC](https://data.cityofnewyork.us/Environment/Food-Scrap-Drop-Off-Locations-in-NYC/if26-z6xq) from NYC OpenData
- [Curbside Composting Program Sign-up Data](https://www1.nyc.gov/assets/dsny/site/services/food-scraps-and-yard-waste-page/bydistrict-curbsidecomposting) from the DSNY's website
- [NYC Community District Profiles](https://communityprofiles.planning.nyc.gov/) from the Department of City Planning
- [Spatial file of NYC Community Districts' boundaries] (https://data.cityofnewyork.us/City-Government/Community-Districts/yfnk-k7r4) from NYC OpenData

Given the low sign-up rates for the curbside composting program in certain eligible districts, I wanted to think about what might motivate households in these districts to sign-up. I chose the amount of residential trash in a district as a factor, since plastic trash bags can be an eye sore and can also more easily be broken into by pests than the brown bins provided by the curbside composting program. And from the DSNY's perspective as a business, going to the areas where there's more trash could mean there's more potential to divert it to organics collection. The best proxy I could find for the amount of residential trash is the monthly tonnage of refuse collected from residences and "institutions" serviced by DSNY (in my research, "institution" doesn't include private businesses, but it does include "non-profits", such as schools).

I also chose limited access to alternative forms of composting as a motivating factor for signing up for the curbside composting program, since the curbside program would be the most convenient way for households to compost. The proxy I used for this was the number of food scrap drop-off sites per square mile in eligible districts.

Here is a [link](https://docs.google.com/spreadsheets/d/1khe92d1-ZcTdI5EMA8bWt69AcS5CJBHnzZdzVamsSLw/edit?usp=sharing) to the Google Sheets document, where I compiled the above data sources and created the final dataset for visualizations in Tableau. The Google Sheets document also contains tabs with pivot tables and charts.

Since the program sign-up data was only available in PDF format, I converted it to a csv in Python before importing it into the Google Sheets document linked above. Here is a [link](https://github.com/chloebs4590/Metis-Business-Fundamentals/blob/main/biz_fundamentals_project.ipynb) to the Jupyter Notebook where I made the conversion.

After compiling the data on household sign-up rates per eligible district (the only data available was from August - December 2021, in aggregate); average monthly tonnage of refuse collection per 10,000 residents per eligible district (I chose the time period June 2020 - September 2021, since that's when the curbside composting program was suspended); and the number of food scrap drop-off sites per square mile per eligible district, I created maps of these metrics. Here is a [link](https://public.tableau.com/app/profile/chloe.bergsma.safar/viz/MetisBusinessFundamentalsProject/RefusevDrop-offSitesvSignups2) to the interactive Tableau dashbord with these maps. In each of the maps, the more darkly shaded the district is, the better a candidate it is for outreach, based on these factors.
