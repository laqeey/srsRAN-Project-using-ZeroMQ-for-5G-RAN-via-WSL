# srsRAN Project using ZeroMQ for 5G RAN via WSL

# srsRAN Project is Open Source RAN

 Open-source 4G and 5G software radio suites developed by [Software Radio Systems](https://www.srs.io/), and In this virtual project, we can use the ZeroMQ network library to transfer radio samples between applications and simulate the facilities of 5GC by constructing a virtual gNodeB.In this example, we use WSL to construct a virtual environment (Ubuntu system) in Windows for installation and configuration.

### Construct a Linux virtual system using Windows Subsystem for Linux (WSL) Install WSL:

1. Enable subsystems for Linux
Check whether the Windows function is turned on and the settings of Windows Subsystem for Liunx are turned on (if it is not turned on, you need to restart the computer after turning it on)
    
    Control Panel>Programs>Programs and Features>Turn Windows features on or off>Windows Subsystem for Linux
    
2. Open settings and turn Windows on developer mode
3. Open cmd administrator mode， Enable virtual machine functionality。
    
    ```jsx
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```
    
4. Download the Linux kernel update package：
    
    [https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
    
5. Set WSL2 as default version
    
    ```jsx
    —set-default-version 2
    ```
    
6.  Install the Linux distribution of choice
    
    Can go to Microsoft store to search for ubuntu installation.
    
    After opening, set the account and password
    
    Check whether the installation is successful in the cmd command interface, enter:
    
    ```jsx
    wsl -1 -v
    ```
    
    If (name >ubuntu) (state > running) (version > 2) appears, the installation is successful.
    

### Install required libraries, including ZeroMQ

1. Install dependencies
    
    Open a WSL terminal and run the following commands to install the required dependencies, including ZeroMQ:
    

```jsx
sudo apt update
```

```jsx
sudo apt install cmake make gcc g++ pkg-config libfftw3-dev libmbedtls-dev libsctp-dev libyaml-cpp-dev libgtest-dev libzmq3-dev
```

1. Clone srsRAN_Project:
    
    Use Git to clone the srsRAN_Project repository in WSL:
    
    ```jsx
    git clone [https://github.com/srsran/srsRAN_Project.git](https://github.com/srsran/srsRAN_Project.git)
    ```
    
2. Build the project:
    
    Go into the srsRAN_Project directory and create a build directory, then run the CMake and make commands to build the project:
    
    ```jsx
    cd srsRAN_Project
    mkdir build
    cd build
    cmake ../ -DENABLE_EXPORT=ON -DENABLE_ZEROMQ=ON -DAUTO_DETECT_ISA=OFF
    make -j$(nproc)
    ```
    
3. Create gNodeB configuration file:
    
    Edit the gNodeB configuration file according to your needs. You can use any text editor to edit the configuration file, 
    
    ```jsx
    wget https://docs.srsran.com/projects/project/en/latest/_downloads/a7c34dbfee2b765503a81edd2f02ec22/gnb_zmq.yaml
    ```
    
    ```jsx
    wget https://docs.srsran.com/projects/project/en/latest/_downloads/fbb79b4ff222d1829649143ca4cf1446/ue_zmq.conf
    ```
    
    Follow the link below to test the network
    
    [https://docs.srsran.com/projects/project/en/latest/tutorials/source/srsUE/source/index.html#zeromq-based-setup](https://docs.srsran.com/projects/project/en/latest/tutorials/source/srsUE/source/index.html#zeromq-based-setup)
