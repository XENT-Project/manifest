XENT
-------

To get started with building, you'll need to get familiar with 
[Setup build environment](http://source.android.com/source/initializing.html )
[Git and Repo](http://source.android.com/source/using-repo.html ).

Getting Started:
----------------------
Installing Dependencies:

	sudo apt-get update
	sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python git openjdk-8-jdk ccache

Create the directories:

	mkdir ~/bin && PATH=~/bin:$PATH
	mkdir -p ~/xent

Install the repo command:
	
	curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo && chmod a+x ~/bin/repo

Config Git:

	git config --global user.name "Your Name"
	git config --global user.email "you@example.com"
	
To initialize:

	cd ~/xent
	repo init -u https://github.com/XENT-Project/manifest.git -b 9.0

To Sync:

	repo sync -f -c -j$(nproc --all)  --force-sync --no-clone-bundle --no-tags --optimized-fetch

Build:
-----------------------
Build XENT:
	
    source build/envsetup.sh && lunch
	make xent -j$(nproc --all)

Clean up:

	make clobber

Optional:
------------------------
Preparing a Compiler Cache:
	
	echo "export USE_CCACHE=1" >> ~/.bashrc
	ccache -M 50G

Configuring Jack:

	export ANDROID_JACK_VM_ARGS="-Xmx#g -Dfile.encoding=UTF-8 -XX:+TieredCompilation"
	./prebuilts/sdk/tools/jack-admin kill-server
	./prebuilts/sdk/tools/jack-admin start-server
