# Azure-Search-Ignite-2018-Demo
This project can be used to build out a demo instance of Azure Search processing documents and images from an Azure Blob Storage container.  This is based on the template that 
<a target="_blank" href="https://www.linkedin.com/in/luisecabrera/">Luis Cabrera-Cordon</a> featured at Ignite 2018. To view the session, go to https://youtu.be/Wh5Dt8wnEhg.  
<br>&nbsp;<br>
<b>Prerequisites</b>
<br>&nbsp;<br>
To use this project, we must do a few things first to create the resources needed...
<ol>
  <li>Create an Azure Storage account to be used for our documents &amp; pictures to be stored in Blob Storage.<br>
  You can follow the instructions at https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal.</li>
  <li>When your Azure storage account is created, create a blob container for your files.<br>
  You can follow the instructions at https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal.</li>
  <li>Create an Azure Search Service.<br>
  You can follow the instructions at https://docs.microsoft.com/en-us/azure/search/search-create-service-portal.</li>
  <li>Upload the files you want to search on into your new blob container.  I suggest using <a target="_blank" href="https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer">Azure Storage Explorer</a> to do so.</li>
  <li>You may need to create a Cognitive Services account to allow the Indexer to fully process large documents with over 65K characters.<br>
  For more information on creating a Cognitive Services account, click <a target="_blank" href="https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account">here</a>.</li>
</ol>

<b>Steps to creating a Custom Data Source, Skillset, Index &amp; Indexer</b>
<br>&nbsp;<br>
Next we will need to create a data source, skillset, index and an indexer.  This can be done manually via the portal using the following instructions...https://docs.microsoft.com/en-us/azure/search/search-get-started-portal.
<br>&nbsp;<br>
However, this does not account for large documents that need to be indexed so I have upload JSON documents to the <a target="-blank" href="https://github.com/jcbendernh/Azure-Search-BUILD-2018-Demo/tree/f619bb3f5b15010bd076ad9a8f510326639f5c47/JSON">JSON folder</a> of this repository that can be used via Postman that account for this scenario.  Thus, if you would like to use Postman to create these, download Postman by going to the following URL... https://www.getpostman.com/products.  
<br> &nbsp; <br>
My instructions below are based on the <a target="_blank" href="https://docs.microsoft.com/en-us/azure/search/search-fiddler">Quickstart: Explore Azure Search REST APIs using Postman</a>.

<ol start="6">
  <li>First we need to obtain the key and URL of our Search Service.  Follow the steps in the <b>Get a key and URL</b> section at https://docs.microsoft.com/en-us/azure/search/search-fiddler#get-a-key-and-url.</li>
  <li>Open Postman and click <b>+New | Request</b>.  Under Request name type <b>POST data source</b> and create a custom collection/folder to add it to.</li>
	<ol type="a">
		<li>Change GET to POST</li>
		<li>Under Enter Request URL add the following...  <b>https://<YOUR-SEARCH-SERVICE-NAME>.search.windows.net/indexes?api-version=2019-05-06</b>.</li>
		<li>Under Headers add the following values...</li>
	  		<ol type="i">
				<li>Line 1 - KEY = <b>Content-Type</b> | VALUE = <b>application/json</b></li>
				<li>Line 2 - KEY = <b>api-key</b> | VALUE = <b><YOUR-ADMIN-API-KEY></b></li>

			</ol>
		<li>Under Body add the body from the <a target="_blank" href="https://github.com/jcbendernh/Azure-Search-BUILD-2018-Demo/blob/master/JSON/1-POST%20datasource.json">1-POST datasource.json</a> file and change the values on lines 2,7 &amp; 10...</li>
		<li>Click Send and you should see the properties of your new data source under the Response section of Postman.</li>
	</ol>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>

</ol>
