# Azure Data Fundamentals

Extra Study Materials at www.exampro.co/dp-900

## Introduction to the DP-900

The Azure Data Fundamentals Certification is for those seeking a data-related role such as Data Analyst, Data Engineer, or Data Scientist.

The certification will demostrate a person can define and understand: Core data concepts, Hadoop workloads, Apache Spark workloads, MS SQL databases, NoSQL databases, data lakes, data warehouses, ELTs, and BigData Analytics.

This certification is generally referred to by its course code DP-900

The natural path for the Azure Data Engineer or the Azure Data Analyst,

This is an easy course to pass, and great to those new to cloud or data-related technology.

## Core Data-Related Azure Services

- Azure Storage Accounts: An umbrella service for various storage types e.g. Table, Files, Blob

- Azure Blob Storage: Data which is stored as objects instead of files. Object storage is distributed storage (spanning multiple machines) for unstructured data

- Azure Tables: A key/value NoSQL data store intended for simpler projects

- Azure Files: A managed file-shared NFS or SMB

- Azure Storage Explorer: An application used to explore data within Azure Storage Accounts

- Azure Synapse Analytics: Data warehouse and unified analytics platform

- CosmoDB: A fully-managed NoSQL database service. Can host various NoSQL engines e.g. Table, Documents, Key/Value, Graph

- Azure Data Lake Store (Gen2): A centralized data repository for big data blob storage desinged for vast amount of data

- Azure Data Analytics: Big data as a service (BDaS). Write U-SQL to return data from your Azure Data Lake

- Azure Data Box: Import or export TB of data via harddrive you mail into Azure DataCenters

- SQL Server on Azure Virtual Machines: When migrating via a lift-and-shift and you want to bring your existing license and need OS access and control of VM

- SQL Managed Instances: A managed MS SQL server but with broad adaptably when migrating to Azure

- Azure SQL: Fully-managed MS SQL databases

- Azure Databases for <open-source>: Managed relational databases on Azure e.g. MySQL, PSQL, MariaDB

- Azure Cache for Redis: In-memory data-store for returning data extremely vast but is also extremely volatile

- Microsoft Office 365 Sharepoint: A shared file-system for organizations. The company owns all the files and apply fine-grain role-based access-controls.

- Azure Databricks: A third-party provider partnered with Azure specializing in Apache Spark to provide very fast ELT jobs, as well as ML and streaming

- Microsoft Power BI: A business intelligence tool used to create dashboards and interactive reports to empower business decisions

- HDinsights: A full-managed Hadoop system, that can run many open-source Big Data engines for doing data transformations for streaming, ETL/ELT

- Azure Data Studio: An IDE that looks very much like Visual Studio Code but desinged around data related tasts. Cross-platform similar to SSIS but broader data workloads

- Azure Data Factory: A managed ETL/ELT pipeline builder. Easily build transformation pipelines via a web-interface

- SQL Server Integration Services (SSIS): A stand-alone Windows app to prepare data for SQL workloads via transformation pipelines

## Types of Cloud Computing

- SaaS (Software-as-a-service) 
    This is for customers.
    A product that is run and managed by the service provider. Don't worry about how the service is maintained. It just works and remains available.
    Examples are PowerBI and Office 365

- PaaS (Platform-as-a-Service)
    This is for developers
    Focus on the deployment and management of your apps.
    Don't worry about, provisioning, configuring, or understanding the hardware or OS.
    Examples are HDinsights, Managed SQL, Azure SQL, and CosmosDB

- IaaS (Infrastructure-as-a-service)
    This is for admins
    The basic building blocks for cloud IT. Provides access to networking features, computers, and data storage space.
    Don't worry about IT staff, data centers and hardware.

## Azure Data Roles

- Database Administrator: Configures and maintains a database e.g. Azure Data services or SQL server.
    Responsibilities:
    - Database management
    - Manage security, granting user access
    - Backups
    - Monitors Performance
    Common Tools:
    - Azure Data Studio
    - SQL Server Management Studio
    - Azure Portal
    - Azure CLI

- Data Engineer: Design and implement data tasks related to the transfer and storage of big data.
    Responsibilities:
    - Database pipelines and process
    - Data ingestion storage
    - Prepare data for analytics
    - Prepare data for analytical processing
    Common Tools:
    - Azure Synapse Studio
    - SQL
    - Azure CLI

- Data Analyst: Analyzes business data to reveal important information
    Responsibilities:
    - Provides insights into the data
    - Visual reporting
    - Modeling data for analysis
    - Combines data for visualization and analysis
    Common tools:
    - PowerBI Desktop
    - PowerBI Portal
    - PowerBI services
    - PowerBI report builder

## Database Administrator- Common Tools

- Azure Data Studio: Connect to Azure SQL, Azure SQL data warehouse, PostgresSQL and SQL server (big data clusters, on-premises)
    - Various libaries and extensions along with automation tools
    - Graphical interface for managing on-premises and cloud-based data services.
    - Runs on Windows, macOS, Linux
    - Possibly a replacement for SSMS (still lacks some features of SSMS)

- SQL Server Management Studio (SSMS)
    - Automation tooling for running SQL commands or common database operations
