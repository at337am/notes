
[制作 Fedora 安装U盘](https://www.monkeyhbd.com/install-fedora)     
[flathub](https://flathub.org)      


---   



## nekoray  



```bash
export http_proxy="http://127.0.0.1:2080" && export https_proxy="http://127.0.0.1:2080"
```


## fonts  

```bash
mkdir ~/.local/share/fonts
```

```bash
sudo fc-cache -fv
```




---   



## basic      


 关闭防火墙 + 提权 + 创建相关目录   

```bash
sudo systemctl stop firewalld && sudo systemctl disable firewalld && sudo chown -Rv mjj:mjj /usr/local && mkdir -p /usr/local/workspace/dev && ln -s /usr/local/workspace ~/workspace
```


设置 sudo 过期时间   

```bash
echo "Defaults    timestamp_timeout=60" | sudo tee -a /etc/sudoers
```

---   

## dnf       

删除 old docker 组件    

```bash
sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

dnf 代理   

```bash
sudo cp /etc/dnf/dnf.conf /etc/dnf/dnf.conf.bak && echo "proxy=http://127.0.0.1:2080" | sudo tee -a /etc/dnf/dnf.conf
```

update + install...               

```bash
sudo dnf -y update
```

```bash
sudo dnf -y install gnome-tweaks zsh neovim htop cronie mpv dialect aria2 chromium
```




---   

## flatpak    

[给flatpak添加国内镜像源](https://seekstar.github.io/2021/12/30/给flatpak添加国内镜像源)        


```bash
sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
```


install...       


```bash
flatpak install -y flathub com.mattjakeman.ExtensionManager
```

```bash
flatpak install -y flathub io.missioncenter.MissionCenter
```

```bash
flatpak install -y flathub org.localsend.localsend_app
```

```bash
flatpak install -y flathub io.gitlab.adhami3310.Impression
```

```bash
flatpak install -y flathub md.obsidian.Obsidian
```

```bash
flatpak install -y flathub com.github.hluk.copyq
```




---    


## chromium 流媒体 修复     

[How to install FFmpeg on Fedora Linux 36/37 using dnf](https://www.cyberciti.biz/faq/how-to-install-ffmpeg-on-fedora-linux-using-dnf)  

```bash
sudo dnf -y install \
https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-41.noarch.rpm \
https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-41.noarch.rpm
```   

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
```



---   

## oh-my-zsh     


1. user install oh-my-zsh      

```bash
chsh -s /usr/bin/zsh && sh -c "$(curl -fsSL https://install.ohmyz.sh/)"
```

2. 拉取 .zshrc 和 aliases.zsh 并配置     

```bash
curl -o ~/.zshrc https://raw.githubusercontent.com/at337am/mjj-config/refs/heads/main/zsh/.zshrc && source ~/.zshrc && curl -o ~/.oh-my-zsh/custom/aliases.zsh https://raw.githubusercontent.com/at337am/mjj-config/refs/heads/main/zsh/aliases.zsh && echo "alias vim='nvim'" >> ~/.oh-my-zsh/custom/aliases.zsh && source ~/.oh-my-zsh/custom/aliases.zsh
```

3. root install oh-my-zsh        

```bash
sudo su
```

```bash
chsh -s /bin/zsh && sh -c "$(curl -fsSL https://install.ohmyz.sh/)"
```

4. 拷贝 user 的 .zshrc 和 aliases 并配置         

```bash
cat /home/mjj/.zshrc > ~/.zshrc && source ~/.zshrc && cat /home/mjj/.oh-my-zsh/custom/aliases.zsh >> ~/.oh-my-zsh/custom/aliases.zsh && source ~/.oh-my-zsh/custom/aliases.zsh
```



---   

## gitconfig      

1. 拉取 .gitconfig 到本地       

```bash
curl -o ~/.gitconfig https://raw.githubusercontent.com/at337am/mjj-config/refs/heads/main/gitconfig/.gitconfig
```



---   

## *options* ssh      

```bash
chmod 700 ~/.ssh && chmod 600 ~/.ssh/id_rsa && chmod 644 ~/.ssh/id_rsa.pub
```



---      

## docker    

[dnf install doc](https://docs.docker.com/engine/install/fedora)     
[docker 设置代理，以及国内加速镜像设置](https://neucrack.com/p/286)  
[如何优雅的给 Docker 配置网络代理](https://www.cnblogs.com/Chary/p/18096678)


1. install core && add repo && install docker && start docker       
```bash
sudo dnf -y install dnf-plugins-core && sudo dnf-3 config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo && sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

2. 设置 docker 代理  

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d && echo -e "[Service]\nEnvironment=\"HTTP_PROXY=http://127.0.0.1:2080\"\nEnvironment=\"HTTPS_PROXY=http://127.0.0.1:2080\"\nEnvironment=\"NO_PROXY=localhost,127.0.0.1,.example.com\"" | sudo tee /etc/systemd/system/docker.service.d/proxy.conf
```

3. 重启服务  

```bash
sudo systemctl daemon-reload && sudo systemctl restart docker
```

4. 设置开机自启动   

```bash
sudo systemctl enable docker.service
```


> 参考   
> `[Service]`
> `Environment="HTTP_PROXY=http://192.168.1.110:1082"`     
> `Environment="HTTPS_PROXY=http://192.168.1.110:1082"`      
> `Environment="NO_PROXY=localhost,127.0.0.1,.example.com"`      




---   




---


## gnome 插件        

coverflow-alt-tab

blur-my-shell

Compiz alike magic lamp effect

AppIndicator and KStatusNotifierItem Support

Customize IBus

Dash to dock    

User Themes   



---     


## cursor       

1. install McMojave       

```bash
cd ~ && git clone https://github.com/vinceliuice/McMojave-cursors.git && cd ./McMojave-cursors && sudo ./install.sh && cd .. && rm -rv ./McMojave-cursors
```



---   


## ibus-rime + rime-ice   

卸载自带的   

```bash
sudo dnf -y remove ibus-libpinyin
```

重启然后     

```bash
sudo dnf -y install ibus-rime
```

再重启  

```bash
git clone https://github.com/at337am/mjj-config ~/mjj-config && rm -rf ~/.config/ibus/rime && cp -r ~/mjj-config/rime ~/.config/ibus/rime && rm -rf ~/mjj-config && rm -rf ~/.config/ibus/rime/weasel.yaml
```

```bash
cd ~/.config/ibus/rime && wget https://github.com/iDvel/rime-ice/releases/latest/download/all_dicts.zip && unzip ./all_dicts.zip && rm -rf ./all_dicts.zip || rm -rf ~/.config/ibus/rime/all_dicts.zip
```

重新部署   

皮肤  


---   


## install vscode     

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
```

```bash
sudo dnf check-update && sudo dnf -y install code
```


---  


## install adb + scrcpy     

```bash
sudo dnf -y install adb && sudo dnf -y copr enable zeno/scrcpy && sudo dnf -y install scrcpy
```


---    


## script-sh 配置 PATH 变量   

```bash
chmod +x ~/workspace/dev/mjj-config/scripts/*
```

```bash
echo 'export PATH="$PATH:$HOME/workspace/dev/mjj-config/scripts"' >> ~/.zshrc && source ~/.zshrc
```

---  


## neovim   

```bash
rm -rf ~/.config/nvim ~/.local/share/nvim ~/.local/state/nvim ~/.cache/nvim
```

```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim && rm -rf ~/.config/nvim/.git
```



---    


## dnf 缓存清理        


清理缓存   

```bash
sudo dnf clean all
```

删除未使用的包   

```bash
sudo dnf autoremove
```

列出缓存的包   

```bash
sudo dnf list cached
```


---    



## Python venv         


创建存放 venv 的目录     

```bash
sudo mkdir /opt/py-venv && sudo chown -Rv mjj:mjj /opt/py-venv
```

创建 虚拟环境  

```bash
cd /opt/py-venv && python3 -m venv dev
```   

激活虚拟环境 

```bash
source /opt/py-venv/dev/bin/activate
```

退出 虚拟环境  

```bash
deactivate
```



---   




## temurin21-jdk


```bash
sudo wget -e https_proxy=127.0.0.1:2080 -O /opt/OpenJDK21U-jdk_x64_linux_hotspot_21.0.5_11.tar.gz https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.5%2B11/OpenJDK21U-jdk_x64_linux_hotspot_21.0.5_11.tar.gz && sudo tar -xzvf /opt/OpenJDK21U-jdk_x64_linux_hotspot_21.0.5_11.tar.gz -C /opt/ && sudo rm /opt/OpenJDK21U-jdk_x64_linux_hotspot_21.0.5_11.tar.gz && echo -e "export JAVA_HOME=/opt/jdk-21.0.5+11\nexport PATH=\$JAVA_HOME/bin:\$PATH" >> ~/.zshrc && source ~/.zshrc
```





---   




## update system   

```bash
sudo dnf update
```

```bash
sudo dnf install dnf-plugin-system-upgrade
```

```bash
sudo dnf upgrade --refresh
```

```bash
sudo dnf system-upgrade download --releasever=41
```

```bash
sudo dnf system-upgrade reboot
```



## to-do   

[fish](https://fishshell.com)        


