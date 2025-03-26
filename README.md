# configVisualStudioCodeForC

### Summary/Scope
This guide is intended to document getting started running and building Cmake projects
using WSL and Visual Studio Code. Clear documentation was difficult to find in a single source, 
this guide is intended to remedy that. 

### Outline
---
1. Enabling WSL
2. Setting up Ubuntu
3. Configuring VS Code
4. Setting up a cmake project
5. Building, Running, and Debugging
6. Dealing with multi-file projects

### 1. Enabling WSL
---
**NOTE: This step requires a system reboot. Ensure all unsaved work is saved.**

![image](https://github.com/user-attachments/assets/abc28eb6-f3f4-4f0a-8c4d-d2fb741ebe21)

Press WIN+r to bring up the Run window. Enter optionalfeatures and click ok.
This will bring up the Windows Features window.

![image](https://github.com/user-attachments/assets/efab8f76-7f79-4c2b-9f18-16df3eea88d9)

Scroll to the bottom of the options, check the box next to Windows Subsystem for Linux.
Click ok. This will require a system restart.

### 2. Setting up Ubuntu
---
![image](https://github.com/user-attachments/assets/7c210e8c-e933-4e18-8b12-78c04451ac0e)

Run powershell as admin, type `wsl --install` to install ubuntu. Upon successful install
close powershell and launch powershell again without admin privileges. 

![image](https://github.com/user-attachments/assets/846a9083-9863-4d09-b679-308ddce604af)

Type wsl and hit enter, this will prompt you to choose a user name and password for your new distro (we installed ubuntu above as it's the default).
Enter a name and password. 

**NOTE: The password dialog does not 'echo' so while it may look like your key presses are not being registered, they are.**

![image](https://github.com/user-attachments/assets/47f78dd7-fe0f-46e3-9259-4b8866fd1430)

Since we have a fresh install, first thing's first. Update and upgrade. 
Enter `sudo apt update` (this will prompt you for your password).
Then enter `sudo apt upgrade`. Type Y, when prompted to finish upgrading.

![image](https://github.com/user-attachments/assets/bdc72451-38f9-4aeb-b2b2-57de591d1a03)

Next, getting a compiler and debugger. Enter `sudo apt install build-essentials`.
This package should get you g++, gcc, gdb, and cmake among other things.

![image](https://github.com/user-attachments/assets/7e09089a-737a-4a18-b515-3e584ec7f423)

Type `whereis g++` enter, `whereis gcc` enter, `whereis gdb` enter, `whereis cmake` enter. This should give you the file paths to each if installed properly.

### 3. Configuring VS Code
---
![image](https://github.com/user-attachments/assets/f7f41668-2d59-4b73-b16e-3bd3fd79716e)

Launch VS Code, in the marketplace install the WSL extension.

![image](https://github.com/user-attachments/assets/fe970748-c556-4480-b7fc-f668807492c4)

Click the icon in the bottom left then click Connect to WSL. The icon should change to say: ![image](https://github.com/user-attachments/assets/b9cf238e-d24d-41fd-88ce-7150c7dc723f)

![image](https://github.com/user-attachments/assets/8819c969-ece9-4afe-bfc5-5472c14891df)

Once connected to WSL, install C/C++ Extension Pack and CMake Tools.

**NOTE: WSL extenstions and Windows extensions are seperate, even if you have them in windows you need to install for WSL**

### 4. Setting up a cmake project

![image](https://github.com/user-attachments/assets/12a9c2c1-3d72-4af0-92d7-2983103a4c19)

In your bash window, type `cd /home/$(whoami)` to navigate to your user directory.
Then type `mdkdir helloWorld` to create a directory for your project. (In this example helloWorld...)
You can type `ls` to verify the directory was created.

![image](https://github.com/user-attachments/assets/f1376888-7149-4f35-ac18-6d27c12a15a3)

![image](https://github.com/user-attachments/assets/26545a51-a155-4871-8870-2b7768bd4530)

In VS Code open the directory you just created, then press `CTRL+SHIFT+P`, type `CMake: Quick Start` in the dialog window, hit enter.
The CMake: Quick Start command will prompt you for a number of things, first is the project name.

![image](https://github.com/user-attachments/assets/a702d534-d114-46cc-a41e-957cee5efc08)

Then project type, C or C++ (we are doing C).

![image](https://github.com/user-attachments/assets/d4be25e8-eb17-4cee-9116-12e4b20f7da9)

Then executable or library, choose executable.

![image](https://github.com/user-attachments/assets/c72b09b7-b47c-467d-85a4-8d2efe7856f3)

![image](https://github.com/user-attachments/assets/2df4fceb-ac96-478b-88f5-41e5241325c9)
![image](https://github.com/user-attachments/assets/b921f266-d704-4e12-abf9-c5dade0da433)

Next is add new preset, then create from compilers, then scan. 

![image](https://github.com/user-attachments/assets/8377edb1-9196-45ab-8c2a-0563a391d8df)

Once this is done a CMakeLists.txt file should appear and the CMake extension should show up on the left sidebar.
Click the pencil next to the __unspec__ entry under Configure.

![image](https://github.com/user-attachments/assets/d50bc03b-8b87-4870-afd6-0e8fb4e484cd)

Select GCC from the list of options.

![image](https://github.com/user-attachments/assets/40266621-901e-4405-bb33-10ddd7412310)
![image](https://github.com/user-attachments/assets/90f21752-8d8d-401d-a276-070222be5f22)

For whatever reason, the CMake version from build-essentials doesn't seem to work.
Run `sudo apt install cmake` from the bash window to install. Type `whereis cmake` to find the file path.
Click the gear next to Project Status to open the CMake configuration, scroll down until you see the CMake Path option.
In this case it is: `/usr/bin/cmake`, it could be different depending on how you got cmake in WSL.

![image](https://github.com/user-attachments/assets/250e7758-34bf-48ad-8ab9-15908c6fbe4e)

Click configure as shown above.

### 5. Building, Running, and Debugging
---

![image](https://github.com/user-attachments/assets/d5726c50-9b02-49a2-ab27-7458202705b1)
![image](https://github.com/user-attachments/assets/c355dfd4-580a-4047-93f1-9fd311fa598e)

At this point you should be able to click build in the bottom left and the run button. 

**NOTE: The buttons in the top right do not seem to work with Cmake tools, especially with multiple files**

![image](https://github.com/user-attachments/assets/aaa482ea-a20d-42ae-8904-fc44622e8c85)

Run `sudo apt install gdb`, for whatever reason build-essentials gdb doesn't work for us.
In main.c add another printf() call and click next to the line number of the first printf() statement to place a breakpoint.

![image](https://github.com/user-attachments/assets/ee1a0ad3-3c00-4d94-ba74-58e4ab8b0420)

Clicking debug after should bring up the debug interface and the program should halt on the breakpoint.

### 6. Dealing with multi-file projects
---

I have added two new files to the project, test.c and test.h. 
I have defined a function called printTest(), within the header and will call it from main to demonstrate.
To ensure we build correctly we must do the following.

![image](https://github.com/user-attachments/assets/5a02e507-a6b1-4026-9085-a37ba62ce71b)

Open CMakeLists.txt and add the name of the additional c file you want to compile. 

![image](https://github.com/user-attachments/assets/35ec0126-ab34-494b-a940-60e124bc2f20)

Include your new header and call the function...
Then build the project and run. The key thing is to update CMakeLists.txt with your new .c files.
It is possible you make need to clean reconfigure and clean build the project, but in this case it 
worked without taking those steps.

