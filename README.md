# BlackHole OS #

### To build BlackHole OS you’ll  need : ###

```bash

sudo apt-get install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev maven adb fastboot ccache repo --fix-missing

```

For Ubuntu versions older than 20.04 (focal), install also:

```bash

sudo apt-get install libwxgtk3.0-dev

```

While for Ubuntu versions older than 16.04 (xenial), install:
```bash

sudo apt-get install libwxgtk2.8-dev

```

### Create the directories ###
```bash
mkdir -p ~/bin
mkdir -p ~/android/blackhole
```
Install the repo command
```bass
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

```
Put the ~/bin directory in your path of execution
```bash

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

```
To update your environment.

```bash

source ~/.profile 

```

### Configure git ###

```bash

git config --global user.email "you@example.com"
git config --global user.name "Your Name"

```

### Turn on caching to speed up build ###

```bash
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache

```
set maximum cache size
```bash

ccache -M 50G

```

You can also enable the optional ccache compression.
```bash

ccache -o compression=true

```

### Sync ###

```bash

# Initialize local repository
repo init -u https://github.com/BlackHoleOS/manifest -b main

# Sync
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

### Build ###

```bash

# Set up environment
$ . build/envsetup.sh

# Choose a target
$ lunch aosp_$device-userdebug

# Build the code
$ m -j$(nproc --all)
