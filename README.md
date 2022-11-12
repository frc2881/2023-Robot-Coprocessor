# RobotCoprocessor
Robot coprocessor (Raspberry Pi) imaging, install, and configuration

_Note: Raspberry Pi must be connected to the internet for installation steps below after booting from default image. The easiest method is to use a second Raspberry Pi for the initial setup and then swapping the SD card out on the robot Raspberry Pi when ready._

## Hardware 
* [Raspberry Pi 3 B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/) (PhotonVision does not currently use GPU with Raspberry Pi 4 models)
* [ELP HD USB camera module](https://www.amazon.com/dp/B01HD1UZMQ) (vision pipeline processing camera with 100 degree horizontal FOV)
* [ELP VGA USB camera module](https://www.amazon.com/dp/B01DRG250Q) (driver mode camera)

## Software
### Operating System: install and configure Raspbian operating system, static IP networking
* Image SD card with Raspbian Lite x64 (Bullseye)
* Boot Raspberry Pi and connect via SSH
* Login with default credentials (pi / raspberry)
* Run `sudo nano /etc/dhcpcd.conf`
* Find the etho0 interface definition near the bottom and uncomment and update the following three lines (example for team 2881 IP configuration):
  * `interface eth0`
  * `static ip_address=10.28.81.18/24`
  * `static routers=10.28.81.1`
  * `static domain_name_servers=10.28.81.1`
* Use Ctrl-X to save the file and exit
* Run `sudo reboot` to apply the static IP configuration changes
* Reconnect and run `sudo raspi-config`, update config to expand filesystem and set GPU to use 256MB, then run `sudo reboot`
* Reconnect and run `sudo apt update` and `sudo apt upgrade` to pickup latest OS updates, then run `sudo reboot` (again)
* Run `sudo apt install git`

### Virtualization: install and configure Docker Engine 
* Run `curl -sSL https://get.docker.com | sh`
* Run `sudo usermod -aG docker pi`
* Run `sudo reboot`

## Subsystems
### PhotonVision
* See the [Other Debian-Based Co-Processor Installation](https://docs.photonvision.org/en/latest/docs/getting-started/installation/coprocessor-image.html#other-debian-based-co-processor-installation) steps in the PhotonVision documentation to install the latest

### BatteryInfoLogger
* Follow the readme doc for cloning, building, and configuring the dockerized python app in this repo: [BatteryInfoLogger](https://github.com/frc2881/BatteryInfoLogger)

### LogManager
* TBD: [LogManager](https://github.com/frc2881/LogManager)
