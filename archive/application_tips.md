## Chrome    

- 关闭chrome的QUIC协议, 步骤:打开chrome://flags将`Experimental QUIC protocol`选项设置为`Disabled`  原因: 国内垃圾运营商对UDP协议不友好  





##### 扩展      

- [Easy Scraper](https://chromewebstore.google.com/detail/easy-scraper-one-click-we/cljbfnedccphacfneigoegkiieckjndh)         

- [uBlock Origin](https://chromewebstore.google.com/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)         

- [WebRTC Control](https://chromewebstore.google.com/detail/webrtc-control/fjkmabmdepjfammlpliljpnbhleegehm)        

- [暴力猴](https://violentmonkey.github.io)           

- [沉浸式翻译](https://chromewebstore.google.com/detail/沉浸式翻译-网页翻译插件-pdf翻译-免费/bpoadfkcbjbfhfodiogcnhhhpibjhbnh?hl=zh-CN)           


##### 插件          

- [Make BiliBili Great Again](https://greasyfork.org/zh-CN/scripts/415714-make-bilibili-great-again)         

- [Github中文插件](https://github.com/maboloshi/github-chinese)       



## Telegram      

1. 关闭windows客户端字体锯齿, 解决办法: 设置, 高级设置, 实验性功能, 拉倒最下选中`FreeType font engine`         




## Git Bash For Windows Terminal  

1. 解决退格闪屏问题：修改Git安装目录下/etc/inputrc文件的`set bell-style visible` 为 `set bell-style none`        

2. 解决历史记录问题：在 `C:\Users\linyz\scoop\apps\git\current\etc\bash.bashrc` 文件中第15行添加一行 `PROMPT_COMMAND='history -a'`               



## MPV    

设置mpv为默认播放器       
[github mpv-install](https://github.com/rossy/mpv-install) 




## Scoop     

1. [Scoop包管理器的相关技巧和知识](https://www.thisfaner.com/p/scoop)    
2. [博客 Scoop入门](https://ericzonglu.gitee.io/posts/tool-scoop-get-start.html)         

如果安装出错尝试           

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

iex "& {$(irm get.scoop.sh)} -RunAsAdmin"
```



## Thunder Client    
[Thunder Client 使用文档](https://docs.thunderclient.com)     



## Rime 输入法     

[小狼毫&雾凇拼音安装及部署 - windows](https://www.cnblogs.com/HookDing/p/17949199)           
[Rime - 最强中文输入法引擎 + 雾凇拼音输入方案 配置](https://zhiqiu.vercel.app/post/2AGco8msp)          



## AHK   

```ahk
CapsLock::Ctrl

; 当按下 Ctrl + Alt + I 时打开指定目录
^!i::  ; ^ 表示 Ctrl，! 表示 Alt
    Run, C:\loading\task-runtime
return
```



## windows 磁盘管理  

[磁盘管理 删除 EFI 系统分区](https://blog.csdn.net/BlacKingZ/article/details/122563000)       
[删除 BIOS/UEFI 启动项](https://www.cnblogs.com/litifeng/articles/18192644)     

##### 禁用 windows 服务: 注册表找到对应服务名称, 点击右边start修改为4    

```text
计算机\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\
```

##### 删除 BIOS/UEFI 启动项

cmd 管理员模式打开, 查看有哪些选项  

```cmd
BcdEdit /enum firmware
```

备份配置  

```cmd
BcdEdit /export oldbcd
```

*可选*  

```bash
cp ./oldbcd ./newbcd
```

删除选项  

```cmd
BcdEdit /store oldbcd /delete {编号}
```

最后, apply

```bash
BcdEdit /import oldbcd /clean
```


##### 删除 EFI 系统分区

cmd 启动 diskpart  

```cmd
diskpart
```

选择磁盘  

```cmd
list disk
```

```cmd
sel disk {磁盘编号}
```


选择分区  

```cmd
list partition
```

```cmd
sel partition {efi 分区编号}
```


格式化分区  

```bash
SET ID=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
```






## adb + scrcpy 局域网连接

```bash
adb tcpip 2024
```   

```bash
adb connect 192.168.1.120:2024
```

```bash
adb devices
```

scrcpy 连接到设备   

```bash
scrcpy -s 192.168.1.120:2024
```





## pixel  

```bash
adb reboot bootloader
```

```bash
fastboot flash boot ./magisk_patched-25200_K0IVs.img
```





## misc  

- 转接微信客服的办法，95017 输入5 输入3 秒接英文的人工客服          





