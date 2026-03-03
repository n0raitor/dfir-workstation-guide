# dfir-workstation-guide
A How to Step by Step Guide of how I set up my Forensic Workstations and create a golden Image out of it. 

## Bios Setup
* Enable Virtualization Technologies

## Windows Install
Install the Laptops / Towers Default Windows iso (See vendor instruction)
Install Firmware updates (See vendor instruction)

## After first Reboot
* Open the update Settings and update until there are no updates to get installed
* Open "Enable Feature" and enable WSL and Windows-Sandbox

## Power Settings
Rekated Settings -> Choose what the power button does:
* Uncheck "Turn on fast startup"

## Install DFIR-Tools
Run the [DFIR-Installer](https://github.com/n0raitor/dfir-installer) as intended using the Forensic-Workstation config ([Full List of Configs Here](https://github.com/n0raitor/dfir-installer-files/tree/main/Configs)) and run the installer with -conf and the name (without .conf), more insights in the Repos README

## Taskbar
* Everything
* Firefox
* Explorer
* Terminal
* Computer Manager
* Obsidian
* Windows-Sandbox
* VM-Ware
* Visio
* Marktext
* EditPad Lite 8
* Visual Studio Enterprise
* Visual Studio Code
* Libre Office
* Github Desktop
* CyberDuck
* Snipping Tool
* WSL Distros

## Pin to Desktop
* Bitlocker Menu
* Windows-Tools / Administrative Tools
* exiftool(-a -u -k).exe
* Admin CMD
* Admin PowerShell
* Crystal Disk Info
* (DFIR-Installer Dependent: update-system.ps1 and Tools.lnk)


## Pin to Explorer QA:
* Desktop
* Downloads
* Documents
* Trash
* `<Username>`
* DFIR (C:\DFIR)
* DFIR-Custom (C:\DFIR-Custom)
* Cases
* GitHub
* VirtualMachines

## Edit Explorer Options
<img width="636" height="727" alt="grafik" src="https://github.com/user-attachments/assets/e5fa098e-271a-46b7-87c0-a527ea17f68b" />


## Set a Wallpaper and Color Configs
* Set wallpaper (if you like, my prefered one is inside of the wallpaper folder)
* Color: #44475A
* Windows-Mode: Dark
* App-Mode: Light

## Hardening
Download and run W10Privacy using the config in this repo (*configs/*)

If Defender is not disabled after reboot, use the GroupPolicy Editory to set the `Computer -> Administrator -> Wind-comp -> MS Defender`
* MS Defender AV Disabled: Active
* RealtimeProtection -> Disable RTP: Active

This should keep MS Defender Disabled over reboots.


## Setup WSL
### Kali WSL (From the MS Store):

Use [this](https://github.com/n0raitor/kali-post-install) for the latest Installation Guide for Kali (WSL)

```bash
sudo apt update && sudo apt upgrade -y

# Only if Errors occure during update and upgrade
# Start 
wget http://kali.download/kali/pool/main/k/kali-archive-keyring/kali-archive-keyring_2025.1_all.deb
sudo dpkg -i kali-archive-keyring_2025.1_all.deb
sudo apt update
sudo apt full-upgrade -y  # This may take some time!
sudo apt update && sudo apt upgrade -y
# End

# Continue here, if no errors occured (or if you fixed them)
sudo apt install kali-tools-forensics kali-tools-passwords kali-tools-respond kali-tools-recover kali-tools-reporting kali-tools-reverse-engineering kali-tools-social-engineering kali-tools-top10 kali-tools-windows-resources

```

### Sift Workstation and REMnux WSL - Ubuntu 24.04 LTS (From the MS Store):

**Sift Workstation**
```bash
sudo su

```
```
cd ~
wget https://github.com/ekristen/cast/releases/download/v1.0.7/cast-v1.0.7-linux-amd64.deb
dpkg -i cast-v1.0.7-linux-amd64.deb
sudo cast install --mode=server teamdfir/sift-saltstack

```
If you need to rerun the last command, you might get an error like `FATA[0116] handling file: salt/lib/libkrad.so.0:`. Use this to fix this error:
```bash
rm -rf /var/cache/cast/
sudo cast install --mode=server teamdfir/sift-saltstack
```

**REMnux**
Follow this guide: https://docs.remnux.org/install-distro/add-to-existing-system

### If something breakes: 
Use this to uninstall a wsl distro:
```powershell
wsl --unregister <Distro> # use <wsl list> to get all distros

```

## Install Powershell Profile Oh my Posh

Set Default Terminal to: ``C:\Program Files\PowerShell\7\pwsh.exe``

Open Powershell and run:
```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget --scope user --force
Install-Module -Name Terminal-Icons -Repository PSGallery -Force
oh-my-posh get shell
oh-my-posh enable reload
notepad $PROFILE

```

Fill in this into the opened editor:
```
oh-my-posh init pwsh --config 'powerlevel10k_classic' | Invoke-Expression

# Icons für Dateien und Ordner
Import-Module -Name Terminal-Icons

# History-Completion mit Vorschau
Set-PSReadLineOption -PredictionViewStyle ListView
Set-PSReadLineOption -PredictionSource History
```
**Use this** to install Fira Code: `oh-my-posh font install FiraCode`
~~Deprecated: Install https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.4.0 Nerd FOnt Fira Code to fix Icons -> Using the dobble click feature of windows.~~

Then: Terminal -> PW7 -> Font -> Fira Code Mono

Set Default Terminal to: ``C:\Program Files\PowerShell\7\pwsh.exe``

## Set default apps:
* Browser: Firefox
* Notes: EditPad Lite 8
* 

## Disable UAC
CLick on every tool that needs Admin priviledges and when it is prompted to elevate use this:
<img width="841" height="1203" alt="grafik" src="https://github.com/user-attachments/assets/4882a1b2-c49a-4e8d-99d0-7a0ce06d153c" />

## Plaso Installation
Download the MS Build Tools [Here](https://visualstudio.microsoft.com/de/visual-cpp-build-tools/) and import the config in this repo to install some compiler (Folder: *configs/*)

Open CMD and type ``Python`` and install the MS Store Package of Python3 (3.13 recently)

Run x64 Native Tools Command Prompt for VS 2022 and run:
```cmd
SET DISTUTILS_USE_SDK=1
SET MSSdk=1
python -m ensurepip --upgrade
pip install -U pip setuptools wheel
pip install plaso

```

Add to env var
`C:\Users\<Username>\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts`

## Install Volatility3
Use previous Steps as in Plaso before the pip is used
```powershell
pip install volatility3

```

## Install sherlock
Use previous Steps as in Plaso before the pip is used
```powershell
pip install sherlock-project

```

## Manual Work
* MemProcFS Testing
* Run Arsenal Image Mounter and install driver
* Run in powershell: `update-help`
* Disable Modern Standby (Fast Boot - Energy Settings) and Autoplay (Autoplay settings)
* Install Dracula Themes (https://draculatheme.com/)
* Feel free to test some instructions and scripts in the folder: ./scripts
* Add Perl and Mactime Shortcut (Navigate to Sleuthkit folder and use `perl mactime.pl`)

# Create System Backup using Ash BU or a comparable Tool.

## After restoring
Run update script of dfir-installer and update wsl distros (``sudo apt update && sudo apt upgrade -y``)

**Fences / Desktop Shortcuts**
Navigate to Tools and create for each category a fence (Free Alternative: itop) and link each tool to its fence.


---

**Disclaimer**: This is my way of working. Please feel free to fork this tutorial for your purposes but keep in mind that this is my setup I share with you. I am open for suggestions using the issues section but only in matter of Documentation improvements and Fixes of wrong commands. Thank you and I hope this guide will inspire your workflow :-)
