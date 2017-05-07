# Dockerfile for noVNC

This repository provides the base image of noVNC.  

# Run (Simple)

You can run this image as follows.

```bash
$ docker run -it --rm -p 8080:8080 uphy/novnc-alpine
```

Please extend this image and install the GUI apps you want,
because there's no applications installed in this image.

# Run (With your apps)

For example, you can run 'xterm' on the docker container and provide the app in the browser as follows.

Create your Dockerfile like below.

```Dockerfile
FROM uphy/novnc-alpine
RUN \
    # Install xterm
    apk add xterm && \
    # Append xterm entry to supervisord.conf
    cd /etc/supervisor/conf.d && \
    echo '[program:xterm]' >> supervisord.conf && \
    echo 'command=xterm' >> supervisord.conf && \
    echo 'autorestart=true' >> supervisord.conf
```

Build and run the image.

```bash
$ docker build -t mynovnc .
$ docker run -it --rm -p 8080:8080 mynovnc
```

Open the browser http://localhost:8080.  
Click 'Connect'.  
Then you can see xterm.