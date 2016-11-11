FROM microsoft/windowsservercore

RUN powershell -Command Add-WindowsFeature Web-Server

ADD ServiceMonitor.exe /ServiceMonitor.exe

CMD ["C:\\ServiceMonitor.exe", "w3svc"]
