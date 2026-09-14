i.MX Repo Manifest README
=========================

This repo is used to download manifests for the MR-NAVQ95 BSP releases.

Specific instructions reside in READMEs in each branch.

The branch name is based on the release type and the Yocto Project release name, with manifests in each branch tied to the base BSP release.

For example, for i.MX Linux BSP releases based on Yocto Project `Wrynose`, the branch is `robotics-0.7.0`.

Install the `repo` utility:
---------------------------

To use this manifest repo, the `repo` tool must be installed first.

```
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
chmod a+x ~/bin/repo
PATH=${PATH}:~/bin
```

Install essential host packages
------------------------------
Your Build Host must install required packages for the Yocto build.
Reference to the section "Build Host Packages" in the document "Yocto Project Quick build".
- https://docs.yoctoproject.org/6.0/brief-yoctoprojectqs/index.html#build-host-packages

Download the Yocto Project BSP
------------------------------

```
mkdir <release>
cd <release>
repo init -u https://github.com/nxp-robotics/robotics-linux-manifest.git -b <branch name> [ -m <release manifest>]
repo sync
```

Examples
--------

To download the 0.7.0 release:

```
repo init -u https://github.com/nxp-robotics/robotics-linux-manifest.git -b robotics-0.7.0 -m imx-6.18.20-2.0.0_wrynose.xml
```

Setup the build folder for the MR-NAVQ95 BSP release:
-----------------------------------------

```
MACHINE=imx95-navqdesktop DISTRO=imx-desktop-xwayland source ./imx-setup-release.sh -b build
```

Build the image:
---------------

```
bitbake <image recipe>
```

Supported images:

Image Name           | Description
---------------------|-----------------------
imx-image-robotics   | Desktop PoC image
