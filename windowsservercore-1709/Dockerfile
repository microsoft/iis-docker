FROM microsoft/windowsservercore:1709

RUN powershell -NoProfile -Command \ 
    Add-WindowsFeature Web-Server \
    Invoke-WebRequest https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.1/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe

EXPOSE 80

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]
