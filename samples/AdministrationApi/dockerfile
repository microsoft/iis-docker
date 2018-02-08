# escape=`

FROM microsoft/iis

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

#
# Download and install IIS Administration API
RUN `
  New-Item -Type Directory C:\Setup | Out-Null ; `
  Invoke-WebRequest 'http://go.microsoft.com/fwlink/?LinkId=829373' -UserAgent '' -OutFile C:/setup/IISAdministrationSetup.exe ; `
  $process = start-process -Filepath C:/setup/IISAdministrationSetup.exe -ArgumentList  @('/install', '/q', '/norestart') -Wait -PassThru ; `
  `
  if ($process.ExitCode -ne 0) { `
    exit $process.ExitCode ; `
  }

COPY ["appsettings.json","api-keys.json", "C:/setup/"]

#
# Place configuration files
# Remove preparation files
RUN `
  $config = 'C:\Program Files\IIS Administration\' + (Get-ChildItem 'C:\Program Files\IIS Administration' | select -First 1).Name +  '\Microsoft.IIS.Administration\config' ; `
  icacls.exe $config /T /grant 'Administrators:(M)' ; `
  Copy-Item -Force 'C:/setup/appsettings.json' $config ; `
  Copy-Item -Force 'C:/setup/api-keys.json' $config ; `
  Remove-Item -Recurse -Force C:\setup ;

EXPOSE 55539
