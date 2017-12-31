<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 5</h1>
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

<h3><strong>Module 5. Processing Big Data using Azure Data Lake Analytics</strong></h3>

<p>Azure Data Lake Analytics (ADLA) is a platform as a service (PaaS) enabling advanced analytics and batch processing at scale on big data.</p>

<p>Source -&gt; Ingest -&gt; Processing -&gt; Storage -&gt; Delivery</p>

<ul>
	<li>Source - Source systems</li>
	<li>Ingest - Azure Data Factory</li>
	<li>Processing - Azure Data Lake Analytics</li>
	<li>Storage - Azure Data Lake Store / Blob Storage</li>
	<li>Delivery - Power BI / Other presentation tools</li>
</ul>

<p>ADLA is concerned with the processing stage.</p>

<p>Stream analytics it best suited for hot data (real time) and ADLA is best suited for cold data (that takes minutes. hours or days to process).</p>

<p>Jobs are written in U-SQL, which combines Transact SQL and C#.</p>

<p>When jobs are executed they are broken down into stages of execution. Each stage performs a task.</p>

<p>Tasks that run in parallel in each stage are referred to as vertices by ADLA. Each vertex is managed and scheduled by using a distributed component called YARN (Yet Another Resource Negotiator).&nbsp;</p>

<p>YARN allocates computing resources and retrieves the results from those resources. This decouples developmental code (U-SQL) from resource management responsibilities.&nbsp;</p>

<p>Computing resources are allocation into AU&#39;s (Analytics Units). Each AU represents two CPU cores and 6GB of RAM. More AU&#39;s means better potential for executing a job with a degree of parallelism, and the faster the job will run. This must be monitored for best performance vs cost of each AU allocated.</p>

<p>Always best practice to sort data on final output, order by on vertices above the output may not be in the correct order depending on how and when they are processed.</p>

<p>ADLA contains two additional join types SEMIJOIN and ANTISEMIJOIN</p>