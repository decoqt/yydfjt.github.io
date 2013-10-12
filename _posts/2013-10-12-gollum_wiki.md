---
layout: post  
title: "gollum_wiki"  
categories: software



tags: gollum

---

#搭建个人wiki
##创建github
1. 在<https://github.com/>上面申请自己的账户，
2. 新建一个repo，获得自己repo的url，在最后.git前面加上.wiki 
3. 在本地git clone your-path-of-repo

##安装ruby 1.9.3
1. 安装rvm，
	
	`sudo bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer )`
	
2. 启一个会话课
3. 安装编译工具链
	+ xcode里面安装gcc，Xcode -> Preference -> Download下，查看“Command Line tools
	+ <https://github.com/kennethreitz/osx-gcc-installer> 来安装
4. 安装ruby，
	`rvm install ruby --head；rvm use 1.9.3 --default`
5. 修改源 
	`gem update --system;
	gem uninstall rubygems-update;
	gem sources -r http://rubygems.org/;
	gem sources -a http://ruby.taobao.org`

##安装gollum
1. 先更新库，做链接brew link(不然nokogiri会和libxml库不匹配)；
2. 安装gollum
   * gem install gollum
   * `git clone https://github.com/github/gollum；bundle install` 
   * 在wiki目录下新建一个文件Gemfile：
   	
   			source "http://rubygems.org"  
   			gem 'redcarpet'gem "grit", '~> 2.5.0',  
   			git: 'https://github.com/gitlabhq/grit.git', ref:'42297cdcee16284d2e4eff23d41377f52fc28b9d'  
   			gem 'gollum',git: 'https://github.com/gollum/gollum.git'，
		
然后执行bundle install；
  
 
		


##运行
在wiki目录下运行gollum，然后open http://localhost:4567就可以看到了

##进一步，使用pow自动化
1. 安装pow，https://github.com/37signals/pow， curl get.pow.cx | sh
2. 在wiki目录下创建文件config.ru，内容如下：

		require"gollum/app"  
		Precious::App.set(:gollum_path,File.dirname(__FILE__))  
		Precious::App.set(:wiki_options, {})  
		run Precious::App  
		#https://github.com/tecnh/gollum/wiki/Gollum-and-Passenger

3. 建立连接：cd ~/.pow ln -s ~/path/to/wiki
4. 设置环境变量，在wiki目录下创建.powrc,.rvmrv;内容分别为

		if [ -f "$rvm_path/scripts/rvm" ] && [ -f ".rvmrc" ]; then  
			source "$rvm_path/scripts/rvm"  
			source ".rvmrc"  
		fi

和

	rvm 1.9.3
5. open http://wiki.dev,网页上的改动会同步到本地，并且git保持其更改；进一步可以使用`git push origin `来推送到远端





