# Docker

This Dockerfile helps to get started using SQL Server Express in Windows Containers. 
The file downloads and installs Microsoft SQL Server 2017 Express Edition with the default setup parameters.

You need to have windows server 2019.

Run the container with below required parameters:

docker run -d -p 1433:1433 -v C:/sqlserver/:C:/sqlserver/ -e sa_password=xxxx -e ACCEPT_EULA=Y -e attach_dbs="<add DB-JSON-CONFIG>" ImageName

  -p HostPort:containerPort is for port-mapping a container network port to a host port.

  -v HostPath:containerPath is for mounting a folder from the host inside the container. This can be used for saving database outside of the container.

  -it :use is to get output of the SQL startup script.For debugging purpose.
  
  accept_eula: Confirms acceptance of the end user licensing agreement.

  sa_password: Sets the sa password and enables the sa login

  attach_dbs: The configuration for attaching custom DBs (.mdf, .ldf files).

  This should be a JSON string, in the following format

[
  {
  	'dbName': 'SampleDB',
  	'dbFiles': ['C:\\sqlserver\\SampleDB.mdf',
  	'C:\\sqlserver\\SampleDB_log.ldf']
  }
}

docker run -d -p 1433:1433 -v C:/sqlserver/:C:/sqlserver/ -e sa_password=xxx -e ACCEPT_EULA=Y -e attach_dbs="[{'dbName':'SampleDB','dbFiles':['c:\\sqlserver\\SampleDB.mdf','c:\\sqlserver\\SampleDB.ldf']}]" --name nameofthecontainer NameofImage
