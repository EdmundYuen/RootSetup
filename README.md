# Root Setup
A rough guide for setting up Root on Windows machines (work in progress)

Before you begin, do consider if the following alternatives are adequate for your needs:
1. [The Swan Service](https://swan.web.cern.ch/): Online data analysis powered by Jupyter.
2. [VirtualBox](https://www.virtualbox.org/): Load a provided disk image with Root installed into a Virtual Machine.
3. [LXPLUS Service](http://information-technology.web.cern.ch/services/lxplus-service): You will probably be running your code on this anyway.


## Root for Windows

### Downloads
#### Root 5.34.36 (Windows Visual Studio 2013)
##### [Release 5.34/36 - 2016-04-05](https://root.cern/content/release-53436)  (Direct link: [root_v5.34.36.win32.vc12.exe](https://root.cern.ch/download/root_v5.34.36.win32.vc12.exe))

Most recent available build of ROOT for Windows.


#### Visual Studio Express 2013 for Windows Desktop with Update 5 (x86) - Web Installer (English)
##### [en_visual_studio_express_2013_for_windows_desktop_with_update_5_x86_web_installer_6815514.exe](https://my.visualstudio.com/Downloads?pid=1819)

_A Visual Studio Dev Essentials subscription is now required to access the above download. See [here](https://www.visualstudio.com/vs/older-downloads/) for more information._

Required to compile C++. Express version does not include the full set of developer tools for Visual Studio, but is sufficient for compiler functionality. Web installer.


### Installation
1. Install Visual Studio
    > (Launch after installation to check that the installation is working. Skip sign in. Initial launch might lag/Sign-in window is hidden.)

2. Install Root
    > (Choose 'Add ROOT to the system PATH for all users.' Default installation directroy = `C:\root_v5.34.36`)

3. Test Root by typing the following commands in Command Prompt
    > `root` (will fail if environment variables are not configured)   
    
    > `.q` (exits Root)

4. For command line C++ compiler functionality, launch cmd.exe from the following shortcut (auto runs vcvarsall.bat that sets up Visual Studio environment variables)
    > VS2013 x86 Native Tools Command Prompt (look in `C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\Tools\Shortcuts`)

5. Test compiler by building the provided Root tests
    > `cd C:\root_v5.34.36\test`
    
    > `nmake /f makefile.win32`(will fail saying w32pragma.h cannot be found if environment variables are not configured)

6. Benchmark
    > `C:\root_v5.34.36\test\stress.exe`

7. Modify cmd shortcut to start in your work directory
    > Shortcut properties > change the directory listed for 'Start in:'
    
8. Modify cmd shortcut to setup Root environmental variables
    > append the following `" && C:\root_v5.34.36\bin\thisroot.bat"` to the target to run thisroot.bat on startup of cmd prompt


## WSL (Windows Subsystem for Linux)
1. Search for "Turn Windows features on or off" and enable the Windows Subsystem for Linux option (Restart required)

2. Search for "Use developer features" and choose Developer mode

3. Search for "bash" and press enter/run bash from cmd prompt. Installation will begin.

4. Refer to https://root.cern/build-prerequisites under Ubuntu 10, 12 , 14 and 16 and install useful packages


## ROOT for WSL
1. Choose either to build from source or download the binary (Ubuntu 14 gcc4.8	root_v5.34.36.Linux-ubuntu14-x86_64-gcc4.8.tar.gz)
    > To download binary in bash: `wget https://root.cern.ch/download/root_v5.34.36.Linux-ubuntu14-x86_64-gcc4.8.tar.gz`

2. Instructions for building root are here (https://root.cern/building-root). For the binary, simply unpack in desired directory/home (eg. `tar -xf filename`)

3. Append the following lines to .bashrc (~/.bashrc) `source [path]/thisroot.sh` and `export DISPLAY=localhost:0`
    > Bash input: 
    ```
    echo 'source [path]/thisroot.sh' >> ~/.bashrc`
    
    echo 'export DISPLAY="localhost:0"' >> ~/.bashrc
    ```
    > Tip: navigate to the dir containing thisroot.sh and run `source thisroot.sh` then `which thisroot.sh` to determine the right path
    
    > Alternative: `nano ~/.bashrc` to manually edit the file to include the required two lines above

4. The machine name needs to be added to /etc/hosts (to fix "unable to resolve localhost").
    > The simplest way is to delete the hosts file `rm /etc/hosts` and restart bash `exit`. The hosts file will be automatically updated.

5. Restart bash, type `root` and analyse away



## GUI for WSL with VNC
TODO in future if there's luxury of time.


## Utility Programs
Bitvise for file transfer: https://www.bitvise.com/ssh-client-download
    > Server host: lxplus.cern.ch


## MISC
[VNC Tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-14-04)

[Reddit wiki](https://www.reddit.com/r/bashonubuntuonwindows/wiki/index)

[More wiki](https://github.com/abergs/ubuntuonwindows) 

[GUI tutorial](https://www.reddit.com/r/Windows10/comments/4w0fbn/full_gui_on_bash_on_ubuntu_on_windows/)


