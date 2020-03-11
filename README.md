# Chinese Aid in the Middle East and Africa

### Problem Statement:

China has been a big player in the international stage as America is retreating in influence. There is a debate on the effect of China's aid and influence in Africa and the Middle East. How has Chinese aid affected the development and politics of countries in the Middle East and Africa? What are the characteristics of countries where China is more likely to invest? I would like to model data to see what the relationship is between Chinese aid and other economic and political indicators.

### Summary 

The Chinese aid data is from a project at William and Mary that breaks down Chinese aid to the project level. Because this data takes a long time to collect, their most recent dataset from Dec 2019 only goes to 2014, so I decided to keep all my aid data in the window of 2000-2014. William and Mary researchers have done exhaustive research to find the data about Chinese projects, but unlike the United States, World Bank, or other large donors, there is little transparency in the realm of Chinese international aid. 39% of the monetary amounts for projects were unknown. 

I was not sure how to deal with my missing data, but ultimately I decided to use NLP to make predictions. The William and Mary datasets have very descriptive text columns, so I fit Random Forest and an Extra Trees regression models. I was able to get 94% accuracy on the testing data, but I suspect this is not as accurate when applied to the unseen missing data. There are a lot of similar projects repeated in the set of known values, so I think the accuracy is probably better on the training set than on unseen data because of some of the repeated similar projects. Nonetheless, I decided to use it to predict those values, and created a column to differentiate the known values from the ones achieved by modeling if those values needed to be excluded later. 

I then used my new dataset to do some unsupervised modeling for clustering. I tried a DBSCAN model without a lot of success, measured by silhouette score, which was negative. However, I did a 2 different K-means models, one with just my aid related data, and another with the aid data along with the other indicators. I got decent silhouette scores for these (.72 and .39, respectively), and when I made a Tableau visualization with the clusters, I could see relationships between the clusters based on my subject matter expertise. 

### Conclusions 

So far my general findings are that there really is not a significant different between the Freedom House ratings and Human Development indices for countries that get Chinese aid as compared to US or World Bank aid. I need to do a bit more analysis to see this for sure. The clusters I have seem to be based more on national interest than anything else. I am going to do EDA on my clustered data to see how the clusters differ for all my measures. From my data analysis and modeling so far, I lean towards the conclusion that Chinese aid has no more of a negative or positive impact on countries than US or World Bank aid. 






### References:

https://www.aiddata.org/data/geocoded-chinese-global-official-finance-dataset

http://hdr.undp.org/en/content/human-development-index-hdi

https://explorer.usaid.gov/data

https://freedomhouse.org/sites/default/files/2020-02/FreedomintheWorld2018COMPLETEBOOK.pdf

https://data.worldbank.org/