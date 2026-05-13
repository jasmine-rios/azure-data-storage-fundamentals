# Understand Normalization

Normalization is a term used by database professionals for a schema design process that minimizes data duplication and enforce data integrity.

While there are many complex rules that define the process of refactoring data into various levels (or forms) of normalization, a simple definition for practical purposes is:

1. Seperate each *entity* into its own table.
2. Seperate each discrete *attribute* into its own column.
3. Uniquely identify each entity instance (row) using a *primary key*.
4. Use *foreign key* columns to link related entities.

To understand the core principles of normalization, suppose the following table represents a spreadsheet that a company uses to track its sales.

![Sales Data Example](assets/image31.png)

Notice that the customer and product details are duplicated for each individual item sold; and that the customer name and postal address, and the product name and price are combined in the same spreadsheet cells.

Now let's look at how normalization changes the way the data is stored.

![Normalized Structured Tables](assets/image32.png)

Each entity that is represented in the data (customer, product, sales order, and line item) is stored in its own table, and each discrete attribute of those entities is in its own column.

Recording each instance of an entity as a row in an entity-specific table removes duplication of data.
For example, to change a customer's address, you need only modify the value in a single row.

The decomposition of attributes into individual columns ensures that each value is constrained to an appropriate data type- for example, product prices must be decimal values, while line item quantities must be integer numbers.
Additionally, the creation of individual columns provide a useful level of granularity in the data for querying- for example, you can easily filter customers to those who live in a specific city.

Instances of each entiy are uniquely identified by an ID or other key value, known as primary key; and when one entity references another (for example, an order has an associated customer), the primary key of the related entity is stored as a *foreign key*.
You can look up the address of the customer (which is stored only onece) for each record in the **Order** table by referencing the corresponding record in the **Customer** table.
Typically, a relational database management system (RDBMS) can enforce referential integrity to ensure that a value entered into a foreign key field has an existing corresponding primary key in the related table--for example, preventing orders for non-existing customers.

In some cases, a key (primary or foreign) can be defined as a *composite* key based on a unique combination of multiple columns.
For example, the **LineItem** table in the example above uses a combination of **OrderNo** and **ItemNo** to identify a line item from an individual order.

# Describe Azure services for Open-source databases

In addition to Azure SQL services, Azure data services are available for other popular relational database systems, including MySQL and PostgreSQL.
The primary reason for these services is to enable organizations that use them in on-premises apps to move to Azure quickly, without making significant changes to their applications.

## What are MySQL and PostgreSQL?

MySQL and PostgreSQL are relational database management systems that are tailored for different specializations.

MySQL started life as a simple-to-use open-source database management system.
It's the leading open source relational database for Linux, Apache, MySQL, and PHP (LAMP) stack apps.
It's available in several editions; Community, Standard, and Enterprise.
The community edition is available free-of-charge, and has histroically been popular as a database management system for web applications, running under Linux.
Versions are also available for Windows.
Standard edition offers higher performance, and uses a different technology for storing data.
Enterprise edition provides a comprehensive set of tools and features, including enhanced security, availability and scalability.
The standard and Enterprise editions are the versions most frequently used by commercial organizations, although these versions of the software aren't free.

PostgreSQL is a hybrid relational-object database.
You can store data in relational tables, but a PostgreSQL database also enables you to store custom data types, with their own non-relational properties.
The database management system is extensible; you can add code modules to the database, which can be run by queries.
Another key feature is the ability to store and manipulate geometric data, such as lines, circles, and polygons.

PostgreSQL has its own query language called *pgsql*.
This language is a varient of the standard relational query language, SQL, with features that enable you to write store procedures that run inside the database.

## Azure Database for MySQL

Azure Database for MySQL is a PaaS implementation of MySQL in the Azure cloud, based on the MySQL community edition.

The Azure Database for MySQL service includes high availability at no additional cost, and scalability as required.
You only pay for what you use.
Automatic backups are provided, with point-in-time restore.

The server provides connection security to enforce firewall rules and, optionally, require SSL connections.
Many server parameters enable you to configure server settings such as lock modes, maximum number of connections, and timeouts.

Azure Database for MySQL provides a global database system that scales up to large databases without the need to manage hardware, network components, virtual servers, software patches, and other underlying components.

Certain operations aren't available with Azure Database for MySQL.
These functions are primarly concerned with security and administration.
Azure manages these aspects of the database server itself.

### Benefits of Azure Database for MySQL

You get the following features with Azure Database for MySQL:

- High availability features built-in
- Predictable performance
- Easy scaling that responds quickly to demand
- Secure data, both at rest and in motion
- Automated backups and point-in-time restore for the last 35 days
- Enterprise-level security and compliance with legislation

The system uses pay-as-you-go pricing so you only pay for what you use.

Azure Database for MySQL server provides monitoring functionability to add alerts, and to view metrics and logs.

### Azure Database for MySQL Flexible Server

The flexible-server deployment option is a fully managed service designed to provide more granular control and flexibility over database management functions and configuration settings.
It provides cost optimization controls and is the recommneded deployment option for new workloads.

## Azure Database for PostgreSQL

If you prefer PostgreSQL, you can choose Azure Database for PostgreSQL to run a PaaS implementation of PostgreSQL in the Azure Cloud.
This service provides the same availability, performance, scaling, security, and administrative benefits as the MySQL service.

Some features of on-premises PostgreSQL databases aren't available in Azure Database for PostgreSQL.
These features are mostly concerned with the extensions that users can add to a database to perform specialized tasks, such as writing store procedures in various programming languages (other than pgsql, which is available), and interacting directly with the operating system.
A core set of most frequently used extensions is supported, and the list of available extensions is under continuous review.

## Azure Database for PostgreSQL Flexible Server

The flexible-server deployment option for PostgreSQL is a fully managed database service.
It provides a high level of control and server configuration customizations, and provides cost optimization controls.

## Benefits of Azure Database for PostgreSQL

Azure Database for PostgreSQL is a highly available service.
It contains built-in failure detetion and failover mechanisms.

Users of PostgreSQL are familiar with the **pgAdmin** tool, which you can use to manage and monitor a PostgreSQL database.
You can continue to use this tool to connect to Azure Database for PostgreSQL.
However, some server-focused functionality, such as performing server backup and restore, aren't available because the server is managed and maintained by Microsoft.

Azure Database for PostgreSQL records information about queries run against databases on the server, and saves them in a database named azure_sys.
You can query the query_store.qs_view to see this information, and use it to monitor the queiries that users are running.
This information can prove invaluable if you need to fine-tune the queries performed by your applications.

# An Overview of Azure SQL Database and SQL Managed Instance security capabilities

This artivle outlines the basics of securing the data tier of an application that uses Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse Analytics.
The security strategy described in this artivle follows the layered defense-in-depth approach as shown in the following diagram, and moves from the outside in:

## Network Security

Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse Analytics provide a relational database service for cloud and enterprise applications.
To help protect customer data, firewalls prevent network access to the server until you explicitly grant access based on IP address or Azure Virtual network traffic origin.

### IP Firewall Rules

IP firewall rules grant access to databases based on the originating IP address of each request.

### Vierual Network Firewall Rules

Virtual network service endpoints extend you virtual network connectivity over the Azure backbone and enable Azure SQL Database to identify the virtual network subnet that traffic originates from.
To allow traffic to reach Azure SQL database, use the SQL service tags to allow outbound traffic through Network Security Groups.

- Virtual network rules enable Azure SQL Database to only accept communications that are sent from selected subnets inside a virtual network.
- Controlling access with firewall rule doesn't apply to SQL Managed Instance.

**Note**

Controlling access with firewall rules doesn't apply to SQL Managed Instance. For more information about the networking configuration needed, see "Connecting to a managed instance"

**EON**

### Network Security Perimeter

An Azure network security perimeter creates logical network boundaries around your platform-as-a-service (PaaS) resources that you deploy outside your virtual networks.

- An Azure network security perimeter helps you control public network access to Azure SQL Database.
- Controlling access with a Azure network security perimeter doen't apply to Azure SQL Managed Instance.

**Important Note**

Azure SQL Database with Network Security parameter is currently in preview.
The previews are provided without a service level aggreement, and it's not recommended for production workloads.
Certain features might not be supported or might have constrained capabilities.

### Authentication

Authentication is the process of providing the user is who they claim to be.
Azure SQL Database and SQL Managed Instance support authentication with Microsoft Entra ID (formerly Azure Active Directory) and SQL authentication.
SQL Managed instance additionally supports Windows authentication for Microsoft Entra principals.

-  Microsoft Entra Authentication
    Microsoft Entra authentication is a mechanism to connect to Azure SQL Database, Azure SQL Managed Instanc, and Azure Synapse Analytics by using identities in Microsoft Entra ID.
    Microsoft Entra authentication allows administrators to centrally manage their identities and permissions of database users along with other Azure services in one central location.
    This feature can help eliminate the user of secrets and passwords.

    To use Microsoft Entra authentication with SQL Database, create a server admin called the Microsoft Entra administrator.
    For more information, see Connecting to SQL Database with Microsoft Entra authentication.
    Microsoft Entra authentication supports both managed and federated accounts.
    The federated accounts support Windows users and groups for a customer domain federated with Microsoft Entra ID.

    Microsoft Entra supports several different authentication options, including multifactor.

    # Explore Analytical data processing

    Analytical data processing typically uses read-only (or read-mostly) systems that store vast volumes of historical data or business metrics.
    Analytics can be based on a snapshot of the data at a given point in time, or a series of snapshots.

    The specific details for an analytical processing system can vary between solutions, but a common architecture of enterprise-scale analytics looks like this:

    1. Operational data is extracted, transformed, and loaded (ETL) into a data lake for analysis.

    2. Data is loaded into a schema of tables- typically in a Spark-based *data lakehouse* with tabular abstrations over files in the data lake, or a data warehouse with a fully relational SQL engine.
    3. Data in the data warehouse may be aggregated and loaded into an online analytical processing (OLAP) model, or *cube*. Aggregated numeric values (measures) from fact tables are calculated for intersections of *dimensions* from dimension tables.
    For example, sales revenue might be totaled by date, customer, and product.
    4. The data in the data lake, data warehouse, and analytical model can be queried to product reports, visualizations, and dashboards.

    *data lakes* are common in large-scale data analytical processing scenarios, where a large volume of file-based data must be collected and analyzed.

    *Data warehouses* are an established way to store data in a relational schema that is optimized for read operations--primarly querires to support reporting and data visualization.
    *Data Lakehouses* are a more recent innovation that combine the flexible and scalable storage of a data lake with the relational querying semantics of a data warehouse.
    The table schema may require some denormalization of data in an OLTP data source (introducing some duplication to make queries perform faster).

    An OLAP model is an aggregated type of data storage that is optimized for analytical workloads.
    Data aggregations are across dimensions at different levels, enabling you to *drill up/down* to view aggregations at multiple hierachical levels; for example to find total sales by region, by cite, or for an individual address.
    Because OLAP data is pre-aggregated, queries to return the summaries it contains can be run quickly.

    Different types of users might perform analytical work at different stages of the overall architecture.
    For example:

    - Data scientists might work directly with data files in a data lake to explore and model data.
    - Data analysts might query tables directly in the data warehouse to produce complex reports and visualizations.
    - Business users might consume pre-aggregated data in an analytical model in the form of reports or dashboards.

# Online transaction processing (OLTP)

The management of transactional data by using computer systems is reffered to as online transaction processing (OLTP).
OLTP systems record business interactions as they occur in the day-to-day operation of the organization, and support querying of this data to make inferences.

## Transactional Data

Transactional data is information that tracks the interactions related to an organization's activities.
These interactions are typically business transactions, such as payment recieved from customers, payments made to suppliers, products moving through inventory, orders taken, or services delivered.
Transactional events, which represent the transactions themselves, typically contain a time dimension, some numeric values, and references to other data.

Transactions typically need to be *atomic* and *consistent*.
Atomicity means that an entire transaction always succeeds or fails as one unit of work, and is never left in a half-completed state.
If a transaction can't be completed, the database system must roll back any steps that were already done as part of that transaction.
In a traditional relational database management system (RDBMS), this rollback happens automatically when a transaction can't complete.
Consistency means that transactions always leave the data in a valid state.
These transactions are informal descriptions of atomicity and consistency.
There are more formal definitions of these properties, such as atomic, consistent, isolated, and durable (ACID).

Transactional databases can support strong consistency for transactions by using various locking strategies, such as pessimistic locking.
These strategies help ensure that all data remains consistent within the context of the workload, for all users and processes.

The most common deployment architecture that uses transactional data is the data store tier in a three-tier architecture.
A three-tier architecture typically consists of a presentation tier, business logic tier, and data store tier.
A related deployment architecture is the N-tier architecture, which can have multiple middle-tiers handling business logic.

Typical traits of transactional data

Requirement | Description
|---|---|
Normalization | Highly normalized
Schema | Schema on write, enforced
Consistency | Strong consistency, ACID guarentees
Integrity | High integrity
Uses transactions | Yes
Locking strategy | Pessimistic or optimistic
Updateable | Yes
Appendable | Yes
Workload | Heavy writes, moderate reads
Indexing | Primary and secondary indexes
Datum size | Small to medium sized
Query flexibility | Highly flexible
Scale | Small (MBs) to large (a few TBs)

### When to use the solution

Choose OLTP when you need to efficently process and store business transactions and immediately make them available to client applications in a consistent way.
Use this architecture when any tangible delay in processing has a negative effect on the day-to-day operations of the business.

OLTP systems are designed to efficently process and store transactions, and query transactional data.
The goal of efficently processing and storing individual transactions by an OLTP system is partly accomplished through data normalization, which breaks up the data into smaller, less redundant chunks.
This step enables the OLTP system to process large numbers of transactions independently.
It also avoids extra processes required to maintain data integrity in the presence of redundant data.

#### Challenges

An OLTP system can create a few challenges:

- When you run analytics against the data that rely on aggregate calculations over millions of individual transactions, it's very resource-intensive for an OLTP system. 
They can be slow to run and cause a slow-down by blocking other transactions in a database.
As a result, OLTP systems aren't always ideal for handling aggregates over large amounts of distributed data.
But there are exceptions, such as a well-planned schema.

- When you conduct analytics and reporing on data that's highly normalized, the queries tend to be complex, because most queries need to denormalized the data by using joins.
The increased normalization can make it difficult for business users to query without the help of a database administrator (DBA) or data developer.

- When you store the history of transactions indefinatley or store too much data in any one tablem it can lead to slow query performance, depending on the number of transactions that you store.
The common solution is to maintain a relevant window of time (such as the current fiscal year) in the OLTP system and offload historical data to other systems, such as a data mart or data warehouse.

### OLTP in Azure

Applications such as websites hosted in App Service Web Apps, REST APIs running in App Service, and mobile or desktop applications typically communicate with the OLTP system by way of a REST API intermediary.

In practice, most workloads aren't enirely OLTP. They often include an analytical component as well and require real-time reporting, such as running reports against the operational system.
This workload is reffered to as hybrid transactional and analytical processing (HTAP).

In Azure, the following data stores meet the core requirements for OLTP and the management of transaction data:

- Azure SQL Database
- Azure SQL Managed Instance
- SQL Server on Azure VM
- Azure Database for MySQL
- Azure Database for PostgreSQL
- Azure Cosmos DB

### Key selection criteria 

To narrow the choices, start by answering the following questions:

- Do you want a managed service rather than managing your own servers?
- Does your solution have specific dependencies for Microsoft SQL Server, MySQL, or PostgreSQL compatibility? Your application might limit the data stores you can choose based on the drivers it supports for communicating with the data store, or the assumptions it makes about which database is used.
- Are your write throughput requirements high? If yes, choose an option that provides in-memory tables or global distribution capabilities like Azure Cosmos DB.
- Is your solution multitenant? 
If so, consider options that support capacity pools.
Multiple database instances draw from a elastic pool of resources, instead of fixed resources per database.
Elastic Pools can help you better distribute capacity across all database instances and make your solutions more cost effective.
Azure Cosmos DB offers multiple isolation models for multitenant scenarios.
- Does your data need to be readable with low latency in multiple regions? If yes, choose an option that supports readable secondary replicas or global distribution.
- Does your database need to be highly available across geo-graphic regions? If yes, choose an option that supports geographic replication.
Also consider the options that support automatic failover from the primary replica to a secondary replica.
- Does your workload require guarenteed ACID transactions? If you work with nonrelational data, consider Azure Cosmos DB, which provides ACID guarentees through transactional batch operations within a logical partition.
- Does your database have specific security needs? If yes, examine the options that provide capabilities like row-level security, data masking, and transparent data encryption.
- Does your solution require distributed transactions? If yes, consider elastic transactions within Azure SQL Database and SQL Managed Instance.
SQL Managed Instance also supports traditional calls through the Microsoft Distributed Transaction Coordinator (MSDTC).

# SQL Advanced Threat Protection

Advanced Threat Protection for Azure SQL Database, Azure SQL Managed Instance, Azure Synapse Analytics, SQL Server on Azure VMs, and SQL Server enabled by Azure Arc detects anomalous activities that indicate unusual and potentially harmful attempts to access or exploit databases.

Advanced Threat Protection is part of the Microsoft Defender for SQL offering, which is a unified package for advanced SQL security capabilities.
You can access and manage Advanced Threat Protections through the central Microsoft Defender fo SQL portal.

## Overview

Advanced Threat Protection provides a new layer of security.
It enables you to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.
You recieve an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access and query patterns.
Advanced Threat Protection integrates alerts with Microsoft Defender for Cloud, which include details of suspicious activity and recommend action on how to investigate and mitigate the threat.
Advanced Threat Protection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.

For a full investigation experience, enabling auditing, which writes database events to an audit log in your Azure storage account.

### Alerts

Advanced Threat Protection detects anomalous activities that indicate unusual and potentially harmful attempts to access to exploit databases.

#### Explore detection of a suspicious event

You recieve an email notification when the system detects anomalous database activities.
The email provides information on the suspicious securty event, including the nature of the anomalous activities, database name, server name, application name, and the event time.
In addition, the email provides information on possible causes and recommended actions to invesigate and mitigate the potential threat to the database.

