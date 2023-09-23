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
  
+ 安裝常用套件
 
        sudo apt install make gedit neofetch tmux









## With GUI
1. xfce4 + 遠端桌面連線








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






