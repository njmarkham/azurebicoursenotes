<h1>20776A: Performing Big Data Engineering on Microsoft Cloud Services &rArr; Module 6</h1>
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

<h3><strong>Module 6. Implementing Custom Operations and Monitoring Performance in Azure Data Lake Analytics</strong></h3>


<p>To extend the ADLA core framework of U-SQL you can use either a code behind file, whereby a temporary assembly is stored in memory for the lifetime of the job execution. This is fully supported and automated as part of Visual Studio, however the main disadvantage is that is not reusable across multiple jobs.</p>

<p>Compiling the same script into a separate assembly and uploading into ADLA account, all jobs may then reference this script making it reusable.</p>

<p>Windowing data uses the OVER PARTITION ORDER BY function</p>

<p>Outputters as part of ADLA can be extended and customised extending the Microsoft.Analytics.Interfaces.IOutputter base class.</p>

<p>UDF (User-Defined functions) can also be created to extend U-SQL,operating on a row-by-row basis, they can take any number of parameters but return a scalar value that is typically used in the SELECT or WHERE clause.</p>

<p>Aggregation functions can also be extended through extending the base class&nbsp;Microsoft.Analytics.Interfaces.IAggregate that expects type parameters for the arguments passed into the aggregator for the type of data being aggregated. The base class contains three methods which should be overwritten if being extended;</p>

<ul>
	<li>Init - The method runs once, initialising any variables that need to be set in order to calculate aggregate values.</li>
	<li>Accumulate - This method is executed for each row being aggregated, containing data for the row passed in at run-time.</li>
	<li>Terminate - Running at the end of the aggregation. The output of the method is returned to the U-SQL as the result.</li>
</ul>

<p><strong>Using R</strong></p>

<p>Statistical analysis can be achieved through the R extension of ADLA. R extensions are available in a separate assembly called ExtR. Add the extension and the supporting files to the catalog area of ADLA through the Azure portal and go to Sample Scripts, Install U-SQL Extensions. You can then use R in your U-SQL by referencing the ExtR assembly at the top of the U-SQL script. Note that only double, string, bool, integer and byte types can passed to R function and byte arrays by serialising them as strings. A dataset passed between R and U-SQL must not exceed 500MB to avoid a vertex exceeding it&#39;s memory limit, however the REDUCE statement can be used to partition the data into smaller rowsets based on the values in a key column of the rowset.</p>

<p><strong>Using Python</strong></p>

<p>Similar to R, ADLA extensions for Python are held in an assembly named ExtPython and&nbsp;installed at the same time as any R extensions when you click Install U-SQL Extensions from the scample scripts in the ADLA Azure Portal. You call Python code by using the Extension.Pythin.Reducer class with the REDUCE statement. Reference your Python code by using the pyScript parameter and it must contain a function named usql_main that takes a pandas Dataframe object as it&#39;s parameter and returns a Pandas DataFrame as it&#39;s result.</p>

<p><strong>Cognitive Capabilities</strong></p>

<p>A collection of machine learning API&#39;s that cover more than 25 different scenerios.</p>

<p>U-SQL supports the following subset through Cognitive Services;</p>

<ul>
	<li>Imaging - facial recognition</li>
	<li>Imaging - emotion detection</li>
	<li>Imaging - object detection and tagging</li>
	<li>Imaging - optical character recognition</li>
	<li>Text - sentiment analyses</li>
	<li>Text - key phrase extraction</li>
</ul>

<p>U-SQL User Defined Extractors, appliers and processors for calling the supported cognitive services API above are;</p>

<ul>
	<li>Cognitive.Vision.FaceDetectionExtractor</li>
	<li>Cognitive.Vision.EmotionExtractor</li>
	<li>Cognitive.Vision.ImageExtractor</li>
	<li>Cognitive.Vision.ImageTagger</li>
	<li>Cognitive.Vision.OCRExtractor</li>
	<li>Cognitive.Text.SentimentAnalyzer</li>
	<li>Cognitive.Text.KeyPhraseExtractor</li>
	<li>Cognitive.Text.Splitter</li>
</ul>

<h2><strong>Opimizing Jobs</strong></h2>

<p><strong>How to Partition data held in ADLA to improve scalability</strong></p>

<p>Partitioning data is concerned with breaking up input data into smaller chunks so that is can be run in parallel, making the job complete quicker and potentially saving money.&nbsp;</p>

<p>Input data is classified into two separate groups;</p>

<ul>
	<li>Unstructured Data - files such as CSV, Text, JSON and XML whereby U-SQL has no prior knowledge of the input schema, U-SQL requires additional information to partition this effectively.</li>
	<li>Structured Data - data held within tables in the ADLA catalog, in these cases the schema&#39;s are predefined by the definition of the table, catalogs can also contain statistical information about the distribution and range of values in each column, helping U-SQL optimise jobs.</li>
</ul>

<p>Partitioning unstructured data can be done if the extractor has the SqlUserDefinedExtractor(AtomicFileProcessing = false) attribute. The input data is considered to be splittable and can be read by using a set of parallel tasks. U-SQL wil split the file into a series of extents, each a maximum size of 250MB. A single vertex reads up to <u>four</u> extents. A new vertex will be required for each 1GB of data. If unstructured data is split up into seperate files for how the input data is to be processed (for instance a year on year basis), then a virtual column can be used within the U-SQL job to dynamically run for the required data set only and not have the added overhead of scanning multiple rows that it may not even require (eg. FROM &quot;/SalesData/{year}.csv&quot;)</p>

<p>ADLA catalog is designed to hold very large tables. All tables must be created wit ha clustered index and the data must be distributed according to a specified key. This will drastically improve lookup times. eg.&nbsp;</p>

<p>INDEX idxName CLUSTERED (fieldID ASC) DISTRIBUTED BY HASH(fieldID)</p>

<p>Regular filtering on a specific filtering can be improved by partioning e.g.</p>

<p>INDEX idxName CLUSTERED (fieldID ASC) PARTINIONED BY (fieldName) DISTRIBUTED BY HASH(fieldID)</p>

<p><strong>Monitoring ADLA jobs</strong></p>

<p>At runtime U-SQL prepares and attempts to determine the most efficient way to run the job.</p>

<p>It will access partitions and how to make sure of them discarding data in partitions&nbsp;that are not required and how to spread the load across multiple AU&#39;s, making use of parallel processing. The optimiser accesses whether this is possible and if so allocates a task within the U-SQL to a vertex for execution.</p>

<p>Executing U-SQL jobs from Visual Studio presents the user with three views after the job has completed successfully and has been profiled.</p>

<ul>
	<li>Vertex Execution View - Shows time spent creating, queuing and running each vertex</li>
	<li>Stage Scatter View - Displays the amount of I/O performed by each vertex</li>
	<li>Vertex Operator View - Examines the way in which various U-SQL operators (extractors, aggregators, outputters) where used and also features processors, appliers, combiners and reducers.</li>
</ul>

<p><strong>User-defined Processors</strong></p>

<p>Let&#39;s you provide your own logic for handling data on a row-by-row basis, extends the Microsoft.Analytics.Interfaces.IProcessor abstract base class. Uses the PROCESS U-SQL command to invoke once the correct assembly has been referenced.</p>

<p><strong>User-defined Appliers</strong></p>

<p>User-defined appliers work with the CROSS APPLY operator in U-SQL. The CROSS APPLY combines two rowsets, joining rows from the first row set (left) to the the second row set (right) across a common set of column values. Extends the base class&nbsp;Microsoft.Analytics.Interfaces.IApplier</p>

<p><strong>User-defined Combiners</strong></p>

<p>A user-defined combiner acts like a JOIN operator except that it perms join that are more complex than those supporting by standard U-SQL. Extending the&nbsp;Microsoft.Analytics.Interfaces.ICombiner base class, performance can be enhanced by providing how the data is partitions to both the left and right side of the join query, using the SqlUserDefinedCombiner attribute with the mode Full, Inner, Left or Right.</p>

<p><strong>User-defined Reducers</strong></p>

<p>A reducer operates on data when you read it in. You use the reducer to filter data and generate custom groupings and then pass on to U-SQL for further processing. The REDUCE statement in a U-SQL script divides the data into groups and the reducer processes the rows in the group to determine which to include or extract.&nbsp;Extends the&nbsp;Microsoft.Analytics.Interfaces.IReducer base class.</p>

<h2><strong>Managing Jobs and Optimising Resources</strong></h2>

<p>ADLA mirrors ADLS in terms of securing resources. Using RBAC (Role based Access Control) to control operations the user can perform and uses ACL (Access Control Lists) to determine what files and catelogs they can use.</p>

<p><strong>Managing Resources for Jobs</strong></p>

<p>ADLA accounts are associated with a number of AU&#39;s available. You need to ensure that a single user or job does not monopolise the resources available. This can be achieved the resource policies.&nbsp;</p>

<p>ADLA supports two types of policies</p>

<ul>
	<li>Account Level - Applied to all jobs that run under a single ADLA account.</li>
	<li>Job Level - Applies to job run be specific users.</li>
</ul>

<p>When configuring policies within ADLA, for a user or group of users you can set both the maximum number of AU&#39;s that a single job can consume and the maximum priority that user or group of users can give a job.</p>

<p>Auditing jobs is done through the activity log section of ADLA. You can send audit logs to a storage account, stream them to an even hub and save them to Azure Log Analytics.</p>

<p><strong>Monitoring Jobs</strong></p>

<p>The monitoring tools provide low-level insight in to the details of jobs, whilst they are running and after they have completed (or failed). Three utilities are available within the monitoring blade of ADLA;</p>

<ul>
	<li>Job Management - Displays the status of the jobs, provides a same job overview given in Visual Studio showing the vertices.</li>
	<li>Job Insights - This utility shows the number of jobs that have been submitted, broken down into succeeded, failed cancelled and active. The queue section shows jobs that have been submitted but not yet running, as long queue may suggest either a lack of resources of a particular job hogging resources. Recurring jobs are also visible on a separate tab.</li>
	<li>Metrics - Quick access to a graphical view of job compute hours, also failed jobs compute hours.</li>
</ul>