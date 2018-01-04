<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 8</h1>
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

<h3><strong>Module 8. Performing Analytics Azure SQL Data Warehouse</strong></h3>

<h4>Querying data in SQL Data Warehouse</h4>
<br/>
<p>
<b>Not supported by SQL DW;</b>
<ul>
<li>Triggers</li>
<li>Primary Keys</li>
<li>Foreign Keys</li>
<li>Unique and Check Table contraints</li>
<li>Unique indexes</li>
<li>Computed columns in tables</li>
<li>Sparse Columns</li>
<li>User-defined types</li>
<li>Sequences</li>
<li>Synonyms</li>
<li>Identity Columns</li>
</ul>
Basic grouping is supported however grouping with ROLLUP, GROUPING SETS, or CUBE is not.
</p>

<p><b>Views in SQL DW</b>
Views can be used to extract the technical know-how for joining different tables and providing a consistent interface to end users. Performance gains can be seen from creating join hints.<br/>
Indexed views are not possible in SQL DW.
</p>

<p><b>Performing Transactions</b>
SQL DW supports transactions for data workloads but is limited compared to SQL Server. SQL Server uses ACID (Atomicity, Consistency, Isolation and Durability) transactions, the isolation level is set to READ UNCOMMITTED and cannot be changed.<br/>
Failed transactions can be monitored through the XACT_STATE() function, returning a -2 when it has failed and is marked for rollback.<br/>
All standard dynamic SQL are supported as standard, variables, if then else constructs, while loops and stored procedures.<br/>
SQL DW will also act as a source for Azure ML (Machine Learning) and PowerBI.
</p>

<h4>Maintaining Performance</h4>
<br/>
<p>
<b>Partitioning Tables</b>
<ul>
<li>Distrubuted tables are already segmeneteed by the defined distribution.</b></li>
<li>Partitioning a table will for partition rows within a distribution.</li>
<li>Optimises the loading of large tables</li>
<li>Enables re-indexing of smaller partitions</li>
<li>Enables piecemeal data reorganization</li>
<li>Partitioned tables with clistered index can hinder data laod times more significantly on an MPP system than a SQL Server SMP system</li>
<li>Page fragmentation can hinder query performance</li>
<li>Partitioned table with a clustered columnstore index may improve range queries, these are column orientated stores (not row stores), benefits are lowest memory footprint in only a few columns of a table are used, also has best compression ratio.</li>
<li>Not recommended to add a partion to table that has a non-clustered index, can increase random input/output and increase cost</li>
<li>Partition for manageability of data, typically on a date key or interger surrogate and usually the same as a the clusterd index key</li>
</ul>
</p>

<p>
<b>Statistics</b><br/>
Statistics is an object in the database that contains information about the distributions of values in a column or multiple columns.
<ul>
<li>Not all stats are automatically created in Azure SQL DW.</b></li>
<li>When creating statistics on a column the default sample size will be set to 20%.</b></li>
<li>Compute node (Brawn - MPP Level) stats are updated with the table changes by 20%.</li>
<li>Stats on Control nodes (Brain) are used to access cardinality, these are not updated automatically</li>
<li>Multi-column stastics are information about joins on multiple key columns</li>
</ul>
</p>


<p>
<b>Concurrency Limits</b><br>
Concurrent Queries: The way to control performance of a SQL DW is to allocation data warehouse units (DWU). A maximum of 32 concurrent queireis can be executed.<br/>
Concurrency Slots: for every 100 DWU, four concurrency slots are allocated. each query requires a set of concurrency slots to run based on the four resource classes (rc) available, as shown in the table below.<br/>
<span style="font-size: small;">

<table style="font-size: 6px;">
<thead>
<tr>
<th style="text-align:left" align="left"><sub>DWU</sub></th>
<th style="text-align:center"><sub>Max concurrent queries</sub></th>
<th style="text-align:center"><sub>Concurrency slots allocated</sub></th>
<th style="text-align:center"><sub>smallrc slots / mem alloc</sub></th>
<th style="text-align:center"><sub>mediumrc slots / mem alloc</sub></th>
<th style="text-align:center"><sub>largerc slots / mem alloc</sub></th>
<th style="text-align:center"><sub>xlargerc slots / mem alloc</sub></th>
<th style="text-align:center"><sub>Compute Nodes</sub></th>
<th style="text-align:center"><sub>Distributions per Node</sub></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left" align="left"><sub>DW100</sub></td>
<td style="text-align:center" align="center"><sub>4</sub></td>
<td style="text-align:center" align="center"><sub>4</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>2 / 200</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>1</sub></td>
<td style="text-align:center" align="center"><sub>60</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW200</sub></td>
<td style="text-align:center" align="center"><sub>8</sub></td>
<td style="text-align:center" align="center"><sub>8</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>2 / 200</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>2</sub></td>
<td style="text-align:center" align="center"><sub>30</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW300</sub></td>
<td style="text-align:center" align="center"><sub>12</sub></td>
<td style="text-align:center" align="center"><sub>12</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>2 / 200</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>3</sub></td>
<td style="text-align:center" align="center"><sub>20</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW400</sub></td>
<td style="text-align:center" align="center"><sub>16</sub></td>
<td style="text-align:center" align="center"><sub>16</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>4</sub></td>
<td style="text-align:center" align="center"><sub>15</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW500</sub></td>
<td style="text-align:center" align="center"><sub>20</sub></td>
<td style="text-align:center" align="center"><sub>20</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>5</sub></td>
<td style="text-align:center" align="center"><sub>12</sub></td>

</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW600</sub></td>
<td style="text-align:center" align="center"><sub>24</sub></td>
<td style="text-align:center" align="center"><sub>24</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>4 / 400</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>6</sub></td>
<td style="text-align:center" align="center"><sub>10</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW1000</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>40</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>10</sub></td>
<td style="text-align:center" align="center"><sub>6</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW1200</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>48</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>12</sub></td>
<td style="text-align:center" align="center"><sub>5</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW1500</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>60</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>8 / 800</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>15</sub></td>
<td style="text-align:center" align="center"><sub>4</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW2000</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>80</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>64 / 6400</sub></td>
<td style="text-align:center" align="center"><sub>20</sub></td>
<td style="text-align:center" align="center"><sub>3</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW3000</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>120</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>16 / 1600</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>64 / 6400</sub></td>
<td style="text-align:center" align="center"><sub>30</sub></td>
<td style="text-align:center" align="center"><sub>2</sub></td>
</tr>
<tr>
<td style="text-align:left" align="left"><sub>DW6000</sub></td>
<td style="text-align:center" align="center"><sub>32</sub></td>
<td style="text-align:center" align="center"><sub>240</sub></td>
<td style="text-align:center" align="center"><sub>1 / 100</sub></td>
<td style="text-align:center" align="center"><sub>32 / 3200</sub></td>
<td style="text-align:center" align="center"><sub>64 / 6400</sub></td>
<td style="text-align:center" align="center"><sub>128 / 12800</sub></td>
<td style="text-align:center" align="center"><sub>60</sub></td>
<td style="text-align:center" align="center"><sub>1</sub></td>
</tr>
</tbody>
</table>
</sub>
</span>
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
<b>Scaling Compute Nodes</b><br/>
The make up of SQL DW consists of 1 control node (brain) and many compute nodes (brawn), as shown in the table above.<br/>
The number of actual distributions remains at 60, regardless of DWU size.<br/>
The three main functions of compute nodes are Pause, Resume and Scale.
</p>


<p>
<b>Best Practices</b><br/>
<ul>
<li>Labels can be assigned to a query before executing the query by adding the OPTION (LABEL = "My Project Name"), this will help categorise all activity when monitoring.</li>
<li>Before you pause the SQL DW, ensure no queries are running else these will be terminated immediately.</li>
<li>Always maintain up to date database statistics.</li>
<li>Always use the most appropriat method to load data into SQL DW initially, BCP, ADF, or polybase if the dataset is very large.</li>
<li>Specify hash distributions where appropriate, round-robin will always be the default.</li>
<li>Do not overuse partitions, this will hinder performance.</li>
<li>Use a higher resource class when queries require more memory.</li>
<li>To increase concurrency, use the lower resource classes.</li>
<li>Use DMV's to monitor and analyse user queries.</li>
</ul>
</p>


<h4>Protecting data in SQL Data Warehouse</h4>
<br/>
<p>
Azure Portal, REST API's and Powershell can be used to configure firewall rules to the Azure SQL DW. All communication to SQL DW is encrypted, there are two ways in which a user can authenticate with SQL DW;
<ul>
<li>Authentication via SQL Server authentication - Standard username and password combination hosted via SQL DW, it's good practice set the login up on the MASTER database, this ensure the user has login access to all databases within the server.</li>
<li>Authentication via Microsoft Azure Active Directory (Azure AD) authentication - An Azure service you can use to manage users and groups across multiple Azure Services.</li>
</ul>
</p>

<p>
<b>Authorising Users</b>
Authorisation centers around what a user can do once they have been authenticated. Granular permissions can control what actions a user can perform, operations such as SELECT, INSERT, UPDATE and DELETE at column, toable or any object level. Authorisation can be given to an individual user or to a role.<br/>
A user can be added to a role, which subsequently determines what actions a user can perform.<br/>
A stored procedure is a good method to secure code, given a user to access to run a stored procedure, gives a user the results they may require, without revealing the code that make up the query delivering the result.
</p>

<p>
SQL DW uses Transparent Data Encryption (TDE) for encrypting and decrypting data at rest. All data including backups and transaction logs are encrypted by default using the AES-256 encryption algorithm.
</p>

