---
title: IOS文件上传PUT和POST
date: 2020-04-03 18:55:42
categories:
- OC
- 上传
tags: 上传
---

## 一、 简介

### 1、简单介绍

1. 在HTTP协议请求中，有8种方法：

-  GET：请求指定的页面信息，并返回实体主体。
-  HEAD：类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头
-  POST：向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改。
-  PUT：从客户端向服务器传送的数据取代指定的文档的内容。
-  DELETE：请求服务器删除指定的页面。
-  CONNECT：HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。
-  OPTIONS：允许客户端查看服务器的性能。
-  TRACE：回显服务器收到的请求，主要用于测试或诊断。
-  PATCH：是对 PUT 方法的补充，用来对已知资源进行局部更新 。

### 2、区别
本文主要介绍put和post上传文件的方式，先来看一下，他们的特点:

1. PUT方法的特点：传输的实体部分是一个无结构的二进制数据。
2. POST方法的特点：倾向于结构化的数据。

上传文件这个行为本身就是无结构数据的传输（文件是一个整体，文件的内容与传输行为无关），所以使用PUT更合适。当然，上传文件这个行为不光是把文件丢到服务器上而已，可能还需要传递一些文件的相关信息，比如文件在客户端的文件名之类的，这在使用POST方法时很容易实现。其实使用PUT方法也不存在什么问题，这些额外信息完全可以用自定义的HTTP请求头来传输。

那为什么现在都流行使用post上传文件呢？

因为当年的Web没有太多API的支持，只能用表单来上传文件，所以后来大家也习惯了使用POST。


备注：本篇只简单介绍有关put和post上传文件的不同，至于上传请求头设置，请求体设置(文件参数和非文件参数拼接)， 小编这里不再赘述，会找出专门的篇幅来叙述这个。

## 二、HTML文件上传  
这里为什么要写html的方式上传文件呢？ 

因为在实际的项目编码中，有时候，使用ios上传文件不成功，可以先试着使用html网页上传文件的方式试一试，如果html的方式能成功，则可以对照html的方式，去找出ios对应的方法来。之前小编就是遇到了这样的问题，最后就是通过这样的方式试出来的。

### 1、post上传文件：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
    <title>post上传文件</title>
</head>
<body>
   <form action="***这里是上传url***" method="post" enctype="multipart/form-data">
       <input type="file" name="fileUpload" />
       <input type="submit" value="上传文件" />
   </form>
</body>
</html>

```

### 2、put上传文件

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
    <title>XMLHttpRequest上传文件进度实现</title>
    <script type="text/javascript">
        var xhr;
        var ot;//
        var oloaded;
        //上传文件方法
        function UpladFile() {
            var file = document.getElementById("file").files[0];
            var reader = new FileReader();
            //将文件以二进制形式读入页面
            reader.readAsArrayBuffer(file);
            reader.onload=function(f){
                var rawData = reader.result;
                var url = "***上传路径***"; // 接收上传文件的后台地址
                xhr = new XMLHttpRequest();  // XMLHttpRequest 对象
                xhr.open("post", url, true); //post方式，url为服务器请求地址，true 该参数规定请求是否异步处理。
                xhr.setRequestHeader("Content-Type", "video/mp4");
                xhr.setRequestHeader("x-content-range", "bytes 0-298327/298328"); //这个参数是后台要求的，自定义的，目前是写死的，调试用，无所谓的。
                xhr.setRequestHeader("content-length", "298328");   //这个值是小编根据文件大小写上的，文件大小是多少，这里就是多少。为啥要写死？ 调试上传文件，不用每次都变一个上传文件
                xhr.onload = uploadComplete; //请求完成
                xhr.onerror =  uploadFailed; //请求失败
                xhr.upload.onprogress = progressFunction;//【上传进度调用方法实现】
                xhr.upload.onloadstart = function(){//上传开始执行方法
                    ot = new Date().getTime();   //设置上传开始时间
                    oloaded = 0;//设置上传开始时，以上传的文件大小为0
                };
                xhr.send(rawData); //开始上传
            }
            
        }
        //上传进度实现方法，上传过程中会频繁调用该方法
        function progressFunction(evt) {
            
             var progressBar = document.getElementById("progressBar");
             var percentageDiv = document.getElementById("percentage");
             // event.total是需要传输的总字节，event.loaded是已经传输的字节。如果event.lengthComputable不为真，则event.total等于0
             if (evt.lengthComputable) {//
                 progressBar.max = evt.total;
                 progressBar.value = evt.loaded;
                 percentageDiv.innerHTML = Math.round(evt.loaded / evt.total * 100) + "%";
             }
            
            var time = document.getElementById("time");
            var nt = new Date().getTime();//获取当前时间
            var pertime = (nt-ot)/1000; //计算出上次调用该方法时到现在的时间差，单位为s
            ot = new Date().getTime(); //重新赋值时间，用于下次计算
            
            var perload = evt.loaded - oloaded; //计算该分段上传的文件大小，单位b
            oloaded = evt.loaded;//重新赋值已上传文件大小，用以下次计算
        
            //上传速度计算
            var speed = perload/pertime;//单位b/s
            var bspeed = speed;
            var units = 'b/s';//单位名称
            if(speed/1024>1){
                speed = speed/1024;
                units = 'k/s';
            }
            if(speed/1024>1){
                speed = speed/1024;
                units = 'M/s';
            }
            speed = speed.toFixed(1);
            //剩余时间
            var resttime = ((evt.total-evt.loaded)/bspeed).toFixed(1);
            time.innerHTML = '，速度：'+speed+units+'，剩余时间：'+resttime+'s';
               if(bspeed==0)
                time.innerHTML = '上传已取消';
        }
        //上传成功响应
        function uploadComplete(evt) {
         //服务断接收完文件返回的结果
         //    alert(evt.target.responseText);
             alert("上传成功！");
        }
        //上传失败
        function uploadFailed(evt) {
            alert("上传失败！");
        }
          //取消上传
        function cancleUploadFile(){
            xhr.abort();
        }
    </script>
</head>
<body>
    <progress id="progressBar" value="0" max="100" style="width: 300px;"></progress>
    <span id="percentage"></span><span id="time"></span>
    <br /><br />
    <input type="file" id="file" name="myfile" />
    <input type="button" onclick="UpladFile()" value="上传" />
    <input type="button" onclick="cancleUploadFile()" value="取消" />
</body>
</html>

```

## 三、 IOS上传文件
以下都是使用AFN框架上传文件（使用 NSURLSession 上传文件，暂时未写)
### 1、post方法上传

```
NSString *urlString = @"";
AFHTTPRequestOperationManager *mgr = [AFHTTPRequestOperationManager manager];
//普通参数
NSMutableDictionary *params = [NSMutableDictionary dictionary];
[params setObject:@"张三" forKey:@"username"];
[mgr POST:urlString parameters:params constructingBodyWithBlock:^(id<AFMultipartFormData> formData) {
    NSData *imageData = UIImagePNGRepresentation([UIImage imageNamed:@""]);   
     /**
     拼接文件参数
     @fileData : 要上传的文件数据
     @name : 后台定义文件的参数名
     @fileName ： 上传到服务器的文件名称
     @mimeType : 上传的文件类型
   */
    [formData appendPartWithFileData:imageData name:@"file" fileName:@"text.png" mimeType:@"image/png"];
} success:^(AFHTTPRequestOperation *operation, id responseObject) {
        
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
        
}];
```

```
/**
 获取文件的MIMEType
 @param url 文件路径
 @return 文件MIMEType
 */
- (NSString *)MIMEType:(NSURL *)url{
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    NSURLResponse *response = nil;
    [NSURLConnection sendSynchronousRequest:request returningResponse:&response error:nil];
    return response.MIMEType;
}
```

### 2、put方法上传

```
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"请求路径url"]];
//设置header参数
[request setValue:@"这是自定义头参数" forHTTPHeaderField:@"x-content-length"];
    
//获取需要上传的Data， 将其保存到沙盒中
_needUploadData = [self getNeedUploadData];
NSString *docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) objectAtIndex:0];
NSString *filePath = [docPath stringByAppendingPathComponent:@"test"];
[_needUploadData writeToFile:filePath atomically:YES];
    
NSURL *url = [NSURL URLWithString:filePath];

AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
_uploadTask = [manager uploadTaskWithRequest:request fromFile:url progress:^(NSProgress * _Nonnull uploadProgress) {
    NSLog(@"uploadProgress：%@",uploadProgress);
    float progress =  1.0 * uploadProgress.completedUnitCount/uploadProgress.totalUnitCount;
    NSLog(@"上传视频进度%f",progress);
} completionHandler:^(NSURLResponse * _Nonnull response, id  _Nullable responseObject, NSError * _Nullable error) {
    NSLog(@"上传结果%@",responseObject);
}];
    
[_uploadTask resume];
```

注： 通过抓包，要注意content-type 和 content-length, 这里的content-length一定要等于要上传的文件大小。

 ![URI结构图](/img/ios_pangzhanli/FileUpload/FileUpload_put_remark.png)


### 3、文件操作
在上传文件的时候，如果文件较小，可以一次性上传，如果文件比较大的话，得将文件切分，分成若干个片断，依次上传。在ios中，操作文件会使用到, NSFileHandle 和 NSFileManager 这两个类。

*  NSFileHandle： 主要是对文件内容进行读取和写入操作

*  NSFileManager： 主要是对文件进行的操作以及文件信息的获取

在上边上传文件的过程，咱们就使用了切分文件这种操作，主要用到 NSFileHandle类的seekToFileOffset这个方法

```
//获取需要上传的数据
-(NSData *)getNeedUploadData{
    //使用传递过来的文件上传
    NSFileHandle *fileHandle = [NSFileHandle fileHandleForReadingAtPath:_filePath];
    [fileHandle seekToFileOffset:_startUploadLoaction];

    NSInteger uploadLength = GMOTPosterAdd_uploadVideoSizeForEveryOne;
    if((_startUploadLoaction + GMOTPosterAdd_uploadVideoSizeForEveryOne) > _fileTotalSize){
        uploadLength = _fileTotalSize - _startUploadLoaction;
    }
    NSData *data = [fileHandle readDataOfLength:uploadLength];

    return data;
}

```

## 四、 Content-Type类型介绍

MediaType，即是Internet Media Type，互联网媒体类型；也叫做MIME类型，在Http协议消息头中，使用Content-Type来表示具体请求中的媒体类型信息。

```
类型格式：type/subtype(;parameter)? type  
主类型，任意的字符串，如text，如果是*号代表所有；   
subtype 子类型，任意的字符串，如html，如果是*号代表所有；   
parameter 可选，一些参数，如Accept请求头的q参数， Content-Type的 charset参数。   
```

常见的媒体格式类型如下：

-   text/html ： HTML格式
-   text/plain ：纯文本格式     
-   text/xml ：  XML格式
-   image/gif ：gif图片格式    
-   image/jpeg ：jpg图片格式 
-   image/png：png图片格式

以application开头的媒体格式类型：

-   application/xhtml+xml ：XHTML格式
-   application/xml     ： XML数据格式
-   application/atom+xml  ：Atom XML聚合格式  
-   application/json    ： JSON数据格式
-   application/pdf       ：pdf格式  
-   application/msword  ： Word文档格式
-   application/octet-stream ： 二进制流数据（如常见的文件下载）
-   application/x-www-form-urlencoded ：  ( <form encType="">)默认的encType，form表单数据被编码为key/value格式发送到服务器（表单默认的提交数据的格式）
-    multipart/form-data ： 需要在表单中进行文件上传时，就需要使用该格式。

在这儿简单介绍一下  application/x-www-form-urlencoded 和  multipart/form-data 以及 application/octet-stream 这三种类型分别用在什么场景下。


### 1、application/x-www-form-urlencoded
最常见的post提交数据的方式。在浏览器的原生表单中，如果不设置enctype属性，那么最终就会以  application/x-www-form-urlencoded 方式提交数据，提交的数据按照 key1=val1&key2=val2的方式进行编码，key和val都进行了URL转码。
在ios中，如果请求参数为：

```
NSDictionary *params = @{
        @"body":@{@"reqType":@"0"},
        @"sn":@"0cec3723ca95c7066a2d56e4ef110989ea7865cf"
        };
```
被转码以后：

```
body=%7B%0A%20%20%22reqType%22%20%3A%20%220%22%0A%7D&sn=0cec3723ca95c7066a2d56e4ef110989ea7865cf
```

### 2、multipart/form-data

Multipart/form-data的基础方法是POST , 也就是说是由POST方法来组合实现的. Multipart/form-data与POST方法的不同之处在于请求头和请求体. Multipart/form-data的请求头必须包含一个特殊的头信息 : Content-Type , 且其值也必须规定为multipart/form-data , 同时还需要规定一个内容分割符用于分割请求体中的多个POST的内容 , 如文件内容和文本内容自然需要分割开来 , 不然接收方就无法正常解析和还原这个文件了. Multipart/form-data的请求体也是一个字符串 , 不过和post的请求体不同的是它的构造方式 , post是简单的name=value值连接 , 而Multipart/form-data则是添加了分隔符等内容的构造体.

请求的头部信息如下:

//其中xxxxx是我自定义的分隔符，每个人都可以选择自己的分隔符
Content-Type: multipart/form-data; boundary=xxxxx
下面我们来看一下一个我的Multipart/form-data请求体:

```
POST /uploadFile HTTP/1.1
Host: 上传文件后台地址
Content-Type: multipart/form-data; boundary=xxxxx
Connection: keep-alive
Accept: /
User-Agent: AFNetWorking3.X%E6%BA%90%E7%A0%81%E9%98%85%E8%AF%BB/1 CFNetwork/808.2.16 Darwin/15.6.0
Content-Length: 32175
Accept-Language: en-us
Accept-Encoding: gzip, deflate

--xxxxx
Content-Disposition: form-data;name="file"

img.jpeg
--xxxxx
Content-Disposition: form-data;name="businessType"

CC_USER_CENTER
--xxxxx
Content-Disposition: form-data;name="fileType"

image
--xxxxx
Content-Disposition:form-data;name="file";filename="img1.jpeg"
Content-Type:image/png

这里是图片数据****************，比较长

--xxxxx--


```
备注：
>1，这里就对应了 第二项中的 【1、post文件上传】 和 第三项中的 【1、post方法上传】   这种类型。

>2，可以上传多个文件。

>3，比较常见的上传文件方式

### 3、application/octet-stream
这种方式只能提交二进制，而且只能提交一个二进制，如果提交文件的话，只能提交一个文件,后台接收参数只能有一个，而且只能是流（或者字节数组）。

备注：
>1,  这里对应了 第二项中的 【2、put上传文件】 和 第三项中的 【2、put方法上传】这种类型。
>
>2,   只能上传单个文件，不常见。
