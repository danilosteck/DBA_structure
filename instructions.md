# Braindump: itens relevantes nas atividades de DBA

Referência principal: [Principles of Database Management](https://validglobal-my.sharepoint.com/:u:/g/personal/danilo_steckelberg_ext_valid_com/EW6O_v2q8yBOs6TB0RV4MVYBGhho6QRaY4YxR4AHjVYvhA?e=Zk0qIS "https://validglobal-my.sharepoint.com/:u:/g/personal/danilo_steckelberg_ext_valid_com/EW6O_v2q8yBOs6TB0RV4MVYBGhho6QRaY4YxR4AHjVYvhA?e=Zk0qIS")

Princípio básico: ACID (Atomicidade, Consistência, Isolamento, Durabilidade)

## Overview (não estruturado)

### Data Modeling

-   Modelo conceitual
    
-   Modelo lógico
    
-   Modelos de dados externos (views, subsets)
    

### Regras de integridade

-   Criação de padrões de dados, formato de datas, etc., para garantir que todos os dados são os mesmos.
    

### Independência de dados

**Data independence** means changes in data definitions have minimal to no impact on the applications using the data. These changes may occur in the internal or the conceptual/logical layer.

-   **Physical data independence** implies that neither the applications, views, or logical data model must be changed when changes are made to the data storage specifications in the internal data model.
    
-   **Logical data independence** implies that software applications are minimally affected by changes in the conceptual or logical data model. Consider the example of adding new data items, characteristics, or relationships. The views in the external data model will act as a protective shield and mitigate the effect of these modifications on the applications. To guarantee logical data independence, the DBMS must provide interfaces between the conceptual/logical and external layer.
    

### Mapeamento de redundância de dados:

-   One of the key drawbacks of the file-based approach to data management is undesirable duplication of data, which can easily lead to inconsistent data. In the database approach, redundant data can be successfully managed. Duplication of data can be desirable in distributed environments to improve data retrieval performance by providing local access to data rather than using resource-intensive network connections. The DBMS is now responsible for the management of the redundancy by providing synchronization facilities to safeguard data consistency.
    
-   Princípios básicos: minimizar redundância e garantir integridade onde deve haver redundância.
    

### Controle de simultaneidade

A DBMS has built-in facilities to support concurrent or parallel execution of database programs, which allows for good performance. A key concept is a database transaction that is a sequence of read/write operations, considered to be an atomic unit in the sense that either all operations are executed or none at all (more details on transactions are provided in Chapter 14). Typically, these read/write operations can be executed at the same time by the DBMS. However, this should be carefully supervised to avoid inconsistencies.

### Backup and Recovery

A key advantage of using databases is the availability of backup and recovery facilities. These facilities can be used to deal with the effect of loss of data due to hardware or network errors, or bugs in system or application software. Typically, backup facilities can perform either a full or incremental backup. In the latter case, only the updates since the previous backup will be considered. Recovery facilities allow restoration of data to a previous state after loss or damage.

### Segurança de dados

Data security can be directly enforced by the DBMS. Depending on the business application considered, some users have read access, while others have write access to the data (role-based functionality). This can also be further refined to certain parts of the data. Trends such as e-business, B2B (business-to-business), B2C (business-to-consumer), and CRM stress the importance of data security because they increasingly expose databases to internal and external parties.

### Desempenho de bases

-   Tempo de resposta
    
-   Throughput Rate (processos / tempo)
    
-   Utilização de espaço
    
-   (time to recovery?)
    
-   (time to backup?)
    
-   (downtime?)
    
-   (_The Recovery Point Objective (RPO)_ specifies the degree to which data loss is acceptable after a calamity?)
    

### Tipos de bases de dados baseado em arquiteturas

#### DBMS centralizada

the data are maintained on a centralized host, e.g., a mainframe system. All queries will then have to be processed by this single host.

#### Client-server DBMS

active clients request services from passive servers. A _fat client variant_ stores more processing functionality on the client, whereas a _fat server variant_ puts more on the

#### n-tier DBMS

a straightforward extension of the client–server architecture. A popular example is a client with GUI (graphical user interface) functionality, an application server with the various applications, a database server with the DBMS and database, and a web server for the web-based access. The communication between these various servers is then handled by middleware.

#### Cloud DBMS

the DBMS and database are hosted by a third-party cloud provider. The data can then be distributed across multiple computers in a network.

#### Federated DBMS

a DBMS that provides a uniform interface to multiple underlying data sources such as other DBMSs, file systems, document management systems, etc. By doing so, it hides the underlying storage details (in particular the distribution and possible heterogeneity of data formats and data management functionality) to facilitate data access.

#### In-memory DBMS

stores all data in internal memory instead of slower external storage such as disk-based storage. It is often used for real-time purposes, such as in Telco or defense applications.

## Aspectos organizacionais

### Data Management

**Data management** entails the proper management of data and the corresponding data definitions or metadata. It aims at ensuring that (meta-)data are of good quality and thus a key resource for effective and efficient managerial decision-making.

#### Catalogs and the role of Metadata

The catalog provides an important source of information for end-users, application developers, and the DBMS itself. Remember, the data definitions are generated by the DDL compiler. The DML compiler and query processor use the metadata to solve queries and determine the optimal access path.

#### Metadata Modeling

A metamodel is a data model for metadata. A metamodel determines the type of metadata that can be stored. Just as with raw data, a database design process can be used to design a database storing metadata.

#### Data Quality

**Data quality (DQ)** is often defined as “fitness for use”, which implies the relative nature of the concept. Data of acceptable quality in one decision context may be perceived to be of poor quality in another decision context, even by the same business user. For instance, the extent to which data are required to be complete for accounting tasks may not be required for analytical sales prediction tasks.

##### Dimensions:

![](blob:https://valid-sa.atlassian.net/7bf34984-e7b8-499e-b776-efd66ad8428b#media-blob-url=true&id=e445afec-7f0e-4e59-9af0-33a826274be5&collection=contentId-2925232176&contextId=2925232176&height=269&width=526&alt=)

![](blob:https://valid-sa.atlassian.net/3dc53e09-c191-45f5-887f-f7650e2e52d1#media-blob-url=true&id=8f96d2f6-e3dd-496e-9652-df8a92133dc3&collection=contentId-2925232176&contextId=2925232176&height=170&width=522&alt=)

##### DQ Problems:

-   Multiple data sources: multiple sources with the same data may produce duplicates – a problem of consistency.
    
-   Subjective judgment in data production: data production using human judgment (e.g., opinions) can cause the production of biased information – a problem of objectivity.
    
-   Limited computing resources: lack of sufficient computing resources and/or digitalization may limit the accessibility of relevant data – a problem of accessibility.
    
-   Volume of data: large volumes of stored data make it difficult to access needed information in a reasonable time – a problem of accessibility.
    
-   Changing data needs: data requirements change on an ongoing basis due to new company strategies or the introduction of new technologies – a problem of relevance.
    
-   Different processes using and updating the same data – a problem of consistency.
    

#### Data Governance

Due to the DQ problems we introduced in the previous section, organizations are increasingly implementing company-wide data governance initiatives to measure, monitor, and improve the DQ dimensions that are relevant to them. To manage and safeguard DQ, a data governance culture should be put in place assigning clear roles and responsibilities. **The aim of data governance is to set-up a company-wide controlled and supported approach toward DQ accompanied by DQ management processes.**

### Data Roles in Data Management

#### Information Architect

The information architect (also called information analyst) designs the conceptual data model, preferably in dialogue with the business users. He/she bridges the gap between the business processes and the IT environment and closely collaborates with the database designer, who may assist in choosing the type of conceptual data model (e.g., EER or UML) and the database modeling tool.

#### Database Designer

The **database designer** translates the conceptual data model into a logical and internal data model. He/she also assists the _application developers_ in defining the views of the external data model. To facilitate future maintenance of the database applications, the database designer should define company-wide uniform naming conventions when creating the various data models.

#### Data Owner

Every data field in every database in the organization should be _owned_ by a **data owner**, who has the authority to ultimately decide on the access to, and usage of, the data. The data owner could be the original producer of the data, one of its consumers, or a third party. The data owner should be able to fill in or update its value, which implies the data owner has knowledge of the meaning of the field and has access to the current correct value (e.g., by contacting a customer, by looking into a file, etc.). Data owners can be requested by data stewards (see the next subsection) to check or complete the value of a field, as such correcting a DQ issue.

#### Data Stewards

**Data stewards** are the DQ experts in charge of ensuring the quality of both the actual business data and the corresponding metadata. **They assess DQ by performing extensive and regular data quality checks. These checks involve, among other evaluation steps, the application or calculation of DQ indicators and metrics for the most relevant DQ dimensions.** They are also in charge of taking initiative and further acting upon the results. A first type of action to be taken is the application of _corrective measures_. However, data stewards are not in charge of correcting data themselves, as this is typically the responsibility of the data owner. The second type of action to be taken upon the results of the DQ assessment involves a deeper investigation into the _root causes_ of the DQ issues detected. Understanding these causes may allow designing _preventive measures_ that aim at eradicating DQ problems.

#### Database Administrator

The database administrator (DBA) is responsible for the implementation and monitoring of the database. Example activities include: installing and upgrading the DBMS software; backup and recovery management; performance tuning and monitoring; memory management; replication management; security and authorization. A DBA closely collaborates with network and system managers.

#### Data Scientist

**Data scientist** is a relatively new job profile within the context of data management. He/she analyzes data using state-of-the-art analytical techniques to provide new insights into, for example, customer behavior.

# Conceitos e cases interessantes

## File-based vs. Database

MIT Sloan Review traz um case interessante a favor do uso de database approach. Entretanto, isso não diz respeito a armazenamento de imagens. [MIT Sloan - Lessons from becoming a data-driven organization.pdf](https://validglobal-my.sharepoint.com/:b:/g/personal/danilo_steckelberg_ext_valid_com/EZYAfqkFjxpOn_4K2E7MSLEBTtzN4mrcpTDGNAJ1g4rPoA?e=PJm6UD)

## Arquitetura de 3 camadas

![](blob:https://valid-sa.atlassian.net/dcbd9d65-cdf5-45b3-a844-ced8aef8be3e#media-blob-url=true&id=4caa528f-69e9-489d-a35f-5ca1af8011e7&collection=contentId-2925232176&contextId=2925232176&height=435&width=1080&alt=)

## Processo de design de Databases

![](blob:https://valid-sa.atlassian.net/509be27f-07c8-4f31-8047-edd736b8dd9a#media-blob-url=true&id=9dc2e30d-4e38-427e-a7bb-43c2e104c2d3&collection=contentId-2925232176&contextId=2925232176&height=458&width=1081&alt=)

## Distributed Databases

Referência:

![](blob:https://valid-sa.atlassian.net/296a8345-187f-47e6-8c10-9479277b88bb#media-blob-url=true&id=efa66bde-27d7-4481-b817-7117587c89db&collection=contentId-2925232176&contextId=2925232176&height=470&width=1231&alt=)

![](blob:https://valid-sa.atlassian.net/c3796b55-4635-4e49-9708-555cbca4a388#media-blob-url=true&id=590675f8-6e62-4ca8-be06-e03a5bb2ae97&collection=contentId-2925232176&contextId=2925232176&height=495&width=1249&alt=)

-   Problema de databases distribuídas: CAP Theorem: you can only choose 2 out of 3
    

![](blob:https://valid-sa.atlassian.net/be4976e6-b6f1-4851-9e5c-aa752f2548d0#media-blob-url=true&id=77e0a825-0900-4af4-a5f9-df86e66cb427&collection=contentId-2925232176&contextId=2925232176&height=492&width=1033&alt=)

In distributed databases, you have to choose Partition Tolerant. So, **the only choice is to choose between consistent and available**.

-   Problema de consenso: o teorema dos dois generais mostra que não é possível garantir consistência quando há informações faltantes.
    

## Transaction Management

### Delineating Transactions and the Transaction Lifecycle

A database application may uphold multiple operations, and even multiple ongoing transactions, at the same time. For a database system to be able to assess which operations belong to which transaction, it is necessary to specify the transaction boundaries – to delineate the transaction. This can be done in an implicit or an explicit way.

The program can mark the first operation of a new transaction explicitly by means of a **begin_transaction** instruction. Alternatively, without an explicit notification, the database management system will assume that the first executable SQL statement in a program execution thread denotes the start of a new transaction.1 The transaction’s operations are received by the transaction manager and put into a schedule, along with other ongoing transactions. Once the first operation is executed, the transaction is active.

The end of a transaction is marked explicitly by means of an **end_transaction** instruction. Upon completion of a transaction, it is to be decided whether the changes made by the transaction should be persisted into the database, or should be undone. If the transaction completed successfully, all changes made by the individual operations belonging to that transaction should be made permanent; the transaction is committed.

After the transaction is committed, the changes become visible to other users and cannot be undone (unless, of course, another transaction would induce exactly the opposite changes afterwards). However, if the transaction is aborted, it means that an error or anomaly occurred during the transaction’s execution. This anomaly may have happened at different levels, but, whatever the cause, the transaction did not complete successfully. **It is possible that the transaction, before being aborted, already made some partial changes to the database. In that case, a rollback of the transaction is required**: all changes made by the transaction’s respective operations should be undone in such a way that, after completion of the rollback, it appears as if the faulty transaction never happened.

### DBMS Components Involved in Transaction Management

The main DBMS component responsible for coordinating transaction execution is called the **transaction manager**. Figure 14.1 depicts the functioning of the transaction manager in interaction with the other main components involved in transaction management: the scheduler, the stored data manager, the buffer manager, and the recovery manager.

![](blob:https://valid-sa.atlassian.net/751047b2-dae0-4d01-9438-6f149914a753#media-blob-url=true&id=edb8bdc1-b433-4455-8477-a001a4026b7a&collection=contentId-2925232176&contextId=2925232176&height=705&width=1079&alt=)

### The Logfile

-   side from the functional DBMS components described above, the logfile is a vital element in transaction management and recovery. Although the logfile essentially contains redundant data, this redundancy is of absolute importance if, for whatever reason, data are lost or damaged in the context of transaction execution. Should this occur, the recovery manager will attempt to recover the lost data by means of the registrations on the logfile. For each transaction and each operation, relevant information is registered on the logfile in log records. In this way, the logfile is a sequential file, consisting of log records that contain the following information:
    
-   a unique log sequence number to identify the log record;
    
-   a unique transaction identifier, relating the log registration to an individual transaction;
    
-   a marking to denote the start of a transaction, along with the transaction’s start time and an indication of whether the transaction is read only or read/write;
    
-   identifiers of the database records involved in the transaction, as well as the operation(s) they were subjected to (select, update, insert, delete);
    
-   before images of all records that participated in the transaction; these are the original values, before the records were updated. Before images are used to undo unwanted effects of failed transactions;
    
-   after images of all records that were changed by the transaction; these are the new values, after the update. After images are used to redo changes that were not adequately persisted in the physical database files in the first place;
    
-   the current state of the transaction (active, committed, or aborted).
    

## Recovery

### Types of failures

-   A **transaction failure** results from an error in the logic that drives the transaction’s operations (e.g., wrong input, uninitialized variables, incorrect statements, etc.) and/or in the application logic. As a consequence, the transaction cannot be completed successfully and should be aborted. This decision is typically made by the application or by the database system itself. If any tentative changes were made by the transaction, these should be rolled back.
    
-   A **system failure** occurs if the operating system or the database system crashes due to a bug or a power outage, for example. This may result in loss of the primary storage’s content and, consequently, the database buffer.
    
-   **Media failure** occurs if the secondary storage (hard disk drive or in some cases flash memory) that contains the database files, and possibly the logfile, is damaged or inaccessible due to a disk crash, a malfunction in the storage network, etc. Although the transaction may have been logically executed correctly, and hence the application or user that induced the transaction was informed that the transaction was committed successfully, the physical files may not be able to capture or reflect the updates induced by the transaction.
    

## Data Distribution and Distributed Transaction Management

Ever since the early days of computing, which were dominated by monolithic mainframes, distributed systems have had their place in the ICT landscape. A distributed computing system consists of several processing units or nodes with a certain level of autonomy, which are interconnected by a network and which cooperatively perform complex tasks. These complex tasks can be divided into subtasks as performed by the individual nodes.

The rationale behind distributed architectures and systems is grounded in the principle that the overhead of a monolithic system increases more than proportionally to the number of tasks and users. By dividing and distributing a complex problem into smaller, more manageable units of work, performed by semi-independent nodes, the complexity becomes, at least in theory, more manageable. This makes the system also more scalable; a monolithic system can only be extended within a limited capacity range, whereas (again, in theory) a distributed system’s capacity can be increased indefinitely by just adding nodes to the system.

### Architectural Implications of Distributed Databases

![](blob:https://valid-sa.atlassian.net/a2736bb2-9db6-4925-bb18-e2e3a45f54b2#media-blob-url=true&id=03cd3aeb-2cca-475f-bdd4-c332dc48d44d&collection=contentId-2925232176&contextId=2925232176&height=243&width=1080&alt=)

In a **shared-memory architecture**, multiple interconnected processors that run the DBMS software share the same central storage and secondary storage. As more processors are added, this shared central storage may become the bottleneck.

**shared-disk architecture**, each processor has its own central storage but shares secondary storage with the other processors. The disk sharing can be realized by, for example, a storage area network or network attached storage. Shared-disk architectures are typically more fault tolerant than shared-memory architectures. However, a possible bottleneck is the network that interconnects the disks with the processors.

The most prevalent approach for distributed databases is the **shared-nothing architecture**. In this set-up, each processor has its own central storage and hard disk units. Data sharing occurs through the processors communicating with one another over the network, not by the processors directly accessing one another’s central storage or secondary storage.

### Fragmentation, Allocation, and Replication

If data distribution is a deliberate choice, and not a consequence of an event like a merger or acquisition, one of the main concerns of a distributed database will be the criteria according to which to partition the data into subsets, called **fragments**,

![](blob:https://valid-sa.atlassian.net/bb629e65-673c-4a48-935c-d44f638fcdba#media-blob-url=true&id=b5598cfc-678f-4739-8b8b-df5a0db4070b&collection=contentId-2925232176&contextId=2925232176&height=465&width=1079&alt=)

With **vertical fragmentation**, every fragment consists of a subset of the columns of the global dataset.1 Vertical fragmentation is especially useful if only some of a tuple’s attributes are relevant to a certain node. For example, a node responsible for order processing only needs the CustomerIDs and customer names, whereas a node performing data analytics on the customer data is mainly interested in demographic data such as country, year of birth, and gender. Both fragments contain the necessary columns (most often the primary key) to combine the respective vertical fragments with a JOIN construct if a view of the global dataset is required

According to **horizontal fragmentation**, each fragment consists of rows that satisfy a certain query predicate.2 For example, in Figure 16.4 the rows are attributed to worldwide nodes according to the country of the customer (Country = “Belgium” or “France”; Country = “UK”; Country = “USA” etc.), so customer data for each country can be stored in the local branch. In this way, network traffic for queries on local customers is reduced and local availability is improved if network failure occurs. Note that all data pertaining to the same customer are now stored at the same node. A global view can be reconstructed with a UNION query over all the horizontal fragments.

## Data Warehousing

A **data warehouse** was first formally defined by Bill Inmon in 1996 as follows: A data warehouse is a subject-oriented, integrated, time-variant, and nonvolatile collection of data in support of management’s decision-making process.

**Subject-oriented** implies that the **data are organized around subjects such as customers, products, sales, etc**. By focusing on the subjects rather than on the applications or transactions, **the data warehouse is optimized to facilitate the analysis of the decision-makers by leaving out any data that are not relevant to the decision-making process**.

![](blob:https://valid-sa.atlassian.net/d9beb9a8-bd65-446b-8c23-d77a7d0e5b6c#media-blob-url=true&id=63b5d9a8-883c-4261-a4c4-3401fdff9c7f&collection=contentId-2925232176&contextId=2925232176&height=398&width=1080&alt=)

**Non-volatile** implies that the data are primarily read-only, and will thus not be frequently updated or deleted over time. Hence, the two most important types of data manipulation operations for a data warehouse are data loading and data retrieval. Furthermore, to avoid duplication and inconsistencies, transactional systems always assume that the data are normalized (e.g., totals and other derived data elements will never be stored). This is in contrast to data warehouses, which often store aggregated/non-normalized data to speed up the analyses. Finally, transaction management, concurrency control, deadlock detection, and recovery management are less of a concern for data warehouses since data are mostly retrieved.

**Time variant** refers to the fact that the data warehouse essentially stores a time series of periodic snapshots. Operational data are always up-to-date and represent the most recent state of the data elements, whereas a data warehouse is not necessarily up-to-date but represents the state at some specific moment(s) in time. Data are not updated or deleted as the business state changes, but new data are added, reflecting this new state. In this way, a data warehouse also stores state information about the past, called historical data. Therefore, every piece of data stored in the data warehouse is accompanied by a time identifier. The latter can then be used to do historical trend analysis.

# Papeis DBA em sistemas Cloud

## Tech Target

Ref: [![](https://www.techtarget.com/favicon.ico)Cloud DBA: How Cloud Changes Database Administrator's Role](https://www.techtarget.com/searchdatamanagement/tip/Cloud-DBA-How-cloud-changes-database-administrators-role)

-   **System provisioning.** Initial system design and resource allocation responsibilities are commonly shared with other IT staffers in on-premises environments. But in the cloud, a DBA often assumes full responsibility for working with the vendor to provision the database system and allocate compute, memory and storage resources to workloads.
    
-   **Disaster recovery.** Another shared responsibility on premises, it typically falls on a cloud DBA to ensure that geo-replicated backups and geo-redundant database system clusters are set up and configured as needed. That requires the DBA to learn the chosen DBaaS vendor's disaster recovery architecture.
    
-   **Backup and recovery.** In on-premises systems, a DBA is responsible for [data backup, recovery and retention processes](https://www.techtarget.com/searchdatabackup/Create-your-data-backup-strategy-A-comprehensive-guide "https://www.techtarget.com/searchdatabackup/Create-your-data-backup-strategy-A-comprehensive-guide"). That becomes a shared responsibility with the DBaaS vendor in the cloud. The vendor handles configuration and execution tasks, while the DBA is responsible for adjusting the backup routines and schedule to meet application needs.
    
-   **System patching and maintenance.** The DBaaS vendor defines maintenance windows, although a DBA can adjust dates and times for regular maintenance as needed. For critical security and system availability updates, the vendor often sets strict deadlines that require them to be done by a specific date and then applies the patches itself, instead of the DBA doing that.
    
-   **Capacity planning.** A DBA continues to work with application developers and end users to forecast system usage and resource requirements. But instead of working with the IT team to expand systems when needed, the DBA is responsible for adjusting the cloud service tiers with the DBaaS vendor to accommodate required capacity growth.
    

### How to succeed as Cloud DBA

#### 1. Cost management

First, a topic that continues to generate a lot of discussion and organizational concern: [cloud cost management](https://www.techtarget.com/searchcloudcomputing/feature/5-ways-to-reduce-cloud-costs "https://www.techtarget.com/searchcloudcomputing/feature/5-ways-to-reduce-cloud-costs"). During the genesis of cloud systems, much of the marketing hype focused on using them to reduce IT costs. As organizations began to implement applications in the cloud, though, they quickly realized that while it provided many advantages compared to on-premises systems, cost savings wasn't always one of them.

These are the key ways that cloud systems change the responsibilities of a database administrator.

That makes [evaluating initial and ongoing costs](https://www.techtarget.com/searchcloudcomputing/tip/How-to-calculate-cloud-migration-costs-before-you-move "https://www.techtarget.com/searchcloudcomputing/tip/How-to-calculate-cloud-migration-costs-before-you-move") for both IaaS and DBaaS systems a critical task for a cloud DBA. You don't purchase cloud environments -- you essentially rent them, and the rental fees are based on resource utilization, which can vary dramatically over time, often in unexpected ways.

During the provisioning of a database system, the DBA should use the vendor-provided cost calculator to check what-if scenarios involving different pricing options, regions, instance classes, disk configurations and other parameters. Every time you make a change, the cost calculator will show an estimate of what your monthly cost will be. Testing different configurations will help you to customize your cloud database environment to better meet both your resource needs and budget.

After you implement the database, one of your top priorities is to monitor usage and resource consumption, ideally on a daily basis. If you don't, you may end up with an unwelcome budgetary surprise -- or shock. A very common problem that organizations face is a cloud system exceeding initial cost estimates. This is usually caused by unpredicted workload increases or changes to an application; the resulting increases in resource utilization may force DBAs to adjust the configuration parameters and performance levels selected when a cloud database was first provisioned.

DBAs also need to carefully read their vendor's documentation on resource limits -- and what happens if systems exceed those specifications. Unlike on-premises platforms that can allow an application to continue to run when resources are overutilized, some cloud systems will automatically suspend your workloads. Helpfully, the leading cloud vendors all provide tools to monitor resource utilization. Most also enable DBAs to set up billing alerts that can warn of potential cost problems.

#### 2. Data security

In the cloud, DBAs share the task of [protecting DBaaS environments](https://www.techtarget.com/searchsecurity/tip/Evaluate-cloud-database-security-controls-best-practices "https://www.techtarget.com/searchsecurity/tip/Evaluate-cloud-database-security-controls-best-practices") with their cloud provider. It typically handles data encryption and other basic security functions. But, under the [shared responsibility model](https://www.techtarget.com/searchcloudcomputing/definition/shared-responsibility-model "https://www.techtarget.com/searchcloudcomputing/definition/shared-responsibility-model") for cloud security, the DBA still needs to secure not only access to cloud databases, but also items such as database load files and report files. Although some of these files may be temporary, appropriate controls must be put in place to protect them and audit their usage.

In addition to common database security commands that are supported in both on-premises and DBaaS systems, each cloud vendor provides its own security tools, controls and features that DBAs will need to employ to fully protect database environments. You should dedicate sufficient time to thoroughly understand your chosen vendor's customized set of security mechanisms.

#### 3. Database auditing

Auditing database usage is another important responsibility for cloud DBAs. Much like data security, monitoring [adherence to regulatory compliance frameworks](https://www.techtarget.com/searchcloudcomputing/tip/How-to-approach-cloud-compliance-monitoring "https://www.techtarget.com/searchcloudcomputing/tip/How-to-approach-cloud-compliance-monitoring") such as the Payment Card Industry Data Security Standard, HIPAA and GDPR is a shared responsibility with the cloud database provider. It typically provides both internal and third-party auditor compliance reports and attestations for various frameworks. But that's only a starting point, not an exact control-by-control listing that matches an organization's unique auditing needs.

Most of the top cloud vendors also offer tools to help DBAs configure identity and access management, secure and monitor their data, and implement audit trails for databases that are governed by compliance frameworks. But responsibility for ensuring that the tools are configured and used effectively to help meet compliance objectives lies solely with the DBA.

#### 4. High availability, backup and recovery

DBaaS vendors offer [cloud service-level agreements (SLAs](https://www.techtarget.com/searchstorage/definition/cloud-storage-SLA "https://www.techtarget.com/searchstorage/definition/cloud-storage-SLA")) that guarantee minimum levels of system uptime. One of the key benefits of cloud database platforms is the ease of [deploying a highly available architecture](https://www.techtarget.com/searchcloudcomputing/feature/3-best-practices-to-achieve-high-availability-in-cloud-computing "https://www.techtarget.com/searchcloudcomputing/feature/3-best-practices-to-achieve-high-availability-in-cloud-computing"). The cloud vendor uses data replication to synchronize redundant database environments that are geographically distant from each other, ensuring that an outage in one region won't affect system availability. It then does automatic failovers to the standby database instances when necessary.

But once again, it's up to the database administrator to understand and select the features that are required to provide the desired level of availability. The DBA may also still need to perform some high availability tasks, such as restoring corrupted or development and test databases. In addition, the DBA usually is responsible for monitoring the DBaaS vendor's compliance with its SLA.

Another aspect that a cloud DBA needs to understand is the DBaaS vendor's maintenance windows and the potential impact that maintenance operations can have on system availability. For example, some work done by the vendor may require that the system be taken offline, but the DBA may be able to modify maintenance times and defer outages to avoid application issues.

Similarly, while DBaaS vendors offer automated mechanisms to back up cloud database systems, DBAs often can temporarily disable backup jobs and modify standard data retention periods. In many cases, they're also responsible for initiating database restore requests to the vendor and making sure that restored data is valid.

#### 5. Performance tuning and monitoring

CPU and memory utilization and disk I/O will always be the DBA's favorite performance indicators, regardless of the database product and platform. The cloud introduces new resources that need to be monitored, but leading DBaaS vendors provide advanced monitoring tools to help facilitate the performance tuning process. In fact, DBAs typically will find that cloud database monitoring tool sets eclipse their on-premises counterparts.

In addition, many DBaaS vendors offer automated advisors that generate performance tuning recommendations. DBAs should run them often, analyze the results and implement suitable changes. Overall, the focus for a cloud database administrator shifts more to improving application performance through optimized database queries and updates, while the vendor monitors the database itself.

#### 6. Basic administration tasks

The same basic principles of [good database administration](https://www.techtarget.com/searchdatamanagement/tip/Best-practices-for-cloud-database-management-systems "https://www.techtarget.com/searchdatamanagement/tip/Best-practices-for-cloud-database-management-systems") apply to both cloud and on-premises platforms. But depending on the database environment, DBAs will be using different tools, utilities and commands to do job scheduling, parameter configuration, schema design and other administrative operations in the cloud.

Database administrators also shouldn't expect an exact one-to-one feature match between DBaaS platforms and on-premises databases. Using Microsoft SQL Server as an example, you'll find that [several features](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SQLServer.html#SQLServer.Concepts.General.FeatureNonSupport "https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SQLServer.html#SQLServer.Concepts.General.FeatureNonSupport") in Microsoft's on-premises software either aren't supported or have limited support in the cloud version that AWS offers as part of its Amazon Relational Database Service.

This feature mismatch isn't just an AWS issue, either. There are also some differences between on-premises SQL Server and Azure SQL Database, Microsoft's own cloud database service. Even Azure SQL Managed Instance, a version of the cloud software that Microsoft developed to make it easier to [migrate on-premises databases to the cloud](https://www.techtarget.com/searchcloudcomputing/feature/How-to-carefully-plan-a-database-migration-to-the-cloud "https://www.techtarget.com/searchcloudcomputing/feature/How-to-carefully-plan-a-database-migration-to-the-cloud"), isn't 100% compatible with SQL Server.

The differences on features aren't a weakness of cloud database platforms. DBaaS vendors optimize their database offerings to take advantage of the benefits that the cloud provides, and many of the differences are because the cloud service provides a better alternative. Cloud DBAs just need to be aware of those differences and plan their database administration processes accordingly.

## 4C Group of Companies

Ref: [![](https://www.4cit.group/wp-content/uploads/2022/06/cropped-Mark-32x32.jpg)The evolving role of database administrators in the cloud - 4C](https://www.4cit.group/the-evolving-role-of-database-administrators-in-the-cloud/)

### **ROLE OF DATABASE ADMINISTRATORS IN THE CLOUD**

Based in the cloud, database-as-a-service (DBaaS) has become popular among enterprises looking to take advantage of cloud computing. Automation is a key feature of DBaaS, eliminating much of the manual maintenance that database administrators have to do with on-site systems. Cloud-based databases automatically perform updates, install patches, run backups and recovery. It is no longer necessary for database administrators to do these tasks.

With cloud-based databases, the admins need skills beyond just maintenance. Their role has changed to focus on improving query performance, code review, custom monitoring and security. A skilled administrator will look at how to use the database to meet business objectives.

Working with application teams, they gather and manipulate data to be used on business applications. When changes to applications are made, the database needs to automatically reflect these changes. The administrator can suggest ways to optimise this process, predicting and preventing possible issues.

Security also falls into the portfolio of a database administrator. They need to know which parts of the database contain sensitive or highly confidential data. Similar to on-site database management, the admins implement corporate security policies. These include access control, permissions, privileges and user management.

### **DATABASE ADMINISTRATORS IN HYBRID ENVIRONMENTS**

Hybrid environments that include both on-site and cloud databases are complex to manage. When dealing with these environments, database administrators need to know how to optimise both types of systems. With large enterprises, data comes from multiple sources: from employees, customers, applications and third-party providers.

There needs to be high levels of integration between cloud and on-site databases if these various data sources are to be accurately stored, retrieved and analysed for business purposes. Database administrators need to know how to architect for effective reporting and data analytics. This requires specialisation in the field of data science.

Maintaining a hybrid system requires high levels of expertise. When migrating to the cloud, administrators need to guide a seamless end-to-end transition. When they are familiar with various cloud platforms, they are more flexible in their approach, choosing the most suitable technologies and solutions.

## Database Trends and Applications

Ref: [![](https://www.dbta.com/favicon.ico)The Cloud and Database Administration](https://www.dbta.com/Columns/DBA-Corner/The-Cloud-and-Database-Administration-143426.aspx)

### _What Will Change_

With database-as-a-service (DBaaS), some traditional DBA tasks will be managed by the cloud provider. DBaaS is a cloud computing managed-service offering that provides access to a database without requiring the set-up of physical hardware, the installation of software, or the configuration of the database. With DBaaS, many maintenance and administrative tasks are overseen by the service provider, freeing up users to quickly benefit from using the database.

For example, most DBaaS providers deliver backup services for cloud databases. This means that some of the manual backup procedures heretofore handled by DBAs are controlled by the cloud service provider. Of course, DBAs are still required to know their business recovery time objectives, understand where failures can occur (both on-premise and in the cloud), and ensure that the backup plans are adequate to meet their company’s requirements.

With cloud databases, availability also can become less of a DBA concern because the cloud can replicate databases across multiple geographical locations. Keep in mind, too, that cloud DBaaS providers manage the maintenance, the upgrading, and the application of fix packs to the DBMS, a particularly time-consuming process most DBAs dislike. Nevertheless, DBAs still need to communicate with the DBaaS provider to know when maintenance is being applied and if there could be any impact that would need to be addressed.

Furthermore, the DBA team must comprehend the exact cloud services being provided and verify that they conform to its usage needs. For example, DBAs need to understand issues such as latency problems, size limitations, and any other considerations that change the way that an organization works with the database.

With these differences, the role of the DBA will likely shift from being more implementation-focused to being more strategic when DBaaS is deployed because many of the routine, day-to-day management tasks can be handled by the cloud provider.

### _New Skills Required_

That said, implementing cloud databases will require that new skills be mastered by the DBA team. For example, loading a cloud database can be a challenge because of latency issues. But it is not just in the initial loading that latency can be problematic; any data access over the cloud can be delayed due to latency issues. DBAs need to build such expectations into their service-level agreements—both with the service provider and end users.

And let’s not imagine that moving databases to the cloud will change the DBA’s responsibility for performance management, security, database change management, and many other typical DBA duties.

There are also many new DBA duties that will arise as organizations embrace cloud computing. One such responsibility is acquiring and maintaining deep knowledge of the cloud architecture. This includes knowing what is in the cloud and what is on-premise—not just for data, but for the entire compute stack— as well as how to utilize the components that are in the cloud from an administrative and development perspective.

### _Working in the New Hybrid Environment_

The DBA must also become a vital cog in the budget management process for the cloud database. Just because it is easy to scale up using cloud database services does not mean there is no cost. As a result, the organization needs an expert who understands the impact of additional workloads on the DBaaS contract. Moreover, the DBA must have knowledge of the impact of database and application design and architecture decisions and how they affect costs.

Finally, it is improbable that all of an organization’s databases will move to the cloud. That means DBAs must be able to work in a hybrid environment, maintaining their traditional skill set for on-premise data, while embracing and extending their capabilities to manage the cloud data.

# DBA Teams and Agile

## CCPACE

Ref: [https://www.ccpace.com/asset_files/Role_of_DBA.pdf](https://www.ccpace.com/asset_files/Role_of_DBA.pdf "https://www.ccpace.com/asset_files/Role_of_DBA.pdf")

The role of the App DBA on an Agile project is not that much different from that required by other development methodologies in terms of tasks and responsibilities. What is different is how and when these tasks and responsibilities are applied in the development process. An Agile project is likely to require some or all of the following from an App DBA:

-   Data modeling
    
-   Creating the other database objects, such as tables, and maintaining the database build script
    
-   Developing stored procedures, stored functions, triggers and views
    
-   Writing and tuning queries
    
-   Establishing database development standards for the other developers
    
-   Reviewing database code and queries to make sure standards are met
    
-   Building sandbox, integration and test database environments for developers and testers
    
-   Creating database user accounts and granting appropriate privileges to those accounts
    
-   Supporting the developers and testers and making sure that there are no impediments to the development team from the perspective of the database
    

### How has Agile changed the role of the Application DBA?

-   The App DBA has to be fully integrated into the development team. A core of Agile development is communication, and preferably co- location. No longer can the App DBA do their work from the “DBA Cave”. With a smooth-running Agile team, a development task that involves the database may turn a programming pair into a programming trio. In addition, the App DBA needs to be available to ensure database problems do not stand in the way of progress.
    
-   Data modeling occurs throughout the development process. While data modeling is not necessarily the responsibility of App DBAs in some organizations, the App DBA on an Agile project will be hard- pressed to avoid it. Data models not only change from release- to-release, but from sprint-to-sprint and story-to-story. The App DBA will have to be able to make different structural changes to different developer databases at the same time, and at any time during the development process.
    
-   Additional development and testing databases are required. Automated unit testing and continuous integration, key engineering components of the Agile development process, work best with individual developer/tester databases, or sandboxes. Ironically, multiple sandboxes with a well-written database build script are significantly easier for an App DBA to maintain than is a database shared by developers.
    
-   Database code is application code. Every component of the application’s database – DDL, stored procedures, reference data, etc. should be stored in the same source code repository as the rest of the application code. A stored procedure being checked-in should cause the same continuous integration process to run as would the check-in of any of the application code
