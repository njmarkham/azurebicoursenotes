<h1><strong>Module 2. Stream Analytics</strong></h1>

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