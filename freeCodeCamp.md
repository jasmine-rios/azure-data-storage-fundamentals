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
    - Graphical interface for managing on-premises and cloud-based data services
    - Runs on Windows
    - More mature than Azure Data Studio

- Azure Portal and CLI
    - Manage SQL database configurations e.g. Create, deleting, resizing, number of cores
    - Manage and provision other Azure Data Services
    - Automate the creating, updating, or modifying resources via Azure Resource Manager templates (IaC)

## Data Engineering - Common Tools

- Azure Synapse Studio: Azure portal integrated to manage Azure Synapse, data ingestion (Azure Data factory), management of Azure Synapse assets (SQL Pools/Spark Pool)

- Knowledge SQL: Create database, tables, views, etc.

- Azure CLI: Support operations SQL cmd to connect to Microsoft Server Azure SQL data and run a talk queries and commands

- HDinsights: Streaming data via Apache Kafka or Apache Spark, applying ELT jobs via HIVE, PIG, Apache Spark

- Azure Databricks: Using apache spark to create ELT or streaming jobs to data ware houses or data lakes

## Data Analyst - Common Tools

- Power BI Desktop: A stand alone application for data visualization.
    You can do data modeling
    Connect to many data sources
    Create interactive reports

- Power BI Portal/ Power BI Service: A web UI for creating interactive dashboards

- Power BI Report Builder: Create paginated reports (printable reports)

## Data Overview

Data- Units of information
    Data Documents - Types of abstract groupings of data
        Data Sets - unstructured logical grouping of data
            Data Structures - structured data
                Data Types - How single units of data are intended to be used

Batch and Streaming Data
    How do we move our data around?

Relational and Non Relational
    How to access, query, and search our data?

Data Modeling
    How we prepare and design our data?

Schema and Schemaless
    How do we structure our data for search?

Data Integrity and Data Corruption
    How do we trust our data?

Normalized and Denormalized
    How do we trade quality vs. speed?

## Introduction to Data

What is data?
Data is units of information that could be in the form of numbers, text, or machine code, images, videos, audio, or physical (handwritting)

What are data documents?

A data document defines the collective form in which data exists.
Common types of data documents:

- Datasets - a logical grouping of data
- Databases - Structured data that can be quickly access and searched
- Datastores - Unstructured or semi-structured data to housing data
- Data warehouses - structured or semi-structured data for creating reports and analytics
- Notebooks - Data that is arranged in pages, designed for easy consumption

Examples:

- MNIST dataset - dataset
- Azure SQL - Database
- Azure Data Lake - Datastore
- Azure Synapse Analytics - Data warehouse
- Jupyter Notebook - Digital Notebook

## Data Sets

A data set is a logical grouping of units of data that generally are closely related and/or share the same data structure.

There are publicly available data seys that are used in the learning of statistics, data analytics, machine learning

MNIST database - Images of hand written digits used to test classification, clustering, and image processing algorithm.
Commonly used when learning how to build computer vision ML models to translate handwritting into digital text

## More Data sets

Common Objects in Context (COCO) dataset: A dataset which contains many common images using a JSON file (coco format) that identify objects or segments within an image.

This dataset features:
- Object segementation
- Recognition in Context
- Superpixel stuff segmentation
- 329K images (>200K labeled)
- 0.5 million object instances
- 79 object categories
- 90 stuff categories
- 4 captions per image

IMBD Reviews Dataset: A movie review dataset with 25,000 highly polar movie reviews for training, and 25,000 for testing.
Could be useful for determining customer sentiment analysis

Free Music Archive (FMA)
A dataset for music analysis
- 106,573 tracks
- 163 genres

LibriSpeech
A dataset of 1000 hours of English speech

There are many more datasets online (some could be paid, or you need to extract the data via an API or scrape the data yourself):

## Data Types

What is a data type?

A data type is a single unit of data that tells a complier or interpreter (computer program) how data is intended to be used

The variety of data types will greatly vary based on the computer program

Let's take the most common data types

Numeric Data Types: A data type involving mathematical numbers
    - Integer: A whole number (could be negative or positive) -100, 7, 11, 21903823091
    - Float : A number that has a decimal e.g. 1.5, 0.0, -10.24, 9.432363535345

Text Data Types: A data type that contains readable and non-readable letters
    - Character: A single letter, alphanumeric (A-Z), Digit (0-9), blank space, punction, special characters ($%&*@)
    - String: A sequence of characters e.g. Words, sentences, and paragraphs
    - Composite: A data type that contains cells of data that can be accessed via an index or a key
        - Array: A group of elements that contain the same data type, can be accessed via their index (position)
        - Hash (dictionary): A group of elements where a key can be used retrive a value. Composites can be both data-types and data structures

Binary Data Type: Represented by a bit or a series of bits (a byte), which is either 0 (off) or 1 (on)

Boolean Data Type - A datatype that is either True or False
- Some languages represents a Boolean as
    - a bit as a boolean e.g. 0 (false) or 1 (true)
    - The first letter e.g. t (true) or f (false)

Enummeration (Enum) Data Type - A group of constant (unchangable) variables e.g. DIAMOND, SPADE, HEART, CLUBS
    - Can be a data type and/or a data structure, varies on the language

