1.DESCRIPTION

This package provides both granular data and visual insights into the Walt Disney World Marathon that occurs every year in early January in Orlando, Florida. In general, this project was multi-pronged -- on the one hand, it provides a comprehensive high-level summary of each of the races and visualizes them in a more effective manner than our team was able to find otherwise. At the same time, the analysis also looks into the overarching effects of weather, geographic, and runner-specific characteristics along with runner sentiment derived from Twitter in an attempt to define the factors that have a significant affect on runner performance. The data for this project was processed and wrangled using a combination of python and R, while the visualization aspect was handled in Tableau. More complex models (i.e. random forests) were handled in python. 

The data strategy involved several disparate datasets. First, runner names, hometowns and run-times had to be scraped from online webpages into pandas dataframes and unioned together. This was complicated by the fact that each age group and gender had a separate url. Then, hometowns (imperfectly-entered information already) had to be mapped to city information in the the geodb-cities API at [https://rapidapi.com/wirefreethought/api/geodb-cities/details] to bring in city, state and country information for each hometown. Then, weather data for each race (e.g. wind speed, temperature) had to be pulled from the world weather online API at [https://www.worldweatheronline.com/developer/api/docs/historical-weather-api.aspx]. This combined dataset was then further aggregated with a twitter sentiment dataset built out separately so that all runners along with their corresponding tweets for each race would be mapped and presented via one medium. We chose Tableau for this task. 

The Tableau file follows a linear path, going from a summary view of the running component down to the fine details of each runner's performance per year in the race, followed by the same structure for the twitter sentiment analysis. Navigation throughout the dashboard is accessible either through menu navigation (click on anything in any dashboard and the tooltip will suggest a navigation to the next page), or via tab navigation at the bottom of the workbook. Furthermore, a much more refined Readme dashboard exists within the actual Tableau workbook to explain the dashboard functionality and readability. 

In sum, this project provides a more insightful and interactive medium by which to analyze and understand marathons. It was specifically built to analyze repetitive years of the same marathon, but can easily analyze any set of marathons the user would like to view. 

Some of the limitations of this project exist in 1) imperfect data entry, and 2) a lack of data on which to join the disparate datasets. First, many of the runners are international, but for hometown they only wrote "Florida" or their first name or something else. This impacted the hometown analysis of runners and, in particular, the regression to check if hometown elevation had an affect on runner performance (for this reason, we left elevation out of our analysis). Second, since runners were not asked to provide their twitter handle for the race and there is no practical way to tie runner names to twitter handles, a roundabout way of matching names with twitter handles was to use Levenshtein distance scores using python's FuzzyWuzzy package. Due to this, the twitter sentiment analysis was not perfectly combined with the running data. However, including this data in the future would allow for an easier combination of said data and an effective way to check whether sentiment has a significant effect on run-time. 

The package is separated into two components:
	1) DOC
		- team143report.pdf
		- team143tableau.twbx

	2) Code (in order of usage)

		Running Data
		- Past_Runner.ipynb   -- to pull data from website pdfs
		- Weather_grab.ipynb  -- to pull weather data using an API key
		- City_Puller.ipynb   -- to pull city detail information using an API key
		- City_Merger.ipynb   -- to merge city information with the output of Past_Runner.ipynb
		- Race_Prediction_CS6242.Rmd -- Stepwise Regression to predict 3rd place qualification time
		- Race_Prediction_Cleanv2.csv -- data for the above code 

		Twitter Sentiment Data
		-- GetOldTweets.ipynb -- use API to gather old tweets from Twitter
		-- Sentiment_Analysis.ipynb -- Pre-process tweets, estimate sentiment, identify emotion association
		-- TwitterMatching.ipynb -- Match runners to most likely twitter handle and estimate likelihood of match
		-- Predict_Runner_Time.ipynb -- Estimate run time for individual runners based on race data and twitter sentiment


2.INSTALLATION

Step 1: Download Tableau 2020.1.2 or newer
Step 2: Open team143tableau.twbx

(Optional) Step 3: Because this is a Tableau workbook, installation of the final product is much simpler. In effect, all of the data has already been pre-processed into the workbook and presented, so no work is required on the part of the user. However, if the user would like to see how the data was wrangled on the back-end, they should have the latest version of Anaconda and Jupyter Notebook installed. This way, the user can access each of the above-delineated .ipynb scripts from top to bottom to follow a step-by-step guide of how the data was compiled. More specific instructions of the steps taken to aggregate the final datasets are noted within the scripts. 

3.EXECUTION

See step 2 of INSTALLATION above. 

