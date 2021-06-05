# Connect_gcloud_postgresql_from_windows
Connect google cloud postgresql instance from windows command prompt and query the tables.


## Step1: Create postgresql instance from google cloud sql 
Lets say the instance name is 'postgresql-1'.  Assuming that you have already created a project. 

## Step2: Create one service account or use the existing one
Existing SA like '****@developer.gserviceaccount.com' 

and add the below role to this SA.

Cloud SQL > Cloud SQL Client

Cloud SQL > Cloud SQL Editor

Cloud SQL > Cloud SQL Admin 

Then download the json keys and place in a windows local folder and set the environment variable path as below

i.e. create new user variable with variable_name: GOOGLE_APPLICATION_CREDENTIALS and variable_value: path of the json key file

## Step3: Download the cloud_sql_proxy for windows OS
Download the cloud_sql_proxy.exe for windows OS from the below link

	https://dl.google.com/cloudsql/cloud_sql_proxy_x64.exe
	
Then rename the cloud_sql_proxy_x64.exe to cloud_sql_proxy.exe  and place this executable file to the folder from where you will execute the command from command prompt.

## Step4: Download the postgresql client for Windows OS to connect the cloud postgressql instance
Download the postgresql from the below link.

	https://www.enterprisedb.com/downloads/postgres-postgresql-downloads
	
Install the executable file by refering the below link.

	https://www.compose.com/articles/postgresql-tips-installing-the-postgresql-client/

## Step4: Connect to cloud sql instance (i.e. postgresql instance postgresql-1) from a command prompt using cloud_sql_proxy
Open a command prompt window and go to the path where cloud_sql_proxy.exe file placed:

	cloud_sql_proxy -instances=<Connection name>=tcp:<port no> &
	
	e.g.  cloud_sql_proxy -instances=project-id:europe-west2:postgresql-1=tcp:5432 &
	
	get the <Connection name> from cloud postgresql instance and default <port no> is 5432
	
Note: This window should not be closed until you are doing the operation with the database else the connection will be closed.
	
## Step5: Connect to database of postgresql instance postgresql-1 from another command prompt	
Open another command prompt window 	and execute the below command to connect to the database and query the tables.

	psql "host=<default ip of cloud_sql_proxy> sslmode=disable dbname=<database name> user=<user name>"
	
	e.g. psql "host=127.0.0.1 sslmode=disable dbname=mart user=postgres"
	
## Step6: Query to the table
	select * from table;


















