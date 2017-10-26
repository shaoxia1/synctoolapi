
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

##### 3.用户信息 `/capi/v1/user`
请求方式：HTTP GET

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "created_at": "2017-09-11 03:02:19",
    "email": "admin@sikaifa.club",
    "id": 1,
    "name": "uc_admin",
    "updated_at": "2017-09-11 03:02:19"
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

##### 2.重启所有错误任务`/capi/v1/worker/restartall`
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

##### ３.删除任务`/capi/v1/worker/delete`
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

##### ４.任务列表`/capi/v1/worker/list`
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
                "end_time": "2017-10-19T09:46:13.703000",
                "start_time": "2017-10-17 12:18:18.078000"
            },
            "state": "running",
            "title": "软件界面",
            "worker_id": "1",
            "worker_name": "web_ui"
        },
        {
            "detail": {
                "args": [
                    "AirRender-Test/1/4/N/1234/1.test",
                    "J:\\download\\1.test"
                ],
                "end_time": "",
                "start_time": "2017-10-20 15:38:05.194000"
            },
            "local_path": "J:\\download\\1.test",
            "oss_path": "AirRender-Test/1/4/N/1234/1.test",
            "rate": "\r6% ",
            "state": "running",
            "title": "上传文件",
            "worker_id": "3",
            "worker_name": "upload"
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
    "folderinfo": [
        "Documents and Settings",
        "KwDownload",
        "libpython",
        "newwindows",
        "PerfLogs",
        "Program Files",
        "Program Files (x86)",
        "ProgramData",
        "QMDownload",
    ],
    "fileinfo": [
        {
            "bootstrap.py": {
                "mtime": 1495693399.321977,
                "size": 1613
            }
        },
        {
            "swapfile.sys": {
                "mtime": 1508223586.186817,
                "size": 268435456
            }
        },
        {
            "tjh_lost_textures_finder.mel": {
                "mtime": 1501742668.1077826,
                "size": 240056
            }
        }
    ],
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
    "fileinfo": [
        {
            "LICENSE.txt": {
                "mtime": 1507798213,
                "size": 38591
            }
        }
    ],
    "folderinfo": [
        "123",
        "libpython"
    ],
    "success": true
}
```

#### 6. 项目信息
##### 1.返回项目信息`/capi/v1/projects`
请求方式：HTTP GET
```
[
    {
        "created_at": "2017-10-11 03:33:16",
        "creator": "admin",
        "creator_id": 1,
        "id": 1,
        "name": "test1",
        "task_count": 0,
        "updated_at": "2017-10-11 03:33:16"
    },
    {
        "created_at": "2017-10-11 03:33:16",
        "creator": "admin",
        "creator_id": 1,
        "id": 2,
        "name": "test2",
        "task_count": 0,
        "updated_at": "2017-10-11 03:33:16"
    }
]
```

#### 7. 切换
##### 1.切换地域｀/capi/v1/endpoint/{endpoint}｀
    
参数：
- endpoint　地域(如“sh”,"sz","bj")

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
##### 1.切换项目｀/capi/v1/local_project｀

请求方式：HTTP POST

参数：
- prefix　线上目录(如“AirRender-Test/1/2","AirRender-Test/1/3")

响应：
- 格式: JSON/JSONP
- JSON 内容:
```
{
    "status": 200,
    "success": true
}
```
