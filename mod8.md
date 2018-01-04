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
<ul>
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


</p>

<h4>Protecting data in SQL Data Warehouse</h4>
<br/>
<p>


</p>