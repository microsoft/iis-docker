FROM microsoft/windowsservercore:10.0.14393.321

RUN powershell -Command Add-WindowsFeature Web-Server

ADD ServiceMonitor.exe /ServiceMonitor.exe

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]