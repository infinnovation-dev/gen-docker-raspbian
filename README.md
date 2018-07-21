# gen-docker-raspbian

This project contains a script for generating a Raspbian filesystem
tarball which can be used as the basis of a docker image.

It is based closely on [schachr/docker-raspbian-stretch](https://github.com/schachr/docker-raspbian-stretch)

Under the hood, it uses 'debootstrap', applying some tweaks to make it
more suitable for using in a docker environment.

## Building an image

### Pre-requisites
- A Raspberry Pi, with the following packages installed:
  - debootstrap
- This repository, e.g. cloned from github

### Procedure

```sh
sudo ./mkimage-raspbian.sh stretch
```

All being well, it should create the file raspbian-stretch.image.tar.xz

Note that you can replace 'stretch' with an earlier version such as
'jessie' or 'wheezy' if you need.

## Next steps

Create a directory containing the image and a Dockerfile such as this

```Dockerfile
FROM scratch
ADD raspbian-stretch.image.tar.gz /

ENV DEBIAN_FRONTEND noninteractive
```

then

```sh
docker build -t raspbian-stretch .
```
