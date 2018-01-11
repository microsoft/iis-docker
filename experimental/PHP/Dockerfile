FROM microsoft/iis

#
# PHP 7.1 x64 running on IIS
#

ENV PHP C:\PHP

# Install VC Redist 14
ADD https://download.microsoft.com/download/6/A/A/6AA4EDFF-645B-48C5-81CC-ED5963AEAD48/vc_redist.x64.exe /vc_redist.x64.exe
RUN C:\vc_redist.x64.exe /quiet /install

# Install PHP
RUN powershell.exe -Command Invoke-WebRequest 'https://sourceforge.net/projects/phpinstallermsi/files/zip/php-7.1.7-nts-Win32-VC14-x64.zip/download' -UserAgent '' -OutFile C:\php.zip
RUN powershell -Command Expand-Archive -Path c:\php.zip -DestinationPath C:\PHP

# Install PHP wincache
RUN powershell.exe -Command Invoke-WebRequest 'https://sourceforge.net/projects/wincache/files/wincache-2.0.0/wincachewpi-2.0.0.8-7.1-nts-vc14-x64.exe/download' -UserAgent '' -OutFile C:\php_wincache.exe
RUN C:\php_wincache.exe /Q /C /T:C:\php_wincache_msi
RUN msiexec /a C:\php_wincache_msi\wincache71x64wpi.msi /qb TARGETDIR=C:\php_wincache_msi\extracted
RUN copy C:\php_wincache_msi\extracted\PFiles\php_wincache.dll c:\PHP\ext

# Enable required IIS Features
RUN powershell.exe -command Enable-WindowsOptionalFeature -Online -FeatureName IIS-CGI -All

# Configure IIS
RUN %windir%\system32\inetsrv\appcmd set config /section:system.webServer/fastCgi /+[fullPath='c:\PHP\php-cgi.exe']
RUN %windir%\system32\inetsrv\appcmd set config /section:system.webServer/handlers /+[name='PHP_via_FastCGI',path='*.php',verb='*',modules='FastCgiModule',scriptProcessor='c:\PHP\php-cgi.exe',resourceType='Either']
RUN %windir%\system32\inetsrv\appcmd set config -section:system.webServer/fastCgi /[fullPath='c:\PHP\php-cgi.exe'].instanceMaxRequests:10000
RUN %windir%\system32\inetsrv\appcmd set config -section:system.webServer/fastCgi /+[fullPath='c:\PHP\php-cgi.exe'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']
RUN %windir%\system32\inetsrv\appcmd set config -section:system.webServer/fastCgi /+[fullPath='c:\PHP\php-cgi.exe'].environmentVariables.[name='PHPRC',value='C:\PHP']

# Configure PHP
RUN copy C:\PHP\php.ini-production C:\PHP\php.ini

# Cleanup
RUN rmdir /Q /S C:\php_wincache_msi
RUN del /Q C:\php.zip

# Configure path
RUN setx PATH /M %PATH%;C:\PHP

# Optional: Add a starter page
# RUN powershell.exe -Command "'<?php phpinfo(); ?>' | Out-File C:\inetpub\wwwroot\phpinfo.php" -Encoding UTF8

#
# ADD any application content and perform any configuration below