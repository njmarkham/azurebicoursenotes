# azurebicoursenotes
Course notes from Big Data Engineering with Azure

<h1>Contents</h1>

<a href="https://github.com/njmarkham/azurebicoursenotes/">Overview (this page)</a><br/>
<a href="https://github.com/njmarkham/azurebicoursenotes/blob/master/faq.md">FAQ</a><br/>

Module 2 and 3 Stream Analytics<br/>
Module 4 - Azure Data Lake Store<br/>
Module 5 and 6 - Data Lake Analytics / Implementing Custom Operations and Monitoring Performance<br/>

<hr/>

<h2>General Overview of Big Data Engineering with Azure</h2>


<p><h4>Three V's of Big Data</h4></p>
<ul>
<li>Volume - How much data is being ingested</li>
<li>Variety - The type of data being ingested</li>
<li>Velocity - The frequency/speed of the data to be ingested and processed</li>
</ul>

<p><h4>Architectures for processing Big Data</h4></p>

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
