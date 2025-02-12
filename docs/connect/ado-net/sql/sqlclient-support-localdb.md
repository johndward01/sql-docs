---
title: "SqlClient support for LocalDB"
description: "Describes SqlClient support for LocalDB databases."
author: David-Engel
ms.author: v-davidengel
ms.reviewer: v-kaywon
ms.date: "08/15/2019"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
---
# SqlClient support for LocalDB

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Beginning in SQL Server code name Denali, a lightweight version of SQL Server, called LocalDB, will be available. This topic discusses how to connect to a LocalDB database.  
  
## Remarks  
For more information about LocalDB, including how to install LocalDB and configure your LocalDB instance, see SQL Server Books Online.  
  
To summarize what you can do with LocalDB:  
  
- Create and start LocalDB instances with sqllocaldb.exe or your app.config file.  
  
- Use sqlcmd.exe to add and modify databases in a LocalDB instance. For example, `sqlcmd -S (localdb)\myinst`.  
  
- Use the `AttachDBFilename` connection string keyword to add a database to your LocalDB instance. When using `AttachDBFilename`, if you do not specify the name of the database with the `Database` connection string keyword, the database will be removed from the LocalDB instance when the application closes.  
  
- Specify a LocalDB instance in your connection string. For example, your instance name is `myInstance`, the connection string would include:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` is not allowed when connecting to a LocalDB database.  
  
You can download LocalDB from [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041). If you will use sqlcmd.exe to modify data in your LocalDB instance, you will need sqlcmd from SQL Server 2012, which you can also get from the SQL Server 2012 Feature Pack.  
  
## Programmatically create a named instance  
An application can create a named instance and specify a database as follows:  
  
- Specify the LocalDB instances to create in the app.config file, as follows.  The version number of the instance should be the same as the version number of your LocalDB installation.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- Specify the name of the instance using the `server` connection string keyword.  The instance name specified in the `server` connection string keyword must match the name specified in the app.config file.  
  
- Use the `AttachDBFilename` connection string keyword to specify the .MDF file.  
  
## Next steps
- [SQL Server features and ADO.NET](sql-server-features-adonet.md)
