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
[create new maps](createMap.md)

## Modify Maps:
To Modify the layout of the map, import the map into Roadrunner and follow the steps from the [Create Maps Section](createMap.md) <br/>
To add Props to an existing maps please refer to the [CARLA Documentation](https://carla.readthedocs.io/en/latest/tuto_A_add_props/)

## Delete Maps:
(Insert: Folders to delete by User)

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
