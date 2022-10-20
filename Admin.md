Welcome to the Admin Documentation
=================================
Before you continue
-------------------
This documentation is **correct** for you if you are not just trying to run the simlulation but want/need to...
- **Setup the host system** - Install Apptainer, Vulcan and a VNCServer. Setup the fakeroot Mapping. 
- **Rebuild the Container** - using the buildfile from scratch
- **Test the installation** - Onto a new computing cluster / node of a computing cluster
- **Update Carla or UnrealEngine** - to get access to new features / bugfixes

If this is not the case, please refer to the [Mainpage](README.md) or the [User Documentation](User.md)

Setting up the host system
--------------------------
This section describes what needs to be done on the host system to allow the framework to be deployed.

To be able to install/deploy our container you will need to complete the following steps on the host system:
1. **Install Apptainer/Singularity** [Website](https://apptainer.org/), [Github](https://github.com/apptainer/apptainer)
2. **Install Vulcan** [Website](https://developer.nvidia.com/vulkan-driver)
*Note: Upon completing the installation the file ```/usr/share/vulkan/icd.d/nvidia_icd.json``` needs to exist on the host system. Otherwise the buildfile will not execute.*
3. **Install a VNCServer** e.g. [TigerVNC](https://tigervnc.org/) or [TightVNC](https://www.tightvnc.com/download.php)
4. **Setup a Fakeroot mapping** - To allow non-root to have root permissions *inside* the container to allow packages etc. you will have to setup a mapping for the users in the following files using the schema ```<user_name>:<uid>:<uid>```:
- ```/etc/subuid```
- ```/etc/subgid```

*Note: this is a process that may needs to be repeated if new users use the simulation. You only need a fakeroot mapping if you make changes to the simulation enviorment, so this process does not have to be done for every user.*


If you have executed all 4 instructions you can now start building the container using the buildfile

Build the Container 
---------------------
*Note: If there has already been an built container and no changes are necessary you can simply copy the existing container and skip this section*
This section describes how you can rebuild the container onto any system. To rebuild the container the following requirements have to be met:
1. You have a set-up host system (Refer to [Setting up your System](https://github.com/KaiPonel/UMDRacingSIM/blob/main/Admin.md#setting-up-the-host-system)
2. You have a Github Account
3. You have access to the [project repository](https://code.ovgu.de/steup/carla_container)

If your system fullfills these requirements you can now build the container from scratch using our buildfile. You can obtain the buildfile by cloning this repo or manually downloading it here: [Buildfile.def] (link/to/BuildFile)

Before you can use the buildfile you will have to add your github credentials to it and link your github account with the EpicGames, the owners of UnrealEngine. To link your accounts please refer to [this guide](https://www.epicgames.com/help/en-US/epic-accounts-c5719348850459/connect-accounts-c5719351300507/how-do-i-link-my-unreal-engine-account-with-my-github-account-a5720369784347). 
Since Github does no longer allow password authentication on HTTPS cloning you will also need to generate a private access token for your account, following [this guide](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). 

Once you linked your accounts and generated a private access token open the buildfile using an editor of your choice. 
Scroll down a bit until you see these lines:
```
#IMPORTANT: Add your GitHub credentials before running! Otherwise it will break here - obviously ;)
git clone --depth 1 -b carla https://{github_username}:{github_private_access_token}@github.com/CarlaUnreal/UnrealEngine.git /opt/umd_simulation/unreal_engine
```
Use your github account name as ```{github_username}``` and your just generated access token as ```{github_private_access_token}```. You can now close the file.


*Note: You will need root permission or have an fakeroot mapping set on your system to run the buildfile. [Setting up the simulation accordingly](https://github.com/KaiPonel/UMDRacingSIM/blob/main/Admin.md#setting-up-the-host-system) and learn more about the fakeroot in the [Apptainer documentation](https://apptainer.org/docs/user/1.0/fakeroot.html) 

Once you have downloaded the buildfile navigate to it and run 
```apptainer build --fakeroot <Container_Dir_Name> Buildfile.def``` or alternativly 
``` sudo apptainer build <Container_Dir_Name> Buildfile.def ```

If you've done everything correctly the buildfile should now start executing. The script takes about one to three hours to complete, depending on your system. 

Testing the installation
----
There are different levels of tests, starting with the bare container, to using the container with VNC and an XServer to using the container with VNC and the persistent overlay from the project repository.

## Testing the bare container

Upon completing the installation you can verify it by running 

1. ```mkdir test_ov && apptainer run --nv --overlay test_ov <Container_Dir_Name> ```
You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```

2. Run ```cd /opt/umd_simulation/carla``` and ```make launch```
After some time you should see the error that the display cannot be found. If this is the case the test is passed.

## Testing the Container using VNC

Upon completing the installation, run the VNCServer on the host system and connect to it with a remote computer.

1. When connected, run ```mkdir test_ov && apptainer run --nv --overlay test_ov <Container_Dir_Name> ```
You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```

2. Run ```cd /opt/umd_simulation/carla``` and ```make launch```
After some time you should see the UnrealEngine editor opening. If this is the case the test is passed.

## Testing the Container using VNC and persistent overlays

Upon completing the installation, run the VNCServer on the host system and connect to it with a remote computer.

1. When connected, clone the [carla_container](https://code.ovgu.de/steup/carla_container) repository if you have not already.

2. Run ```apptainer run --nv --overlay carla_container/Overlay_opt <Container_Dir_Name> ``` <br/>
*Note: Depending on your installation, the* ```Overlay_opt``` *directory may be in the same folder as your container.*
You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```

3. Run ```cd /opt/umd_simulation/carla``` and ```make launch```

4. After some time you should see the UnrealEngine editor opening. Open a terminal in the container and run <br/>```python3 /opt/umd_simulation/carla/PythonAPI/dummyscript.py```
If the file has been found and the UnrealEngine editor opened, this test is passed. 

Updating the Container
----------------------
There may be new releases of CARLA in the future to update to. In order to do so you need to modify the buildfile.
Our Carla installation is based on this guide: [Build Carla on Linux](https://carla.readthedocs.io/en/latest/build_linux/)

This is our buildfile for Carla version 0.9.12:

```
Bootstrap: docker
From: ubuntu:20.04

%files
	/usr/share/vulkan/icd.d/nvidia_icd.json

%post
	DEBIAN_FRONTEND=noninteractive
	apt-get update && apt-get install -y gnupg2 tzdata keyboard-configuration
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 15CF4D18AF4F7421
  
	apt-get update &&
	apt install -y ubuntu-desktop-minimal # Desktop install needed for Graphic Support
  
  # CARLA-START
  
	apt-get update &&
	apt-get install -y wget software-properties-common &&
	add-apt-repository ppa:ubuntu-toolchain-r/test &&
	wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add - &&
	apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main" &&
	apt-get update
	apt-add-repository "deb http://apt.llvm.org/focal/ llvm-toolchain-focal main"
	apt-get install -y build-essential clang-8 lld-10 g++-7 cmake ninja-build libvulkan1 python python-dev python3-dev python3-pip libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev git
	update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-10/bin/clang++ 100 &&
	update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-10/bin/clang 100
	update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-8/bin/clang++ 180 &&
	update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-8/bin/clang 180
	pip3 install --upgrade pip
	pip install --user setuptools &&
	pip3 install --user -Iv setuptools==47.3.1 &&
	pip install --user distro &&
	pip3 install --user distro &&
	pip install --user wheel &&
	pip3 install --user wheel auditwheel

	mkdir /opt/umd_simulation
	
	#IMPORTANT: Add your GitHub credentials before running! Otherwise it will break here - obviously ;)
	git clone --depth 1 -b carla https://{github_username}:{github_private_access_token}@github.com/CarlaUnreal/UnrealEngine.git /opt/umd_simulation/unreal_engine
	cd /opt/umd_simulation/unreal_engine
	./Setup.sh && ./GenerateProjectFiles.sh && make

	cd /opt/umd_simulation
	git clone https://github.com/carla-simulator/carla /opt/umd_simulation/carla
	cd /opt/umd_simulation/carla
	./Update.sh
	export UE4_ROOT=/opt/umd_simulation/unreal_engine 
	make PythonAPI
  
  # CARLA-END
	
	chmod -R o+rwx /opt/umd_simulation
	chmod o+w /opt
```

The section between the "CARLA-START" and "CARLA-END" comments is basically copied from the [installation instructions](https://carla.readthedocs.io/en/latest/build_linux/) as mentioned above. If there has been a new version of Carla look for changes and modify the buildfile accordingly. 
