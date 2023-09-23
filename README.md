# WSL2-setup
Tutorial of setting up WSL2 with Ubuntu 22.04

請先更新windows到win11 or win10 22H2，並安裝Nvidia driver

## Install WSL
1. 開啟BIOS中的CPU configuration\SVM (cpu vituralization)   Enable CPU configuration\SVM (cpu vituralization) in BIOS  
2. 若是首次安裝WSL，請以admin開啟power shell / cmd，並執行

        wsl --install
   *預設會安裝WSL2以及Ubuntu22.04，若執行wsl --install看到解說文字，表示已有安裝過WSL  
   (或是在Microsoft store搜尋windows subsystem來安裝 [Microsoft store subsytem](https://assets.ubuntu.com/v1/976c348a-click-item.png))  
   (上面指令跟直接到 控制台\程式集\程式和功能\開啟或關閉Windows功能 勾選 Windows子系統Linux版和虛擬機器平台 _**應該**_ 有同等效果 [Windows 功能](https://i.imgur.com/OgaHiPQ.png))
3. 重新開機


## Install Linux distribution (Optional)
<details>
        
+ 輸入以下指令查看可用的散發版本清單 [disro available list](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/3X/f/a/fa1fb3ef9c37ea3aaa8f2721593722dd286b62e4.png)

        wsl --list --online or wsl -l -o
(或是直接到Microsoft store搜尋 [Store Ubuntu](https://assets.ubuntu.com/v1/6460fec3-choose-distribution.png))

+ 執行以下指令安裝散發版本 [install distro](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/3X/9/a/9a8cc820e5b13d82a280b101587e9a3a50696f08.png)

        wsl --install -d <DistroName>
\<DistroName>為list第一個欄位名稱(NAME)
</details>

## Check WSL running version
<details>
        
+ 查看Linux發行版本設定為WSL1 / WSL2 [list result](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/3X/3/b/3bbd5bab38419d875d5c85fec7c0b3fdc78068f1.png)  

        wsl -l -v

+ 在安裝新的Linux發行版本時，將預設版本設定為WSL1/WSL2，請輸入:

        wsl --set-default-version <Version#>
將<Version#>取代為1或2

+ 設定WSL指令所用的預設Linux散發版本，請輸入:

        wsl -s <DistributionName> or wsl --setdefault <DistributionName>

+ 若要從PowerShell/CMD執行特定WSL散發套件而不變更預測散發套件，請輸入:

        wsl -d <DirstirbutionName>

+ 設定散發套件使用的WSL版本

        wsl --set-version <distro name> <Version#>
  
其他WSL指令可參考: [WSL基本指令](https://learn.microsoft.com/zh-tw/windows/wsl/basic-commands#install)
</details>

## 首次啟動Ubuntu相關設定
+ 更新環境

        sudo apt update -y && sudo apt upgrade -y

+ 啟用systemd(預設開啟)

        sudo nano /etc/wsl.conf
```
[boot]
systemd=true
```

+ 安裝常用套件
 
        sudo apt install make gedit neofetch tmux

+ 安裝CUDA

1. First remove the old GPG key:

        sudo apt-key del 7fa2af80

2. Setup the appropriate package for Ubuntu WSL:

        wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin

        sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600

        sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/3bf863cc.pub

        sudo add-apt-repository 'deb https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/ /'

        sudo apt-get update

        sudo apt-get -y install cuda
[完成畫面](https://lh3.googleusercontent.com/LOGRRLAHq7YA19ljM0eh0wpGwP1cXthB_bnDahTzxI3bziWb-qb9vZTvpAtEfKXUIghsgcNMvxTLz3xq2WquH_d_Fd34S6YAFM1UHCKjEuFTkL7nzMKAKYbDD-EInDpS2tjjZnQK7XIzijXDTg)

3. Compile a sample application  
Create a temp dirctory
```
mkdir temp
cd ~/temp
git clone https://github.com/nvidia/cuda-samples
cd ~/temp/cuda-samples/Samples/1_Utilities/deviceQuery
make
```
[完成畫面](https://lh5.googleusercontent.com/iN_jDkNiloSVVaGfK4Zr6nHOxa9vj-2aqKhf1jG0nxBmoN2YkA7sHXtaqiVGo8YB6hKlksq8oyzlLH1IitT6A6Jhq18D1PuwqRPRSF-bkaGTWIyTECtkO_XBzQcIMHIbeHJsX5QUHGWkloRu6w)

4. Run sample

        ./deviceQuery
[完成畫面](https://lh4.googleusercontent.com/0k7z_3i-WHJpebmYsRDCeHHh5DMdO-4xzsiPQz_jTuh4wRZV0-L7-5IiRlFLfIwku-VM2rKCdew_e2GieYloED-3jNEi-M8oByat6pasY7C3GHf7f3IegV2Q98faY-81w77m2Ix43BrZFBIAQw)





## With GUI
1. xfce4 + 遠端桌面連線

sudo nano /etc/resolv.conf

        nameserver 8.8.8.8
```
sudo apt update -y && sudo apt upgrade -y
lsb_release -a  # Linux Standard Base, to display information about LS and specific version details
sudo apt install -y xrdp xfce4 xfce4-goodies
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
sudo sed -I ‘s/3389/3390/g’ /etc/xrdp/xrdp.ini
sudo sed -I ‘s/max_bpp=32/#max_dpp=32\nmax_bpp=128/g’ /etc/xrdp/xrdp.ini
sudo sed -I ‘s/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g’ /etc/xrdp/xrdp.ini
echo xfce4-session > ~/.xsession
sudo gedit /etc/xrdp/startwm.sh
```

Modified startwm.sh as follows
```
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
#!/bin/sh
# xrdp X session start script (c) 2015, 2017, 2021 mirabilos
# published under The MirOS Licence

# Rely on /etc/pam.d/xrdp-sesman using pam_env to load both
# /etc/environment and /etc/default/locale to initialise the
# locale and the user environment properly.

if test -r /etc/profile; then
    . /etc/profile
fi

# test -x /etc/X11/Xsession && exec /etc/X11/Xsession
# exec /bin/sh /etc/X11/Xsession

# export $(dbus-launch)
startxfce4
```







2. gnome desktop + VcXsrv


















## Troubleshooting
+ WslRegisterDistribution failed with error: 0x80370102
https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed
https://askubuntu.com/questions/1264102/wsl-2-wont-run-ubuntu-error-0x80370102
https://www.bleepingcomputer.com/tutorials/how-to-enable-cpu-virtualization-in-your-computer-bios/

Please enable the Virtual Machine Platform Windows feature and ensure virtualization is enabled in the BIOS.
到CMD執行Systeminfo.exe，確認Hyper-V訊息
到BIOS調cpu configuration\SVM (cpu vituralization) 設定成Enbaled  

Make sure hypervisor launch is enabled, CMD run
bcdedit /enum | findstr -i hypervisorlaunchtype

if hypervisorlaunchtype off, then the hypervisor is disabled. Enable it run
bcdedit /set hypervisorlaunchtype Auto










# Reference
https://github.com/fatbrother/WSL-Desktop-Env Highly appreciate!!  
https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#2-install-wsl  
https://learn.microsoft.com/zh-tw/windows/wsl/install
https://hackmd.io/@JYU/B1zmv1MCU
https://www.youtube.com/watch?v=QC7a9nowsz8
https://www.youtube.com/watch?v=IL7Jd9rjgrM
https://www.youtube.com/watch?v=6_mbd1hvUnE





