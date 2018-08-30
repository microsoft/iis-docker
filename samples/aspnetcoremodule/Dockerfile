# escape=`

FROM microsoft/iis

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

#
# Download and install IIS Administration API
RUN `
  New-Item -Type Directory C:\Setup | Out-Null ; `
  Invoke-WebRequest 'https://download.microsoft.com/download/6/E/B/6EBD972D-2E2F-41EB-9668-F73F5FDDC09C/dotnet-hosting-2.1.3-win.exe' -UserAgent '' -OutFile C:/setup/dotnet-hosting-2.1.3-win.exe ; `
  $process = start-process -Filepath C:/setup/dotnet-hosting-2.1.3-win.exe -ArgumentList  @('/install', '/q', '/norestart', 'OPT_NO_RUNTIME=1', 'OPT_NO_SHAREDFX=1') -Wait -PassThru ; `
  `
  if ($process.ExitCode -ne 0) { `
    exit $process.ExitCode ; `
  } `
  Remove-Item -Force C:/setup/dotnet-hosting-2.1.3-win.exe
