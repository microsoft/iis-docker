# PHP On IIS

## What is PHP

PHP (PHP: Hypertext Processor) is a server side scripting language as well as web framework that can be used to develop applications ranging from simple to complex.

## Getting Started

To add a PHP application into the container, first put the application content into a folder named _content_ and then append the following commands to the dockerfile located within this directory

```Dockerfile
# PHP dockerfile
# The content of the docker file will be here
# Add your content below

WORKDIR /inetpub/wwwroot

COPY ./content .
``` 

You can then build the image:

```
docker build -t iis-php .
docker run -d -p 80:80 --name my-php-site iis-php
```

## Testing PHP

To test the PHP functionality of the container without the need for a PHP application uncomment the following _RUN_ line within the docker file

```
# Optional: Add a starter page
# RUN powershell.exe -Command "'<?php phpinfo(); ?>' | Out-File C:\inetpub\wwwroot\phpinfo.php" -Encoding UTF8
```

Once the container is running, navigate to http://\<container host name\>/phpinfo.php

The generic php info page should be returned from the container. This verifies that PHP is functioning as expected.
