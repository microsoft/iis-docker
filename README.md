![IIS Docker Image](https://avatars2.githubusercontent.com/u/6154722?v=3&s=200)
# IIS Docker Image

NOTE: This is a Windows container image. [Learn more about Windows containers](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview).

## Supported tags and respective `Dockerfile` links

* servercore, latest [servercore/Dockerfile](https://github.com/microsoft/iis-docker/blob/master/servercore/Dockerfile)

This image is built from the [microsoft/iis-docker GitHub repo](https://github.com/microsoft/iis-docker).

## What is IIS?
Internet Information Services (IIS) for Windows® Server is a flexible, secure and manageable Web server for hosting anything on the Web.

## How to use this image?
### Create a Dockerfile with your website
```
FROM microsoft/iis

RUN mkdir C:\site

RUN powershell -NoProfile -Command \
    Import-module IISAdministration; \
    New-IISSite -Name "Site" -PhysicalPath C:\site -BindingInformation "*:8000:"

EXPOSE 8000

ADD content/ /site
```
You can then build and run the Docker image:
```
$ docker build -t iis-site .
$ docker run -d -p 8000:8000 --rm --name my-running-site iis-site
```

There is no need to specify an `ENTRYPOINT` in your Dockerfile since the `microsoft/iis` base image already includes an entrypoint application that monitors the status of the IIS World Wide Web Publishing Service (W3SVC).


In addition to static content, IIS can run other workloads including, but limited to ASP.NET, ASP.NET Core, PHP, and Apache Tomcat.
Check out [ASP.NET on DockerHub](https://hub.docker.com/microsoft/aspnet/) to learn how to run ASP.NET workloads on top of IIS.

## Supported Docker Versions
This image has been tested on Docker Versions 1.12.1-beta26 or higher.

## License
MICROSOFT SOFTWARE SUPPLEMENTAL LICENSE TERMS

CONTAINER OS IMAGE

Microsoft Corporation (or based on where you live, one of its affiliates) (referenced as “us,” “we,” or “Microsoft”) licenses this Container OS Image supplement to you (“Supplement”). You are licensed to use this Supplement in conjunction with the underlying host operating system software (“Host Software”) solely to assist running the containers feature in the Host Software. The Host Software license terms apply to your use of the Supplement. You may not use it if you do not have a license for the Host Software. You may use this Supplement with each validly licensed copy of the Host Software.

## User Feedback
If you have any issues or concerns, reach out to us through a [GitHub issue](https://github.com/Microsoft/iis-docker/issues/new).