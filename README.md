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
