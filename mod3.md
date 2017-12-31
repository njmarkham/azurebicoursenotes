<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 3</h1>
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

<h3><strong>Module 3. Performing Custom Processing in Azure Stream Analytics</strong></h3>



<p><strong>User Defined Functions</strong></p>

<p>Javascript or Machine Learning UDF&#39;s can be created</p>

<p>Collect() is a ASA function and returns an array containing all the records from a specific time window.</p>

<p><strong>Machine Learning</strong></p>

<p>Machine learning is an iterative process which consists of the following key components</p>

<ul>
	<li>Azure Machine Learning Studio - graphical tool to design, implement, test and deploy</li>
	<li>Data PreProcessing modules - large library to process and prepare raw data into processed data ready for algorithms&nbsp;</li>
	<li>Machine Learning algorithms&nbsp;-&nbsp;</li>
	<li>Machine Learning API - after models are deployed, these are API that allow downstream applications to plug into them and consume - eg. Restful web services.</li>
</ul>

<p>ML Output</p>

<p>Records - key value pair typically used by JSON</p>

<p>Arrays - an ordered collection of values, useful when you do not know how many sets of name value pairs to be received.</p>

<p>Machine learning is deployed as a web service and is invoked using inline syntax in the stream analytics job as a function call.</p>