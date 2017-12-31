<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 2</h1>
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

<h3><strong>Module 2. Stream Analytics</strong></h3>



<p>Inputs</p>

<ul>
	<li>IoT Hub</li>
	<li>Event Hubs</li>
	<li>Azure Blob Storage</li>
	<li>Azure Blob Storage - reference data</li>
</ul>

<p>Outputs</p>

<ul>
	<li>Azure Data Store</li>
	<li>Azure SQL DB</li>
	<li>Azure Blob Storage</li>
	<li>Event Hubs</li>
	<li>Power BI</li>
	<li>Azure Table Storage</li>
	<li>Service Bus Queues</li>
	<li>Service Bus Topics</li>
	<li>Azure Cosmos DB</li>
</ul>

<p><strong>Grouping data by time (temporal windows)</strong></p>

<ul>
	<li>Sliding Window - Slides the window of any given event however only starts when an event enters or exits the window.</li>
	<li>Tumbling Window - Fixed window positions of any given length</li>
	<li>Hopping Window - Moves according to the hop size given however the window size can extend into other hops (eg. 0-10 secs, 5-15sec, 10-20 secs, with a window size of 10 and a hopsize of 5), means analysis can overlap.</li>
</ul>