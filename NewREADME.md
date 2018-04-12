Copyright 2016-2018 Storage Networking Industry Association (SNIA), USA. All rights reserved. For the full SNIA copyright policy, see [http://www.snia.org/about/corporate_info/copyright](http://www.snia.org/about/corporate_info/copyright)

Contributors that are not SNIA members must first agree to the terms of the SNIA Contributor Agreement for Non-Members:  [www.snia.org/cla](www.snia.org/cla)

----

# Swordfish-API-Emulator

The Swordfish API Emulator can emulate a Swordfish-based system that responds to create, read, update, and delete RESTful API operations to allow developers to model new Swordfish functionality, test clients, demonstrate Swordfish, and do other similar functions.

The Swordfish API Emulator extends the [DMTF Redfish Interface Emulator](https://github.com/DMTF/Redfish-Interface-Emulator) by adding code to an installation of the Redfish Interface Emulator code.

The Swordfish API Emulator code is maintained on GitHub by the SNIA, and the Redfish Interface Emulator code is maintained on GitHub by the DMTF.

----

## Prerequisites for the emulator

The Redfish Interface Emulator and the Swordfish API Emulator both require Python 3.6 or higher. If this is not already installed, go to www.python.org to download and install an appropriate version of Python.

It is recommended (but not required) to run the emulator using virtualenv, because it helps keep the emulator environment separate from other Python environments running on the same system. If this is not already installed, enter the following command into a command prompt window to install virtualenv after Python is installed: ```pip install virtualenv```

----

## Installing the Swordfish API Emulator on Windows

The Redfish Interface Emulator must be installed first, and then the Swordfish API Emulator must be installed on top of the Redfish Interface Emulator installation. This can be done on Windows using the sequence of steps given below. The steps for installing the emulator on Linux are similar.


### These installation steps assume the following:

- The prerequisites for the emulator have been installed and virtualenv is being used.
- The emulator is being installed in a folder named **SwordfishEmulator** in the Documents directory.
- The GitHub code for the Redfish Interface Emulator is in a folder named **RedfishCode**.
- The GitHub code for the Swordfish API Emulator is in a folder named **SwordfishCode**.


### Installation steps for the Redfish Interface Emulator:

(1) Open a command prompt window and create a virtualenv environment folder for the emulator in the Documents directory by entering the following commands:

```
cd Documents
virtualenv SwordfishEmulator
```

(2) Using the file explorer, go to the **RedfishCode** folder, select and copy all the files using ```Control-A``` and ```Control-C```, then go to the **SwordfishEmulator** folder and paste all the files into it using ```Control-V```. This can also be done using a drag-and-drop copying operation.

(3) In the command prompt window, enable the virtualenv environment, and install the Python packages required by the emulator by entering the following commands:

```
cd SwordfishEmulator
Scripts\activate
pip install setuptools markupsafe itsdangerous flask
pip install aniso8601 pytz flask_httpauth requests
pip install flask_restful StringGenerator==0.2.1 urllib3
```

(4) If desired, a simple installation test can now be run on the Redfish Interface Emulator by entering the following command in the command prompt window:

```
python emulator.py
```

Use a browser to access http://localhost:5000/redfish/v1/ on the system where the emulator has been installed. If the emulator is working properly, the Redfish service root should be displayed by the browser.

(5) If the emulator is running, cause it to stop by entering ```Control-C``` in the command prompt window.


### Installation steps for the Swordfish API Emulator

These steps should only be done after the Redfish Interface Emulator has been installed in the **SwordfishEmulator** folder. It is assumed that the virtualenv environment in the **SwordfishEmulator** folder is still activated in the command prompt window.

(1) Using the file explorer, go to the **SwordfishCode** folder, select and copy all the files using ```Control-A``` and ```Control-C```, then go to the **SwordfishEmulator** folder and paste all the files into it using ```Control-V```. This can also be done using a drag-and-drop copying operation.

(2) Windows will indicate that several files in the destination have the same names. Select the Windows “Replace the files in the destination” option.

(3) Using the file explorer, go to the **SwordfishEmulator\api_emulator\swordfish** folder, select and copy all the files using ```Control-A``` and ```Control-C```, then go to the **SwordfishEmulator\api_emulator\redfish** folder and paste all the files into it using ```Control-V```. This can also be done using a drag-and-drop copying operation.

(4) The Swordfish API Emulator can now be run in its default configuration by entering the following command in the command prompt window:

```
python emulator.py
```

As a simple installation test, use a browser to access http://localhost:5000/redfish/v1/ on the system where the emulator has been installed. If the emulator is working properly, the Redfish service root should be displayed on the browser, with two additional Swordfish resources added: StorageServices, and StorageSystems.

The Swordfish API Emulator should now be ready to use in its default configuration.

To stop the emulator, enter ```Control-C``` in the command prompt window, or close the command prompt window.

To exit the virtualenv environment after the emulator is stopped, enter ```deactivate``` in the command prompt window, or close the command prompt window.


### Restarting the emulator after exiting the virtualenv environment

To restart the emulator after exiting the virtualenv environment, or to run the emulator from a new command prompt window, do the following:

In a command prompt window, go to the **SwordfishEmulator** folder, then enter the following commands:

```
Scripts\activate
python emulator.py
```

To stop the emulator, enter ```Control-C``` in the command prompt window, or close the command prompt window.

To exit the virtualenv environment after the emulator is stopped, enter ```deactivate``` in the command prompt window, or close the command prompt window.

----

## Notes about the Swordfish API Emulator

- The [Redfish Interface Emulator *README.md* file](https://github.com/DMTF/Redfish-Interface-Emulator/blob/master/README.md) should be reviewed before working with the Swordfish API Emulator or changing the default configuration.

- The configuration of the overall emulator is controlled by the *emulator-config.json* file in the directory where the emulator is installed. (This is the *SwordfishEmulator* folder in the installation steps above.) Instructions for using this file can be found in the Redfish Interface Emulator *README.md* file.

- The Swordfish API Emulator code files generally do not overlap the Redfish Interface Emulator code files, but there are currently two files that must contain code for both the Redfish Interface Emulator and the Swordfish API Emulator:
  - *api_emulator\resource_manager.py*
  - *api_emulator\utils.py*

  The Redfish Interface Emulator files are maintained on GitHub by the DMTF.

  The Swordfish API Emulator files are maintained on GitHub by the SNIA.

- The *api_emulator\resource_manager.py* file controls which emulator resources are static and which emulator resources are dynamic. Create/Read/Update/Delete (CRUD) operations can be done on dynamic resources via the API using normal REST operations, but the static resources are read-only and cannot be changed via the API.

  The Swordfish resources in the emulator are dynamic, and most of the Redfish resources are also dynamic, but four Redfish resources are currently still static in the default configuration of the Redfish Interface Emulator:
  - TaskService
  - SessionService
  - AccountService
  - Registries

  These resources will remain static until the Redfish Interface Emulator is updated to make them dynamic.

- The static resources in the emulator are populated by placing appropriate JSON mockup folders into the *api_emulator\redfish\static* directory. Instructions for this can be found in the Redfish Interface Emulator “README.md” file. Note that the dynamic resources in the emulator are NOT populated or initialized by the mockups in this directory.

- The dynamic resources in the emulator can be populated via the API using Create/Read/Update/Delete (CRUD) operations, and they can also be pre-populated by creating an appropriate JSON file that describes the desired dynamic resources for the Redfish Interface Emulator’s INFRAGEN Module. Instructions for using the INFRAGEN Module can be found in the Redfish Interface Emulator *README.md* file.

- The current default configuration of the Redfish Interface Emulator pre-populates several of the Redfish dynamic resources. Instructions for starting the emulator without any pre-populated dynamic resources can be found in the Redfish Interface Emulator *README.md* file.

- Occasionally a ```Control-C``` in the command prompt window does not immediately stop the emulator. When this occurs, the emulator will stop as soon as another API access is attempted. A web browser can be used to access the Redfish service root to force this to happen, if no other REST client is readily available.

----
