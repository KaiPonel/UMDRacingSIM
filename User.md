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
4. **Start a Container** - Upon being connected via SSH use <br/> ```cd path/to/workdir ``` <br/> to open the working directory (INSERT OVERLAY CREATE STEP?). Following that you can start the container by typing <br/> ```apptainer run --nv --overlay <overlay> <container_name>``` <br/> If everything went accordingly you should see that your bash user is now "Apptainer"<br/>
5. **Open a VNC Connection** - 
# Manage Maps

# Manage Vehicles

# Write Scripts
