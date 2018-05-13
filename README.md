# Lora packages feed

## Description
The collection of packages for OpenWrt that contains libraries, applications, tests, etc. for lora network.

## Usage
To use these packages, add the following line to the feeds.conf
in the OpenWrt buildroot:

```
src-git lora https://github.com/toxxin/openwrt-lora-feed.git
```

To install all its package definitions, run:

```
./scripts/feeds update lora
./scripts/feeds install -a -p lora
```

The lora network packages should now appear in menuconfig.
