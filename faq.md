<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; FAQ</h1>
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

<h3><strong>FAQ</strong></h3>

<p><h2>What is Azure Log Analytics?</h2></p>
 

<p><h2>What is a Service Bus?</h2></p>

<p><h2>What's the difference between a clustered and non-clustered index on a table?</h2>
A clustered index dictates teh way rows are sorted, which can provide very godo performance when reading from a table. However insertion of data can be slow as the index has to be rearranged frequently, only one clustered index can exist on a single table.<br/>
By contrast, a non-clustered index does not alter the way in which the rows are stored, seperate objects are created for the table as the data changes over the time which act as pointers for back to the rows being queried. Many non-clustered indexes can exist on a table. These indexes are good for  joins columns or queries that target a column.
</p>
 

<p><h2>What are Vertices?</h2>
<br/>
A vertex represents the resources used to perform a given task. Each vertex runs using an Analytics Unit (AU), each AU provides the processing power of two CPU cores and 6GB RAM. A vertex is also allotted a maximum of five hours run-time before it's forcible terminated to avoid runaway costs.
</h2>

<p><h2>SMP vs MMP</h2>
SMP - Symmetric Multi-Processing. In a symmetrical multi-
processing environment, the CPU's share the same memory, 
and as a result code running in one CPU can affect the 
memory used by another.<br/>
MMP - Massively Parallel Processing. computer system with 
many independent arithmetic units or entire 
microprocessors, that run in parallel.
</p>

<p><h2>What is Round-Robin/Hash?</h2>
Round Robin relates to distribution of data across multiple nodes of a database. Data is spread across multiple servers. Used where there a multiple primary/foreign keys and staging tables. <br/>
Hash is where the value of a single column gets hashed to define the distribution number where the entire record will get inserted. Data is all in same place. Best for fact/detail tables if there is a common distribution key which is used in multi-distributed table joins.<br/>
Neither of these are the same as a partition, replicated or temporary tables.
</p>

<p><h2>What is a heap table?</h2>
<br/>
Reletes to the table structure. When you are temporarily landing data on SQL Data Warehouse, you may find that using a heap table will make the overall process faster. This is because loads to heaps are faster than to index tables and in some cases the subsequent read can be done from cache. If you are loading data only to stage it before running more transformations, loading the table to heap table will be much faster than loading the data to a clustered columnstore table. In addition, loading data to a temporary table will also load much faster than loading a table to permanent storage.
<br/><br/>
For small lookup tables, less than 100 million rows, often heap tables make sense. Cluster columnstore tables begin to achieve optimal compression once there is more than 100 million rows.
</h2>

<p><h2>What is a Polybase?</h2>
Polybase allows the querying of both structured data (database tables with predefined schemas) and unstructured data (flat files in a HDFS).</p>