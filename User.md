Welcome to the User Documentation
=================================
# Before you continue
This documentation is **correct** for you if you have access to Carla already (either locally or on the Cluster of the OVGU) and want to do the following things:
- **Start Working** - Start the Container upon getting access to the Cluster. 
- **Write Scripts** - Creating an actual simulation using python scripts.
- **Manage Maps** - Import, Create, Delete or Change maps.
- **Manage vehicles** - Import, Create, Delete or Change Vehicles.

If this is not the case, please refer to the [Mainpage](README.md) or the [Admin Documentation](Admin.md)

# Start Working
## Quickstart
1. **Install a VNC-Client** - Install a VNC Client of your choice. Popular Client are (INSERT VNC CLIENTS (WITH TESTED))
2. **Install a VPN** - In order to access the cluster you may have to use a VPN (DONT KNOW IF THIS IS THE CASE). Please refer to [OVGU - VPN ACCESS](https://www.urz.ovgu.de/vpn-path-204,616.html) for more information. After installation, start the client. 
3. **Connect via SSH** - After activating the VPN connect to the Cluster using ssh. You can do this using the following command (TODO: COMMAND UPDATE): ```ssh <username>@ants.cs.ovgu.de``` <br/>*Upon entering the command you will be asked for a password. The password is your URZ password (the same you use for moodle or the lsf)* <br/>
4. **Start a Container** - Upon being connected via SSH use ```cd path/to/workdir ``` to open the working directory (INSERT OVERLAY CREATE STEP?). Following that you can start the container by typing ```apptainer run --nv --overlay <overlay> <container_name>``` <br/> If everything went accordingly you should see that your bash user is now "Apptainer"<br/>
5. **Open a VNC Connection** - On your own system, open your VNCClient and enter the following command: ```<vnc connnect command to be inserted>```
6. **Login** - If the connection was successful you should see an Gnome Login screen. Enter your URZ Credentials to continue.
7. **Start Carla** - Navigate to the working directory in the container using ```cd path/to/working_dir_in_container``` and start carla using ```make launch``` <br/> Note: This process might take a while (on the first launch approximately 20 minutes). If you did everything correctly you should now see an UnrealEngine V4 Editor.

## Troubleshooting
This is ToDo - Maybe also just expand the Quickstart Section and make it more detailed.

# Manage Maps
## Create new Maps

To add a new map in Carla (or Unreal Engine), we use the [Roadrunner](https://de.mathworks.com/products/roadrunner.html) software from MathWorks. <br/>
You need a license for this software. The OVGU has a MathLab license, but Roadrunner is not included in this license. <br/>
To get this license, you have to contact [URZ](https://www.urz.ovgu.de/MATLAB.html).) <br/>

Tips for installing Roadrunner:
[here](https://de.mathworks.com/help/roadrunner/ug/install-and-activate-roadrunner.html?s_tid=srchtit)

Now that you have a license, install Roadrunner as described above (link). Remember that your computer must be logged in!

![licenses](./docs/source/images/licenses.png)

Quick links: 
- [Tutorials](https://de.mathworks.com/videos/search.html?q=&fq[]=product:RD&page=1)
- [Roadrunner Documentation](https://de.mathworks.com/help/roadrunner/index.html)

Once you have successfully installed Roadrunner, create a new project by creating a new Scene.

![RoadrunnerHomepage](./docs/source/images/RoadrunnerHomepage.png)
 

### Most important tools in Roadrunner:

![Item 1](./docs/source/images/rrItem1.png)

With this tool you can easily drag roads by right-clicking, the design of the road can be selected at the bottom right (Library Browser/RoadStyles) (Hint: first select the design and then drag the roads).

![Item 2](./docs/source/images/rrItem2.png)

With these two tools you can customize the width of the road. Also, once you have customized a road design to your own liking, you can save it and reuse it at a later time.

![Item 3](./docs/source/images/rrItem3.png)

With this tool you can connect two roads.

![Item 4](./docs/source/images/rrItem4.png)

This allows you to specify a surface (off the road). The default is lawn, but this can be easily changed by drag and drop (just drag a material (Library Browser) into the specified area.

![Item 5](./docs/source/images/rrItem5.png)

With this tool you can add single object. Select an object (Library Browser/Props/...) and position it by right-clicking.

![Item 6](./docs/source/images/rrItem6.png)

This tool is very handy when you need to add several objects with the same distance. As with the tool above, select the object to be added. On the right side an attribute window will open where you can specify the distance between the objects.


### Adding objects that do not yet exist

If you want to add object which is not included in the Library Browser of Roadrunner, you can simply add the .fbx file to the file path (C:UsersUSERSPEICHERORT_DES_PROJEKTESAssets).

Sometimes there can be problems with the alignment of the added object. Either you rotate your object again and add it to the Library Browser again or you rotate the object manually in Roadrunner.

### Export map from Roadrunner

File => Export => CARLA (.fbx / .xodr / .rrdata.xml)

Unfortunately, the position of the track is not so easy to read from the export. If you need this, I recommend the export with Apollo (.xml / .bin), because there in the XML file the positions of the left and right side, as well as the position of the center of the track is easy to read (I would write a small Python script to get the coordinates, then goes faster than to write them out).

### Import into Carla

To import your map into the carla simulation please refer to the official guide from the [Carla Documentation](https://carla.readthedocs.io/en/0.9.7/how_to_make_a_new_map/) (Section 3 onwards). 

--- 
## Modify Maps:
To Modify the layout of the map, import the map into Roadrunner and follow the steps from the [Create Maps Section](createMap.md) <br/>
To add Props to an existing maps please refer to the [CARLA Documentation](https://carla.readthedocs.io/en/latest/tuto_A_add_props/)
---
## Delete Maps:
(Insert: Folders to delete by User)
--- 
# Manage Vehicles
## Create a new Vehicle
- To Create a new Vehicle please refer to the [CARLA Documentation](https://carla.readthedocs.io/en/latest/tuto_A_add_vehicle/)
### Know Problems Adding a Vehicle
- Insert: Problem with Bones

## Adjust existing Vehicles
- Insert: files where important information regarding vehicle Parameters is located
- Insert: Option to modify Vehicle Parameters using scripts.

# Write Scripts
1. Open a new terminal in your VNC Session and navigate to the folder where carla is located using ```cd /home/carla/carla```
2. Navigate to the PythonAPI/Examples using ```cd /PythonAPI/Examples```
3. Copy the dummyscript to have something to start with using ```cp ./dummy_script.py <desired_path/script_name>.py```
4. Navigate to the directory you copied your script to and open it using ```code <script_name>```
5. Write some code
6. Deploy a map in the UnrealEngine Editor (in the top-right corner). Once the server is started execute your script in bash. 

- ToDo: Could be more Precise. Add Information where Deploy button in UE4 is located - Overall: add more images!!
