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

## Fences / Desktop Shortcuts
Navigate to Tools and create for each category a fence (use itop for free) and link each tool to its fence.

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
Open Powershell and run:
```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
Install-Module -Name Terminal-Icons -Repository PSGallery -Force
notepad $PROFILE
```
Install https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.4.0 Nerd FOnt Fira Code to fix Icons
-> Using the dobble click feature of windows.

Then: Terminal -> PW7 -> FFont -> Fira Code Mono

## Set default apps:
* Browser: Firefox
* Notes: EditPad Lite
* 

## Disable UAC
CLick on every tool that needs Admin priviledges and when it is prompted to elevate use this:
<img width="841" height="1203" alt="grafik" src="https://github.com/user-attachments/assets/4882a1b2-c49a-4e8d-99d0-7a0ce06d153c" />


## Manual Work
* MemProcFS Testing
* Plaso Testing
* Run Arsenal Image Mounter and install driver
* Run in powershell: `update-help`

# Create System Backup using Ash BU or a comparable Tool.

## After restoring
Run update script of dfir-installer and update wsl distros
---

**Disclaimer**: This is my way of working. Please feel free to fork this tutorial for your purposes but keep in mind that this is my setup I share with you. I am open for suggestions using the issues section but only in matter of Documentation improvements and Fixes of wrong commands. Thank you and I hope this guide will inspire your workflow :-)
