<properties 
	title="Elastic database jobs overview" 
	pageTitle="Elastic database jobs overview" 
	description="Illustrates the elastic database job service" 
	metaKeywords="azure sql database elastic databases" 
	services="sql-database" documentationCenter=""  
	manager="jeffreyg" 
	authors="sidneyh"/>

<tags 
	ms.service="sql-database" 
	ms.workload="sql-database" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="06/25/2015" 
	ms.author="sidneyh" />

# Elastic Database jobs overview

**Elastic Database jobs** (preview) enables you to run T-SQL scripts (jobs) against all of the databases in an [elastic database pool (preview)](sql-database-elastic-pool.md). For example, you can easily update the schema in every database to include a new table. Normally, you must connect to each database independently in order to run T-SQL statements or perform other administrative tasks. An **elastic database job** handles the task of logging in, and reliabily running the script for you, while logging the status of execution for each database. For instructions on installing the preview, go to [Installing the Elastic Database job components](sql-database-elastic-jobs-service-installation.md).

![Elastic database job service][1]

## Benefits

* Define, maintain and persist T-SQL scripts to be executed across an elastic database pool
* Execute T-SQL scripts reliably with automatic retry and at scale
* Track job execution state

## Scenarios

* Performance administrative task, such as deploy new schema
* Update reference data, for example product information common across all databases
* Rebuild indexes to improve query performance

## How the job works

1.	Install the services used by elastic database jobs. See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md). If the installation fails, see [how to uninstall](sql-database-elastic-jobs-uninstall.md).
2.	Configure the elastic database pool for job execution by [adding a user to each database](sql-database-elastic-jobs-add-logins-to-dbs.md).
3.	Create an itempotent T-SQL script that can be run against every database in the pool.
4.	Follow these steps to run the script: [Creating and managing Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) 

## Components and pricing 

The following components work together to create an Azure Cloud service that enables ad-hoc execution of administrative jobs. The components are installed and configured automatically during setup, in your subscription. You can identify the services as they all have the same auto-generated name. The name is unique, and consists of the prefix "edj" followed by 21 randomly generated characters.

* **Azure Cloud Service**: elastic database jobs (preview) is delivered as a customer-hosted Azure Cloud service to perform execution of the requested tasks. From the portal, the service is deployed and hosted in your Microsoft Azure subscription. The default deployed service runs with the minimum of two worker roles for high availability. The default size of each worker role (ElasticDatabaseJobWorker) runs on an A0 instance. For pricing, see [Cloud services pricing](http://azure.microsoft.com/pricing/details/cloud-services/). 
* **Azure SQL Database**: The service uses an Azure SQL Database known as the **control database** to store all of the job metadata. The default service tier is a S0. For pricing, see [SQL Database Pricing](http://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: An Azure Service Bus is for coordination of the work within the Azure Cloud Service. See [Service Bus Pricing](http://azure.microsoft.com/pricing/details/service-bus/).
* **Azure Storage**: An Azure Storage account is used to store diagnostic output logging in the event that an issue requires further debugging (a common practice for [Azure diagnostics](../cloud-services-dotnet-diagnostics.md)). For pricing, see [Azure Storage Pricing](http://azure.microsoft.com/pricing/details/storage/).

## Next steps
[Install the components](sql-database-elastic-jobs-service-installation.md), then [create and add a log in to each database in the pool](sql-database-elastic-jobs-add-logins-to-dbs.md). To further understand job creation and management, see [creating and managing elastic database jobs](sql-database-elastic-jobs-create-and-manage.md).

[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->

 