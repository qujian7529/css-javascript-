http://yujiangshui.com/grunt-basic-tutorial/  
Grunt一种自动化任务处理工具，是一个工具框架，有很多插件扩展它的功能，基于 Node.js，用 JS 开发，这样就可以借助 Node.js 实现跨系统跨平台的桌面端的操作，例如文件操作等等。
此外，Grunt以及它的插件们，都作为一个包 ，可以用NPM安装进行管理.  
所以 NPM 生成的 package.json 项目文件，里面可以记录当前项目中用到的 Grunt 插件，而 Grunt 会调用 Gruntfile.js 这个文件，解析里面的任务（task）并执行相应操作。
安装

    sudo npm install -g grunt-cli
    
项目加载包

    //合并文件：grunt-contrib-concat
    //语法检查：grunt-contrib-jshint
    //Scss 编译：grunt-contrib-sass
    //压缩文件：grunt-contrib-uglify
    //监听文件变动：grunt-contrib-watch
    //建立本地服务器：grunt-contrib-connect
    npm install grunt --save-dev
    npm install --save-dev grunt-contrib-concat grunt-contrib-jshint grunt-contrib-sass grunt-contrib-uglify grunt-contrib-watch grunt-contrib-connect

除了 Grunt 之外，同类型比较火的还有 Gulp 这个工具。其实两个东西的功能是一样的，只不过是任务配置 JS 的语法不同，Gulp 的 Gulpfile.js 的写法更加通俗易懂，上手更快。但是 Gulp 的插件等感觉不如 Grunt，Grunt 官方提供了一些常见的插件，满足大部分日常工作，而且可靠值得信赖，而 Gulp 好像没有太多官方出品，各种插件不太规范。

gulp 也类似  
gulpfile.js  
将需要的包下载下来引入包，然后创建一个任务  
    
    var sass = require('gulp-sass');
    gulp.task('sass',function(){
      return gulp.src('stylesheets/**/*.scss');
        .pipe(sass())
        .pipe(gulp.dest('dist/css'));
    });
