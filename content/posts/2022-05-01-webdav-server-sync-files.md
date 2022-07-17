---
title: WebDAV server to synchronize files
date: 2022-05-01
tags: [tutorial, webdav]
---

I have been using [Orgzly](https://github.com/orgzly/orgzly-android)
for managing tasks and taking notes on my mobile device. Sometimes, I
need notes taken in Orgzly app on my laptop. Hence I was looking for
different methods to synchronize org files from Orgzly to my
laptop. Orgzly has provided an option to create repository to sync
files to it. Currently app has support for local storage and WebDAV
repositories.

[WebDAV](https://en.wikipedia.org/wiki/WebDAV) is an extension of HTTP
protocol to manage files on the server. It provides methods like COPY,
MOVE, PROPFIND, LOCK, UNLOCK etc. to work on files.

To synchronize files to my laptop, I need to start a WebDAV server on
my laptop. Different web servers like Nginx, Apache HTTP server, Caddy
has support to start a WebDAV server. I choose Caddy to create WebDAV
server because it is easy and I have used Caddy before.

## Start WebDAV server using Caddy

Caddy application can extend using other Caddy modules. [Caddy webDAV
module](https://github.com/mholt/caddy-webdav) is required to
implement simple webDAV. You can use following Dockerfile to build an
caddy-webdav image using
[xcaddy](https://github.com/caddyserver/xcaddy).

```Dockerfile
FROM caddy:2.5.0-builder AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-webdav@f7b67f8ca1e655103bbe7a96577c88fe96f1dfb2

FROM caddy:2.5.0

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
```

Run command to build a Docker image:

```
docker build -t caddy-webdav:latest .
```

Note: I have already built and pushed a
[akshayg96/webdav-caddy](https://hub.docker.com/r/akshayg96/caddy-webdav)
image to use.

Now you need an Caddyfile for your webDAV configuration.

```
:8080

route {
	basicauth {
		<user> <hashed-password>
	}
	rewrite /orgzly /orgzly/
	webdav /orgzly/* {
		root orgzly
		prefix /orgzly
	}
	file_server
}
```

This will serve files under `<basepath-of-caddyfile>/orgzly/`
directory. One can generate hashed password using `caddy hash-password`
command.

Alternatively one can serve all folders and files instead of just
`orgzly` using below Caddyfile:

```
:8080

@get method GET

route {
	basicauth {
		<user> <hashed-password>
	}
	file_server @get browse
	webdav
}
```

Now run following command to start webdav-caddy server in the container:

```
docker run -d -p 8080:8080 \
    --name caddy-webdav \
    --restart always \
    -v $PWD/Caddyfile:/etc/caddy/Caddyfile \
    -v caddy_data:/data \
    -v $PWD:/srv \
    caddy-webdav:latest
```

## Test server using WebDAV client

GNOME Files does support for access webDAV files. For that, open Files
and go to Other Locations and add following address to connect to
webDAV.

```
dav://localhost:8080/orgzly
```

It will ask for username and password. Provided one that you used in
your Caddyfile. After successful authentication, you will be able to
get, read and write files under orgzly directory.

## Synchronize org files from Orgzly app

When your mobile phone and laptop are connected to a same network (or
if can access laptop from mobile) then, you'll be able to sync org
file from Orgzly to laptop.

Add repository in Orgzly with below URL:

```
webdav://<laptop-ip>:8080/orgzly/
```

Provide correct username and password and connect.

Now you can sync Orgzly Notebooks to your laptop as per the sync
policy you have set.

Note: If you have multiple repositories, you can set link for
notebooks.

## Bonus: Access webDAV files using mobile file manager

I use [Xplore](https://www.lonelycatgames.com/apps/xplore) as a file
manager on mobile. Xplore has option to add webDAV web storage. Once
you add webDAV storage in Xplore same way how we added repository in
Orgzly, you will be able to access files from laptop.
