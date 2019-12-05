## An end-to-end process for lifting and shifting your applications to Azure
This blog describes how to streamline the migration journey for Microsoft Azure web workloads across your application and relevant databases. By taking advantage of Azure Migrate, the Azure App Service Migration Assistant, the Data Migration Assistant, and Azure Database Migration Service, we simplify the migration of your web apps and databases to Azure with minimal or no code changes.
# Overview
Application overview
Parts Unlimited is a sample eCommerce website site built on .Net Core 2.0. The site includes a front-end ordering page, a mobile experience, an order database, and a variety of other common eCommerce features. The application features a modern HTML5 responsive layout using bootstrap for mobile, tablet, and PC. It supports multiple authentication options including Azure Active Directory, Google, and Facebook. At the same time, it leverages a variety of Azure App Service features including testing in production, staging slots, and environment variables for feature flags (to turn on/off recommendations). The site works with **Visual Studio 2017** and includes a docker file and sample publishing profile to deploy as a docker container.

The application that will be migrated is hosted on a **Windows server 2016** running **Internet Information Services (IIS)**, while the database is hosted on a computer running **SQL Server 2017**.

You can find a repo with the site code here: http://aka.ms/pulabs

### Phases in the migration journey
Migrating to the cloud involves moving your web apps and databases, and there are different tools and techniques for each. However, the typical migration journey consists of four phases: **pre migration, migration, post migration, and optimization**.

 During pre-migration, you:
1. Discover the server, application, and database assets.
2. Determine application dependencies.
3. Identify artifacts that need to be migrated together.
4. Assess Azure target readiness.
5. Determine the optimal target SKU.
6. Detect database objects or ad hoc queries from the application layer that may break when migrating to Azure because of legacy syntax.
7. Prepare the necessary fixes to apply during the post migration phase.

During **migration**, you migrate the application and your schema and data, as well as any other server objects (such as logins, SQL Server Agent jobs, and SSIS packages) upon which your application depends.

During **post-migration**, you:

1. Make the necessary fixes to breaking changes reported in assessment.
2. Perform a few functional tests.
3. Address any performance issues that you may encounter during the testing.
 

Finally, during **optimization**, you perform continuous evaluation and refinement. The goals of optimization are to:

* Gather operational insights.
* Fine-tune performance.
* Reduce TCO.
* Begin leveraging cloud native services for better business insights.
* Improve security to meet compliance goals.
 
With this high-level road map of the migration journey in place, let’s take a look the details associated with the process associated with migrating applications and the databases supporting them.


## Discovery
The first step in the migration journey is to “discover” the servers hosting the application and databases to determine if there are the dependencies that would require migrating these entities to Azure together.

You can use Azure Migrate to assesses on-premises workloads for migration to Azure. The service discovers and assesses the migration suitability of on-premises virtual servers and servers running SQL Servers. Azure Migrate sizes things based on performance and provides cost estimations for running on-premises computers in Azure.

You can also use the **Microsoft Assessment and Planning Toolkit (the "MAP Toolkit")** to assess your current IT infrastructure for a variety of technology migration projects. This Solution Accelerator provides a powerful inventory, assessment, and reporting tool to simplify the migration planning process.

For the Parts Unlimited application, we already know the application and database servers and their respective dependencies, so we skip the discovery process for purposes of this blog post. Both the application and SQL Server database are hosted on a server named “SQL2017.redmond.corp.microsoft.com”.


 
