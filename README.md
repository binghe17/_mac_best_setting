# Mac OS 最佳开发环境搭建


node -v
npm -v


---------------安装node.js (包含npm)------------------------------------

[Nodejs安装配置与教程](http://www.runoob.com/nodejs/nodejs-install-setup.html)
[Nodejs-文档](http://nodejs.cn/api/)

[Nodejs下载页](http://nodejs.cn/download/) : [node-v8.4.0.pkg](https://npm.taobao.org/mirrors/node/v8.4.0/node-v8.4.0.pkg)

# 说明：
#### This package will install Node.js v8.4.0 and npm v5.3.0 into /usr/local/.
#### Node.js was installed at /usr/local/bin/node
#### npm was installed at /usr/local/bin/npm
#### Make sure that /usr/local/bin is in your $PATH.

[express实例](http://www.cnblogs.com/chyingp/p/hbs-getting-started.html)


#细节：
	#### nodejs.org官网中下载mac版本程序。
	#### 安装node.js：从官网下载mac版的安装程序安装（#npm install node）

		#安装程序后显示信息
		#Node.js was installed at  	/usr/local/bin/node
		#npm was installed at 		/usr/local/bin/npm
		#Make sure that /usr/local/bin is in your $PATH.

	node -v		#显示版本号。（安装成功正常显示）



	#### 安装第三方插件
		#npm install -g 时保存路径为 /usr/local/lib/node_modules/
		#npm install --save * 时保存路径为 /Users/binghe17/node_modules/
		#npm install * 时保存路径为 /usr/local/node_modules/ (不正确要加--save)

	npm install --save redis		#安装redis数据库
	npm install --save mysql  		#安装mysql数据库
	npm install --save phantom		#网页截图
	npm install --save pageres
	npm install --save express
	npm install body-parser --save
	npm install cookie-parser --save
	npm install multer --save

	npm install --save socket.io

	npm install -g browser-sync		#前端实时可视化
	browser-sync start --server --files "**"



	######## 终端命令

	> process.env.PATH
	'/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'


		#添加环境变量
		#export PATH=/usr/local/python/bin:/usr/local/node/bin:$PATH


	# ============================================================================
	###########################sublime text的快捷键

		/Users/binghe17/Library/Application Support/Sublime Text 3/Packages/User/javascript.sublime-build文件内容
		####
		{
		"cmd": ["/usr/local/bin/node", "$file"],
		"file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
		"selector": "source.js"
		}
		####


	command+b 开始nodejs服务器
	control+c 关闭nodejs服务器



	#----------------nodejs能够监听80端口吗？

	#----防火墙
	首先，非root用户不能监听<1024的端口，这个是内核代码里写着的。
	其次，不应该用root用户运行你的程序，这样会有安全问题。
	答案是用iptables：
	$ sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3000
	$ sudo iptables-save

		#linux
		iptables -t nat -A OUTPUT -p tcp --dport 80 -d 192.168.1.7 -j DNAT --to-destination 127.0.0.1:3000
		
		#mac os x 临时
		$ sudo ipfw add fwd 127.0.0.1,8000 tcp from any to 192.168.1.7 80
		$ sudo ipfw list 
			00100 fwd 127.0.0.1,8000 tcp from any to 192.168.1.7 dst-port 80
			65535 allow ip from any to any
		$ sudo ipfw del 00100


	#----
	linux平台的非root用户要让node运行在80端口下，可以这样：
	然后用普通用户试试， 注意这要linux内核在2.2后的系统，更多详细的解释可以 man capabilities.
	$ sudo setcap CAP_NET_BIND_SERVICE+ep  /usr/local/bin/node




---------------安装 Bower (twitter 推出的一款包管理工具)------------------

[bower使用方法](http://blog.fens.me/nodejs-bower-intro/) [1](https://www.biaodianfu.com/bower.html)

# 1. bower介绍
一个新的web项目开始，我们总是很自然地去下载需要用到的js类库文件，比如jQuery，去官网下载名为jquery-1.10.2.min.js文件，放到我们的项目里。当项目又需要bootstrap的时候，我们会重复刚才的工作，去bootstrap官网下载对应的类库。如果bootstrap所依赖的jQuery并不是1.10.2，而是2.0.3时，我们会再重新下载一个对应版本的jQuery替换原来的。

# 2. bower安装
### 全局安装bower
	npm install bower -g

### 新建一个express3的项目nodejs-bower
	express -e nodejs-bower
	cd nodejs-bower && npm install


# 3. bower命令
	》bower

	Usage:
	    bower [] []
	Commands:
		cache:bower缓存管理
		help:显示Bower命令的帮助信息
		home:通过浏览器打开一个包的github发布页
		info:查看包的信息
		init:创建bower.json文件
		install:安装包到项目
		link:在本地bower库建立一个项目链接
		list:列出项目已安装的包
		lookup:根据包名查询包的URL
		prune:删除项目无关的包
		register:注册一个包
		search:搜索包
		update:更新项目的包
		uninstall:删除项目的包


# 4. bower使用
1). 安装jQuery到项目nodejs-bower
	bower install jquery
	ls bower_components/jquery -a
	bower install d3

2). 查看项目中已导入的类库
	bower list

3). 安装bootstrap库，并查看依赖情况
	bower install bootstrap
	bower list

4). 删除jQuery库，破坏依赖关系
	bower uninstall jquery
	bower list

5). 安装低版本的jQuery，制造不版本兼容
	bower install jquery#1.7.2
	bower list

6).升级jQuery，让版本兼容
	bower update jquery
	bower list

7). 查看本地bower已经缓存的类库
	bower cache list

8). 查看D3库信息
	bower info d3

9). 查看dojo库的url
	bower lookup dojo

10). 用浏览器打开dojo的发布主页
	bower home dojo

11). 查询包含dojo的类库
	bower search dojo


# 5. 用bower提交自己类库
1). 生成bower.json配置文件
	bower init

2). 在github创建一个资源库：nodejs-bower
3). 本地工程绑定github
	git init
	git add .
	git commit -m "first commit"
	git remote add origin https://github.com/bsspirit/nodejs-bower
	git push -u origin master

4). 注册到bower官方类库
	bower register nodejs-bower git@github.com:bsspirit/nodejs-bower.git

5). 查询我们自己的包
	bower search nodejs-bower

6). 安装我们自己的包
	bower install nodejs-bower


# 如何把自己的插件发布到bower平台(bower.json) [!](https://getpocket.com/a/read/1183696629)
git tag 0.1.0  
git push origin --tags   
bower register ajaxData  https://github.com/bxcn/ajaxData   
bower install --save-dev ajaxData  

bower login  
#### enter username and password  
#### bower unregister <package>  
bower unregister ajaxData


-----------------升级 ruby版本（当前版本为ruby 2.0.0p648 2015-12-16）----------------

[ruby升级教程](http://blog.csdn.net/sharpyl/article/details/52786676)

第一步：安装rvm
ruby -v 
curl -L get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
ruby -v 

第二步：安装ruby
rvm list known				#列出ruby可安装的版本信息
rvm install 2.1.4			#安装一个ruby版本
rvm use 2.1.4 --default 	#设置为默认版本
rvm list					#查看已安装的ruby
rvm remove 2.1.4  			#卸载一个已安装ruby版本

第三步：更换源
gem source
gem update --system
gem uninstall rubygems-update
gem sources -r http://rubygems.org/
gem sources -a http://ruby.taobao.org


-----------------安装 brew (又叫Homebrew软件包管理工具)-----------------------------------

[brew安装教程](http://www.cnblogs.com/TankXiao/p/3247113.html)
[brew官方网站](http://brew.sh/)

# 1.安装 (保存在/usr/local/)
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### 不要顺序执行，命令参考（先了解命令的作用，然后选择性执行）
brew install git
brew install wget
brew search /wge*/
cd /usr/local
find Cellar
ls -l bin
brew create https://foo.com/bar-1.0.tgz
brew edit wget #opens in $EDITOR!

brew list       #列出已安装的软件
brew update     #更新brew
brew home       #用浏览器打开brew的官方网站
brew info       #显示软件信息
brew deps       #显示包依赖


sudo chmod -R 775 /usr/local/Library
sudo chmod -R 775 /usr/local/Cellar

cd /usr/local/Library
git pull origin master


-----------------安装git----------------------------

1.下载并安装
[git官网下载](https://git-scm.com/downloads) [mac下载](https://git-scm.com/download/mac) [git-2.7.1-intel-universal-mavericks.dmg](https://downloads.sourceforge.net/project/git-osx-installer/git-2.7.1-intel-universal-mavericks.dmg?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fgit-osx-installer%2F&ts=1503217856&use_mirror=jaist)

2.创建SSH
cd ～/.ssh & ssh-keygen -t rsa -C xxxxx@qq.com
#### 将生成的id_rsa.pub文件打开，拷贝其中的公钥内容，再github上进行粘贴。即可创建和github的ssh链接。

3.测试链接是否成功
ssh -T git@github.com



-----------------MongoDB-------------------------

[MongoDB安装教程](http://www.runoob.com/mongodb/mongodb-osx-install.html)
[MongoDB可视化管理工具](http://www.mongoing.com/archives/3651) : [adminMongo不错](https://github.com/mrvautin/adminMongo)

#进入 /usr/local
cd /usr/local
#下载
sudo curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-3.4.2.tgz
#解压
sudo tar -zxvf mongodb-osx-x86_64-3.4.2.tgz
#重命名为 mongodb 目录
sudo mv mongodb-osx-x86_64-3.4.2 mongodb

#把MongoDB的二进制命令文件目录（安装目录/bin）添加到PATH路径中
export PATH=/usr/local/mongodb/bin:$PATH

# 使用 brew 安装 (选第一个命令执行)
sudo brew install mongodb
sudo brew install mongodb --with-openssl
sudo brew install mongodb --devel

# 运行 MongoDB
sudo mkdir -p /path/mongo_dbfiles/
cd /usr/local/mongodb/bin/
sudo ./mongod --dbpath /path/mongo_dbfiles/
./mongo


------------------mysql------------------------------

# MySQL 5.7 for Mac v5.7.19 苹果电脑版(附安装教程)Mac版MySQL5.7
[mysql下载页](http://www.jb51.net/softs/567704.html) : [mysql-5.7.19-macos10.12-x86_64.dmg下载](http://www.jb51.net/do/softdown.php?url=https%3A%2F%2Fcdn.mysql.com%2F%2FDownloads%2FMySQL-5.7%2Fmysql-5.7.19-macos10.12-x86_64.dmg) 软件大小：339MB

MySQL 是最流行的关系型数据库管理系统之一，目前市面上大部分网站都是使用的MySQL数据库，
MySQL Community Server mac版是用于苹果mac系统的数据库软件，
而且MySQL Community Server这个不要钱！下载好之后发现只有一个dmg主文件，
貌似5.7之前的版本会有多个安装文件。点开mysql-5.7.19-macos10.12-x86_64.dmg这个文件，
逐步安装，注意在成功的时候会弹出提示框，给出临时密码，一定要记住，一定要记住，一定要记住！！！！ 
如果没找到，请桌面右拉看notifications。

安装教程
　　#下载Mac版MySQL 5.7，我下载的是 mysql-5.7.19-macos10.12-x86_64.dmg
　　#下载完直接安装，一路无话。
　　#值得注意的是：安装完后会提示 弹窗root账号密码，请把他它记录下来后面我们会用到
　　#安装完后在终端并不能识别 mysql 命令，需要配置一下

cd /usr/local/bin/
sudo ln -fs /usr/local/mysql/bin/mysql mysql
mysql --version  #能显示 mysql 版本说明 mysql 安装成功

## 修改root账号的密码：
sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
mysql -u root

## 会进入 mysql 命令模式，逐行输入下面命令
UPDATE mysql.user SET authentication_string=PASSWORD('*****') WHERE User='root';
FLUSH PRIVILEGES;
\q

## 修改完后验证密码
mysql -u root -p




