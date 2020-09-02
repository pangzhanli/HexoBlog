---
title: ios原生API文件上传(NSURLSession)
date: 2020-04-03 19:06:04
categories:
- OC
- 上传
tags: 上传
---


## 一、 简介

以前，在上传文件时，可以使用NSURLConnection类，由于这个类已经过期，只支持到ios9, 所以，本节使用NSURLSession来上传文件。

NSURLSession针对下载/上传等复杂的网络操作提供了专门的解决方案，针对普通、上传和下载分别对应三种不同的网络请求任务：NSURLSessionDataTask, NSURLSessionUploadTask和NSURLSessionDownloadTask 。创建的task都是挂起状态，需要resume才能执行。

## 二、使用 

### 1、引入框架和定义编码宏

```
#import <MobileCoreServices/MobileCoreServices.h>

#define GMEncode(str) [str dataUsingEncoding:NSUTF8StringEncoding]
```

### 2、编写上传方法

```
-(void)upload:(NSString *)filePath params:(NSDictionary *)params{
    NSURL *url = [NSURL URLWithString:@"http://192.168.1.103:9088/up/upload"];
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
    [request setHTTPMethod:@"POST"];
    
    //分隔符
    NSString *boundary = [self generateBoundaryString];
    
    //设置ContentType
    NSString *contentType = [NSString stringWithFormat:@"multipart/form-data; boundary=%@", boundary];
    [request setValue:contentType forHTTPHeaderField: @"Content-Type"];
    
    //获取body体数据
    NSString *fieldName = @"CustomFile";
    NSData *bodyData = [self createBodyWithBoundary:boundary parameters:params filePath:filePath fieldName:fieldName];
    
    NSURLSessionTask *task = [[NSURLSession sharedSession] uploadTaskWithRequest:request fromData:bodyData completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        if (error) {
            NSLog(@"error : %@", error);
            return;
        }
        NSString *result = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
        NSLog(@"上传返回结果 : %@", result);
    }];
    
    [task resume];
}

```

### 3、body体拼接
```
- (NSData *)createBodyWithBoundary:(NSString *)boundary
                        parameters:(NSDictionary *)parameters
                          filePath:(NSString *)filePath
                         fieldName:(NSString *)fieldName {
    //创建可变Data
    NSMutableData *bodyData = [NSMutableData data];
    
    //文本参数
    [parameters enumerateKeysAndObjectsUsingBlock:^(NSString *key, NSString *obj, BOOL * _Nonnull stop) {
        //开始
        NSString *startStr = [NSString stringWithFormat:@"--%@\r\n",boundary];
        [bodyData appendData:GMEncode(startStr)];
        
        //描述
        NSString *dispositionStr = [NSString stringWithFormat:@"Content-Disposition: form-data; name=\"%@\"\r\n\r\n", key];
        [bodyData appendData:GMEncode(dispositionStr)];
        
        //值
        NSString *valueStr = [NSString stringWithFormat:@"%@\r\n", obj];
        [bodyData appendData:GMEncode(valueStr)];
    }];
    
    //文件
    NSString *fileName  = [filePath lastPathComponent];
    NSData   *data      = [NSData dataWithContentsOfFile:filePath];
    NSString *mimetype  = [self mimeTypeForPath:filePath];
    
    //文件分割
    NSString *fileBoundaryStr = [NSString stringWithFormat:@"--%@\r\n",boundary];
    [bodyData appendData:GMEncode(fileBoundaryStr)];
    
    //文件描述
    NSString *fileDispositionStr = [NSString stringWithFormat:@"Content-Disposition: form-data; name=\"%@\"; filename=\"%@\"\r\n", fieldName, fileName];
    [bodyData appendData:GMEncode(fileDispositionStr)];
    
    //类型
    NSString *contentTypeStr = [NSString stringWithFormat:@"Content-Type: %@\r\n\r\n", mimetype];
    [bodyData appendData:GMEncode(contentTypeStr)];
    
    //文件NSData
    [bodyData appendData:data];
    
    //换行
    [bodyData appendData:GMEncode(@"\r\n")];
    
    //结尾
    NSString *endStr = [NSString stringWithFormat:@"--%@--\r\n",boundary];
    [bodyData appendData:GMEncode(endStr)];

    return bodyData;
}
```

### 4、获取mimeType
```
///根据文件路径获取mimeType
- (NSString *)mimeTypeForPath:(NSString *)path {
    CFStringRef extension = (__bridge CFStringRef)[path pathExtension];
    CFStringRef UTI = UTTypeCreatePreferredIdentifierForTag(kUTTagClassFilenameExtension, extension, NULL);
    NSString *mimetype = CFBridgingRelease(UTTypeCopyPreferredTagWithClass(UTI, kUTTagClassMIMEType));
    
    CFRelease(UTI);
    
    return mimetype;
}
```

### 5、生成分隔符字符串

```
- (NSString *)generateBoundaryString {
    return [NSString stringWithFormat:@"Boundary-%@", [[NSUUID UUID] UUIDString]];
}
```