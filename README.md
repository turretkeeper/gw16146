# GW16146 OpenWrt packages

## Usage guide

In your OpenWrt toolchain, add the following line:
```
src-git gw16146 https://github.com/turretkeeper/gw16146.git
```

Then, run

```
./scripts/feeds update -a
./scripts/feeds install -a
```

The packages should be selectable in your `make menuconfig` after.
