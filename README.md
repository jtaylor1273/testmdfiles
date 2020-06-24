# 2.1 - Analytics - Azure Machine Learning

## Customer Use Case
Advocate Aurora Health was performing a Tenant migration where there was no co-existence configured between environments.  Advocate Aurora Health (AAH) was experiencing issues after each migration because migrated team members were unable to communicate with team members that were not migrated.  

CDW collected mailbox and user data on each team member.  This data will be ingested into Azure Machine Learning (AML) and run through the K-means clustering algorithm to identify which groups should be migrated together based on several features.

Key Azure services that are part of their solution:  

* Azure Machine Learning

Portal/Service Catalog/UI

* Configured through the Azure Machine Learning Portal


## Solution - Reference Architecture
The Figure below describes the overview of the AAH architecture and highlights the different components of the solution.
![Solution Diagram](/images/solution.png)

Advocate Aurora Health provided environmental information regarding their mailboxes and current planning schedule.  Both files were provided in a comma delimited format.  The files were imported into Microsoft SQL server as new tables.  Several features were not in 1NF format, so additional linking tables were created to comply with 1NF.  This normalization was needed to prevent having to parse features inside of AML.  The database was then imported as a data source in Azure Machine Learning.

![Solution Diagram](/images/experiment.png)

1.	The dataset was imported from SQL.  
1.	Feature Hashing was enabled to allow text data to be evaluated as numerical features
1.	There was no training data we knew the number of clusters we needed (k), so the k-means clustering was selected with 60 centroids
1.	The model was exported to a CSV file for consumption by the customer

## Provision Solution
The solution followed the Cross-industry standard process for data mining (CRISP-DM).  
![Solution Diagram](/images/crisp.png)

* Business Understanding (described above)
* Data Understanding – (described above)
* Data Preparation – (described above)
* Modeling – (described above)
* Evaluation – The intra-cluster distances were evaluated and approximated a normal distribution
* Deployment - (described above)

## Configure Solution
The solution was configured using the following process

* Navigate to studio.azureml.net
* Import new dataset
* Create new experiment

![Solution Diagram](/images/exp_overview.png)


## Change/Update Solution
This solution was for a transient use case and will not be needed again.  Changes or Updates to this solution will be performed during the model’s short lifecycle using the Azure Machine Learning Studio at studio.azureml.net.  

## Delete Solution
This solution will be discarded by deleting the Machine Learning Workspace this solution was included in.
![Solution Diagram](/images/settings.png)

## References
[Microsoft Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-ml)
[Enterprise and Basic Editions of Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-editions)
[K-Means Clustering](https://docs.microsoft.com/en-us/azure/machine-learning/algorithm-module-reference/k-means-clustering?WT.mc_id=docs-article-lazzeri)
[CRoss-Industry Standard Process for Data Mining](http://www.datascience-pm.com/crisp-dm-2/)
