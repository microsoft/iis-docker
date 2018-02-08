FROM microsoft/nanoserver:sac2016

RUN powershell -NoProfile -Command \
    New-Item -Type Directory C:\install \
    Invoke-WebRequest https://az880830.vo.msecnd.net/nanoserver-ga-2016/Microsoft-NanoServer-IIS-Package_base_10-0-14393-0.cab -OutFile C:\install\Microsoft-NanoServer-IIS-Package_base_10-0-14393-0.cab \
    Invoke-WebRequest https://az880830.vo.msecnd.net/nanoserver-ga-2016/Microsoft-NanoServer-IIS-Package_English_10-0-14393-0.cab -OutFile C:\install\Microsoft-NanoServer-IIS-Package_English_10-0-14393-0.cab \
    dism.exe /online /add-package /packagepath:c:\install\Microsoft-NanoServer-IIS-Package_base_10-0-14393-0.cab & \
    dism.exe /online /add-package /packagepath:c:\install\Microsoft-NanoServer-IIS-Package_English_10-0-14393-0.cab & \
    dism.exe /online /add-package /packagepath:c:\install\Microsoft-NanoServer-IIS-Package_base_10-0-14393-0.cab & \
    Remove-Item -Recurse C:\install\ ; \
    Invoke-WebRequest https://dotnetbinaries.blob.core.windows.net/servicemonitor/1342334/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe \
    Start-Service Was; \
    While ((Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\WAS\Parameters\ -Name NanoSetup -ErrorAction Ignore) -ne $null) {Start-Sleep 1}

EXPOSE 80

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]
