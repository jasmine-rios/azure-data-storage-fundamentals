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

1. Select the **view recent SQL alerts** link in the email to launch the Azure portal and show the Microsoft Defender for Cloud alerts page.
This page provides an overview of active threats detected on the database.

2. Select a specific alert to get additional details and actions for investigating this threat and remediating future threats.

For example, SQL injection is one of the most common Web applicaiton security issues on the Internet that bad actors use to attack data-driven applications.
They take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.
For SQL injection alerts, the alert's details include the vulnerable SQL statement that was exploited.

#### Explore alerts in the Azure Portal

Advanced Threat Protection integrate its alerts with Microsoft Defender for cloud.
Live SQL Advanced Threat Protection tiles within the database and SQL Microsoft defender for cloud blades in the Azure portal track the status of active threats.

Select **Advanced Threat Protection alert** to launch the Microsoft Defender for Cloud alerts page and get an overview of active SQL threats detected on the database.

# Explore file Storage

The ability to store data in files is a core element of any computing system.
Files can be stored in local file systems on the hard disk of your personal computer, and on removable media such as USB drives; but in most organizations, important data files are stored centrally in some kind of shared file storage system.
Increasingly, that central storage location is hosted in the cloud, enabling cost-effective, secure, and reliable storage for large volumes of data.

The specific file format used to store data depend on a number of factos, including:

- The type of data being stored (structured, semi-structured, or unstructured).
- The applicaitons and service that will need to read, write, and process the data.
- The need for the data files to be readable by humans, or optimized for efficent storage and processing.

Some common file formats are discussed below

## Delimited text files

Data is often stored in plain text format with specific field delimiters and row terminators.
The most common format for delimited data is comma-seperated values (CSV) in which fields are seperated by commas, and rows are terminated by a carriage return / new line.
Optionally, the first line may include the field names.
Other common formats include tab-separated values (TSV) and space-delimited (in which tabs or spaces are used to seperate fields), and fixed-width data in which each field is allocated a fixed number of characters.
Delimited text is a good choice for structured data that needs to be accessed by a wide range of applications and services in a human-readable format.

The following example shows customer data in comma-delimited format:

```bash
FirstName, LastName, Email
Joe, Jones, joe@litware.com
Samir, Nadoy, samir@northwind.com

```

## JavaScript Object Notation (JSON)

JSON is a ubiquitious format in which a hieracrchical document schema is used to define data entities (objects) that have multiple attributes.
Each attribute might be an object (or a collection of Objects); making JSON a flexible format that's good for both structured and semi-structured data.

The following example shows a JSON document containing a collection of customers.
Each customer has three attributes (firstName, lastName, and contact) and the *contact* attribute contains a collection of objects that represent one or more contact methods (email or phone).
Note that objects are enclosed in braces ({..}) and collections are enclosed in square brackets ([..]).
Attributes are represented by *name: value pairs* and seperated by commas (,).

```JSON
{
  "customers":
  [
    {
      "firstName": "Joe",
      "lastName": "Jones",
      "contact":
      [
        {
          "type": "home",
          "number": "555 123-1234"
        },
        {
          "type": "email",
          "address": "joe@litware.com"
        }
      ]
    },
    {
      "firstName": "Samir",
      "lastName": "Nadoy",
      "contact":
      [
        {
          "type": "email",
          "address": "samir@northwind.com"
        }
      ]
    }
  ]
}

```
## Extensible Markup Language (XML)

XML is a human-readable data format that was populat in the 1990s and 2000s. It's largely been superseded by the less verbose JSON format, but there are still some systems that use XML to represent data.
XML uses *tags* enclosed in angle-brackets (<../>) to define *elements* and *attributes* as shown in this example.

```XML
<Customers>
  <Customer name="Joe" lastName="Jones">
    <ContactDetails>
      <Contact type="home" number="555 123-1234"/>
      <Contact type="email" address="joe@litware.com"/>
    </ContactDetails>
  </Customer>
  <Customer name="Samir" lastName="Nadoy">
    <ContactDetails>
      <Contact type="email" address="samir@northwind.com"/>
    </ContactDetails>
  </Customer>
</Customers>

```

## Binary Larger Object (BLOB)

Ultimately, all files are stored as binary data (1's and 0's), but in the human-readable formats discussed above, the bytes of binary data are mapped to printable characters (typically through a character encoding schme such as ASCII or Unicode).
Some file formats however, particularly for unstructured data, store the data as raw binary that must be interpreted by applications and rendered.
Common types of data stored as binary, include images, video, audio, and application-specific documents.

When working with data like this, data professionals often refer to the data files as BLOBs (Binary Large Objects).

## Optimized file formats

While human-readable formats for structured and semi-structured data can be useful, they're typically not optimized for storage space or processing.
Over time, some specialized file formats that enalbe compression, indexing, and efficent storage and processing have been developed.

Some common optimized file formats file formats you might see include Avro, ORC, and Parquet:

- Avro is a row-based format.
It was created by apache.
Each file contains a header that describes the structure of the data in the file.
This header is stored as JSON.
The data is stored as binary information in one or more blocks of records.
An application uses the information in the header to parse the binary data and extact the fields it contains.
Avro is a good format for compressing data and minimixing storage and network bandwidth requirements.

- ORC (Optimized Row Columar format) organizes data into columns rather than rows. 
It is an Apache project, originally devloped as a Hadoop-native format for optimizing read and write operations in Apache Hive (Hive is a data warehouse system that supports fast data summarization and querying over large datasets).
An ORC files contains *stripes* of data.
Each stripe holds the data for a column or set of columns.
A stripe contains an index into the rows in the stripe, the data for each row, and a footer that holders statistical information (Count, sum, max, min, and so on) for each column.

- Parquet is another columnar data format.
It is an Apache Project. A Parquet file contains row groups.
Data for each column is stored together in the same row group.
Each row group contains one or more chunks of data.
A Parquet file includes metadata that descrives the set of rows found in each chunk.
An application can use this metadata to quickly located the correct chunk for a given set of rows, and retrieve the data in the specified columns for these rows.
Parquet specialized in storing and processing nested data types efficently.
It supports very efficent compression and encoding schemes.

# Explore databases

A database is used to define a central system in which data can be stored and queried.
In a simplistic sense, the file system on which files are stored is a kind of databasel but when we use the term in a professional data context, we usually mean a dedicated sysem of managing data records rather than files.

## Relational Databases

Relational databases are commonly used to store and query structured data.
The data is stored in tables that represent entities, such as customers, products, or sales orders.
Each instance of an entity is assigned a primary key that uniquely identifies it; and these keys are used to reference the entity instance in other tables.
For example, a customer's primary key can br referenced in a sales order record to indicate which customer placed the order.
The use of keys to reference data entities enables a relational database to be normalized; which in part means the elimination of duplicate data values so that, for exmaple, the details of an individual customer are stored only once, not for eaach sales order the customer places.
The tables are managed and queried using Structured Query Language (SQL), which is based on an ANSI standard, so it's similar across multiple database systems.

### Non-relational databases

Non-relational databases are data management systems that don't apply a relational schema to the data.
Non-relational databases are often referred to as a NoSQL database, even though some support a variant of the SQL language.

There are four common types of non-relational databases commonly in use.

- Key-value databases in which each record consists of a unique key and an associated value, which can be in any format.

- Document databases, which are specific form of key-value database in which the value is a JSON document (which the system is optimized to parse and query)

- Column family databases, which store tabular data comprising rows and columns, but you can divide the columns into groups known as column-families.
Each column family holds a set of columns that are logically related together.

- Graph databases which stores entities as nodes with links to define relationships between them.

# Explore analytical data stores

There are two common types of analytical data store.

## Data Warehouses

A data warehouse is a relational database in which the data is stored in a schema that is optimized for data analytics rather than transactional workloads.
Commonly, the data from a transactional store is transformed into a schema in which numeric values are stored in central fact tables, which are related to one or more dimension tables that represent entities by which the data can aggregated.
For example a fact table might contian sales order data, which can be aggregated by customer, product, store, and time dimensions (enalbing you, for example, to easily find monthly total sales revenue by product for each store).
This kind of fact and dimension table schema is called a star schema; though it's often extended into snowflake schema by adding additional tables related to the dimension tables to represent dimensional hierachies (for example, product might be related to product categories).
A data warehouse is a great choice when you have transactional data that can be organized into a structured schema of tables, and you want to use SQL to query them.

## Data Lakes

A data lake is a file store, usually on a distributed file system for high performance data access.
Technologies like spark or Hadoop are often used to process queries on the stored files and return data for reporting and analytics.
These systems often apply a schema-on-read approach to define tabular schemas on semi-structured data files at the point where the data is read for analysis, without applying constraints when it's stored.
Data lakes are great for supporting a mix of structured, semi-structured, and even unstructured data that you want to analyze without the need for schema enforcement when the data is written to the store.

## Hybrid Approaches

You can use a hybrid approach that combines features of data lakes and data warehouses in a data lakehouse.
The raw data is sotred in a data lake, and Microsoft Fabric SQL analytics endpoints expose them as tables, which can be queried using SQL.
When you create a Lakehouse with Microsoft Fabric, a SQL analytics endpoint is automatically created.
Data lakehouses are a relatively new approach in Spark-based systems, and are enabled through technologies like Delta Lake; which adds relational storage capabilities to Spark, so you can define tables that enforce schemas and transactional consistency, support batch-loaded and streaming data sources, and provide a SQL API for querying.

## Azure Services for Analytical Stores

On Azure, there are several services that you can use to implement a large-scale analytical store including:

Microsoft Fabric is a unified, end-to-end solution for large scale data analytics.
It brings together multiple technologies and capabilities, enabling you to combine the data integrity and reliability of a scalable, high-performance SQL server based relational data warehouse with the flexibility of a data lake and open-source Apache Spark.
It also includes native support for log and telemetry analytics with Microsoft Fabric Real-Time Intelligence, as well as built in data pipelines for data ingestion and transformation.
Each Microsoft Fabric product experience has its own home, for example the Data Factory Home.
Each Fabric Home displays the items that you create and have permision to use from all the workspace that you access.
Microsoft Fabric is a great choice when you want to create a single, unified analytics solution.

Azure Databricks is an Azure implementation of the popular Databricks platform.
Databricks is a comprehensive data analytics solution built on Apache Spark, and offers native SQL capabilities as well as workload-optimized Spark clusters for data analytics and data science.
Databricks provides an interactive user interface through which the system can be managed and data can be explored in interactive notebooks.
Due to common use on multiple cloud platforms, you might want to consider using Azure Databricks as your analytical store if you want to use existing expertise with the platform or if you need to operate in a multicloud environment or support a cloud-portable solution.

**Note**

Each of these services can be thought of as an analytical data store, in the sense that they provide a schema and interface through which the data can be queried.
In many cases however, the data is actually stored in a data lake and the service is used to process the data and run queries.
Some soltuions might even combine the use of these services.
An extract, load, and tranform (ELT) ingestion process might copy data into the data lake, and then use one of these services to transform the data, and  another to query it.
For example, a pipeline might use a notebook running in Azure Databricks to process a large volume of data in the data lake, and then load it into tables in a Microsoft Fabric Warehouse.

# Databricks - Understand Key Concepts

Azure Databricks is a single service platform with multiple technologies that enable working with data at scale.
When using Azure Databricks, there are some key concepts to understand.

## Workspaces

A workspace in Azure Databricks is a secure, collaborative environment where you can access and organize all Databricks assets, such as notebooks, clusters, jobs, libraries, dashboards, and experiments.

You can open an Azure Databricks Workspace from the Azure portal, by selecting **Launch Workspace**.

It provides a web-based user interface (UI) as well as REST APIs for managing resources and workflows.
Workspaces can be structured into folders to organize projects, data pipelines, or team assets, and permissions can be applied at different levels to control access.
They support collaboration by allowing multiple users--such as data engineers, analysts, and data scientists--to work together on shared notebooks, track experiments, and manage dependencies.

In addition, workspaces are tied to Unity Catalog (when enalbed) for centralized data governance, ensuring secure access to data across the organization.
Each workspace is also linked to underlying Azure resource group (including a managed resource group) that holds the compute, networking, and storage resources Databricks uses behind the scenes.

## Notebooks

Databricks notebooks are interactive, web-based documents that combine runnable code, visualizations, and narrative text in a single environment.
They support multiple languages--such as Python, R, Scala, and SQL--and allow users to switch between languages within the same notebook using magic commands.
This flexibility makes notebooks well-suited for exploratory data analysis, data visualization, machine learning experiments, and building complex data pipelines.

Notebooks are also designed for collaboration: multiple users can edit and run cells simultaneously, add comments, and share insights in real time.
They integrate tightly with Databricks clusters, enabling users to process large datasets efficently, and can connect to external data sources through Unity Catalog for governed data access.
In adddition, notebooks can be version-controlled, scheduled as jobs, or exported for sharing outside the platform, making them central to both ad-hoc exploration and production-grade workflows.

Notebooks contain a collection of two types of cells: code cells and Markdown cells.
Code cells contain runnable code.
Markdown cells contain Markdown code that renders as text and graphics.
You can run a single cell, a group of cells, or the whole notebook.

Azure databricks leverages a two-layer architecture:

- Control plane: This intenal layer, Managed by Microsoft handles backend services specific to your Azure Databricks account.

- Compute Plane: This is the external layer tha processes the data and lives in your Azure Subscription.

Clusters are the core computational engines in Azure Databricks.
They provide the processing power required to run data engineering, data science, and analytics tasks.
Each cluster consists of a driver node, which cooredinates execution,and one of more worker nodes, which handle the distributed computations.
Clusters can be created manually with fixed resources or set to auto-scale, allowing Databricks to add or remove worker nodes depednding on workload demand.
This flexibility ensures efficent resouce use and cost control.

Azure Databricks Compute offers a broad set of compute options available for different workload types:

- Severless compute: Fully managed, on-demand compute that automatically scales up or down to meet workload needs. Ideal for teams that want fast startup times, minimal management overhead, and elastic scaling.

- Classic Compute: User-provioned and configured clusters that offer full control over compute settings, such as VM size, libraries, and runtime versions.
Best for specialized workloads that require customization or consistent performance.

- SQL warehouses: Compute resources optimized for SQL-based analytics and BI queries.
SQL warehouses can be provisioned as either severless (elastic, managed) or classic (user-configured) depending on governance and performance requirements.

This allows you to tailor compute to specific needs--from exploratory analysis in notebooks, to large-scale ETL pipelines, to high-performance dashboards and reporting.

## Databricks Runtime

The Databricks Runtime is a set of customized builds of Apache Spark that include performance improvements and additional libraries.
These runtimes make it easier to handle tasks such as machine learning, graph processing, and genomics, while still supporting general data processing and analytics.

Databricks provides multiple runtime versions, including long-term support (LTS) releases.
Each release specifies the underlying Apache Spark version, its release date, and when support will end.
Over time, older runtime versions follow a lifecycle:

- Legacy - available but no longer recommended
- Deprecated - marked for removal in a future release
- End of Support (EoS) - no further patches or fixes are provided
- End of Life (EoL) - retired and no longer available.

If a maintenance update is released for a runtime version you're using, you can apply it by restarting your cluster

## Lakeflow Jobs

Lakeflow Jobs provide workflow automation and orchestration in Azure Databricks, making it possible to reliably schedule, coordinate, and run data processing tasks.
Instead of running code manually, you can use jobs to automate repetitive or production-grade workloads such as ETL pipelines, machine learning training, or dashboard refreshes.

A job in Databricks is essentially a container for one or more tasks.
Tasks define the work to be done--for example, running a notebook, executing a Spark job, calling external code,..

Jobs can be triggered in different ways:

- On a schedule (for example, every night at midnight)
- In response to an event
- Manually, when needed

Because they're repeatable and managed jobs are critical for production workloads.
They ensure that data pipelines run consistently, ML models are trained and deployed in a controlled manner, and downstream systems recieve updates, accurate data.

## Delta Lake

Delta Lake is an open-source storage framework that improces the reliability and scalability of data lakes by adding transactional features on top of cloud object storage, such as Azure Data Lake Storage.
Traditional data lakes can suffer from issues like data, partial writes, or difficulties managing concurrent access.
Delta Lake addresses these problems by supporting: 

- ACID transactions (atomicity, consistency, isolation, durability) for reliable reads and writes.
- Scalable metadata handling so tables can grow to billons of files without performance loss.
- Data versioning and rollback, enabling time travel queries and recovery of previous states.
- Unified batch and streaming processing, so the same table can handle real-time ingestion and historical batch loads.

On top of this foundation, Delta tables provide a familar table abstration that makes it easier to work with structured data using SQL queries or the DataFrame API.
Delta tables are the default table format in Azure Databricks, ensuring that new data is stored with transactional guarentees by default.

## Databricks SQL

Databricks SQL brings data warhousing capabilities to the Databricks Lakehouse, allowing analysts and business users to query and visualize data stored in open formats directly in the data lake.
It supports ANSI SQL, so anyone familiar with SQL can run queries, build reports, and create dashboards without needing to learn new languages or tools.

Databricks SQL is available only in the Premium tier of Azure Databricks. 
It includes:

- A SQL editor for writting and running queries.
- Dashboards and visualization tools for sharing insights
- Integration with external BI and analytics tools

## SQL Warehouses

All Databricks SQL queries run on SQL warehouses (fomerly called SQL endpoints), which are scalable compute resource decoupled from storage.
Different warehouse types are available depending on performance, cost, and management needs.

- Serverless SQL Warehouses
    - Instant and elastic compute with faster startup and autoscaling.
    - Low management overhead since Databricks handles capacity, patching, and optimization.
    - Cost efficency by scaling automatically and avoiding idle resource costs.

- Pro SQL Warehouses
    - Supports Photon and Predictive IO, but not intelligent Workload Management.
    - Use when serverless is unavailable, or when custom networking is required (for example, federation or hybrid/on-premises connections).

- Classic SQL Warehouses
    - Compute resources in your own Azure subscription, not in Databricks.
    - Takes approximately 4 minutes to start and scales with less responsiveness than serverless.
    - Supports only Photon; no Predictive IO or intelligent workload management
    - Use only for basic interactive exploration when severless or pro aren't options.

## MLflow

MLflow is an open-source platform designed to manage the end-to-end machine learning (ML) lifecycle.
It helps data scientists and ML engineers track experiments, manage models, and streamline the process of moving models from development to production.
MLflow also supports generative AI workflows and includes tools for evaluating and improving AI agents.\

# Explore Apache Spark Structured Streaming

Apache Spark is a distributed processing framework for large scale data analytics.
You can use Spark on Microsoft Azure in the following services:

- Microsoft Fabric
- Azure Databricks

Spark can be used to run code (usually written in Python, Scala, or Java) in parallel across multiple cluster nodes, enabling it to process very large volumes of data efficiently.
Spark can be used for both batch processing and stream processing.

## Spark Structured Streaming

To process streaming data on Spark, you can use the Spark Structured Streaming library, which provides an application programming interface (API) for ingesting, processing, and outputting results from perpetual streams of data.

Spark Structured Streaming is built on a ubiquitous structure called a dataframe, which encapsulates a table of data.
You use the Spark Structured Streaming API to read data from a real-time data source, such as a Kafta hub, a file store, or a network port, into a "boundless" dataframe that is continually populated with new data from the stream.
You then define a query on the dataframe that selects, projects, or aggregates the data--often in temporal windows.
The results of the query generate another dataframe, which can be persisted for analysis or further processing.

Spark Structured Streaming is a great choice for real-time analytics when you need to incorporate streaming data into a Spark based data lake or analytical data store.

## Delta Lake

Delta Lake is an open-source storage layer that adds support for transactional consistency, schema enforcement, and other common data warehousing features to data lake storage.
It also unifies storage for streaming and bath data, and can be used in Spark to define relational tables for both batch and stream processing.
When used for stream processing, a Delta Lake table can be used as a streaming source for queries against real-time data, or as a sink to which a stream of data is written.

The spark runtimes in Microsoft Fabric and Azure Databricks include support for Delta Lake.

Delta Lake combined with Spark Structured Streaming is a good solution when you need to abstract batch and stream processed data in a data lake behind a relational schema for SQL-based querying and analysis.