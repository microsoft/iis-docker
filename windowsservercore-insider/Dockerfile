# escape=`

FROM mcr.microsoft.com/windows/servercore/insider:10.0.19035.1

# Install IIS, LogMonitor.exe and ServiceMonitor.exe
RUN powershell -Command `
    Add-WindowsFeature Web-Server; `
    New-Item -ItemType Directory C:\LogMonitor; `
    $downloads = `
    @( `
        @{ `
            uri = 'https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.6/ServiceMonitor.exe'; `
            outFile = 'C:\ServiceMonitor.exe' `
        }, `
        @{ `
            uri = 'https://github.com/microsoft/windows-container-tools/releases/download/v1.0/LogMonitor.exe'; `
            outFile = 'C:\LogMonitor\LogMonitor.exe' `
        }, `
        @{ `
            uri = 'https://raw.githubusercontent.com/microsoft/iis-docker/master/windowsservercore-insider/LogMonitorConfig.json'; `
            outFile = 'C:\LogMonitor\LogMonitorConfig.json' `
        } `
    ); `
    $downloads.ForEach({ Invoke-WebRequest -UseBasicParsing -Uri $psitem.uri -OutFile $psitem.outFile })

# Change the startup type of the IIS service from Automatic to Manual
RUN sc config w3svc start=demand

# Enable ETW logging for Default Web Site on IIS
RUN c:\windows\system32\inetsrv\appcmd.exe set config -section:system.applicationHost/sites /"[name='Default Web Site'].logFile.logTargetW3C:"File,ETW"" /commit:apphost

EXPOSE 80

# Start "C:\LogMonitor\LogMonitor.exe C:\ServiceMonitor.exe w3svc"
ENTRYPOINT ["C:\\LogMonitor\\LogMonitor.exe", "C:\\ServiceMonitor.exe", "w3svc"]
