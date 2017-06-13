#Core引擎盒子环境安装步骤#


##1.设置系统的管理员密码、永不过期、重启后自动登录##

- 操作系统前提: win7, 管理员登录，请设置管理员密码为`core`，便于防止陌生人登录及病毒后门入侵。
- 右键“我的电脑”》选择“管理”》选择“本地用户和组”》选择“用户”》选择你要设置密码的用户名》右键“属性”》勾选“密码永不过期”。
- 设置win7自动登录：[怎样让计算机自动登录(Windows 7)](http://jingyan.baidu.com/article/455a9950ec8ae8a16627788a.html)) 



##2. 安装数据库##

- 安装mysql community server 5.1.60 windows版本（32或64位均支持)，安装过程中设置字符集为utf8，root账户密码为调试密码（该密码需向公司询问），安装目录可采用默认方式。 
- MySQL官方下载地址：[MySQL官方下载地址](http://downloads.mysql.com/archives/community/))

##3.安装引擎核心程序##
- Gatewaycore  下载地址: [core.rar](http://beop.rnbtech.com.hk/static/help/BEOPGatewayCore_2015_12_18.rar)，本软件为绿色软件，下载后可任意位置放置，建议统一在d:\core目录下，解压即可。
- 将GatewayCore.exe加入系统的启动项中，在开始菜单中在启动上右键-打开，创建快捷方式到Gatewaycore.exe


##4.启动引擎##
- 通过双击GatewayCore.exe即可启动引擎
- 启动后console窗口显示 `engine started successfully`表示启动成功

		提示：当Gatewaycore引擎启动时，将有看门狗软件BeOPWatch.exe同时自动运行在后台，
		在桌面右下角通知区看到BEOPWatch的图标，通过点击可以看到监视状态。

##5.将数据远传到数据服务器##

设置前，确保上述安装均正确，并且core已经正常启动，同时请索取到**数据服务器地址**。

当项目使用DTU作为远传通道时，请参考5.1进行设置；如果直接可以联网，请参考5.2设置。 设置完均需执行5.3的设置。

###5.1 使用DTU作为远传通道时的设置###


推荐使用配备到现场的数据引擎PC网线连接路由器DTU进行设置,操作数据引擎PC可以直接使用鼠标键盘等输入设备,也可以使用自带笔记本远程连接数据引擎PC.(开始菜单->附件->远程桌面连接->输入数据引擎PC的IP->连接)

以下介绍的是使用数据引擎PC,首次设置路由器DTU的步骤: 硬件接线准备：确保调试笔记本或引擎盒子连接到了DTU的LAN口。

1由于DTU默认地址为192.168.8.1，因此首先将需要数据引擎MiniPC的IP 设置成192.168.8.X(路由器DTU的IP默认192.168.8.1)
 ![](http://beop.rnbtech.com.hk/static/images/download/dtu001.png)

2:打开浏览器中输入网址192.168.8.1（路由器默认地址） ，用户名：admin密码：admin
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu002.png)

3：将下图”网页设置”->”LAN”中的IP1中的“192.168.8.1/24”改成现场网段(例如”192.168.1.241/24”或者”192.168.5.241/24”,即跟现场设备环境同一网段),保存。（一般无IP冲突的情况下，默认将数据引擎PC的IP配成“192.168.1.240”，路由器DTU的IP配成“192.168.1.241”。）
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu003.png)

4：将数据引擎PC的IP改成“192.18.1.240”，默认网关填“192.168.1.241”（路由器DTU的IP）。在浏览器中输入网址192.168.1.241（路由器默认地址） ，用户名：admin密码：admin ，重新登陆路由器DTU。
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu004.png)

5：进入“网络设置”->“移动网络”,点击编辑按钮，在网络接入点中填写”cnet”,保存.
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu005.png)

6: 进入“网络设置”->“DHCP服务”,点击禁用按钮，将DHCP服务禁用，保存. 禁用的主要目的是屏蔽内网用户通过dtu访问网页。
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu006.png)

7: 进入“状态”->“移动网络状态”,查看信号强度（3格为普通，基本满足传输需求，信号太弱，容易造成通讯掉线）
  ![](http://beop.rnbtech.com.hk/static/images/download/dtu007.png)

8：最后测试网络状态，可以从“开始菜单”->“运行”-> 输入cmd，打开命令窗口，输入ping命令，ping一下数据服务器地址，ping通即设置完成。

以上步骤完成后，可进入5.3设置。

		备注：已修改过的路由器DTU设置方法：如果忘记路由器DTU的IP只能恢复出场设置,再重新按前面设置路由器DTU的步骤操作。

###5.2 使用局域网直接上网作为远传通道时的设置###
  从“开始菜单”->“运行”-> 输入cmd，打开命令窗口，输入ping命令，ping一下数据服务器地址，如果成功表示可以进入5.3部分设置。


###5.3 使用局域网直接上网作为远传通道时的设置###
以下介绍的是使用数据引擎盒子,首次设置Core启用该路由器传输数据设置:

 使用Factory中调试工具，连接数据引擎盒子的IP，登录后，打开“通讯调试”面板，勾选“启用TCP”，最小发送类型设为“5分钟”，数据中心地址填入索取到的**数据服务器地址**，端口“9500”，TCP项目标识“xxxxxxxxxx”（TCP项目标识用于区分项目，只能使用英文字母及数字，长度不能超过11位，一般使用城市+项目缩写+补齐数字，例如郑州万达商业项目起名参考：zzwdsy20159），修改完成点击“修改设置”保存即可。
![](http://beop.rnbtech.com.hk/static/images/download/dtu008.png)

其他配置选项请使用默认。

以上步骤完成后，重启core软件（直接关闭Core软件即可，看门狗程序会自动将core重启）
