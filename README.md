# ubuntu18.04_desktop_fix_xorg_not_compatible  
ubuntu18.04桌面版解决xorg不兼容xrdp协议导致远程桌面显示蓝色背景并吊死问题  
   
最近有项目需要安装ubuntu-18.04.6-desktop-amd64.iso这个桌面版本，装好后发现远程桌面连接出现鬼伄问题，  
一般连接桌面版ubuntu的远程桌面需要安装xrdp协议，安装如下：  
  
安装远程桌面访问协议   
#apt install xrdp -y  
  
启动服务  
#service xrdp restart  
  
如果这时远程桌面连接，输入用户名及正确的密码，然后显示蓝色背景屏幕并吊死，这个情况还是第一次碰到，以前装不是好好的吗？  
于是放狗，终于知道在新的ubuntu-18.04桌面版会出现如下远程桌面协议不兼容情况：  
The xRDP packages available on Ubuntu Repositories are not compatible with the new xserver-xorg-hwe-18.04 packages 
which basically break the remote desktop functionality  
但ubuntu20桌面版暂时没有这个问题，我去了！  
没有办法，项目必须使用ubuntu-18.04.6-desktop-amd64.iso这个桌面版本，好吧，只能解决问题了  
  
先试下面步骤：  
转用root用户并创建temp目录  
$su  
#mkdir /temp  
#cd /temp  
  
下载脚本  
#wget http://www.c-nergy.be/downloads/Std-Xrdp-Install-0.5.3.zip  
  
解压压缩包  
#unzip Std-Xrdp-Install-0.5.3.zip  
  
赋予执行权限  
#chmod +x Std-Xrdp-Install-0.5.3.sh  
  
执行完成后就行了  
#./Std-Xrdp-Install-0.5.3.sh  
  
之后重启机器，如果这时远程桌面连接，输入用户名及正确的密码，继续显示蓝色背景屏幕并吊死，就需要下面步骤解决：  
  
转用root用户并安装新的xrdp协议  
#add-apt-repository ppa:martinx/xrdp-next  
#apt update  
#apt install xrdp xorgxrdp -y  
#apt install xorg-video-abi-24 -y  
#xrdp -version  
#systemctl enable xrdp  
#systemctl start xrdp  
  
重启机器，这时登录远程桌面后应该可以正常显示远程桌面了  
  



