<h2>AJAX函数封装</h2>

```
window.jQuery.ajax = function(obj){
    let url=obj.url
    let method=obj.method
    let body=obj.body
    let successFn=obj.successFn
    let headers=obj.heaaders
    let failFn=obj.failFn
    let request = new XMLHttpRequest()
    request.open(method, url) // 配置request第一部分
    for(let key in headers){
        let value = headers[key];
        request.setRequestHeader(key,value)
    }
    request.onreadystatechange = ()=>{
        if(request.readyState===4){
            if(request.status >= 200 && request.status < 300){
                successFn.call(undefined,x)
                //假如同时调用f1和f2可以这样写这里的x===request.responseText
                //f1.call(undefined,x)
                //f2.call(undefined,x)           
            }else if(request.status >= 400){
                failFn.call(undefined,request)
            }
        }
    }
    request.send(body)//设置请求的第四部分
}
```
<h2>AJAX函数调用</h2>
```
window.jQuery.ajax({
    url:'/xxx',
    method:'post',
    body:'a=1&b=2',
    headers:{
        'content-type':'application/x-www-form-urlencoded',
        'yukaka':'25'
    },
    successFn:function sss(x){console.log(x)},
    failFn:function fff(resquest){console.log('失败了')}  
})
```