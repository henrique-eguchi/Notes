# SQL Server
Useful SQL Server commands

## Get the data type associated with a specific column
```
SELECT DATA_TYPE 
FROM INFORMATION_SCHEMA.COLUMNS
WHERE 
     TABLE_NAME = 'tableName' AND 
     COLUMN_NAME = 'columnName'

```

## Check the max value from table, before alter the identity
```
SELECT MAX(column_name) FROM table1
```

## Reset auto identity
If number equals 0 then in the next insert the auto increment field will contain value 1
```
DBCC CHECKIDENT('databasename.dbo.tablename', RESEED, number)
```

## Search for procedure, view, function, systable or usertable that contains some given text

```
USE DBName
GO

SELECT A.NAME, A.TYPE, B.TEXT
  FROM SYSOBJECTS  A (nolock)
  JOIN SYSCOMMENTS B (nolock) 
    ON A.ID = B.ID
WHERE B.TEXT LIKE '%SELECT DISTINCT%'  --- Information to be searched inside procedure, function or view body.
  AND A.TYPE = 'P'                     --- Object Type
 ORDER BY A.NAME
 
GO
```
Object Types:
**U** => User Table

**S** => System Table

**P** => Procedure

**V** => View

**F** => Function

## Commands to check blocked process
```
SELECT SPID, BLOCKED, HOSTNAME=LEFT(HOSTNAME,20), PROGRAM_NAME=LEFT(PROGRAM_NAME,20),WAITTIME_SEG = CONVERT(INT,(WAITTIME/1000)),OPEN_TRAN, STATUS
FROM MASTER.DBO.SYSPROCESSES
WHERE BLOCKED = 0 
AND SPID IN (SELECT BLOCKED FROM MASTER.DBO.SYSPROCESSES WHERE BLOCKED >0 ) ORDER BY SPID 
```
```
exec sp_lock
```
```
exec sp_who
```
```
exec sp_who2
```
```
SELECT
    R.SESSION_ID,
    S.LOGIN_NAME,
    C.CLIENT_NET_ADDRESS,
    S.HOST_NAME,
    S.PROGRAM_NAME,
    ST.TEXT
FROM SYS.DM_EXEC_REQUESTS R
INNER JOIN SYS.DM_EXEC_SESSIONS S
ON R.SESSION_ID = S.SESSION_ID
LEFT JOIN SYS.DM_EXEC_CONNECTIONS C
ON R.SESSION_ID = C.SESSION_ID
OUTER APPLY SYS.DM_EXEC_SQL_TEXT(R.SQL_HANDLE) ST
WHERE ST.TEXT LIKE '%YOUR QUERY STRING TO SEARCH FOR%';
```

# NuGet
Useful NuGet commands 

## Install a package
Install-Package ```<Package name>``` -Version <Version>

Example
```shell
Install-Package Newtonsoft.Json -Version 6.0.1
```

## Uninstall a package
Uninstall-Package ```<Package name>```

Example
```shell
Uninstall-Package Newtonsoft.Json
```
## List packages
### Basic command to list all available versions of a package including prerelease (betas)
Get-Package -Filter ```<Package name>``` -ListAvailable -AllVersions -IncludePrerelease
  
Example
```shell
Get-Package -Filter Newtonsoft.Json -ListAvailable -AllVersions -IncludePrerelease
```
### With column autosize
Get-Package -Filter ```<Package name>``` -ListAvailable -IncludePrerelease -AllVersions | ft -AutoSize
  
Example
```shell
Get-Package -Filter Newtonsoft.Json -ListAvailable -AllVersions -IncludePrerelease | ft -AutoSize
```

# Docker
## Initial boarding tutorial
### Build
Mac
```shell
cd doodle/cheers2019 && docker build -t <USER>/cheers2019 .
```
Win
```shell
cd doodle\cheers2019 ; docker build -t <USER>/cheers2019 .
```
### Run
Mac/Win
```shell
docker run -it --rm <USER>/cheers2019
```
### Ship
Mac
```shell
docker login && docker push <USER>/cheers2019
```
Win
```shell
docker login ; docker push <USER>/cheers2019
```

# Plugins VS
- Add New File
- AutoHistory
- Commentator
- Editor Guidelines
- EF 6.x EntityObject Generator for C#
- Productivity Power Tools
- Web Essentials
- ReSharper (Paid - Own compiler) or Code Cracker (Free and run over Roslyn compiler :D)
- WSCFblue [External]
