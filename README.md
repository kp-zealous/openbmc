# OpenBMC new

[![Build Status](https://jenkins.openbmc.org/buildStatus/icon?job=latest-master)](https://jenkins.openbmc.org/job/latest-master/)

OpenBMC is a Linux distribution for management controllers used in devices such
as servers, top of rack switches or RAID appliances. It uses
[Yocto](https://www.yoctoproject.org/),
[OpenEmbedded](https://www.openembedded.org/wiki/Main_Page),
[systemd](https://www.freedesktop.org/wiki/Software/systemd/), and
[D-Bus](https://www.freedesktop.org/wiki/Software/dbus/) to allow easy
customization for your platform.

## Setting up your OpenBMC project

### 1) Prerequisite

See the
[Yocto documentation](https://docs.yoctoproject.org/ref-manual/system-requirements.html#required-packages-for-the-build-host)
for the latest requirements

#### Ubuntu

```sh
sudo apt install git python3-distutils gcc g++ make file wget \
    gawk diffstat bzip2 cpio chrpath zstd lz4 bzip2
```

#### Fedora

```sh
sudo dnf install git python3 gcc g++ gawk which bzip2 chrpath cpio \
    hostname file diffutils diffstat lz4 wget zstd rpcgen patch
```

### 2) Download the source

```sh
git clone https://github.com/openbmc/openbmc
cd openbmc
```

### 3) Target your hardware

Any build requires an environment set up according to your hardware target.
There is a special script in the root of this repository that can be used to
configure the environment as needed. The script is called `setup` and takes the
name of your hardware target as an argument.

The script needs to be sourced while in the top directory of the OpenBMC
repository clone, and, if run without arguments, will display the list of
supported hardware targets, see the following example:

```text
$ . setup <machine> [build_dir]
Target machine must be specified. Use one of:

bletchley               mori                    s8036
dl360poc                mtjade                  swift
e3c246d4i               mtmitchell              tatlin-archive-x86
ethanolx                nicole                  tiogapass
evb-ast2500             olympus-nuvoton         transformers
evb-ast2600             on5263m5                vegman-n110
evb-npcm750             p10bmc                  vegman-rx20
f0b                     palmetto                vegman-sx20
fp5280g2                qcom-dc-scm-v1          witherspoon
g220a                   quanta-q71l             witherspoon-tacoma
gbs                     romed8hm3               x11spi
greatlakes              romulus                 yosemitev2
gsj                     s2600wf                 zaius
kudo                    s6q
lannister               s7106
```

Once you know the target (e.g. romulus), source the `setup` script as follows:

```sh
. setup romulus
```

### 4) Build

```sh
bitbake obmc-phosphor-image
```

Additional details can be found in the [docs](https://github.com/openbmc/docs)
repository.

## Build openBmc qemu

steps to build qemu

#### step 1


```sh
apt-get install -y pkg-config
apt install ninja-build
apt install libglib2.0-dev
apt install build-essential libcairo2-dev libpango1.0-dev libjpeg-dev libgif-dev librsvg2-dev
apt-get install libvirt libvirt-bin bridge-utils uml-utilities qemu-system-common
```

Installing pkg-config package, ninja-build package, libglib2.0-dev package, libcairo2-dev libpango1.0-dev libjpeg-dev libgif-dev librsvg2-dev package and 
rt libvirt-bin bridge-utils uml-utilities qemu-system-common package on ubuntu

#### step 2

```sh
git clone https://github.com/openbmc/qemu.git
cd qemu
git submodule update --init dtc
mkdir build
cd build
../configure --target-list=arm-softmmu
make
```

Now clone the website and build a file 

#### step 3

Built file will be located at: ```sh arm-softmmu/qemu-system-arm```

This one is contributed by Krithika Priya.PR
