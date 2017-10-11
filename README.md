
### 同步工具在 http://127.0.0.1:8081 监听 GET 和 POST 请求。

### 在所有发往这个地址的请求中，带上 callback 参数即可支持 JSONP 响应，解决 Ajax 跨域的问题。

#### １. 同步工具信息
##### １.获取本机同步工具信息 `/capi/ping`
请求方式：HTTP GET

响应:
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "login": true, // >是否登录
    "status": 200,
    "version": 0.1　　//> 同步工具版本
}
```

#### 2. 用户
##### 1. 登录 `/capi/login`
请求方式：HTTP POST

参数：
- email必须
- password必须 

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSU....",
    "status": 200,
    "success": true
}
```


##### 2.退出 `/capi/quit`
请求方式：HTTP GET

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "status": 200,
    "success": true
}
```

#### 3. 任务
##### 1.重启任务`/capi/v1/worker/restart`
请求方式：HTTP POST

参数：
-  job_id 需要重启的任务ID
 
响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "status": 200,
    "success": true
}
```

##### 2.删除任务`/capi/v1/worker/delete`
请求方式：HTTP POST

参数：
-  job_id 需要删除的任务ID
 
响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "status": 200,
    "success": true
}
```

##### 3.任务列表`/capi/v1/worker/list`
请求方式：HTTP GET

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "success": true,
    "workers": [
        {
            "detail": {
                "args": "[1]",
                "end_time": "2017-09-13T09:21:45.255662",
                "start_time": "2017-09-13 15:45:19.117051"
            },
            "state": "delete",
            "title": "软件界面",
            "worker_id": "1",
            "worker_name": "web_ui"
        }
    ]
}
```

#### 4. 上传下载任务
##### 1.上传任务`/capi/v1/file/upload`
请求方式：HTTP POST

参数：
- local_path: 要上传的本地文件 / 文件夹的路径
- clould_path: 线上path > 目录

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "is_alive": true,
    "success": true,
    "worker_id": "3"
}
```

##### 2.下载任务`/capi/v1/file/download`
请求方式：HTTP POST

参数：
- local_path: 本地文件夹目录
- clould_path: 线上文件 / 文件夹的路径　

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "is_alive": true,
    "success": true,
    "worker_id": "2"
}
```


##### ３.删除本地文件`/capi/v1/file/delete_local`
请求方式：HTTP POST

参数：
- path: 路径

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "success": true,
}
```

##### ４.删除线上文件`/capi/v1/file/delete_server`
请求方式：HTTP POST

参数：
- path: 路径

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "success": true,
}
```

#### 5. 文件夹信息
##### 1.返回本地文件夹信息`/capi/v1/info/localfiles`
请求方式：HTTP POST

参数：
- prefix　本地目录

响应：
- 格式: JSON/JSONP
- JSON 内容:
 /home/
├── reg <目录
├── test
├── test0.txt < 文件
└── xie
```
{
    "folderinfo": {
        "reg": "directory",
        "test": "directory",
        "test0.txt": "file",
        "xie": "directory"
    },
    "success": true
}
```

##### 2.返回oss文件夹信息`/capi/v1/info/ossfiles`
请求方式：HTTP POST

参数：
- prefix　线上目录

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "folderinfo": {
        "index.html": "file",
        "mel": "directory",
        "nuke": "directory",
        "python": "directory",
        "style.css": "file",
        "yeti": "directory"
    },
    "success": true
}
```

