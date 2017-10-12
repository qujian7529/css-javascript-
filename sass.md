#### １．安装
安装Sass和Compass需要使用“Ruby”的gem命令，所以你要先确保在你的机器上已安装了Ruby著作权归作者所有。
  
    sudo gem install sass
    
    基本使用  
    //单文件转换命令
    sass input.scss output.css
    //单文件监听命令
    sass --watch input.scss:output.css
    //如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
    sass --watch app/sass:public/stylesheets
#### 2.compass安装

    sudo gem install compass
    //输出Sass时，输出一份详细的统计报告,输出的报告会包括Sass的规则，属性，mixin和使用mixin输出的CSS规则，以及相关统计
    gem install css_parser
    
#### 3.sass-->css

    compass watch

#### 4.css-->cass
工具：
CSS2Sass：复制你项目中的代码粘贴到工具中，看看它是如何转换成Sass。我不建议你将整个项目的代码复制，你可以复制几段代码尝试一下。一旦你感觉不错，你可以手写一些特性，包括选择器嵌套等。
Sassmeister：这基本上是Codepen的Sass。其最新版本引入了一个HTML组件，这样就可以帮助修改代码的时候就能看到效果。这个非常有用，不紧可以帮助你学习，而且这引入了Compass。
