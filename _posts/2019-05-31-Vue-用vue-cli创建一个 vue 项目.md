一句话：在命令行  vue init webpack “项目名”


1. 安装node.js
	+ 官网 download LTS（更稳定）对应安装包
2. cmd 
	+ -- node -v => node是否安装成功
	+ -- npm -v => npm是否安装成功
3. 码云注册 
	+ 创建项目（仓库）
``本地代码与线上代码通过Git相关联``
4. download Git
5.  cmd 
	+ git --version
		+ ==报错== https://blog.csdn.net/wochunyang/article/details/70674252
	+ git --version =》 git是否安装成功
6. 码云--个人--设置--SSH公钥 --点击怎样生成公钥
7. windows桌面点击右键--git bash (类似Linux)
8. git bash 中
	+ 运行![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530200925479.png)
	+ 查看![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530201001233.png)里面的内容![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530201025371.png)
	+ 将公钥粘贴回码云公钥的地方![在这里插入图片描述](https://img-blog.csdnimg.cn/2019053020110185.png)
9. 复制地址![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530221922607.png)
10. git bash 中  切换到自己想要的文件夹内
	+ git clone ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530222251390.png)
11. vue官网安装vue cli脚手架工具
``大型项目：webpack进行构建，做一些语法的解析=》通过命令行工具来构建工程 ``
12. 命令行内：安装vue cli
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530230152347.png)
13. 命令行内：切换到自己所需要的文件夹下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224029452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224507434.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224625770.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224727243.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224811318.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530224922633.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530225117109.png)
14. 进入建立的那个文件夹里![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530225309963.png)
![15.](https://img-blog.csdnimg.cn/20190530225347423.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190530225423963.png)
==localhost：8080运行后如此代表项目创建成功==![在这里插入图片描述](https://img-blog.csdnimg.cn/20190531104845552.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
15. 命令行内把文件添加到线上仓库
	+ 命令行--输入git status ==》可以查看到有很多文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190531103325951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
	+ git add . 先把所有文件增加到git的缓冲区 
	+ git commit -m 'project initialized'
	==报错==![在这里插入图片描述](https://img-blog.csdnimg.cn/20190531104315286.png)
	Windows内使用双引号，即 git commit -m “project initialized”
=》https://blog.csdn.net/eebaicai/article/details/84672393
	+ git push
	==至此文件已添加到线上仓库==
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190531104641841.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191010202245687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FkYV9sYWtl,size_16,color_FFFFFF,t_70)

总结：
16. 查看node、npm是否安装成功
17.将git和本地联系起来   
	 1. git bash中  ssh-keygen -t rsa -C "XXX@163.com"
	 2.  cat ~/.ssh/id_rsa.pub 找到公钥
	 3. 复制公钥到线上仓库
17. 在Git上创建仓库并拉到本地
	1. 【在自己想要放置的文件夹内】git clone "仓库地址" 
	2. 【命令行中】npm install --global vue-cli
	3. 【自己想要放置的文件夹内】 vue init webpack "项目名【和仓库名一样】"

# ==命令行中==
## == 1. 安装vue-cli==
# 此后只需：
## ==2. vue init webpack "项目名" ==【vue初始化一个基于webpack的项目】
# 接下来按步骤操作即可
===》

***`命令行中 vue init webpack "项目名"`***


