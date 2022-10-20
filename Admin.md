Welcome to the Admin Documentation
=================================
# Before you continue
This documentation is **correct** for you if you are not just trying to run the simlulation but want/need to...
- **Rebuild the Container** - using the buildfile from scratch
- **Deploy the framework** - Onto a new computing cluster / node of a computing cluster
- **Update Carla or UnrealEngine** - to get access to new features / bugfixes

If this is not the case, please refer to the [Mainpage](README.md) or the [User Documentation](User.md)


Rebuild the Container 
---------------------
*Note: If there has already been an built container and no changes are necessary you can simply copy the existing container and skip this section*
This section describes how you can rebuild the container onto any system. To rebuild the container the following requirements have to be met:
1. **Apptainer/Singularity** is installed on your host system.
2. **Vulcan** is installed and the ```nvidia_icd.json``` file is present in ```/usr/share/vulkan/icd.d/``` on your host system.
3. **Fakeroot mapping (/ root permissions)** - There either needs to exist a [fakeroot mapping](Link/To/Fakeroot/Explaination) for your account or you need to have root privileges. 
4. 

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
