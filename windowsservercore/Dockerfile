FROM microsoft/windowsservercore

RUN powershell -Command Add-WindowsFeature Web-Server

ADD ServiceMonitor.exe /ServiceMonitor.exe

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]