FROM microsoft/windowsservercore:ltsc2016

RUN powershell -Command Add-WindowsFeature Web-Server

ADD ServiceMonitor.exe /ServiceMonitor.exe

EXPOSE 80

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]
