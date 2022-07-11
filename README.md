# Online Shoppers Purchasing Intent

Summary
---
Predicts if an online shopping session will result in a purchase

Data Set
---
The data set used for this project is 12,330 rows, and 18 columns. Each row represents an online shopping session. Each session is unique, and the data covers 1 year.

The target column for this data set is "Revenue" - whether or not a session resulted in a purchase.

Besides the target column, the data set consists of 10 numerical and 7 categorical features:

* #of pages visited and time spent on those pages for three types of web pages: Administrative, Informational, Product
* Three features from google analytics: Bounce Rate/Exit Rate/Page Value
* Three features based on time of session:
* * Special Day – a measure of closeness to a specific holiday (Xmas, mother’s day, etc..)
* * Month – Month of the year
* * Weekend – Weekend yes/no
* Two features based on the customer’s PC:
* * Operating System
* * Browser
* Customer location (region)
* Traffic type
* Visitor type (Returning visitor/new visitor/other

Exploratory Analysis
---
The following are some observations about the data:

![image](https://user-images.githubusercontent.com/99829862/164612937-193ab476-1247-45ca-bdd6-449b6dcf36a7.png)

* A majority of sessions (85%) do not result in a purchase

![image](https://user-images.githubusercontent.com/99829862/164613042-8b3b85c4-a9f6-467c-92bf-c0a22767888a.png)

* A majority of sessions (85%) are repeat customers

![image](https://user-images.githubusercontent.com/99829862/164613137-8bef3407-57e2-4d34-8a0e-cc76dab4ea2e.png)

* Peak months for website visits are: March, May, November, and December

![image](https://user-images.githubusercontent.com/99829862/164613340-eb589500-38ce-4ca1-b246-a1edf0ae5276.png)

* A large majority of visits occur near a holiday

![image](https://user-images.githubusercontent.com/99829862/164613523-d5c19503-4600-4deb-b450-376a2e9ad058.png)

The three columns with the highest correlation with Revenue are:
* Page Values (positive/moderate)
* Exit Rate (negative/weak)
* Bounce Rates (negative/weak)

Customer Segmentation
---

To better understand the customer base. I performed a clustering of the sessions. This was done using a KMeans clustering method.

Number of clusters was chosen based on the Inertia and Silhouette score.
![image](https://user-images.githubusercontent.com/99829862/164613650-c4cfa9ac-0795-40da-b3d9-91d315156bf0.png)

* Based on these scores, n_clusters=5 was chosen.

Here are the mean values for all numeric columns grouped by cluster:
![image](https://user-images.githubusercontent.com/99829862/164613736-dcc25c79-892d-4bdb-98c9-05369bf553b8.png)

Based on these values there are 4 customer segments I believe are worth highlighting:

Cluster 3 – The buyers
* 1651 Members (13%)
* These customers mean business, quickly find the product they want and make a purchase
* Visit a moderate amount of sites
* Spend a moderate amount of time
* 96% of sessions result in purchases

Cluster 1 – Researchers
* 1160 Members (9%)
* These customers spend a long time looking for that perfect purchase, but are hesitant to actually buy
* Visit the most sites
* Spend the most amount of time on these sites
* 23% of sessions result in purchases

Cluster 3 – The Buyers
* 1651 Members (13%)
* Visit a moderate amount of sites
* Spend a moderate amount of time
* 96% of sessions result in purchases

Cluster 2 – Stumblers
* 748 Members (65)
* These customers stumbled upon the product pages and have no intention of buying
* On average <1 administrative/informational, and 2.5 product sites visited
* Spend the least amount of time on these sites
* Highest bounce/exit rates
* 0.4% of sessions result in purchases

Modeling
---

For this classification problem, I tried multiple models, and tuned hyperparameters using GridSearchCV.

Before tuning, I oversampled the Revenue = 1 rows.

I tried the following models and tuned the listed parameters (if any):

Dummy Model (stratified)
* No parameter tuning
* Overall accuracy
* * Training set: 50%
* * Testing set: 50%

Random Forest
* Parameters tuned: max depth
* Overall accuracy
* * Training set: 100%
* * Testing set: 96%

KNN Classifier
* Parameters tuned: weights, n_neighbors
* Overall accuracy
* * Training set: 100%
* * Testing set: 94%

Gradient Boosting Classifier
* Parameters tuned: max depth
* Overall accuracy
* * Training set: 100%
* * Testing set: 96%

The best overall model, when taking into account all metrics and speed of fit/prediction was Random Forest. 

![image](https://user-images.githubusercontent.com/99829862/165889306-8ad315c6-e2df-4281-8372-3cc8982bb646.png)
* Classification Report for Random Forest Model

![image](https://user-images.githubusercontent.com/99829862/165889344-54456779-ffb4-4ebb-b20b-f653940d62ce.png)
* Confusion Matrix for Random Forest Model
