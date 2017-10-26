1.fetch 使用了 JavaScript Promises 来处理结果/回调,从 fetch()返回的 Promise 将不会拒绝HTTP错误状态,  
即使响应是一个 HTTP 404 或 500。相反，它会正常解决 (其中ok状态设置为false), 并且仅在网络故障时或任何阻止请求完成时，它才会拒绝。
2. 默认情况下, fetch在服务端不会发送或接收任何 cookies, 如果站点依赖于维护一个用户会话，则导致未经认证的请求(要发送 cookies，必须发送凭据头).  

function ajax(url, fnSucc, fnFaild)
{
    //1.创建Ajax对象
    if(window.XMLHttpRequest){
       var oAjax=new XMLHttpRequest();
    }else{
       var oAjax=new ActiveXObject("Microsoft.XMLHTTP");
    }

    //2.连接服务器（打开和服务器的连接）
    oAjax.open('GET', url, true);

    //3.发送
    oAjax.send();

    //4.接收
    oAjax.onreadystatechange=function (){
       if(oAjax.readyState==4){
           if(oAjax.status==200){
              //alert('成功了：'+oAjax.responseText);
              fnSucc(oAjax.responseText);
           }else{
              //alert('失败了');
              if(fnFaild){
                  fnFaild();
              }
           }
        }
    };
}


var xhr = new XMLHttpRequest();
xhr.open('GET', url);
 
xhr.onload = function() {
    // To do with xhr.response
};
 
xhr.onerror = function() {
    // Handling errors
};
 
xhr.send();

Fetch 目前还不是 W3C 规范，由 whatag 负责出品。与 Ajax 不同的是，它的 API 不是事件机制，而采用了目前流行的 Promise 方式处理。我们知道 Promise 是已经正式发布的 ES6 的内容之一。

fetch("doAct.action", {
    method: "POST",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded"
    },
    body: "keyword=荣耀7i&enc=utf-8&pvid=0v3w1kii.bf1ela"
}).then(function(res) {
    if (res.ok) {
        // To do with res
    } else if (res.status == 401) {
        // To do with res
    }
}, function(e) {
    // Handling errors
});
