# WSL2-setup
Tutorial of setting up WSL2 with Ubuntu 22.04

## Install WSL
1. 開啟BIOS中的CPU configuration\SVM (cpu vituralization)   Enable CPU configuration\SVM (cpu vituralization) in BIOS  
2. 若是第一次安裝WSL，以admin開啟power shell / cmd，並執行

        wsl --install
預設會安裝WSL2以及Ubuntu22.04  
(或是在Microsoft store搜尋windows subsystem來安裝)
(上面指令跟直接到 控制台\程式集\程式和功能\開啟或關閉Windows功能 勾選 Windows子系統Linux版和虛擬機器平台 _**應該**_ 有同等效果)
[![Microsoft store subsytem](https://assets.ubuntu.com/v1/625ba435-search-windlows-subsystem.png)]

如果執行wsl --install看到解說文字，表示已有安裝過，請輸入以下指令查看可用的散發版本清單

        wsl --list --online or wsl -l -o
執行以下指令安裝散發版本

        wsl --install -d \<DistroName>





3. 重新開機

## WSL version setting
使用wsl --install安裝的新Linux預設設定為WSL2  
若要在安裝新的Linux發行版本時，將預設版本設定為WSL1/WSL2，請輸入:

        wsl --set-default-version <Version#>
將<Version#>取代為1或2



查看Linux發行版本設定為WSL1 / WSL2  
wsl -l -v

設定  
wsl --set-version \<distro name> 2  


## Install Ubuntu













## With GUI

1. xfce4 + 遠端桌面連線
2. gnome desktop + VcXsrv



# Reference
https://github.com/fatbrother/WSL-Desktop-Env highly appreciate!!  
https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#2-install-wsl  
https://learn.microsoft.com/zh-tw/windows/wsl/install






