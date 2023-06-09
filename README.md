# repliss
Repliss is a tool to mask your test/staging databases to keep sensitive data safe.

Repliss supports databases
SQL Server
Prerequisites
Windows	
Installation
To install it on a Windows machine go to the link 

https://github.com/viveknsigithub/repliss and install the latest version of exe file.

Store it in any location and add this path in the PATH ENV variable on your machine and restart the machine.

Check that repliss command is working correctly on your machine from the terminal.

Usage

It has mainly three steps.

Create a configuration file(.yaml)  as per the requirements

The sample configuration file is described below and shared in GitHub repo as well.


source:
  connection_details:
    server: LAPTOP115
    database: testdb
    username: viveknsi
    password: password
  transformers:
    - table: students
      columns:
        - name: address
          transformer_name: rndvar
        - name: age
          transformer_name: rndint4    
        - name: email
          transformer_name: email
        - name: email_bck
          transformer_name: email          
        - name: phone
          transformer_name: rndvar          
        - name: name
          transformer_name: rndvar                                                
    - table: studentsnew
      columns:
        - name: age
          transformer_name: rndint2        
        - name: name
          transformer_name: rndvar    
        - name: email
          transformer_name: email                                                              
datastore:
  path: ./datasource




connection_details
	server: SQL server hostname
	database: SQL server DB name
	username: DB User name
	password: DB Password

transformers: Columns of the tables that need to transform
		table: SQL server table name
		columns: Define all columns which need to mask
		name: Table column name
		transformer_name: Type of transformation rule
			It supports a different kinds of transformation rules for ex:
			email: To mask the field which has the client’s email address
			rndvar : To mask string type field (nchar , nvarchar)
			rndint2 : To mask int type field with 2 digit value change
			rndint4 : To mask int type field with 4 digit value change
			rndint6 : To mask int type field with 6 digit value change
			rndint8 : To mask int type field with 8 digit value change

datastore: Where do you want to store the transform data (on the local machine).Create folder with same name inside your root folder


Create a dump with the help of the configuration file

Open the terminal from the folder where conf.yml file exists.

Use the below command to generate transformed data on the configured data source(local).


repliss create dump


Restore the latest dump in a remote/local database


repliss apply latest

Help
	For any help use the command 

repliss --help
	
	or

	Email me at vivek.singh@netsolutions.com
