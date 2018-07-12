# Mender Raspberrypi manifest

Install repo:

```
mkdir ~/bin
PATH=~/bin:$PATH
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

Create a directory for your `mender-raspberrypi` setup to live in and clone the
meta information.
```
$ mkdir mender-raspberrypi
$ cd mender-raspberrypi
$ repo init -u https://github.com/mirzak/mender-raspberrypi-manifest.git -b sumo
$ repo sync
```

Setup build environment.
```
$ export TEMPLATECONF=${PWD}/rpi-templates
$ . layers/poky/oe-init-build-env build
```

The template files that are in `rpi-templates` should contain
everything that is needed to build an image with integrates Mender.

**NOTE** Default `MACHINE` is set to `raspberrypi3`, adjust if you want to build
for another machine.

**NOTE!** You only need to export TEMPLATECONF the first time you setup the
environment. Subsequent usage only requires you to source `oe-init-build-env`.

Start baking!
```
$ bitbake rpi-basic-image
```
