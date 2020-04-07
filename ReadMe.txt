https://stackoverflow.com/questions/21592062/ef6-migrations-localdb-update-database-login-failed

I'm working with VS 2013 and EF6.1 .
I got similar kind of error when I work with migration and delete database. I was unable to recreate database again. Found that error due to SQLExpress local database instance is running on background and keeping the deleted database connection with it.
following are the steps to handle this situation.
Delete the database files (.mdf and .ldf) files.
Delete Migration Folder from your application.
Delete any database connection to that database from server Explorer data connections.
Go to windows Command Prompt (IF VS 2012 or earlier you have to use the VS Command prompt).
Run "sqllocaldb.exe stop v11.0" (This will stop the v11.0 service)
Run "sqllocaldb.exe delete v11.0" (This will delete the v11.0 service)
Go to Package Manager Console in Visual studio.
Run "Enable-Migrations" (This will create Migration folder and content)
Run "Add-Migration init" (This will scaffold the changes to next migration)
Run "Update-Database" (This will create the database again)