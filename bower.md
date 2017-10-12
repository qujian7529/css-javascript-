前端开发包管理工具
    
    $ npm install -g bower
    //安装包
    $ bower install <package>
    //如
    $ bower install jquery
    //他会自动下载相关依赖
    
    //使用包
    <script src="bower_components/jquery/dist/jquery.min.js"></script>
    
    //描述项目
    //列出需要的东西
    bower init
    
    //下载所有需要的东西
    bower install
    
    
    //查看包是干什么的,包的信息　　
    bower info bootstrap
    //查看摸个版本具体版本信息
    bower info bootstrap#3.0.0
    
 －－－－－－－－－－－－－－－－－－－－－－－－－　　
 
    //描述包　生成一个bower.json的文件,install会执行其内容下载相关文件
    bower init 
    //查看版本以及最新版本
    bower list 
    //更新,更改bower.json，然后update
    bower update
    //将更新的东西，记录到bower.json
    //"backbone":"~1.1.2" ~更新时更新　1.1.x
    //"bootstrap":">=3.0.0" 更新
    bower install backbone --save 
    //卸载
    bower uninstall backbone --save
    //对比bower.json 没有的就删除
    bower prune
    bower install
    //缓存查看
    bower cache list
    //用缓存安装
    bower install angular --offline --save
    //清空缓存
    bower cache clean
－－－－－－－－－－－－－－－－－－－－－－－－　　

    //major(变化比较大) minor(增加了一些功能) patch(修改了一些错误)
    //版本号更改
    //会将对应位置加１
    bower version　patch 
    bower version　minor
    bower version　major
    //指定
    bower version 0.0.2
    //自定义提交信息
    //%s包含版本号
    bower version patch -m '%s每次的改动注释'
 －－－－－－－－－－－－－－－－－－－－－－  
 
    
