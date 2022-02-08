# List of features

* f0001: Download and Restore MongoDB archives 
* f0002: Create Index
* f0003: Group Rows in CSV Files
* f0004: Read records from MongoDB and write into a CSV file
* f0005: Count the number of connections between two hashtags
* f0006: Aggregate all grouped csv into one csv
* f0007: Get accurate location based on user location
* f0008: Monitor NIFI
* f0009: MongoDB Insertions(JSON)
* f0010: Jenkins Backup
* f0011: MongoDB Backup
* f0012: Count the number of hashtag daily
* f0013: Concatenate files
* f0014: Collection Level Report
* f0015: Geoname
* f0016: Get User Location per Collection
* f0017: Convert CSV to JSON array
* f0018: Add new column in CSV
* f0019: Convert XML to CSV
* f0020: Convert CSV to Excel
* f0021: Convert JSON to CSV
* f0022: Census R Script for SA1 & SA2
* f0023: Geocoding
* f0024: Compare Two Collections on MongoDB
* f0025: Update Records on MongoDB
* f0026: R Script For National Social Resilience (Used in P0015)
* f0027: QGIS
* f0028: Search Query In Twitter Collection
* f0029: Download Collections from MongoDB and Convert Them to CSV Files
* f0030: Read Census CSV Files (output of f0029) and Scaling Values with Relevant Population
* f0031: Read a Census CSV File (output of f0030) and Clustering Data by Using PCA and Kmeans.
* f0032: Upload/Download Files from Nectar Container Using Swift

## Detailed Description
### f0002: Create Index
Create Text Index for all MongoDB collections

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* Contain-String : filter the collection by the contained string in the name
* Create-Index : 
  - If "1", then create index.
  - If "2", it lists the collections that require index.

### f0003: Group Rows in CSV Files
Group rows and count the number of the same records

Inputs:
* Input-Folder : read all files from this path
* Output-Folder : write output files into this path
* Language : 
  - If "1", keep the rows with English letters and numbers
  - If "2", keep all rows
  - If "3", keep the rows with non-English letters
* Delete-None : 
  - If "1", the rows with "none" value will be deleted
  - If "2", the rows with "none" value will not be deleted
  
Outputs:
* CSV files 

### f0004: Export CSV from MongoDB

#### f0004-a: Read selected records from MongoDB and write into a csv file
Create a csv file with two columns (hashtag, user_location) for each collection

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* Contain-String : filter the collection by the contained string in the name

Outputs:
* CSV files

#### f0004-b: Read all records from MongoDB and write into a csv file

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : Database name
* User-Name : MongoDB user name
* Psword : MongoDB password
* Output-Folder : ended with "/"
* Collection-Number : Process on "1" or "all" collections
* Collection-Name : if "Collection-Number" is "1", then set the coolection name

Outputs:
* CSV files

### f0005: Count the number of connections between two hashtags
Create csv file with three columns (hashtag, linked_hashtag, number) for each collection

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* Contain-String : filter the collection by the contained string in the name

Outputs:
* CSV files

### f0006: Aggregate all grouped csv into one csv
Aggregate every two csv files into one csv file at each time, after f0003 is completed

Inputs:
* Input-Folder : read all files from this path
* Output-Folder : write output files into this path
* Column-List : column name, if more than one, then separated by ","
* Column-Type-List : column name's type, if more than one, then separated by ","
                     Options: "string","int","float"

Outputs:
* CSV files


### f0007: Get accurate location based on user location
Comparing user location with geo file and add three columns (city, state, country) in the new csv file

Inputs:
* Input-Folder : read all files from this path
* Output-Folder : write output files into this path
* Aus-File-Path : path of the au.csv in the supporting-files
* World-File-Path : path of the world-cities.csv in the supporting-files

Outputs:
* CSV files

### f0008: Monitor NIFI
Send a message to Slack only if the record number of collection is reduced or the same compared with the last run

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* Slack-Token : Slack API token
* Channel : Slack channel
* File-Path : result.txt path
* Log-File-Path : log.txt path
* Out-Folder : output file folder (create if not exists)

Outputs:
* result.txt (overwrite the previous one)
* log.txt

### f0009: MongoDB Insertions(JSON)

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* Folder-Path : read all JSON files from this path
* DB-Name : database name
* Contain-String : filter the JSON files by the contained string in the name
* JSON-Key : key for the array (if no key then set it to "none" )
* User-Name : MongoDB user name
* Psword : MongoDB user password

### f0011: MongoDB Backup
Dump collections and drop them optional

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* Drop-Collection : if "1", then drop the collection after dump finished
* Start-Str : start string of the collection name

Outputs:
* gzip files

### f0012: Count the number of hashtag daily

#### f0012-a: Without Geoname

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* Contain-String : filter the collection by the contained string in the name
* Output-Path : write output files into this path

Outputs:
* CSV files

### f0012-b: With Geoname
Multiprocessing program

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* Contain-String : filter the collection by the contained string in the name
* Output-Path : write output files into this path
* CPU-Number

Outputs:
* CSV files

### f0013: Concatenate files
This is a bash script file

Inputs:
* $1 : input folder - read files from this path
* $2 : start name - filter the files by the started string in the name
* $3 : output file - name of the output file

Outputs:
* CSV file

### f0014: Collection Level Report
#### f0014-a: Restore archived collection file from the folder and calculate

Inputs:
* $1 : input folder - read files from this path
* $2 : database name
* $3 : output file - name of the output file

Outputs:
* CSV file
  - Number of records in each collection
  - Status of Index in each collection
 
#### f0014-b: Get top 100 hashtags from MongoDB
Generate one csv file for each collection

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name

Outputs:
* CSV files

### f0015: Geoname

#### f0015-a: Get geoname information based on user location
multiprocessing program

Inputs:
* Flag : 
  - If "Other" collection, then "1".
  - If "Australia" collection, then "2".
* Input-Folder
* Prefix : prefix of the collection files' names
* Output-File
* Ratio-Value
* Column-Number : choose which column in input file to process the geoname
* World-Cities-File : world-cities.csv in supporting-files
* World-States-File : world-states.csv in supporting-files
* World-Countries-File : world-countries.csv in supporting-files
* AU-Cities-File : au-cities.csv in supporting-files
* AU-States-File : au-states.csv in supporting-files
* AU-Countries-File : au-country.csv in supporting-files
* CPU-Number

Outputs:
* CSV files

#### f0015-b: Insert geoname information into MongoDB

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* AU-Geo-File : Australia geoname file (The output file from f0015-a)
* World-Geo-File : World geoname file (The output file from f0015-a)

#### f0015-c: Collection Level Report (python version)
Including : record count, index information, English tweets count, geoname count

* Code Usage: f0015-c.py collection_name

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name

Outputs:
* JSON file

#### f0015-d: Delete empty geoname field from MongoDB

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* Contain-String : filter the collection by the contained string in the name

### f0016: Get User Location per Collection
Get unique user location csv file for each collection

#### f0016-a: Restore archived collection file, Run f0016-b and Drop the collection

Inputs:
* $1 : input folder - read files from this path
* $2 : database name
* $3 : python file - name of the file
* $4 : prefix - prefix of the collection files' names

Output:
* CSV files

#### f0016-b: Get unique user location csv file for each collection

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* Output-Folder : output folder ended with "/"

Outputs:
* CSV files

#### f0016-c: Get new user location

Inputs:
* Input-Folder : read files from this path
* Output-Folder : output folder ended without "/"
* Geo-Aus-File
* Geo-World-File 

Outputs:
* CSV files

### f0017: Convert CSV to JSON array
process files with same start string each time

Inputs:
* CSV-Folder-Path : read file from this folder path
* JSON-Folder-Path : write into this folder
* Start-String : String that filenames start with

Outputs:
* JSON files

### f0018: Add new column in CSV

#### f0018-a: Split one column and add to separate new columns

Inputs:
* Input-File : csv file
* Output-File : csv file
* Column-Name
* Split-Character
* Rename: 
  - if "1", then append the original header as a prefix to the new header
  - if "2", then do not append

Outputs:
* CSV file

#### f0018-b: Add new columns based on file name

Inputs:
* Input-Folder : read csv files from this folder ended with "/"
* Output-Folder : ended with "/"

Outputs:
* CSV files

### f0019: Convert XML to CSV

Inputs:
* Input-File : xml file
* Output-File : csv file

Outputs:
* CSV file

### f0020: Convert CSV to Excel

Inputs:
* Input-File : csv file
* Output-File-Name : xlsx file name without extension

Outputs:
* xlsx file

### f0021: Convert JSON to CSV

Inputs:
* Input-Folder : read json files from this folder ended with "/"
* Output-File
* Input-File : weekly_report.csv

Outputs:
* updated weekly_report.csv


### f0022: Census R Script for SA1 & SA2

#### SA1:

* f0022-a.r : main R script
* f0022-b.r : function R script

#### SA2:

* f0022-a.r : main R script
* f0022-b.r : function R script

### f0023: Geocoding

Inputs:
* Input-File : csv/excel file
* Output-File : csv file
* Threshold : default value is 1000
* Google-API-Key
* Address-Column : "address" column number or name in csv file

Outputs:
* CSV file

### f0024: Compare Two Collections on MongoDB
To get new address list

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* User-Name : MongoDB user name
* Psword : MongoDB user password
* Output-File : csv file
* Collection-Raw-Name : Raw data collection name
* Collection-Geocode-Name : geocoded address collection name

Outputs:
* CSV file

### f0025: Update Records on MongoDB

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* User-Name : MongoDB user name
* Psword : MongoDB user password
* Collection-Raw-Name : Raw data collection name
* Collection-Geocode-Name : geocoded address collection name

### f0027: QGIS

f0027.sh: activate the anaconda environment first, then process f0027.py

Inputs:
* Atlas-Dataset: exact file path of atlas dataset
* Shapefile: exact file path of shape file
* Output-File
* Shape-File-Year : "2016" or "2011"

### f0028: Search Query In Twitter Collection

Inputs:
* IP : MongoDB server IP
* MongoDB-Port
* DB-Name : database name
* User-Name : MongoDB user name
* Psword : MongoDB user password
* Debug : if equal any string, then create log file, otherwise, keep it empty
* Query-Input : CSV file with one column (no header)

Outputs:
* csv_result/{collection}/{query}/{tweet_id}.json
* json_result/{collection}_{query}.csv


### f0029: Download Census collections from MongoDB and convert them to CSV files

Inputs:
* Config file:
	* IP : MongoDB host server IP
	* MongoDB-Port : MongoDF port
	* DB-Name : Database name
	* User-Name : MongoDB user name
	* Psword : MongoDB user password
	* Collection-Name : Collection name
	* Import-Option-File: Text file including import options
	* Output-Population-File: Name of output file
* import_options2016.txt
	- This file contains information about required collections and columns name.

Outputs:
* CSV files: CSV files containing downloaded collections with selected columns. 

### f0030: Read generated Census CSV files (by f0029) and scaling values with relevant population

Inputs:
* Config file:
	* Input-Files-Directory: f0029 directory where stores all generated census CSV data
	* Import-Option-File: Text file including import options
	* Extracted-Census: list of the generated Census files by f0029 
	* Population-data: name of generated population file by f0029 
	* Name: Text file including column names to be changed
	* Output-File: Name of output file
* import_options2016.txt
	* This file contains information about which population has to be used for scaling
* names.txt
	* This file contains old column name and new column name that all the old column name need to be changed to the new column name.

Outputs:
* CSV file: CSV file containing scaled 2016 Census data 

### f0031: Read a generated Census CSV file (by f0030) and clustering the data by using PCA and Kmeans.

Inputs:
* Config file:
	* Input-Files-Directory: f0030 directory where stores generated census data
	* Input_Data: name of generated census data
	* Output-File: Name of output file
	* PCA_Component_No: Number of Component for PCA
	* Kmeans_Init_Status: Method for initialization:
	* Kmean_Cluster_No: The number of clusters to form as well as the number of centroids to generate.
	* Kmeans_Init_No: Number of time the k-means algorithm will be run with different centroid seeds.
	* Kmeans_Max_iter: Maximum number of iterations of the k-means algorithm for a single run.
	* Kmeans_Random_State: Determines random number generation for centroid initialization. Use an int to make the randomness deterministic
		
Outputs:
* CSV file: CSV file containing clustered 2016 Census data 

### f0032: Upload/Download Files from Nectar Container Using Swift

* Usage: 
  * bash f0032.sh $1 $2 $3 $4

* Parameter:
  * $1 : config file
  * $2 : container name
  * $3 : files separated by comma ","
  * $4 : "upload" OR "download" OR "download_prefix" OR "tempurl"
