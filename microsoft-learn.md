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

    Microsoft Entra supports several different authentication options, including multifactor 