Welcome to the Admin Documentation
=================================
# Before you continue
This documentation is **correct** for you if you are not just trying to run the simlulation but want/need to...
- **Setup the host system** - Install Apptainer, Vulcan and a VNCServer. Setup the fakeroot Mapping. 
- **Rebuild the Container** - using the buildfile from scratch
- **Deploy the framework** - Onto a new computing cluster / node of a computing cluster
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
4. **Setup a Fakeroot mapping** - To allow non-root to have root permissions *inside* the container to allow packages etc. you will have to setup a mapping for the users in the following files using the schema ```<user_name>:<what_does_this_mean?>:<I_have_no_idea_right_now>```:
- ```/etc/subuid```
- ```/etc/subgid```

*Note: this is a process that may needs to be repeated if new users use the simulation. You only need a fakeroot mapping if you make changes to the simulation enviorment, so this process does not have to be done for every user. *


If you have executed all 4 instructions you can now start building the container using the buildfile

Build the Container 
---------------------
*Note: If there has already been an built container and no changes are necessary you can simply copy the existing container and skip this section*
This section describes how you can rebuild the container onto any system. To rebuild the container the following requirements have to be met:
1. You have a set-up host system (Refer to [Setting up your System](Link/to/h1)
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


*Note: You will need root permission or have an fakeroot mapping set on your system to run the buildfile. learn more about the fakeroot feature here [ToDo](ToDo)

Once you have downloaded the buildfile navigate to it and run 
```apptainer build --fakeroot <Container_Dir_Name> Buildfile.def``` or alternativly 
``` sudo apptainer build <Container_Dir_Name> Buildfile.def ```

If you've done everything correctly the buildfile should now start executing. The script takes about one to three hours to complete, depending on your system. 

## Testing the installation
There are different levels of tests, starting with the bare container, to using the container with VNC and an XServer to using the container with VNC and the persistent overlay from the project repository.

### Testing the bare container

Upon completing the installation you can verify it by running 

```mkdir test_ov && apptainer run --nv --overlay test_ov <Container_Dir_Name> ```

You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```

Run ```cd /opt/umd_simulation/carla``` and ```make launch```

After some time you should see the error that the display cannot be found. If this is the case the test is passed.

### Testing the Container using VNC

Upon completing the installation, run the VNCServer on the host system and connect to it with a remote computer.
When connected, run ```mkdir test_ov && apptainer run --nv --overlay test_ov <Container_Dir_Name> ```
You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```
Run ```cd /opt/umd_simulation/carla``` and ```make launch```
After some time you should see the UnrealEngine editor opening. If this is the case the test is passed.

### Testing the Container using VNC and persistent overlays

Upon completing the installation, run the VNCServer on the host system and connect to it with a remote computer.
When connected, clone the [carla_container](https://code.ovgu.de/steup/carla_container) repository if you have not already.
Run ```apptainer run --nv --overlay carla_container/Overlay_opt <Container_Dir_Name> ```
*Note: Depending on your installation, the* ```Overlay_opt``` *directory may be in the same folder as your container.*
You should now be in the apptainer container, noticeable by the Prefix ```Apptainer>```
Run ```cd /opt/umd_simulation/carla``` and ```make launch```
After some time you should see the UnrealEngine editor opening. Open a terminal in the container and run ```python3 /opt/umd_simulation/carla/PythonAPI/dummyscript.py```
If the file has been found everything has been installed correctly. 
