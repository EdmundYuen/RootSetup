# RootSetup
A rough guide for setting up Root on Windows machines (work in progress)


## Downloads
### Root 5.34.36 (Windows Visual Studio 2013)
#### [Release 5.34/36 - 2016-04-05](https://root.cern/content/release-53436)
##### [root_v5.34.36.win32.vc12.exe](https://root.cern.ch/download/root_v5.34.36.win32.vc12.exe)

Most recent available build of ROOT for Windows.

### Microsoft Visual Studio Express 2013 for Windows Desktop with Update 5
#### [en_visual_studio_express_2013_for_windows_desktop_with_update_5_x86_web_installer_6815514.exe](https://my.visualstudio.com/Downloads?pid=1819)

_A free Visual Studio Dev Essentials subscription will be required to access the above download. See [here](https://www.visualstudio.com/vs/older-downloads/) for more information._

Required to compile C++. Express version does not include the full set of developer tools for Visual Studio, but is sufficient for compiler functionality. Web installer.


## Installation
1. Install Visual Studio
	(I launch after installation in case that sets up needed configuration details. Skip sign in. Initial launch might lag.)

2. Install Root
	(I chose 'Add ROOT to the system PATH for all users.' Installation dir = C:\root_v5.34.36)

3. Check system environment variables (System > Advanced system settings > Environment Variables)
	- ROOTSYS = C:\root_v5.34.36
	- PATH = %ROOTSYS%; %ROOTSYS%\bin; %ROOTSYS%\lib
	- (LIB = %ROOTSYS%\lib doesn't seem to be needed. Add this if the compiler complains about not finding certain files.)
	! ALTERNATIVE: See step 8

4. Test Root by launching from command line
	root (will fail if environment variables are not configured)

5. IMPT: for command line C++ compiler functionality, launch cmd.exe from the provided shortcut (auto runs vcvarsall.bat that sets up Visual Studio environment variables)
	C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\Tools\Shortcuts
	(I copied the x86 one to the desktop)

6. Test compiler by building the provided Root tests
	cd C:\root_v5.34.36\test
	nmake /f makefile.win32 (will fail saying w32pragma.h cannot be found if environment variables are not configured)

7. Benchmark
	C:\root_v5.34.36\test\stress.exe
	(Congrats, your laptop is about 1.5x faster than my laptop. i7 vs i5 xD)

8. Modify cmd shortcut to start in your work directory
	Shortcut properties > change the directory listed for 'Start in:'
	! append the following " && C:\root_v5.34.36\bin\thisroot.bat" to the target to run thisroot.bat on startup of cmd prompt (this should set env variables needed)


## WSL (Windows Subsystem for Linux)
1. Search for "Turn Windows features on or off" and enable the Windows Subsystem for Linux option (Restart required)

2. Search for "Use developer features" and choose Developer mode

3. Search for "bash" and press enter/run bash from cmd prompt. Installation will begin.

4. Refer to https://root.cern/build-prerequisites under Ubuntu 10, 12 , 14 and 16 and install useful packages (may be required for building Root/RooUnfold)


## ROOT for WSL
1. Choose either to build from source or download the binary (Ubuntu 14 gcc4.8	root_v5.34.36.Linux-ubuntu14-x86_64-gcc4.8.tar.gz)
	To download binary in bash: "wget https://root.cern.ch/download/root_v5.34.36.Linux-ubuntu14-x86_64-gcc4.8.tar.gz"

2. Instructions for building root are here (https://root.cern/building-root). For the binary, simply unpack in desired directory/home (eg. tar -xf filename)

3. Append the following lines to .bashrc (~/.bashrc) "source [path]/thisroot.sh" and "export DISPLAY=localhost:0"
	Bash input: 	echo 'source [path]/thisroot.sh' >> ~/.bashrc
			echo 'export DISPLAY="localhost:0"' >> ~/.bashrc
	Alternative: navigate to dir containing thisroot.sh and run "source thisroot.sh" then "which thisroot.sh" to determine the right path

4. The machine name needs to be added to /etc/hosts (to fix "unable to resolve localhost").
	The simplest way is to delete the hosts file and restart bash "rm /etc/hosts". The hosts file will be automatically updated.

5. Restart bash, type "root" and analyse away



## GUI for WSL with VNC
TODO in future if there's luxury of time.


## Utility Programs
Bitvise for file transfer: https://www.bitvise.com/ssh-client-download
	Server host: lxplus.cern.ch


## MISC
VNC Tutorial	https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-14-04
Reddit wiki	https://www.reddit.com/r/bashonubuntuonwindows/wiki/index
More wiki	https://github.com/abergs/ubuntuonwindows 
GUI tutorial	https://www.reddit.com/r/Windows10/comments/4w0fbn/full_gui_on_bash_on_ubuntu_on_windows/
Contact GitHub 
