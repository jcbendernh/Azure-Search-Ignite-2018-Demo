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
<li>First we need to obtain the key and URL of our Search Service.  Follow the steps in the <b>Get a key and URL</b> section at https://docs.microsoft.com/en-us/azure/search/search-fiddler#get-a-key-and-url. </li>
  <li>Open Postman and click <b>+New | Request</b>.  Under Request name type <b>POST data source</b> and create a custom collection/folder to add it to.</li>
	<ol>
		<li>Change GET to POST</li>
		<li>Under Enter Request URL add the following...  <b>https://YOUR-SEARCH-SERVICE-NAME.search.windows.net/indexes?api-version=2019-05-06</b>.</li>
		<li>Under Headers add the following values...</li>
	  		<ol>
				<li> KEY = <b>Content-Type</b> | VALUE = <b>application/json</b> </li>
				<li> KEY = <b>api-key</b> | VALUE = <b>YOUR-ADMIN-API-KEY</b><br> 
					
![Alt text](/imgs/POSTdatasourceheader.gif?raw=true)
				</li>
			</ol>
		<li>Under Body add the content from the <a target="_blank" href="https://github.com/jcbendernh/Azure-Search-Ignite-2018-Demo/blob/master/JSON/1-POST%20datasource.json">1-POST datasource.json</a> file and change the values on lines 2,7 &amp; 10.<br>

![Alt text](/imgs/POSTdatasourcebody.gif?raw=true)
		</li>
		<li>Click Send and you should see the properties of your new data source under the Response section of Postman.</li>
	</ol>
  </li>
    <li>Click <b>+New | Request</b>, under Request name type <b>POST index</b> and add it to your new custom collection/folder.</li>
	<ol>
		<li>Change GET to POST</li>
		<li>Under Enter Request URL add the following...  <b>https://YOUR-SEARCH-SERVICE-NAME.search.windows.net/indexes?api-version=2019-05-06</b>.</li>
		<li>Under Headers add the following values...</li>
	  		<ol>
				<li> KEY = <b>Content-Type</b> | VALUE = <b>application/json</b> </li>
				<li> KEY = <b>api-key</b> | VALUE = <b>YOUR-ADMIN-API-KEY</b><br> </li>
			</ol>
		<li>Under Body add the content from the <a target="_blank" href="https://github.com/jcbendernh/Azure-Search-Ignite-2018-Demo/blob/master/JSON/2-POST%20index.json">2-POST index.json</a> file and change the value on line 2.<br>

![Alt text](/imgs/POSTindexbody.gif?raw=true)
		</li>
		<li>Click Send and you should see the properties of your new data source under the Response section of Postman.</li>
	</ol>
  </li>
  <li>For this section, we are going to enable the Text and OCR skills. Click <b>+New | Request</b>.  Under Request name type <b>POST skillset</b> and add it to your new custom collection/folder.</li>
	<ol>
		<li>Change GET to POST</li>
		<li>Under Enter Request URL add the following...  <b>https://YOUR-SEARCH-SERVICE-NAME.search.windows.net/indexes?api-version=2019-05-06</b>.</li>
		<li>Under Headers add the following values...</li>
	  		<ol>
				<li> KEY = <b>Content-Type</b> | VALUE = <b>application/json</b> </li>
				<li> KEY = <b>api-key</b> | VALUE = <b>YOUR-ADMIN-API-KEY</b><br> </li>
			</ol>
		<li>Under Body add the content from the <a target="_blank" href="https://github.com/jcbendernh/Azure-Search-Ignite-2018-Demo/blob/master/JSON/3-POST%20skillset.json">3-POST skillset.json</a> file and change the value on line 2.</li>
		<li>For lines 68-72, this will depend if you setup a Cognitive Services subscription.  If not, change the section to <b>"cognitiveServices": null</b>. Otherwise, change the values in lines 70 &amp; 71.</li>
		<li>Click Send and you should see the properties of your new skillset under the Response section of Postman.</li>
	</ol
  </li>
  <li>Finally we are going to create and run the Indexer.  The settings in the JSON for this particular example are set to run once, which will run immediately after creation.  Click <b>+New | Request</b>, under Request name type <b>POST indexer</b> and add it to your new custom collection/folder.</li>
	<ol>
		<li>Change GET to POST</li>
		<li>Under Enter Request URL add the following...  <b>https://YOUR-SEARCH-SERVICE-NAME.search.windows.net/indexes?api-version=2019-05-06</b>.</li>
		<li>Under Headers add the following values...</li>
	  		<ol>
				<li> KEY = <b>Content-Type</b> | VALUE = <b>application/json</b> </li>
				<li> KEY = <b>api-key</b> | VALUE = <b>YOUR-ADMIN-API-KEY</b><br> </li>
			</ol>
		<li>Under Body add the content from the <a target="_blank" href="https://github.com/jcbendernh/Azure-Search-Ignite-2018-Demo/blob/master/JSON/4-POST%20indexer.json">4-POST indexer.json</a> file and change the values on line 2,4,5 &amp; 6</li>
		<li>Click Send and you should see the properties of your new indexer under the Response section of Postman.</li>
	</ol>
  </li>
  <li>Next, go into the Azure Portal and check the status of your indexer.  You can see it in the Indexers tab of the Overview blade.  The status upon completion may depend on your Subscription and pricing levels.  For more details check out https://docs.microsoft.com/en-us/azure/search/search-sku-tier. </li>
</ol>

# Steps to creating the web application to utilize the Search Service.
Now we will utilize this repository to publish a search page in a web app so we can utilize the search service from a browser.
<br>
<ol start="12">
	<li>Clone/Download this repository and open it in Visual Studio</li>
	<li>Under solution explorer, right click on the <b>CognitiveSearch.UI</b> and select <b>Set as Startup Project</b>. </li>
	<li>Under solution explorer, double click <b>appsettings.json</b> to activate it in the window and change lines 8-14.</li>
	<li>Next we need to create a SAS toekn to be used to access the files in Blob storage via the web application.  To create the SAS Token, go the Storage Account in the Azure Portal and click on the <b>Shared access signature</b> blade.  Fill out the proper fields and click <b>Generate SAS and connection string</b> button.</li>
	<li>Copy the value in the SAS token field generated.</li>
	<li>Under solution explorer, expand <b>Controllers</b> and double click on the <b>HomeController.cs</b> to activate it in the window and copy the SAS token value to line 109.</li>
	<li>It is time to Publish the project to Azure, under solution explorer, right click on the <b>CognitiveSearch.UI</b> and select <b>Publish</b> and fill out the approrpriate settings and save the Web App in the same resource group as your other Azure Search resources.</li>
	<li>Open the new App Service in the azure portal and click on the Web URL in the properites blade to open the search page in the browser.</li>
	<li>Type in a search term and click the find button to test.  If successful, you should see a result like below.
	
	![Alt text](/imgs/searchresults.gif?raw=true)
	</li>
</ol>