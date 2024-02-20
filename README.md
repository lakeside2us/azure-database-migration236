# azure-database-migration236

## Table of Contents

- [azure-database-migration236](#azure-database-migration236)
  - [Table of Contents](#table-of-contents)
    - [Project Title](#project-title)
    - [Project Description](#project-description)
    - [Setting up Production Environment](#setting-up-production-environment)
    - [Migrating to Azure SQL Database](#migrating-to-azure-sql-database)
    - [Data Backup and Restore](#data-backup-and-restore)
    - [License Information](#license-information)
    - [Author](#author)
    - [Acknowledgments](#acknowledgments)


### Project Title

Azure Database Migration

### Project Description

<p style='text-align: justify;'>The aim of this is to architect and implement a Cloud-Based Database system on Microsoft Azure. In the project, an On-Premise Database will be transitioned to the Azure SQL Database.<p>

<p style='text-align: justify;'>A Windows VM will be provisioned on Azure to serve as the production environment. This VM will host the On-Premise Database which will later be migrated to the Azure SQL Database.

<p style='text-align: justify;'>A backup of the On-Premise Database will be created and the backup will be securely stored on Azure Blob Storage.<p>

<p style='text-align: justify;'>Another Windows VM will be provisioned on Azure and this will serves as the development environment (testing). The reason for this VM is to have a separate environment where we can stimulate disaster recovery scenarios without impacting our live data in production environment.<p>

<p style='text-align: justify;'>SQL Server Management Studio will be utilized to create an automated backup solution of the development environment and the backup will be uploaded to the Blob Storage.<p>

<p style='text-align: justify;'>To enhance data protection, a Geo-replication will be configured for the production database by establishing a synchronized copy of the production database to the Azure SQL Database in a secondary region. This is a strategic redundancy which will ensure a continuos data availability and reduces any potential downtime during any unforeseen disruptions.<p>

<p style='text-align: justify;'>FInally, a disaster recovery will be simulated by intentionally mimicking data loss in the production environment.<p>

### Setting up Production Environment

<p style='text-align: justify;'>The first requirement of this project is the have an Azure account because this project will utilize different services running on Azure.<p>

<p style='text-align: justify;'>A production environment will be setup by provisioning a Windows VM on Azure. After provisioning the Production VM, Remote Desktop Service (RDS) access to the Production VM will be configured.<p>

<p style='text-align: justify;'>Using Remote Desktop Protocol (RDP) and Microsoft Remote Desktop, a remote connection will be established to the production VM and the following actions will be performed on the VM:<p>

- **Download and install SQL Server**
   <br>
    >*SQL Server* is a robust and widely used Relational Database Management System (RDMS) and it will be used together with SQL Server Management Studio (SSMS) to manage the database in this project. [Click here](https://www.microsoft.com/en-gb/sql-server/sql-server-downloads) to download SQL Server for Windows.<p>
  
- **Download and install SQL Server ManagementStudio (SSMS)**
  <br>
     >*SQL Server Management Studio (SSMS)* is a powerful graphical user interface (GUI) tool provided by Microsoft for managing SQL Server instances and databases. It serves as a central hub for database administrators and developers to perform various tasks related to SQL Server.  
    <br />After a successful SQL Server installation, SSMS will be available to install.Alternatively, it can be downloaded by [clicking here](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16). 
 
- **Create the Production Database**
   <br>
    >A production Database called *AdventureWorks* will be created by restoring from a the backup file from [this link](https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak). The database is a sample database with various tables, views, stored procedures, and data with a rich and diverse dataset.

### Migrating to Azure SQL Database
<p style='text-align: justify;'>The focus here is to migrate the production database, the on-premise database, to the Azure Cloud Database. In order to achieve this, the following actions will be performed:<p>

- **Create Azure Database**
   <br>
  >This is the Azure Database that will serve as the target for migrating your on-premise database. To create an Azure Database, an Azure SQL Server will need to be created first. This will serves as the logical container for the cloud databases. The SQL Server will have the appropriate firewall rules to allow our specific IP address to access the server.
  <br />After creating the server successfully, the next step is to create the *SQL database*. SQL Database supports two primary authentication methods: *Microsoft Entra ID* authentication and *SQL Server authentication*. For now, we will use the *SQL Server authentication* (SQL Server username and password).

- **Install Azure Data Studio**
   <br>
  >Azure Data Studio is is a lightweight cross-platform data management and development tool with connectivity to popular cloud and on-premises databases.  
  <br>Download Azure Data Studio from [here](https://learn.microsoft.com/en-us/azure-data-studio/download-azure-data-studio?tabs=win-install%2Cwin-user-install%2Credhat-install%2Cwindows-uninstall%2Credhat-uninstall)

- **Connect to Azure Database**
   <br>
  >In the Azure Data Studio, we will connect to both the on-premise that is running on the VM and the Azure cloud databases that we created earlier. This will sever as the starting point for the migration process.

- **Schema Migration**
   <br>
  >The next stage is migrating the schema in the on-premise database to the Azure cloud database. Before we can do this, we need to first download and install the *SQL Server Scheme Compare* extension. This extension is a valuable tool for seamless database migration. It simplifies the comparison and synchronization of database schemas.

- **Data Migration**
   <br>
  >It should be noted data will not be migrated during schema migration, therefore, we need to perform the data migration process. we need to download and install another extension called  *Azure SQL Migration* in Azure Data Studio.

### Data Backup and Restore


### License Information

This project is licensed under the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.en.html).

### Author

***Name: Olawale Olalekan***

### Acknowledgments

AiCore.
