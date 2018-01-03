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


<p>
<b>Data Distribution</b>
<ul>
<li>Round Robin relates to distribution of data across multiple nodes of a database. Data is spread across multiple servers. Used where there a multiple primary/foreign keys. </li>
<li>Hash is where the value of a single column gets hashed to define the distribution number where the entire record will get inserted. Data is all in same place. Best for fact/detail tables if there is a common distribution key which is used in multi-distributed table joins.</li>
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
<li>Maximum bytes per row is 8060./li>
<li>Identity and PK, FK and unique index constraints are not supported</li>
<li>Case insesitive</li>
<li>Physical table structures supported, heap, clustered/non-clustered index, clustered columnstore index and partitions</li>
</ul>
</p>

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
<li>Partitioned table with a clustered columnstore index may improce range queries, these are column orientated stores (not row stores), benefits are lowest memory footprint in only a few columns of a table are used, also has best compression ratio.</li>
<li>Not recommended to add a partion to table that has a non-clustered index, can increase random input/output and increase cost</li>
<li>Partition for manageability of data, typically on a date key or interger surrogate and usually the same as a the clusterd index key</li>
</ul>
</p>