# 2.1 - Azure Event Grid

This template deploys a Event Hub. The Event Hub is a fully managed, real-time data ingestion service that’s simple, trusted, and scalable.

## Customer Use Case
ABC Corporation is running a production website on IaaS servers hosted in Azure.  Recently some configuration changes have been made to the website resources that have caused outages.  The team is unsure what or who is making the changes.  

ABC has asked CDW to develop a solution that would alert them whenever changes are made to resources within that resource group.  This early notification will allow ABC to quickly reverse unscheduled changes and track down the root cause easier.

Key Azure services that are part of their solution:  

*	Azure Event Grid
*	Azure Logic App
*	Azure Function App

## Solution - Reference Architecture
The diagram below describes the overview of the architecture and highlights the different components of the solution.
![Solution Diagram](/images/solution.png)

The website resources were all inside of a single resource group called websiterg.  The Event Grid subscription will monitor the Production Azure Subscription for changes to the websiterg resource groups.  

When successful changes are made within the resource group, the event grid will trigger an Azure Function App which will then initiate a Logic App to send an email from a shared mailbox to the website administrators.

## Provision Solution
The solution was setup using the following process

+ The Event Grid can be provisioned using the ARM Template in GitHub.
+ Additional configuration will be performed through the UI and vary based on customer requirements


## Configure Solution
The solution was configured using the following processes
* Build the Azure Function App with an Event Grid Trigger
* ![Solution Diagram](/images/function.png)
* Build an Event Grid Subscription tracking all changes to a resource group.  The Event Grid subscription shows 52 events being generated. 
* ![Solution Diagram](/images/subscription.png)
* Made change to the targeted resource group and received a hit on the Azure Function as noted in screen capture below.  The screen capture shows the Azure Function App was triggered 23 times.  The difference between the number of generated events and successfully triggered Function calls is a result of me working through an issue.
* ![Solution Diagram](/images/monitor.png)
* The HTTP trigger initiates the Logic App to send an email to the administrators of the website.
* ![Solution Diagram](/images/logicapp1.png)


## Change/Update Solution
The change/update process is as follows

* The Azure Function can be modified by going into the Azure Portal
* Search for Azure App
* Select the appropriate Trigger and modify the code
* ![Solution Diagram](/images/trigger.png)

## Delete Solution
Since all resources for this solution are created under the same resource group, deleting the resource group will delete Event Grid Subscription and Azure Function App.

The deprovisionSolution.ps1 can be used with a single parameter to remove the resource group
`<deprovisionSolution.ps1 "ResourceGroupName">`

## References
[Microsoft Event Grid](https://docs.microsoft.com/en-us/azure/event-grid/overview)
[Microsoft.EventGrid eventSubscriptions Template](https://docs.microsoft.com/en-us/azure/templates/microsoft.eventgrid/eventsubscriptions)
[Microsoft.EventGrid Topics Template](https://docs.microsoft.com/en-us/azure/templates/microsoft.eventgrid/topics)
