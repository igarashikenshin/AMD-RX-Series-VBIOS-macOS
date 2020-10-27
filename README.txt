RX580在macOS下, 适用的VBIOS Serial：
			113-4E353BU-O4E (Samsung) 
			113-4E3531U-O4V (Hynix)
			113-4E353BU-O50 (Micron)
其他RX显卡可爬贴查询自己型号显卡在macOS对应的VBIOS Serial。


引言
起因：
从macOS 10.13起，当时我还在用1066，用webdriver的时候，一直感觉mac玩游戏虽然帧数很高，但就是有种顿卡的感觉（时钟型卡顿：每隔3s或每隔5s卡顿一下），起初以为是webdriver性能不好，后面更换rx580后，依然有这种顿卡的感觉，因为也没接触过白的imac，所以认为这就是macOS的通病。
后来去apple store用imac19.2体验了一下dota2，发现丝般顺滑，于是百思不得其解，难道是显卡没有完美驱动？在尝试丢掉weg，用默认inject ati启动后发现各种bug，退而求其次还是用回weg。
再后来在论坛里看到了注入fb name调用Orinoco的帖子，尝试注入之后发现显卡运行效率还不如直接用weg驱动，于是又排除了这一项解决方案。
很长一段时间这个事情就不了了之。

后续：
在疫情期间，升级了下主机，又开始了折腾之路，在逛论坛发现了RX580强刷VBIOS教程 原生调用 Orinoco FBname(http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1844201&highlight=vbios)
这篇内容，在一番尝试之后发现修改vbios会破坏固件签名，导致uefi gop没法加载，不能关闭csm，故放弃。
后来又尝试了xjn大佬的注入efi、rom的方法，发现注入进去之后还没有之前流畅，使用中也有卡顿现象，也放弃这种方法了。

再后续：
在爬tonymacx86时发现rx580在白果下对应的有3个vbios serial，分别是113-4E353BU-O4E (Samsung) ；113-4E3531U-O4V (Hynix)；113-4E353BU-O50 (Micron)。
同时我在github上面发现了428Yotsuba大佬整理的rx400-500系列显卡rom的仓库，我自己也fork整合了一份，下面教程会放上仓库地址。
然后开始了我的尝试，我是rx580 8G 2304sp镁光显存版，找到对应的113-4E353BU-O50 (Micron)，用amdvbflash刷入rom，重启进入macOS，清除缓存，再次重启，打开游戏，丝般顺滑，之前的顿卡都消失了。

特将此经验写成教程分享给各景友，希望能帮助到之前被黑果下游戏卡顿困扰的朋友@a6360280 @chengsitom

正文
本教程需要使用到的工具
1、atiflash_293(windows环境下操作）
2、对应型号的vbios rom文件（windows环境下刷入）
（仓库地址https://github.com/igarashikenshin/AMD-RX-Series-VBIOS-macOS）

操作步骤
1、找到显卡对应的vbios rom文件，这里以我的镁光显存rx580为例（rx580 rom链接https://github.com/igarashikenshin/AMD-RX-Series-VBIOS-macOS/tree/master/RX580/AppleDefaultROM），
打开链接找到对应镁光显存的113-4E353BU-O50 (Micron)，将rom下载到atiflash文件夹。
2、打开atiflash文件夹，在路径栏输入cmd，进入command line模式。
3、输入amdvbflash -i ，查询显卡对应slot编号，如为0，则用amdvbflash -f -p 0 xxx.rom（xxx.rom为你的rom名称）刷入vbios rom。（注意：rom名称不可命名过长，会产生未知错误。
4、修复权限 sudo mount -uw / && killall Finder  重建缓存sudo kextcache -i 
5、重启你的macOS，打开游戏，体验顺滑。
