# Azure-Serverless-SQL-Pool-Transform-files
## Transform files using a azure serverless SQL pool
## Overview
Often as part of **a data ingestion pipleline** or **extract**, **transform** and **load (ETL) process, **SQL** is utilised to **manipulate** and **transform** data. It is the goal of this project to use a serverless SQL pool in **Azure Synapse Analytics** to transform data in files.
1. 1. Sign into the [Azure portal](https://portal.azure.com).<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/79445bfb-318f-4bad-91bb-bab1858ab0dd)<p>
2. Click on the [>] button located to the right of the search bar at the top of the page in the Azure portal to initiate the creation of a new Cloud Shell. Choose a PowerShell environment and set up storage if requested.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/d0fb4215-99bc-4c2e-9706-361dd56f778a)<p>
**NB**: Change a previously created Bash environment in a cloud shell to PowerShell by using the drop-down menu at the top left of the cloud shell pane.<p>
3. In the PowerShell pane, type in the following commands to clone this repo:
```
 rm -r dp-203 -f
 git clone https://github.com/MicrosoftLearning/dp-203-azure-data-engineer dp-203
```
4. After the repo has been cloned, enter the following commands to change to the folder for this lab and run the setup.ps1 script it contains:
```
 cd dp-203/Allfiles/labs/03
 ./setup.ps1
```
5. Enter a suitable password when prompted to be set up for the **Azure Synapse SQL pool**.
6. If prompted, choose which subscription you want to use (this will only happen if you have access to multiple Azure subscriptions).
7. Wait for the script to complete the set up.
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/3332f660-05f2-4c88-bd88-9f74ecd7218e)

## Query Data in Files 
The script in the **./setup.ps1** sets up **an Azure Synapse Analytics workspace** and **an Azure Storage account** to store the **data lake**, and then uploads some data files to the **data lake**.
### View Files in the Data Lake
1. After the script finishes, in the Azure portal, navigate to the dp500- xxxxxxx resource group it generated, and choose your Synapse workspace.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/f38d6abf-5b0f-42ca-b991-76a91cab5304)<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/fceb4be1-be43-4bc7-b9d6-465f92670f56)<p>
2. On the Overview page for your Synapse workspace, click "Open" on the Open Synapse Studio card to launch Synapse Studio in a new browser tab, and sign in if prompted.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/d86656df-4d2b-4334-94c3-cfd74f69c6b7)<p>
3. On the left side of Synapse Studio, click the ›› icon to expand the menu, which will display the various pages used to manage resources and perform data analytics tasks within Synapse Studio.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/90e9f68c-e4e0-47da-964e-49208f119200)<p>
4.Navigate to the Data page, go to the Linked tab, and confirm that your workspace has a link to your Azure Data Lake Storage Gen2 storage account, which should have a name similar to "synapse xxxxxxx (Primary - datalake xxxxxxx)".<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/40f5d67e-d85b-49f0-bc8a-a634f94c4f07)<p>
5. Expand the storage account and ensure that it includes a file system container named "files".<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/2cd6a8a4-79f6-4721-a145-3f20bda8ece4)<p>
6. Choose the **files** container, and observe that it includes a folder named "sales" containing the data files we intend to query.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/164078ce-3b98-4b5d-b60a-2b8bb0a6d59f)<p>
7. Open the **sales** folder and the **csv** folder within it, and note that the latter contains .csv files for three years of sales data.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/d84e9f81-2c98-4395-b50d-552747b20cb1)<p>
8. Right-click on any of the files and choose **Preview** to view the data it contains. Please note that the files do not include a header row, so you can deselect the option to display column headers.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/df231755-f1eb-4490-945c-4735ae63cd1c)<p>
9. Close the preview, and then use the ↑ button to navigate back to the sales folder.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/da649f27-3e0e-442f-a3cc-90af1a1490c9)<p>

### Use SQL to Query CSV Files
1. Choose the csv folder, and then from the New SQL script list on the toolbar, select "Select TOP 100 rows".<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/2e91fbc8-da1a-4e1e-8b1d-c70d036802d0)<p>
2. In the File type list, select Text format, and then apply the settings to open a new SQL script that queries the data in the folder.<p>
![image](https://github.com/JonesKwameOsei/Azure-Synapse-Serverless-SQL-Pool-/assets/81886509/24cf00b1-d4e8-4ffa-9293-049b66eb71c0)<p>
3. In the Properties pane for SQL Script 1, change the name to **Query Sales CSV files**, and adjust the result settings to display **All rows**. Then, click "Publish" on the toolbar to save the script, and use the **Properties button (which looks similar to 🗏)** at the right end of the toolbar to hide the **Properties** pane.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/2976d4a9-1321-4790-afbf-ce2c7d4a8965)<p>

Review the SQL code that has been generated, which should be similar to this:
```
-- This is auto-generated code
SELECT
    TOP 100 *
FROM
    OPENROWSET(
        BULK 'https://datalake7rn80bt.dfs.core.windows.net/files/sales/csv/**',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0'
    ) AS [result]
```
This code utilises the OPENROWSET to read data from the CSV files in the sales folder and fetches the first 100 rows of data.<p>
5. In this case, the data files include the column names in the first row; so modify the query to add **a HEADER_ROW = TRUE** parameter to the **OPENROWSET** clause, as shown here (don’t forget to add a comma after the previous parameter):
```
SELECT
    TOP 100 *
FROM
    OPENROWSET(
        BULK 'https://datalake7rn80bt.dfs.core.windows.net/files/sales/csv/**',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0',
        HEADER_ROW = TRUE
    ) AS [result]
```
6. On the toolbar, click the ▷ Run button to execute the SQL code, and examine the results, which should resemble this:<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/0204624c-e05b-4035-98e6-3eda66d25e7c)<p>
7. Save the changes to your script by clicking **Publish**, and then close the script pane.

## Transform data using CREATE EXTERNAL TABLE AS SELECT (CETAS) statements
A simple method to use SQL for transforming data in a file and saving the results in another file is to employ a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement. This statement generates a table based on the query's requirements, with the table's data being stored as files in a data lake. The modified data can then be queried through the external table or accessed directly in the file system, for instance, to be used in a downstream process for loading the transformed data into a data warehouse.<p>

### Create an External Data Source and File Format
Defining an external data source in a database can reference the data lake location where we want to store files for external tables. An external file format allows us to specify the format for those files, such as Parquet or CSV. To utilize these objects with external tables, we must create them in a database other than the default master database.
1. In Synapse Studio, on the **Develop** page, in the + menu, select **SQL script**.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/968522b7-06c1-4946-bd79-b3fd94d5569a)<p>
2. In the new script pane, add the following code (replacing "datalakexxxxxxx" with the name of your data lake storage account) to create a new database and add an external data source to it.
```
 -- Database for sales data
 CREATE DATABASE Sales
   COLLATE Latin1_General_100_BIN2_UTF8;
 GO;
    
 Use Sales;
 GO;
    
 -- External data is in the Files container in the data lake
 CREATE EXTERNAL DATA SOURCE sales_data WITH (
     LOCATION = 'https://datalakexxxxxxx.dfs.core.windows.net/files/'
 );
 GO;
    
 -- Format for table files
 CREATE EXTERNAL FILE FORMAT ParquetFormat
     WITH (
             FORMAT_TYPE = PARQUET,
             DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
         );
 GO;
```
3. Modify the script properties to change its name to **Create Sales DB**, and publish it.
4. Make sure that the script is connected to the **Built-in** SQL pool and the **master database**, and then run it.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/0619865d-0402-4297-a9cd-c10b469a285f)<p>
5. Return to the **Data** page and use the **↻ button** at the top right of Synapse Studio to refresh the page. Then view the **Workspace tab** in the **Data pane**, where a SQL database list is now displayed. Expand this list to verify that the Sales database has been created.<p>
6. Expand the **Sales database**, its **External Resources folder**, and the **External data sources folder** under that to see the **sales_data** external data source you created.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/b8aadf1a-4c54-4f22-95b5-484de6cf055f)<p>

### Create an External Table
1. In Synapse Studio, on the **Develop** page, go to the + menu and select **SQL script**.
2. In the new script pane, add the following code to retrieve and aggregate data from the CSV sales files using the external data source. Note that the BULK path is relative to the folder location where the data source is defined.
3. Run the script. The results should look similar to this:<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/1d139580-0316-432a-af5b-bb2ff5c1d1fa)<p>
4. Modify the SQL code to save the results of query in an external table, like this:
```
 CREATE EXTERNAL TABLE ProductSalesTotals
     WITH (
         LOCATION = 'sales/productsales/',
         DATA_SOURCE = sales_data,
         FILE_FORMAT = ParquetFormat
     )
 AS
 SELECT Item AS Product,
     SUM(Quantity) AS ItemsSold,
     ROUND(SUM(UnitPrice) - SUM(TaxAmount), 2) AS NetRevenue
 FROM
     OPENROWSET(
         BULK 'sales/csv/*.csv',
         DATA_SOURCE = 'sales_data',
         FORMAT = 'CSV',
         PARSER_VERSION = '2.0',
         HEADER_ROW = TRUE
     ) AS orders
 GROUP BY Item;
```
5. Run the script to create an external table based on the query results.
6. Name the script **Create ProductSalesTotals table** and **publish** it.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/49c4b3b3-c821-43b5-ad62-24c9926ce79e)<p>
7. Then, in the **Workspace tab** on the **data** page, check the **External tables** folder for the **Sales** SQL database to confirm that a new table named **ProductSalesTotals** has been created.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/3141c70b-327f-4dd7-aef6-d5f6315d6695)<p>
8. In the menu for the **ProductSalesTotals** table, select **New SQL script** > **Select TOP 100 rows** to run the resulting script and verify the aggregated product sales data.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/3f5f4ddb-2f92-4bd6-b492-356f47360020)<p>
9. Additionally, in the file system for your data lake, check the contents of the sales folder to ensure that a new **productsales** folder has been created.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/8d626398-21f5-4eb3-a594-7a6c63d5eb15)<p>
10. Within the **productsales** folder, observe the creation of one or more files with names similar to **ABC123DE—-.parquet**, which contain the aggregated product sales data. You can select one of these files and use the **New SQL script** > **Select TOP 100 rows** menu to query it directly.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/df3b9711-ad43-424d-bfea-2b35a79dec2f)<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/04c63eef-1e5b-4573-8e35-a5ee1ef41142)<p>

## Encapsulate data transformation in a stored procedure
If a project will need to transform data frequently, a stored procedure czn be used to encapsulate a CETAS statement.

1. In Synapse Studio, on the Develop page, in the + menu, select SQL script.
2. In the new script pane, add the following code to create a stored procedure in the Sales database that aggregates sales by year and saves the results in an external table:
```
 USE Sales;
 GO;
 CREATE PROCEDURE sp_GetYearlySales
 AS
 BEGIN
     -- drop existing table
     IF EXISTS (
             SELECT * FROM sys.external_tables
             WHERE name = 'YearlySalesTotals'
         )
         DROP EXTERNAL TABLE YearlySalesTotals
     -- create external table
     CREATE EXTERNAL TABLE YearlySalesTotals
     WITH (
             LOCATION = 'sales/yearlysales/',
             DATA_SOURCE = sales_data,
             FILE_FORMAT = ParquetFormat
         )
     AS
     SELECT YEAR(OrderDate) AS CalendarYear,
             SUM(Quantity) AS ItemsSold,
             ROUND(SUM(UnitPrice) - SUM(TaxAmount), 2) AS NetRevenue
     FROM
         OPENROWSET(
             BULK 'sales/csv/*.csv',
             DATA_SOURCE = 'sales_data',
             FORMAT = 'CSV',
             PARSER_VERSION = '2.0',
             HEADER_ROW = TRUE
         ) AS orders
     GROUP BY YEAR(OrderDate)
 END
```
3. Run the script to create the stored procedure, and then, under the code you just ran, add the following code to call the stored procedure:
```
EXEC sp_GetYearlySales;
```
4. Select only the **EXEC sp_GetYearlySales;** statement you just added, and use the ▷ **Run** button to execute it.
5. Then, in the *file system** tab for your data lake, check the contents of the sales folder to confirm the creation of a new "yearlysales" folder. Inside the **yearlysales** folder, verify the creation of a parquet file containing the aggregated yearly sales data.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/6c1f75b5-93f8-4890-bda7-ea22e997e816)<p>
6. Afterwards, switch back to the SQL script and re-run the **EXEC sp_GetYearlySales;** statement, and observe that an error occurs.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/24d80b95-2f55-4b25-a52c-4736c16f6242)<p>
7. Despite the script dropping the external table, the folder containing the data is not deleted. To re-run the stored procedure, you must delete the old data.
8. Return to the files tab, view the sales folder, select the yearlysales folder, and delete it.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/aaf8d6b1-165f-47f1-a2e5-3121416ee91f)<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/92adb21e-8358-4f57-9c39-e21fefe4777b)</p>
9. Then, go back to the SQL script and re-run the "EXEC sp_GetYearlySales;" statement. This time, the operation should succeed and a new data file will be generated.<p>
![image](https://github.com/JonesKwameOsei/Azure-Serverless-SQL-Pool-Transform-files/assets/81886509/bf7157dc-4a3a-4015-bd97-d0204bc6a566)

## Conclusion
In this project, we leveraged the transformation capabilities of **Azure Synapse Analytics Serverless SQL Pool** to tranform files. 























