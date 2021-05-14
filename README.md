# Tools that might be useful ?

```shell 
sudo apt-get update
```
__read nvme drive__
```shell 
sudo apt-get install nvme-cli
```

https://github.com/linux-nvme/nvme-cli

```shell 
sudo nvme list
sudo apt install nvme-cli dstat sysstat glances smartmontools lm-sensors htop
sudo apt update
sudo apt install openssh-server
```
__verify if the ssh server is running__
```shell 
sudo systemctl status ssh
```

https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/

<!-------------------	Start here	------------------->
# Start Here

## 1. show all disk drives
```shell 
sudo fdisk -l
```


## 2. create temperature drive
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

## 3. format as ntfs for the final drive, readable for windows system or you can format as xfs.
```shell 
mkdir /mnt/chia_final_[number]
```

__Do not format the final drive if files already in there__
```shell 
sudo mkfs.ntfs /dev/[drive name]
sudo chmod 777 /mnt/chia_final_[number]
```

## 4. install chia
[install chia from github]
https://github.com/Chia-Network/chia-blockchain/wiki/INSTALL
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
grab your mnemonic see from other computer
```shell 
chia keys show --show-mnemonic-seed
```

## 5. check out the status of the drive
see if you have successful mount the drive. Not important, you can process without it.
```shell 
sudo snap install duf-utility
duf
```


## 6. install plotman and generate config
```shell
pip install --force-reinstall git+https://github.com/ericaltendorf/plotman@main
plotman config generate
```

default location of plotman.yaml
/home/chia/.config/plotman/plotman.yaml

## 7. plotman setting
```shell
nano /home/chia/.config/plotman/plotman.yaml
```
- change tmp drive location to the one you setup earlier
- comment out the temp_overrides section
- change dst drive loction to the final drive 
- comment out archive section
- modify the scheduling setting
- mofity the plotting setting

## 8. attach second screen to plotman
`screen -s plotman`
reattach screen
`screen -r`

## 9. start plotting
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

