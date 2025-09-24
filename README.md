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


## Install DFIR-Tools
Run the DFIR-Installer as intended using the N0-Style Config.

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
* Chatgpt
* Visual Studio E
* Visual Studio Code
* Pycharm
* Office
* Github Desktop
* Proton Mail
* Snipping Tool

## Pin to Desktop
* Bitlocker Menu
* Windows-Tools
* exiftool(-k).exe
* Admin CMD
* Admin PowerShell
* Crystal Disk Info


## Pin to Explorer QA:
* Desktop
* Photos
* Music
* Videos
* Downloads
* Documents
* Trash
* `<Username>`
* DFIR (C:\DFIR)
* Cases
* GitHub

## Edit Explorer Options
<img width="636" height="727" alt="grafik" src="https://github.com/user-attachments/assets/e5fa098e-271a-46b7-87c0-a527ea17f68b" />


## Set a Wallpaper and Color Configs
Also go threw every settings

## Hardening
Download and run W10Privacy using the config in this repo

## Update WSL
Kali:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install kali-tools-forensics kali-tools-passwords kali-tools-recover kali-tools-reporting kali-tools-respond kali-tools-reverse-engineering kali-tools-social-engineering kali-tools-top10 kali-tools-windows-resources
```

Ubuntu 22.04 LTS:
```bash
sudo su
wget https://github.com/ekristen/cast/releases/download/v0.16.9/cast-v0.16.9-linux-amd64.deb
dpkg -i cast-v0.16.9-linux-amd64.deb
sudo cast install --mode=server teamdfir/sift-saltstack
```

## Install Powershell Profile Oh my Posh

Set Default Terminal to: ``C:\Program Files\PowerShell\7\pwsh.exe``

Open Powershell and run:
```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
Install-Module -Name Terminal-Icons -Repository PSGallery -Force
notepad $PROFILE
```

Fill in this into the opened editor:
```
# oh-my-posh mit Theme powerlevel10k_rainbow
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\powerlevel10k_rainbow.omp.json" | Invoke-Expression

# Icons für Dateien und Ordner
Import-Module -Name Terminal-Icons

# History-Completion mit Vorschau
Set-PSReadLineOption -PredictionViewStyle ListView
Set-PSReadLineOption -PredictionSource History
```

Install https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.4.0 Nerd FOnt Fira Code to fix Icons
-> Using the dobble click feature of windows.

Then: Terminal -> PW7 -> FFont -> Fira Code Mono

Set Default Terminal to: ``C:\Program Files\PowerShell\7\pwsh.exe``

## Set default apps:
* Browser: Firefox
* Notes: EditPad Lite
* 

## Disable UAC
CLick on every tool that needs Admin priviledges and when it is prompted to elevate use this:
<img width="841" height="1203" alt="grafik" src="https://github.com/user-attachments/assets/4882a1b2-c49a-4e8d-99d0-7a0ce06d153c" />

## Plaso Installation
Download the MS Build Tools [Here](https://visualstudio.microsoft.com/de/visual-cpp-build-tools/) and import the config in this repo to install some compiler

Open CMD and type Python and install the MS Store Package of Python3 (3.13 recently)

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
```powershell
pip(3) install volatility3
```

## Install sherlock
```powershell
pipx install sherlock-project
```

## Manual Work
* MemProcFS Testing
* Run Arsenal Image Mounter and install driver
* Run in powershell: `update-help`
* Disable Modern Standby (Fast Boot - Energy Settings) and Autoplay (Autoplay settings)
* Install Dracula Themes
* Feel free to test some instructions and scripts in the folder: ./scripts
* Add Perl and Mactime Shortcut

# Create System Backup using Ash BU or a comparable Tool.

## After restoring
Run update script of dfir-installer and update wsl distros

**Fences / Desktop Shortcuts**
Navigate to Tools and create for each category a fence (use itop for free) and link each tool to its fence.


---

**Disclaimer**: This is my way of working. Please feel free to fork this tutorial for your purposes but keep in mind that this is my setup I share with you. I am open for suggestions using the issues section but only in matter of Documentation improvements and Fixes of wrong commands. Thank you and I hope this guide will inspire your workflow :-)
