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

A DWU is a datawarehouse unit that can be scaled independently of storage. A DWU is charagable through monitoring CPU, memory and IOPS to SQL Data Warehouse.
The default size of a SQL Datawarehouse is 10GB.

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
<b>Concurrency Limits</b><br>
Concurrent Queries: The way to control performance of a SQL DW is to allocation data warehouse units (DWU). A maximum of 32 concurrent queireis can be executed.<br/>
Concurrency Slots: for every 100 DWU, four concurrency slots are allocated. each query requires a set of concurrency slots to run based on the four resource classes (rc) available, as shown in the table below.<br/>
<font size="1">
<table>
<thead>
<tr>
<th style="text-align:left" align="left">DWU</th>
<th style="text-align:center">Max concurrent queries</th>
<th style="text-align:center">Concurrency slots allocated</th>
<th style="text-align:center">smallrc slots / mem alloc</th>
<th style="text-align:center">mediumrc slots / mem alloc</th>
<th style="text-align:center">largerc slots / mem alloc</th>
<th style="text-align:center">xlargerc slots / mem alloc</th>
<th style="text-align:center">Compute Nodes</th>
<th style="text-align:center">Distributions per Node</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left" align="left">DW100</td>
<td style="text-align:center" align="center">4</td>
<td style="text-align:center" align="center">4</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">2 / 200</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">1</td>
<td style="text-align:center" align="center">60</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW200</td>
<td style="text-align:center" align="center">8</td>
<td style="text-align:center" align="center">8</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">2 / 200</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">2</td>
<td style="text-align:center" align="center">30</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW300</td>
<td style="text-align:center" align="center">12</td>
<td style="text-align:center" align="center">12</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">2 / 200</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">3</td>
<td style="text-align:center" align="center">20</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW400</td>
<td style="text-align:center" align="center">16</td>
<td style="text-align:center" align="center">16</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">4</td>
<td style="text-align:center" align="center">15</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW500</td>
<td style="text-align:center" align="center">20</td>
<td style="text-align:center" align="center">20</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">5</td>
<td style="text-align:center" align="center">12</td>

</tr>
<tr>
<td style="text-align:left" align="left">DW600</td>
<td style="text-align:center" align="center">24</td>
<td style="text-align:center" align="center">24</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">4 / 400</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">6</td>
<td style="text-align:center" align="center">10</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW1000</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">40</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">10</td>
<td style="text-align:center" align="center">6</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW1200</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">48</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">12</td>
<td style="text-align:center" align="center">5</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW1500</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">60</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">8 / 800</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">15</td>
<td style="text-align:center" align="center">4</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW2000</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">80</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">64 / 6400</td>
<td style="text-align:center" align="center">20</td>
<td style="text-align:center" align="center">3</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW3000</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">120</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">16 / 1600</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">64 / 6400</td>
<td style="text-align:center" align="center">30</td>
<td style="text-align:center" align="center">2</td>
</tr>
<tr>
<td style="text-align:left" align="left">DW6000</td>
<td style="text-align:center" align="center">32</td>
<td style="text-align:center" align="center">240</td>
<td style="text-align:center" align="center">1 / 100</td>
<td style="text-align:center" align="center">32 / 3200</td>
<td style="text-align:center" align="center">64 / 6400</td>
<td style="text-align:center" align="center">128 / 12800</td>
<td style="text-align:center" align="center">60</td>
<td style="text-align:center" align="center">1</td>
</tr>
</tbody>
</table>
</font>
</p>

<p>
The following queries adhere ot the concurrency limits:
<ul>
<li>SELECT</li>
<li>INSERT-SELECT, UPDATE or DELETE</li>
<li>ALTER INDEX REBUILD or REORGANIZE</li>
<li>CREATE INDEX or ALTER TABLE REBUILD</li>
<li>CREATE CLUSTERED COLUMNSTORE INDEXCREATE TABLE AS SELECT (CTAS)</li>
<li>Data loads and data movement processes by the Data Movement Service (DMS)</li>
</ul>
<br/>
The following queries <b><u>do not adhere</u></b> ot the concurrency limits:
<ul>
<li>CREATE or DROP or TRUNCATE</li>
<li>IALTER TABLE or ALTER TABLE INDEX</li>
<li>DROP INDEX</li>
<li>CREATE, UPDATE or DROP STATISTICS</li>
<li>CREATE LOGIN or ALTER AUTHORIZATION</li>
<li>CREATE, ALTER or DROP USER</li>
<li>CREATE, ALTER or DROP PROCEDURE</li>
<li>CREATE or DROP VIEW</li>
<li>SELECT from system views and Dynamic Management Views (DMVs)</li>
<li>EXPLIAN and DBCC</li>
</ul>
<p>
<b>Monitoring and Securing DW</b><br/>
Azure provides an interface to veiw database activity, queries, performance, settings, drivers and connectiong strings. There is also a notifcation log to show the activities taking place and evidences how long certain activities takes at a database level. Azure takes care of backups, netowrk and disks. Data securuity is the responsibility of the user.
<br/><br/>How Can Azure be Secured?
<ul>
<li>Connection</b></li>
<li>Authentication</li>
<li>Authorisation</li>
<li>Encryption</li>
<li>Auditing</li>
<li>Threat Detection</li>
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