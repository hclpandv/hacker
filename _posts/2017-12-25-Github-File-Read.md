---
title: How to read or extract data from a csv file kept on a github repository? 
published: true
---

Wonder!!! Yes, We are expecting to read the csv file which is kept on a github repository.  
This is very common now a days to keep the files in github repository and a Windows powershell users can install git for windows and then clone and entire repository localy.  
  
However, here we are trying to read directly from the github file. Solution to this challenge is hidden in the feature of github which allows you to interact with github repository using RestFull api service.  
The modern Powershell versions have `Invoke-RestMethod` however, from v3.0 Onwards we had `Invoke-WebRequest`  
  
I am using a very simple example where the file is kept in public repository, hence the authentication will not be a constraint, so I will first use the `Invoke-WebRequest` which is actually pulling the data over a simple http request however, you should be smartly calling the https://raw.githubusercontent.com which uses the REST Api service to produce the csv content over http.  
  
Alternatively `Invoke-RestMethod` can be used specialy if you have kept the file on a private github repository and you have your credential or api key to access. Invoke-RestMethod will provide you parameters to pass on Cred or Api Keys. (play with it to achive desired results)  
Below is snippet of a working code.

```powershell
#NOTE: Remember to use raw code url i.e. https://raw.<your github path>
$csv = "https://raw.githubusercontent.com/hclpandv/psbootcamp-temp/master/users.csv"
Invoke-WebRequest $csv | ConvertFrom-Csv 
#Or
Invoke-RestMethod -Method GET -Uri $csv
}
```

The output will be produced as:  
```

FirstName      : SQL
LastName       : Install Account
SamAccountName : sqlinstall
Title          : Service Account
Manager        : 

FirstName      : Amit
LastName       : Shukla
SamAccountName : ashukla
Title          : Application Packager
Manager        : TBD

FirstName      : Akhilendra
LastName       : Pandey
SamAccountName : apandey
Title          : Application Packager
Manager        : TBD

FirstName      : Vikas
LastName       : Pandey
SamAccountName : vpandey
Title          : PsBootcamp Admin
Manager        : TBD

FirstName      : Ashwani
LastName       : Kumar
SamAccountName : akumar
Title          : PsBootcamp Admin
Manager        : TBD

FirstName      : Md
LastName       : Mobin
SamAccountName : mmobin
Title          : PsBootcamp Admin
Manager        : TBD

.......
.......

```
