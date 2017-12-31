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

<h3><strong>Module 4. Managing Big Data in Azure Data Lake Store</strong></h3>

<p>Data lake store is a hyperscale distributed file service that plays a key role in the processing and management of big data.</p>

<p>Encrypted data throughout the lifecycle it manages access and authorisation through Role-Based Access Control (RBAC), ADL is compatible with many analytical solutions and is used in place of HDFS services like Apache Store, Spark, MapReduce and Hive running on HDInsight.</p>

<ul>
	<li>No limit for account sizes or the amount of data stored</li>
	<li>Can be controlled programmatically by external interfaces using powershell, visual studio, Python etc.. to perform common data lake tasks.</li>
</ul>

<p>Data is transferred into the data lake as a result of a streaming process, for example when you specify the output of a streaming process to be a data lake sink.</p>

<p>AZ Copy can be used to transfer on-premise (offline) datastores to Azure Blob Storage</p>

<p>ADL Copy can be used to transfer data from Azure Blob Storage to Azure Data Lake Storage.</p>

<p>Disaster recovery is the responsibility of the customer, critical data should always be stored in two separate regions to help protect from unscheduled outages and other regional disasters.</p>

<p>Data should also be protected using security controls so it cannot be overridden (maliciously or accidentally). Additionally, resource locks should be used to prevent the entire data lake from being removed.</p>

<p><strong>Encrypting and Securing Data</strong></p>

<p>Data is always encrypted in Azure, all interactions take place over a HTTPS connection.The most efficient way is to let the services you provision manage it for you. However you can use Azure Key Vault to manage encryption keys over two separate Master Encrypted Key (MEK) modes.</p>

<ul>
	<li>Service Managed Keys</li>
	<li>Customer Managed Keys</li>
</ul>

<p>Both methods encrypt data before its sent, the only major difference between the two approaches is that customer managed keys can be revoked and deleted, which brings risks to no one being able to view the data.</p>

<p>There are two further grains of encryption used within a data lake store,</p>

<ul>
	<li>DEK (Data Encryption Key) - Always managed by the Azure Service, encrypted by the MEK.</li>
	<li>BEK (Block Encryption Key) - Tied to the data built using the the DEK and the block of data, not stored.</li>
</ul>

<p>Contains a simple software-based firewall to lock down access from specific IP or IP ranges. Firewalls can also be configured externally, through Powershell for instance.</p>

<p>Authorising users works on two levels for access to a Data Lake. RBAC (Role-based Access Control) to specifiy or limit what actions a user performs across the entire store. ACL (Access Control Lists) are then used to control the operations that users perform over files and folders in the store.</p>

<p>Files inherit the permissions of the folder in which they are created.</p>
