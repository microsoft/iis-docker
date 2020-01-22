# escape=`
FROM mcr.microsoft.com/windows/servercore/insider:10.0.19035.1

RUN powershell -Command `
    Add-WindowsFeature Web-Server; `
    Invoke-WebRequest -UseBasicParsing -Uri "https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.6/ServiceMonitor.exe" -OutFile "C:\ServiceMonitor.exe"

RUN powershell -Command `
    New-Item -ItemType Directory C:\LogMonitor; `
    Invoke-WebRequest -UseBasicParsing -Uri "https://github.com/microsoft/windows-container-tools/releases/download/v1.0/LogMonitor.exe" -OutFile "C:\LogMonitor\LogMonitor.exe"; `
    Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/microsoft/iis-docker/master/windowsservercore-insider/LogMonitorConfig.json" -OutFile "C:\LogMonitor\LogMonitorConfig.json"

RUN c:\windows\system32\inetsrv\appcmd.exe set config  -section:system.applicationHost/sites /"[name='Default Web Site'].logFile.logTargetW3C:"File,ETW""  /commit:apphost

EXPOSE 80

SHELL ["C:\\LogMonitor\\LogMonitor.exe", "powershell.exe"]
ENTRYPOINT C:\ServiceMonitor.exe w3svc
