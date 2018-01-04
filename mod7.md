<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 7</h1>
<i>Course notes from Big Data Engineering with Azure</i>

<h2>Contents</h2>

<ul>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/">Overview</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/faq.md">FAQ</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod2.md">Module 2 - Processing Event Streams using Azure Stream Analytics</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod3.md">Module 3 - Performing Custom Processing in Azure Stream Analytics</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod4.md">Module 4 - Managing Big Data in Azure Data Lake Store</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod5.md">Module 5 - Processing Big Data using Azure Data Lake Analytics</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod6.md">Module 6 - Implementing Custom Operations and Monitoring Performance in Azure Data Lake Analytics</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod7.md">Module 7 - Implementing Azure SQL Data Warehouse</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod8.md">Module 8 - Performing Analytics Azure SQL Data Warehouse</a></b></li>
<li><b><a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/mod9.md">Module 9 - Automating Data Flow with Azure Data Factory</a></b></li>
</ul>

<br/>

<hr/>

<h3><strong>Module 7. Implementing Azure SQL Data Warehouse</strong></h3>

A DWU is a datawarehouse unit that can be scaled independently of storage. A DWU is charagable through monitoring CPU, memory and IOPS to SQL Data Warehouse.<br/>
The default size of a SQL Datawarehouse is 10GB.<br/>
You are limited to 1024 connections to the Azure SQL DW at any one time.

<p>
<b>Data Distribution</b>
<ul>
<li>Round Robin relates to distribution of data equally across 60 nodes of a distrubution. Data is spread across multiple servers. Used where there a multiple primary/foreign keys and staging tables. </li>
<li>Hash is where the value of a single column gets hashed to define the distribution number where the entire record will get inserted. Data is all in same place. Best for fact/detail tables if there is a common distribution key which is used in multi-distributed table joins.</li>
<li>Replication is a very good method for bringing smaller datasets that a frequently joined with other datasets over to the same distribution for processing (e.g. small dimension tables)</li>
</ul>
<i>Neither of these are the same as a partition, replicated or temporary tables.</i>
</p>

<p>
<b>Schema's and Database</b>
<ul>
<li>A schema is a collection of database objects. Important to note that <b>cross database joins are not permitted in SQL DW</b></li>
<li>All tables are created with page compression enabled</li>
<li>Large fact tables should spefically be created as distrubuted hash tables, if not specified it will default to round robin</li>
<li>Maximum of 2 billion tables per database</li>
<li>Up to 1024 columns per table</li>
<li>Number of rows limited only by available storage</li>
<li>Maximum bytes per row is 8060</li>
<li>Identity and PK, FK and unique index constraints are not supported</li>
<li>Case insesitive</li>
<li>Physical table structures supported, heap, clustered/non-clustered index, clustered columnstore index and partitions</li>
</ul>
</p>

<p>
<b>Importing data into SQL DW</b><br/>
<ul>
<li>Bulk Copy Program (BCP) - used to import data from binary/text files directly into SQL DW, can also read out of a SQL DW (good for smaller datasets)</b></li>
<li>AzCopy - Copy data from a local folder to blob storage, then using polybase an external table can be used to pick up the data from blob storage and write it into SQL DW (good for datasets under 10TB).</li>
<li>Ship physical disks to Microsoft to load into Azure to be loaded into a virtual drive, a single import or export job can only handle up to 10 physical hard disks.</li>
<li>Polybase/(Create Table As Select)CTAS - Polybase will natively query structured tables within a database, you can then add external tables provided a valid credential, external source and file format are specified. You can then create a table in Azure DW using CTAS from the external table.</li>
<li>Import data using SSIS - ADO or OLE DB directly into the SQL DW table, or and Azure SQL DW Uplaod Task that uploads the files to Azure Blob storage then use polybase as mentioned above to insert into SQL DW.</li>
<li>Azure Data Lake Store - This approach would be identical to the polybase method described above.</li>
<li>Azure Stream Analytics - Simply create a target destination (output) in the Azure Stream Analytics that references the SQL DW table you require your data to be streamed to.</li>
</ul>
</p>