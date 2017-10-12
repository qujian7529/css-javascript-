1.ajax
原生：

      var request;
      if(window.XMLHttpRequest){
        request = new XMLHttpRequest();
      } else{
        request = new ActiveXObject('Microsoft.XMLHTTP');
      } 

      console.log(request);

      // request.open(method,url,async) 　类型　url 是否异步
      // 表单提交　　请求头
      // request.setRequestHeader('Content-type','application/x-www-form-urlencoded');

      // request.send() get 不需要填写　post 需要

      request.open('GET','192.168.1.158',true);

      request.setRequestHeader('Content-type','application/x-www-form-urlencoded');	

      request.send();

      // request.status  :200: "OK"  ,404: 未找到页面
      // request.readyState存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
      if(request.readyState === 4 && request.status === 200){
        // 获得字符串形式的响应数据。
        request.responseText
        // 获得 XML 形式的响应数据
        request.responseXML
      }
      ---------------------------------------------------
      <script type="text/javascript">
    // 兼容低版本ie浏览器的代码,对于现代浏览器可以省略部分代码
    function createXHR() {
        if (typeof XMLHttpRequest != "undefined") {
            return new XMLHttpRequest();
        } else if (typeof ActiveXObject != "undefined") {
            if (typeof arguments.callee.activeXString != "string") {
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                        "MSXML2.XMLHttp"
                    ],
                    i, len;
                for (i = 0, len = versions.length; i < len; i++) {
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        break;
                    } catch (ex) {
                        //跳过
                    }
                }
            }
            return new ActiveXObject(arguments.callee.activeXString);
        } else {
            throw new Error("No XHR object available.");
        }
    }



    //拼接get方法传递的数据
    function addURLParam(url, name, value) {
        url += url.indexOf('?') == -1 ? '?' : '&';

        //encodeURIComponent编码
        url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
        return url;
    }



    var btn1 = document.querySelector("#btn1");
    var btn2 = document.querySelector("#btn2");

    //发送get请求
    btn1.onclick = function() {
        var url = addURLParam("http://127.0.0.1:8000/index", "name", "lisi");
        url = addURLParam(url, "age", 22);

        //创建xhr对象
        var xhr = createXHR();


        //状态切换时，要执行的代码
        xhr.onreadystate
        nge = function() {
            if (xhr.readyState == 4) {
                console.log(xhr.response);// "{name:'lisi', age: 22}"

                //解析json字符串
                var obj = JSON.parse(xhr.response);

                $(".stu tbody").append("<tr><td>" +obj.name + "</td><td>" + obj.age + "</td></tr>");
            }
        };

        //使用open创建一个异步请求
        xhr.open("get", url, true);


        //使用send方法 发送一个http请求
        //send方法不管有没有数据，都必须执行
        xhr.send(null);

    };


    //发送post
    btn2.onclick = function() {
        var xhr = createXHR();

        //创建post请求
        xhr.open("post", "http://127.0.0.1:8000/index", true);

        //设置传输的数据格式
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

        //send方法发送请求
        xhr.send("name=zhangsan&age=66");
    };
    </script>
jquery:

     <script src="./js/jquery-3.0.0.min.js"></script>
     

2.跨域
同源　：端口　协议 子域名　主域名　需要相同  　
跨域的方式：JSONP CORS  
jsonp只能发送 get 请求 script的特点时一旦加载成功就会立刻执行

html:

      <script type="text/javascript" src="http://127.0.0.1:8000?callback=handler"></script>
后台js:

      var fs = require("fs");
      var http = require("http");
      var url = require("url");
      http.createServer(function(req, res){


             var queryObj = url.parse(req.url, true).query;
             /*
                queryObj = {"callback": "handler"}
             */

             console.log(queryObj);

             fs.readFile("./test.json", function(err, data){
                  console.log(data);


                  // "hanlder(obj)";	 
                   res.write(queryObj.callback + "(" + data  + ")");

                   res.end();
             });


      }).listen(8000);

test.json:

      {
            "name": "lisi",
            "age": 10
      }
      
XHR2跨域：
服务端　
      
      header('Access-Control-Allow-Origin:*');
      header('Access-Control-Allow-Methods:POST,GET');
      
html:用ajax数据传输

      $.ajax({
            type:'GET',
            url:'http://127.0.0.1:8000',
            dataType:'json',
            success:function(data){
                  if(data.success){
                        console.log(111);
                  }else{
                        console.log(222);
                  }
            },error:function(jqXHR){
                  console.log(333);
            }
      })
3. apply() call()  
apply：应用某一对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即A对象应用B对象的方法.  
call：调用一个对象的一个方法，以另一个对象替换当前对象。例如：B.call(A, args1,args2);即A对象调用B对象的方法.  
共同点：都“可以用来代替另一个对象调用一个方法，将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象”.  
不同之处：参数传递方式不同　apply()数组的方式传递.  
用途：继承　多继承.

            function Class10(){
                    this.showSub = function(a,b){
                          alert(a - b);
                      }   
            }

            function Class11(){
              this.showAdd = function(a,b){
                    alert(a + b);
                }  
            }

            function Class12(){
              Class10.apply(this);
              Class11.apply(this);   
              // Class10.call(this);
              //Class11.call(this);  
            }

            var c2 = new Class12();
            c2.showSub(3,1);    //2
            c2.showAdd(3,1);    //4
4.js内置对象
