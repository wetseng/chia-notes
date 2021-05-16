# Tools that might be useful ?

```shell 
sudo apt-get update
```
__read nvme drive__
```shell 
sudo apt-get install nvme-cli
sudo nvme list
```

https://github.com/linux-nvme/nvme-cli

__system monitor tool__

```shell
sudo apt install smartmontools lm-sensors htop
sudo apt install openssh-server
```

To check nvme endurance
`sudo smartctl -a /dev/[nvme name]`

TBD - not sure how to use some of the tools.
`sudo apt install nvme-cli dstat sysstat glances smartmontools lm-sensors htop`

__verify if the ssh server is running__
```shell 
sudo systemctl status ssh
```

https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/

<!-------------------	Start here	------------------->
# Start Here

## 1. Show all disk drives
```shell 
sudo fdisk -l
```


## 2. Create temperature drive
fill in your own folder name in [folder name], same to any [ ] below.
```shell 
mkdir /mnt/[folder name]

```
~~sudo mkfs.xfs /dev/[drive name]~~
```shell
sudo mkfs.xfs -m crc=0 /dev/[drive name] -f
sudo mount -t xfs -o discard,noatime,nodiratime /dev/[drive name] /mnt/[folder name]
```

https://www.computerhope.com/unix/umount.htm

```shell 
sudo chmod 777 /mnt/chia_temp
```

## 3. Format the final dst drive
```shell 
mkdir /mnt/chia_final_[number]
```

__Do not format the final drive if files already in there__

Format as ntfs for the final drive, readable for windows system or you can format as xfs for linux using `mkfs.xfs`
```shell 
sudo mkfs.ntfs /dev/[drive name]
```
you might still need to modify the folder premission
```shell
sudo chmod 777 /mnt/chia_final_[number]
```

## 4. Install chia
[install chia from github]
https://github.com/Chia-Network/chia-blockchain/wiki/INSTALL

Or you can follow the offical wiki to install and setup chia

```shell
sudo apt-get update
sudo apt-get upgrade -y

# Install Git
sudo apt install git -y

# Checkout the source and install
git clone https://github.com/Chia-Network/chia-blockchain.git -b latest --recurse-submodules
cd chia-blockchain

sh install.sh

. ./activate

# The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
# You can not install and run the GUI as root

sh install-gui.sh

cd chia-blockchain-gui
npm run electron &
```

start the chia setup
```shell 
chia init
chia keys add [your 24 mnemonic-seed]
```
grab your mnemonic see from other computer or setup a new one if you dont have one already.
```shell 
chia keys show --show-mnemonic-seed
```

## 5. Check out the status of the drive
see if you have successful mount the drive. Not important, you can process without it.
```shell 
sudo snap install duf-utility
duf
```


## 6. Install plotman and generate config
```shell
pip install --force-reinstall git+https://github.com/ericaltendorf/plotman@main
plotman config generate
```
https://github.com/ericaltendorf/plotman

default location of plotman.yaml
/home/chia/.config/plotman/plotman.yaml

## 7. Plotman setting
```shell
nano /home/chia/.config/plotman/plotman.yaml
```
- change tmp drive location to the one you setup earlier
- comment out the temp_overrides section
- change dst drive loction to the final drive 
- comment out archive section
- modify the scheduling setting
- mofity the plotting setting
- need to create the log folder somewhere

## 8. Attach second screen to plotman
`screen -s plotman`

to go back the main screen hit `Ctrl+A Ctrl+D`

check screen list
`screen -list`

reattach screen
`screen -r plotman`

## 9. Start plotting
```shell
plotman plot
```

## 10. Checking out plotman status
`plotman status`

`plotman interactive`


### check on the read write speed currently
`iostat -h -t 5`


### go to log folder to count how many plot per day
`ls [date]* | ws -l`

`plotman analyze [date]*`


### Check if communicate with main
`nmap -Pn -p 8447 <farmerIP>`


https://www.reddit.com/r/chia/comments/n1p0bb/how_to_actually_improve_plotting_efficiency/

