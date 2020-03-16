#Connecting to BigQuery from Tableau 

##Before you begin

Before you begin, gather this connection information:

-	Google BigQuery email or phone, and password

Reference-style: 
![alt text][logo]

(https://help.tableau.com/current/pro/desktop/en-us/Img/example_googlebigquery2.png "Logo Title Text 1")



Make the connection and set up the data source

1.	Start Tableau and under Connect, select `Google BigQuery`. For a complete list of data connections, select More under To a Server. In the tab Tableau opens in your default browser, do the following:

a.	Sign in to Google BigQuery using your email or phone, and then select Next to enter your password. If multiple accounts are listed, select the account that has the Google BigQuery data you want to access and enter the password, if you're not already signed in.
 
b.	Select Accept so that Tableau can access your Google BigQuery data.

c.	Close the browser window when notified to do so.

2.	On the data source page, do the following:

a.	(Optional) Select the default data source name at the top of the page, and then enter a unique data source name for use in Tableau. For example, use a data source naming convention that helps other users of the data source figure out which data source to connect to.

b.	(Optional) From the Billing Project drop-down list, select a billing project. If you don't select a billing project, EmptyProject appears in the field after you have selected the remaining fields.

c.	From the Project drop-down list, select a project. Alternatively, select publicdata to connect to sample data in BigQuery.

d.	From the Dataset drop-down list, select a data set.

e.	Under Table, select a table.

Use custom SQL to connect to a specific query rather than the entire data source. For more information, see Connect to a Custom SQL Query.
Note: Google BigQuery has changed support from BigQuery legacy SQL (BQL) to standard SQL. 

Your workbooks will upgrade to support standard SQL when you open them in Tableau.
Google BigQuery data source example
Here is an example of a Google BigQuery data source using Tableau Desktop on a Windows computer:
 
Note: Because of the large volume of data in BigQuery, Tableau recommends that you connect live.
Use customization attributes to improve query performance
Note: Customization attributes aren't currently supported in Tableau Prep Builder.
You can use customization attributes to improve the performance of large result sets returned from BigQuery to Tableau Online and Tableau Server, and on Tableau Desktop.
You can have the customization attributes included in your published workbook or data source, as long as you specify the attributes before you publish the workbook or data source to Tableau Online or Tableau Server.
Use Google BigQuery customization attributes
Customization attributes accept integer values and affect both live queries and extract refreshes for the specified connection.
The following attributes help the most to increase performance of large result sets:
bq-fetch-tasks	Number of parallel background tasks to use when fetching data using HTTP. The default is 10.
bq-large-fetch-rows	Number of rows to fetch in each batch for spool queries. The default is 50000.
The following attributes are also available and are primarily used for small queries:
bq-fetch-rows	Number of rows to fetch in each batch for non-spool queries. The default is 10000.
bq-response-rows	Number of rows returned in non-spool non-batched queries. The default is 10000.
This capability setting accepts yes or no values and can be useful when testing:
CAP_BIGQUERY_FORCE_SPOOL_JOB	Force all queries to use the temp table approach. The default value is “no.” Change the value to “yes” to turn this attribute on.
How Tableau returns rows from Google BigQuery
Tableau uses two approaches to return rows from BigQuery: the default non-spool approach, or the temp table (spool) approach:
•	On the first attempt, queries are executed using the default, non-spool query, which uses the bq-fetch-rows setting.
•	If the result set is too large, the BigQuery API returns an error and the Tableau BigQuery connector retries the query by saving the results into a BigQuery temp table. The BigQuery connector then reads from that temp table, which is a spool job that uses the bq-large-fetch-rows setting.
How to specify the attributes
You can specify attributes in one of two ways: in a Tableau Datasource Customization .tdc file, or in the workbook or data source XML.
Specify attributes in a .tdc file
To specify customization attributes during a publish workbook or publish data source operation from Tableau Desktop, follow these steps:
1.	Create an XML file that contains the customization attributes.
2.	Save the file with a .tdc extension, for example, BigQueryCustomization.tdc.
3.	Save the file to the My Tableau Repository\Datasources folder.
The customization attributes in the .tdc file are read and included by Tableau Desktop when the data source or workbook is published to Tableau Online or Tableau Server.
Important: Tableau does not test or support TDC files. These files should be used as a tool to explore or occasionally address issues with your data connection. Creating and maintaining TDC files requires careful manual editing, and there is no support for sharing these files.
Example of a .tdc file with recommended settings for large extracts
<connection-customization class='bigquery' enabled='true' version='8.0' >
  <vendor name='bigquery' />
  <driver name='bigquery' />
  <customizations>
    <customization name='bq-fetch-tasks' value='10' />
    <customization name='bq-large-fetch-rows' value='10000' />
  </customizations>
</connection-customization>
Manually embed attributes in the XML of the workbook or data source file
You can manually embed customization attributes inside the 'connection' tag in the workbook .twb file or the data source .tds file. The BigQuery customization attributes are bold in the following example to make them easier for you to see.
Example of manually embedded attributes
<connection CATALOG='publicdata' EXECCATALOG='some-project-123' REDIRECT_URI='some-url:2.0:oob' SCOPE='https://www.googleapis.com/auth/bigquery https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email' authentication='yes' bq-fetch-tasks='10' bq-large-fetch-rows='10000' bq_schema='samples' class='bigquery' connection-dialect='google-bql' connection-protocol='native-api' login_title='Sign in to Google BigQuery' odbc-connect-string-extras='' project='publicdata' schema='samples' server='googleapis.com/bigquery' server-oauth='' table='wikipedia' username=''>
Check if your workbook uses standard SQL or legacy SQL
In 2016, Google updated the BigQuery APIs to support standard SQL, in addition to still supporting BigQuery SQL (now called legacy SQL). Starting in Tableau 10.1, the Google BigQuery connector has been upgraded to support standard SQL, and also still supports legacy SQL. Standard SQL enables users of the BigQuery connector to use level of detail expressions, get faster metadata validation, and select a billing project with the connection.
Now, when you create a new workbook, Tableau supports standard SQL by default. Tableau also supports legacy SQL using the Use Legacy SQL option on the Data pane. For example, when you open a workbook that was created using a previous version of Tableau Desktop, and if your workbook uses legacy SQL, the Use Legacy SQL option is selected.
You might want to configure the Use Legacy SQL option for the following reasons:
•	You have an existing workbook that you want to update to use standard SQL in order to write level of detail expressions or to take advantage of other improvements. In this case, make sure that the Use Legacy SQL option is not selected.
•	You are creating a new workbook that needs to connect to a legacy SQL view. You can’t mix legacy SQL with standard SQL, so you need to select the Use Legacy SQL option for the workbook to function.
In Google BigQuery, views are written in standard SQL or legacy SQL. You can join views written in standard SQL to views written in standard SQL, or views written in legacy SQL to views written in legacy SQL, and you can join views written in either version of SQL to a table. But you can’t join views written in standard SQL and views written in legacy SQL in one workbook. When you join views, you must set the Use Legacy SQL check box to correspond to the SQL type used in the view you are connecting to.
Note: Tableau Desktop provides limited support for nested data when you use legacy SQL or standard SQL. For example, if a table contains nested data and you're using legacy SQL or standard SQL, on the data source page, Update Now won't work.
For more information about migrating from legacy SQL to standard SQL, see Migrating from legacy SQL on the Google Cloud Platform website.
See also
•	Set Up Data Sources – Add more data to this data source or prepare your data before you analyze it.
•	Build Charts and Analyze Data – Begin your data analysis.
•	Set up Oauth for Google -Configure Oauth connections for Tableau Server.
•	Oauth Connections - Configure Oauth connections for Tableau Online.
•	Google BigQuery & Tableau: Best Practices - Read the Tableau whitepaper (registration or sign in required)


