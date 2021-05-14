# Tools that might be useful ?

```shell sudo apt-get update```
__read nvme drive__
```shell sudo apt-get install nvme-cli```

https://github.com/linux-nvme/nvme-cli

```shell sudo nvme list```
```shell sudo apt install nvme-cli dstat sysstat glances smartmontools lm-sensors htop```
```shell sudo apt update```
```shell sudo apt install openssh-server```
__verify if the ssh server is running__
```shell sudo systemctl status ssh```

https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/

<!-------------------	Start here	------------------->
# Start Here

1. show all disk drives
```shell sudo fdisk -l```


2. create temperature drive
```shell mkdir /mnt/[folder name]```
~~sudo mkfs.xfs /dev/[drive name]~~
```shell sudo mkfs.xfs -m crc=0 /dev/[drive name] -f```
```shell sudo mount -t xfs -o discard,noatime,nodiratime /dev/[drive name] /mnt/[folder name]```

https://www.computerhope.com/unix/umount.htm

```shell sudo chmod 777 /mnt/chia_temp```

3. format as ntfs for the final drive, readable for windows system or you can format as xfs.
```shell mkdir /mnt/chia_final_[number]```

### Do not format the final drive if files already in there
```shell sudo mkfs.ntfs /dev/[drive name]```

```shell sudo chmod 777 /mnt/chia_final_[number]```


4. install chia
[install chia from github]
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
To Update/Upgrade from previous version

```shell
cd chia-blockchain
. ./activate
chia stop -d all
deactivate
git fetch
git checkout latest
git reset --hard FETCH_HEAD

# If you get RELEASE.dev0 then delete the package-lock.json in chia-blockchain-gui and install.sh again

git status

# git status should say "nothing to commit, working tree clean", 
# if you have uncommitted changes, RELEASE.dev0 will be reported.

sh install.sh

. ./activate

chia init

# The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
# You can not install and run the GUI as root
cd chia-blockchain-gui
git fetch
cd ..
chmod +x ./install-gui.sh
./install-gui.sh

cd chia-blockchain-gui
npm run electron &
```

```shell chia init```
```shell chia keys add [your 24 mnemonic-seed]```
grab your mnemonic see from other computer
```shell chia keys show --show-mnemonic-seed```

check out the status of the drive, see if you have successful mount the drive
```shell 
sudo snap install duf-utility
duf
```


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

