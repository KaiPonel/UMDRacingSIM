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

If your system fullfills these requirements you can now build the container from scratch using our buildfile. You can obtain the buildfile by cloning this repo or manually downloading it here: [Buildfile.def] (link/to/BuildFile)

Once you have downloaded the buildfile open it using the editor of your choice.






*Note: You will need root permission or have an fakeroot mapping set on your system to run the buildfile. learn more about the fakeroot feature here [ToDo](ToDo)

Once you have downloaded the buildfile navigate to it and run 
```apptainer build --fakeroot <Container_Dir_Name> Buildfile.def``` or alternativly 
``` sudo apptainer build <Container_Dir_Name> Buildfile.def ```


