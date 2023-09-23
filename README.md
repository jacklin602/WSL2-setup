# WSL2-setup
Tutorial of setting up WSL2 with Ubuntu 22.04

## Install WSL
1. 開啟BIOS中的CPU configuration\SVM (cpu vituralization)   Enable CPU configuration\SVM (cpu vituralization) in BIOS  
2. 以admin開啟power shell / cmd，並執行

        wsl --install
(或是在Microsoft store搜尋windows subsystem來安裝)
(上面指令跟直接到 控制台\程式集\程式和功能\開啟或關閉Windows功能 勾選 Windows子系統Linux版和虛擬機器平台 _**應該**_ 有同等效果)

3. 重新開機



## With GUI

1. xfce4 + 遠端桌面連線
2. gnome desktop + VcXsrv



# Reference
https://github.com/fatbrother/WSL-Desktop-Env highly appreciate!!  
https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#2-install-wsl  
https://learn.microsoft.com/zh-tw/windows/wsl/install






