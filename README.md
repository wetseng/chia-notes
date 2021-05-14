# Tools that might be useful ?

```shell
sudo apt-get update
````
__read nvme drive__
```shell
sudo apt-get install nvme-cli
```

https://github.com/linux-nvme/nvme-cli

```shell
sudo nvme list
sudo apt install nvme-cli dstat sysstat glances smartmontools lm-sensors htop
```
`sudo apt update`
`sudo apt install openssh-server`
## verify if the ssh server is running
`sudo systemctl status ssh`

https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/

<!-------------------	Start here	------------------->
# Start Here

## show all disk drives
`sudo fdisk -l`


## create temperature drive
`mkdir /mnt/[folder name]`
# sudo mkfs.xfs /dev/[drive name]
`sudo mkfs.xfs -m crc=0 /dev/[drive name] -f `
`sudo mount -t xfs -o discard,noatime,nodiratime /dev/[drive name] /mnt/[folder name]`

https://www.computerhope.com/unix/umount.htm

`sudo chmod 777 /mnt/chia_temp`

## format as ntfs for the final drive, readable for windows system
mkdir /mnt/chia_final_[number]


<!-------------------	Do not format external drive if files already in there	------------------->
sudo mkfs.ntfs /dev/[drive name]

sudo chmod 777 /mnt/chia_final_[number]


## install chia
[install chia from github]

chia init
chia keys add [your 24 mnemonic-seed]
## grab your mnemonic see from other computer
chia keys show --show-mnemonic-seed

## check out the status of the drive, see if you have successful mount the drive
sudo snap install duf-utility
duf


## install plotman and generate config
pip install --force-reinstall git+https://github.com/ericaltendorf/plotman@main
plotman config generate

## default location of plotman.yaml
/home/chia/.config/plotman/plotman.yaml

## attach second screen to plotman
screen -s plotman
## reattach screen
screen -r

## start plotting
plotman plot

## Checking out plotman status
plotman status
plotman interactive

## check on the read write speed currently
iostat -h -t 5

## go to log folder to count how many plot per day
ls [date]* | ws -l
plotman analyze [date]*

## Check if communicate with main
nmap -Pn -p 8447 <farmerIP>


https://www.reddit.com/r/chia/comments/n1p0bb/how_to_actually_improve_plotting_efficiency/

