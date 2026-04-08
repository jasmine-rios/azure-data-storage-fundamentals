# Chapter 6 Azure SQL Services and Open Source Options

The cloud has revolutionized how we think about and work with databases.
Whether you're building a new applciation or migrating an existing one, understanding Azure's database offerings is crucial for success in modern data management.
In this chapter, we'll expolore both the Azure SQL family of products and Azure's robust support for open source database systems.

**Coverage of Curriculum Objectives**

This chapter addresses the following DP-900 exam objectives:

- Describe relational Azure data services, including the Azure SQL family of products: Azure SQL Database, Azure SQL Managed Instance, and SQL server on Azure virtual machines (VMs).
- Identify Azure database services for open source database systems.

## Understanding the Azure SQL Family

When organizations consider moving their databases to the cloud, they often face a crucial decision: how much control and responsibility do they want to maintain over their database infrastructure? Azure provides a spectrum of options through its SQL family of products, each designed to meet different requirements and comfort levels with cloud adoption.

Figure below illustates the key decision points when choosing between Azure SQL services.
Let's explore each option in detail to understand its unique characteristics and ideal use cases.

![The Azure SQL family of choices](image-12.png)

### Azure SQL Database: Cloud Native Database Solution

Azure SQL Databases represents Microsoft's vision of a truly cloud native database service.
It takes the core capabilities of SQL Server and transforms them into a fully managed platform-as-a-service (PaaS) offering.
This transformation means that while you maintain complete control over your data and access, Microsoft handles the underlying infrastructure management tasks that traditionally consume significant IT resources.

**NOTE**

Azure SQL Database exemplifies the DBaaS model which we discussed in Chapter 4, in which traditional database administration taks are automated, allowing organizations to focus on data and applications rather than infrastructure managment.

**EON**

#### Features that drive cloud adoption

The appeal of Azure SQL Database lies in its ability to simplify database management while enhancing reliability and security.
When you create an Azure SQL Databse, you automatically get:

- *Automated maintance* that keeps your database running smoothly without manual intervention.
Think of it having a dedicated database administrator working 24/7, handling routine tasks like patching and updates.
This automation extends to performance tunning, where the service continuously monitors your workload and adjusts settings for optimal performance.
- *Built-in high availability* that becomes part of your database's DNA rather than an additonal feature to configure.
The service maintains multiple copies of your data and automaticall fails over to a healthy copy if issues arise, typically within seconds and without requiring any application changes.

The intelligent performance monitoring system acts like a vigilant guardian, constantly watching your database's behavior.
It can alert you to potential problems before they impact your applications and even provide specific recommendations for improvement.

#### Deployment decisions

When implementing Azure SQL Database, you'll need to choose between two primary deployment models, each suited to different scenarios.

The *single database* option deployment model provides a fully isolated database environment with dedicated resources.
Unlike a full SQL Server instance, you work with individual databases rather than server-level objects.
This choice is ideal for:

- Applications with predictable resource requirements
- Scenarios where guarenteed performance levels are essential
- Organization seeking simplicity in database management while maintaining isolation

The *elastic pools* deployment model implements a shared-resource approach that pools resources across multiple databases.
It's particularly beneficial for:

- Environments managing multiple databases with varying workloads
- Organizations looking to optimize costs through resource sharing
- Scenarios where databases have flunctuating resource demands and can benefit from a dynamic resource allocation model

When implementing Azure SQL Databse, you'll need to carefully evaluate these deployment models based on your specific requirements and use cases.
Each option offers distinct advantages that can significantly impact your database performance, cost efficency, and management overhead.

#### The shared responsibility model

Azure SQL Database operates as a true PaaS offering with a clear division of responsibilities.
Microsoft manages everything below the database level--the SQL Server instance, host server, storage, network infrastructure, and physical security.
You manage the database itself, including your data, user access, and database-level configurations.

The shared responsiblity model brings both benefits and considerations.

Microsoft manages:

- Physical infrastructure and hardware
- Operating system patching and updates
- SQL Server instance configuration
- High availability and disaster recovery infrastructure
- Physical and network security

You manage:

- Database schema and objects
- Data and access control
- Query optimization and indexing
- Database-level security setting
- Application connections

Because of this archictectural design, certain server-level features available in traditional SQL Server installations aren't accessible in Azure SQL Database.
For instance, SQL Server Agent jobs need to be replaced with Azure Automation or Logic Apps, and cross-database queries require different approaches using external tables or elastic queries.

### Azure SQL Managed Instance: The Bridge to the Cloud

Azure SQL Managed Instance serves as a strategic middle ground in Microsoft's database portfolio.
It's desinged for organizations that want the benefits of a managed service but need greater compatibility with SQL Server features.

#### The value proposition

SQL Managed Instance provides an experience remarkably similar to traditional SQL Server but with the added benefits of cloud automation.
This familiarity makes it particulary valuable for organizations with existing SQL Server deployments looking to move to the cloud.

The service maintains near-complete compatiability with on-premises SQL Server instances, supporting features like SQL Server Agent, Service Broker, and Database Mail.
This compatibility extends to security features, with support for Windows authentication and Azure AD integration

#### Real-world migration scenarios

The true strength of SQL Managd Instance becomes apparrent in migration scenarios.
Consider a company with a complex application that uses linked servers and cross-database queries.
With SQL Managed Instance, the company can often move its databases to the cloud with minimal code changes, maintaining existing functionality while gaining cloud benefits.

Another common scenario involves organizations using SQL Server Agent for job scheduling and automation.
Rather than redesigning these processes for Azure SQL Database, these companies can maintain their existing jobs while moving to SQL Manged Instance.

#### Operational considerations

Operating SQL Managed Instance requires understanding its unique characteristics.
While it provides greater compatibility than Azure SQL Database, it also introduces some operational considerations:

- Network connectivity works differently, with the service deployed within your virtual network.
This provides better security and isolation but requires careful network planning
- Resource allocation follows a differnt model, with more granular control over compute and storage resources.
This flexibility comes with the responsibility of proper capacity planning.

Success with SQL Managed Instance often depends on proper planning and understanding of its operational model.
Organizations that take the time to understand these aspects typically experience smoother migrations and better long-term results.

**Exam Tip**

For the DP-900 exam, focus on the role of SQL Managed Instance as a bridge between on-premises SQL Server and cloud native Azure SQL Database.
Understanding when to choose it over other options is crucial

**EOET**

### SQL Server on Azure Virtual Machines: Maximum Control and Flexibility

For organizations that need complete control over their database environment or have specific requirements that can't be met by managed services, running SQL Server on Azure VMs provide a solution that combines the familiarity of SQL server with the benefits of cloud infrastructure.

#### Control and responsibility

Running SQL Server on Azure VMs means you maintain control over every aspect of your database environment, from the operating system to the SQL Server configuration.
This control comes with the responsibility of managing updates, security, and performance tunning.

Consider an organization that needs to run a specific version of SQL Server with custom patches or configurations.
With SQL Server on Azure VMs, the organization can maintain these requirements while still benefiting from Azure's infrastructure capabilities.

#### Cost and performance optimization

Azure provides several tools and features to optimize the cost and performance of SQL Server on VMs:

Azure Hybrid Benefit allows you to use existing SQL Server licenses in the cloud, potentially reducing costs significantly.
The automated patching and backup features help maintain security and reliability without manual intervention.

Performance optimization tools in the Azure portal provide insights and recommendations specific to SQL Server workloads, helping you maintain optimal performance even in a self-managed environment.

## Exploring Open Source Databases in Azure

The modern data landscape extends far beyond Microsoft's SQL Server ecosystem.
Recognizing this, Azure provides robust support for popular open source databases through fully managed services.
Let's explore these options and understand their unique characteristics.

### Azure Database for MySQL: Powering Web Applications

MySQL has long been the backbone of many web applications, particularly those built on the LAMP (Linux, Apache, MySQL, PHP) stack.
Azure Database for MySQL brings this popular database engine to the cloud as a fully managed service.

#### Service capabilities

Azure Database for MySQL maintains compatibility with communit MySQL while adding enterprise-grade features.
When you create a MySQL database in Azure, you get:

- Automated patching and updates that keep your database secure and up-to-date
- Built-in high availability with up to 99.99% uptime SLA
- Automated backups with point-in-time restore capabilities
- Intelligent performance recommendations
- Advanced threat protection

#### Deployment models

Azure Database for MySQL Flexible Server provides three distinct service tiers to meet different workload requirements.

Each tier provides flexible scaling options, with compute scaling requiring a brief 60 to 120-second restart, while storage scaling can be performed online without downtime.
The service also includes automated storage management features and comprehensive backup capabilities across all tiers.

#### Burstable tier

Designed for workloads that don't need continous full CPU