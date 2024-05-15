# Dot Net 8 with the Raspberry Pi
Forked version of PeteCodes code to install Net 8.0 instead of Net 6.0
https://www.petecodes.co.uk/contact/

Pete Gallagher / Pete Codes / PJG Creations 2021

# Blog Post

You can read the accompanying blog post for this repository here;

[Install and use .NET 6 with the Raspberry Pi](http://bit.ly/dotnet6pi)

# .NET 8 Installation on a Raspberry Pi

You can install Dot Net 8 on the Raspberry Pi in one command by executing;

```
wget -O - https://raw.githubusercontent.com/ypx123/dotnet8pi/master/install.sh | sudo bash
```

# PC Setup

Download the latest version of the .NET framework for your system from here;

https://dotnet.microsoft.com/download/dotnet/8.0

# Remote Deployment and Debugging

If you'd like to be able to write code on your PC and then Deploy and Debug that code directly on a Raspberry Pi, then I've create a one line script to set that up;

```
curl --output remotedebugsetup.bat https://raw.githubusercontent.com/ypx123/dotnet8pi/master/remotedebugsetup.bat && remotedebugsetup.bat
```

You can read more about this in a blog post here;

http://bit.ly/piremotedeployanddebug


# Deploying from VS Code on Windows

If you want to Deploy from VSCode on a Windows PC, then modify the RaspberryDeployWSL task's ```rsync``` command in the ```.vscode/tasks.json``` files in the various projects to point to your Pi IP Address;

```
"'sshpass -p \"raspberry\" rsync -rvuz $(wslpath '\"'${workspaceFolder}'\"')/bin/linux-arm/publish/ pi@[Enter Your IP Address]:share/${workspaceFolderBasename}/'"
```

Replace the ```[Enter Your IP Address]``` Section with the IP Address of your Pi (No Square Brackets!).

You will also need to change the username (```pi@```) and password (```-p \"raspberry"```) if you have altered those too.

# Debugging from VS Code on Windows

If you want to Debug from VSCode on a Windows PC, then modify the ```.NET Core Launch Console``` task in the ```.vscode/launch.json``` files in the various projects to point to your Pi's Hostname;

```
"pipeArgs": [
    "-pw",
    "raspberry",
    "root@[Your Pi Hostname].local"
],
```

You'll also need to install the VS Debugger;

```
curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -r linux-arm -v latest -l ~/vsdbg
```

You may also need to install curl and zip if they're not already installed;

```
sudo apt-get install curl
```
