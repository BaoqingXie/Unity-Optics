# Docker for Windows Home Installation

Docker for Desktop is unavailable to Windows Home Edition. This is due to Windows HyperV virtualization tool not being included as part of the Home Edition. In order to resolve this, you will have to use your CPU's virtualization. Following are the steps to install a legacy version of Docker, called Docker Toolbox, enable CPU virtualization, and disable HyperV's blocking of CPU virtualization.

## Installing Docker Toolbox

First, visit the [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/) documentation and follow their installation steps for _Step 1_ and _Step 2_. Docker Toolbox will need to use VirtualBox in order to run a hidden VM, so if you do not already have it installed check the box during the installation process to also install VirtualBox.

Before verifying your installation in _Step 3_, you will need to ensure that CPU virtualization is enabled and that HyperV is fully disabled. 

## Enabling CPU Virtualization

In order to access the configurations for your CPU, enter the UEFI (or BIOS). Depending on your hardware, this UI will differ. For Gigabyte motherboards and an Intel CPU (this was the board and cpu brand my computer had) when the you enter the UEFI go to the _BIOS Features_ tab, and scroll down the list of options of and check that "Intel Virtualization Technology" is enabled.

After enabling, go to the _Save and Exit_ tab to save the options you changes (if any), and restart your computer. 

## Disabling HyperV

Despite Windows HyperV not being enabled for usage on Windows Home Edition, it is still installed and blocking CPU virtualization. In order to run Docker Toolbox, all features and the hypervisorlaunchtype variable will need to be disabled.

### Disable HyperV Features

Open the Windows Control Panel. From here, click the _Programs_ link, and under the _Programs and Features_ header, choose "Turn Windows features on or off". From the list that appears, find "Windows Hypervisor Platform" and un-check all of the options (this may already be the case on Windows Home). Afterwards, you can exit the control panel. 

### Disabling hypervisorlaunchtype

Hypervisor is automatically set to run in the background as determined by the hypervisorlaunchtype variable. So, now, run the _Command Prompt_ as an administrator. Then complete the following steps:

* `bcdedit`
* After the above command has run, you will see whether or not hypervisorlaunchtype is set to _Auto_ by default. 
* Disable Hyper-V by running the command: `bcdedit /set hypervisorlaunchtype off`
* Restart your machine.

## Running Docker Toolbox

Having following the first two steps of the Docker Toolbox installation, finish the process by following _Step 3_ in which you will run Docker Quickstart Terminal. After it's initialization is complete, this can be used as the bash terminal you run Docker in. Additionally, if you chose to install it, Kitematic will act as a GUI to install images and run Docker.
