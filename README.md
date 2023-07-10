# OpenWrt Braiins OS Feed

## Description

This OpenWrt package feed contains packages for Braiins OS (BOS).

## Usage

This repository is intended to be layered on-top of an OpenWrt buildroot.
See the documentation at: [OpenWrt Buildroot - Installation][1] on the OpenWrt
support site.

This feed have to be enabled manually. Your feeds.conf.default (or feeds.conf)
must contain a line like:

```
src-git bos https://github.com/braiins/bos-packages.git
```

To install all its package definitions, run:

```
./scripts/feeds update bos
./scripts/feeds install -a -p bos
```

[1]: https://openwrt.org/docs/guide-developer/build-system/install-buildsystem
