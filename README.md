# Summary
Currently, webOS image build system is depended on Ubuntu. Linux users who usually use other distros, such as Fedora, Arch and so on could not build the image on their host for reasons, but one of them is the library dependencies. To provide the build system on any distros, dockerize it.


# Architecture
![Imgur](https://i.imgur.com/GmsKMGw.jpg)


# Tutorial
### 0. Clone the repository
```
$ git clone https://github.com/webosce/dockerize-build-system.git

$ cd dockerize-build-system
```

### 1. Make an image from Dockerfile
```
$ docker build --tag webos-base ubuntu-xenial/
```
It makes an image named ``webos-base`` by ``ubuntu-xenial/Dockerfile``.

### 2. Make a container from the image
```
$ docker run -i -t --network host --name webos -v /path/to/mountpoint:/home/webos/mpoint webos-base /bin/bash
```
``/path/to/mountpoint`` must be a path that point to an external storage which is 100GB and above.

If your distro causes an error of *SELinux* permission, add ``:Z`` flag in the end of ``-v`` like ``-v /path/to/mountpoint:/home/webos/mpoint:Z``. That is usually required on the distros related to Red Hat Linux.

### 3. Get ready to build
``~/mpoint`` is a mount point that ``/path/to/mountpoint`` must be mounted, but **webos** can do nothing since the point has been owned by root. Instead of it, run everything with ``sudo``.

To clone ``build-webos``,
```
$ sudo git clone https://github.com/webosce/build-webos.git
```

**webos** must be able to read/write files in the repository, chown it.
```
$ sudo chown -hR webos:webos build-webos
```

### 4. Go build
```
$ cd build-webos
```
