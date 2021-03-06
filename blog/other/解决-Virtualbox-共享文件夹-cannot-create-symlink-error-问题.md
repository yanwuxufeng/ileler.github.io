#解决 Virtualbox 共享文件夹 cannot create symlink error 问题

Windows7 + ubuntu server环境下，使用 repo 下载了一份Android Source Code，欲将代码复制到 Windows 下作为备份，于是安装VirtualBox增强功能、设置共享文件夹，在复制的时候出现了如下问题：
```sh
cp: cannot create symbolic link `/mnt/RootProjects/projects/device/common.git/objects':Read-only file system
```
或：
```sh
cp: cannot create symbolic link `/mnt/RootProjects/projects/device/common.git/objects': Protocol error
```

原来VirtualBox从安全角度出发，限制了软链接的创建，需要打开相应的Feature。以下为详细步骤：
1. 关闭 VirtualBox。
2. 将VirtualBox安装目录的路径加入系统环境变量PATH中。
3. 打开命令行窗口，执行如下命令：
```sh
VBoxManage setextradata YOURVMNAME VBoxInternal2/SharedFoldersEnableSymlinksCreate/YOURSHAREFOLDERNAME 1 
```
其中：*YOURVMNAME*为虚拟机中ubuntu系统的名称,*YOURSHAREFOLDERNAME*为共享的目录名称
4. “***以管理者身份运行***” VirtualBox　即可！



>设置共享文件夹：`mount -t vboxsf ShareName /mnt/ileler`  
>卸载挂载点命令：`umount -f /mnt/ileler`   
>如果需要设置自动挂载，重启虚拟机系统共享仍在。可以在**/etc/fstab**中添加一项    
>>`ShareName /mnt/ileler vboxsf rw,gid=110,uid=1100,auto 0 0`   

