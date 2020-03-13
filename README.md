# Chinese Aid in the Middle East and Africa

### Problem Statement:

China has been a big player in the international stage as America is retreating in influence. There is a debate on the effect of China's aid and influence in Africa and the Middle East. How has Chinese aid affected the development and politics of countries in the Middle East and Africa? What are the characteristics of countries where China is more likely to invest? 

### Summary 

Some criticisms of Chinese aid say that it can cause debt, encourage local corruption, and does not really help the development of struggling countries. In order to evaluate the effects of Chinese aid, I collected data on Chinese aid, US aid, World Bank aid, Human Development Index, Freedom House ratings (on political and civil rights), Corruption Perception Index, resource rents, per capita gdp, and per capita debt. I engineered some features to see the difference between some of these indicators between 2000 and 2014. 

The Chinese aid data is from a project at William and Mary that breaks down Chinese aid to the project level. Because this data takes a long time to collect, their most recent dataset from Dec 2019 only goes to 2014, so I decided to keep all my aid data in the window of 2000-2014. William and Mary researchers have done exhaustive research to find the data about Chinese projects, but unlike the United States, World Bank, or other large donors, there is little transparency in the realm of Chinese international aid. 39% of the monetary amounts for projects were unknown. 

I was not sure how to deal with my missing data, but ultimately I decided to use NLP to make predictions. The William and Mary datasets have very descriptive text columns, so I fit Random Forest and an Extra Trees regression models. I was able to get 94% accuracy on the testing data, but I suspect this is not as accurate when applied to the unseen missing data. There are a lot of similar projects repeated in the set of known values, so I think the accuracy is probably better on the training set than on unseen data because of some of the repeated similar projects. Nonetheless, I decided to use it to predict those values, and created a column to differentiate the known values from the ones achieved by modeling if those values needed to be excluded later. 

I then used my new dataset to do some unsupervised modeling for clustering. I tried a DBSCAN model without a lot of success, measured by silhouette score, which was negative. However, I did a few different K-means models, some with just my aid related data, and some with the aid data along with the other indicators. I got decent silhouette scores for these (in the 10s to 70s), and when I made a Tableau visualization with the clusters, I could see relationships between the clusters based on my knowledge of Africa. 

I also tried regression and classification models to see if I could predict the amount of Chinese aid based on other factors or to predict if a country had more Chinese or US aid. The data set is too small for this to really be effective, and scores on my models were really low. 

### Data Dictionary 

|Feature|Type|Description|
|---|---|---|
|country|object|Country, limited to Middle East and Africa for this project|
|world_bank_totals|float|Total World Bank aid from 2000-2014| 
|chinese_aid_totals|float|Total Chinese aid from 2000-2014|
|usaid_totals|float|Total US aid from 2000-2014|
|hdi_00|float|Human Development Index in 2000|
|hdi_14|float|Human Development Index in 2014|
|pr_score00|float|Freedom House political rights score in 2000|
|cl_score00|float|Freedom House civil rights score in 2000|
|fh_status00|object|Freedom House status in 2000 (Free, Partially Free, Not Free|
|pr_score14|float|Freedom House political rights score in 2014|
|cl_score14|float|Freedom House civil rights score in 2014|
|fh_status14|object|Freedom House status in 2014 (Free, Partially Free, Not Free|
|cpi_2014|float|Corruption Perception Index score for 2014 (lower is more corrupt)|
|population|integer|Population of country|
|gdp_per_cap14|float|GDP per capita in 2014|
|gdp_per_cap00|float|GDP per capita in 2000|
|resource_rents|float|resource income as percentage of GDP|
|debt_to_gdp|float|Percentage of debt compared to GDP|
|fh_change|float|Change in total Freedom House scores from 2000 to 2014|
|pc_gdp_change|float|Change in per capita GDP from 2000 to 2014|
|hdi_change|float|Change in Human Development Index from 2000 to 2014|
|world_bank_pc|float|Per capita World Bank aid|
|chinese_aid_pc|float|Per capita Chinese aid|
|usaid_pc|float|Per capita US aid|

### Conclusions 

Th data does not show evidence that critiques of Chinese aid are accurate. China and the World Bank overall invested in poorer developing nations, whereas US has given more to nations such as Israel and Gulf States. Countries with United States military involvement, like Iraq, have recieved huge amounts of US aid. Aid from all sources comes with political motivations, which in the case of China and the United States, are competing motivations. However, generally aid is good, and in the absence of US aid, it is good for African nations to get aid to help with their development.

### References:

https://www.aiddata.org/data/geocoded-chinese-global-official-finance-dataset

http://hdr.undp.org/en/content/human-development-index-hdi

https://explorer.usaid.gov/data

https://freedomhouse.org/sites/default/files/2020-02/FreedomintheWorld2018COMPLETEBOOK.pdf

https://data.worldbank.org/

https://voxeu.org/article/political-bias-and-economic-impact-chinese-aid

https://www.brookings.edu/opinions/chinas-aid-to-africa-monster-or-messiah/