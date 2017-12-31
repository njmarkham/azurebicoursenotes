
<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services</h1>
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

<h3>General Overview of Big Data Engineering with Azure</h3>


<p><h4>Three V's of Big Data</h4></p>
<ul>
<li>Volume - How much data is being ingested</li>
<li>Variety - The type of data being ingested</li>
<li>Velocity - The frequency/speed of the data to be ingested and processed</li>
</ul>

<p><h4>Architectures for Processing Big Data</h4></p>

<p>Lambda</p>

<ul>
	<li><strong>Hot Path</strong> - Instant access to analytics at the expense of lower accuracy</li>
	<li><strong>Cold Path</strong> - Batch processing, usually at a lower grain to ensure better accurac</li>
</ul>

<p>Kappa</p>

<p><strong>Uses log files</strong> to replay the old data when logic is changed, hot and cold paths use the same data, historical data can be fed back through the hot path to give updated results.</p>

<p>Both architectures could use the following services</p>

<ul>
	<li>Azure Stream Analytics</li>
	<li>Azure Machine Learning</li>
	<li>Azure Blob Storage</li>
	<li>Azure Data Lake Storage</li>
	<li>Azure Data Lake Analytics</li>
	<li>Azure SQL Data Warehouse</li>
</ul>

<p><i>Note: Data lake provides storage for very large amounts of unstructured data which typically ties in the the above architectures. SQL Data Warehouse supports structure and processed data in a pre-configured schema. SQL Data warehouse may contain the output from the above architectures, if required.</i></p>

<p><b>Security</b></p>

<p><strong>Azure ExpressRoute</strong> for private network connectivity to cloud datacenters.&nbsp;</p>

<p><strong>Azure Virtual Networks</strong> - access to Azure cloud in which only your subscription has access, full control over DNS and security policies etc.</p>

<p><strong>Network Security Groups</strong> - create rules at various levels Access Control Lists (ACL&#39;s)</p>

<p><strong>Azure Perimeter Networks </strong>- in bound packets must travel through firewalls and intrusion detection systems.</p>
