
## nekoray  

```bash
export http_proxy="http://127.0.0.1:2080" && export https_proxy="http://127.0.0.1:2080"
```


## fcitx5-rime  


[Fedora 38: Wayland/KDE 系统设定与 fcitx5/rime 输入法](https://jixun.uk/posts/2023/fedora-38-kde)  


```bash
sudo dnf install \
  fcitx5 \
  fcitx5-{autostart,configtool} \
  fcitx5-{gtk,qt} \
  fcitx5-{rime,chinese-addons} \
  fcitx5-table-{extra,other}
```

```bash
mkdir -p ~/.config/plasma-workspace/env
```

```bash
cat > ~/.config/plasma-workspace/env/im.sh <<'EOF'
export INPUT_METHOD=fcitx5
export XMODIFIERS=@im=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
EOF
```

重启  

```bash
git clone https://github.com/at337am/mjj-config ~/mjj-config && rm -rf ~/.local/share/fcitx5/rime && cp -r ~/mjj-config/rime ~/.local/share/fcitx5/rime && rm -rf ~/mjj-config && rm -rf ~/.local/share/fcitx5/rime/weasel.yaml
```

```bash
cd ~/.local/share/fcitx5/rime && wget https://github.com/iDvel/rime-ice/releases/latest/download/all_dicts.zip && unzip ./all_dicts.zip && rm -rf ./all_dicts.zip || rm -rf ~/.local/share/fcitx5/rime/all_dicts.zip
```


重新部署   


Telegram 输入法提示框错位  

```bash
flatpak override --user --env=QT_IM_MODULE=fcitx5 org.telegram.desktop
```


皮肤  




## faltpak

```bash
alias flatpak='http_proxy="$http_proxy" https_proxy="$https_proxy" ftp_proxy="$ftp_proxy" all_proxy="$all_proxy" flatpak'
```





## todo  

鼠标, 输入法, 终端, 代理  

https://github.com/alacritty/alacritty



