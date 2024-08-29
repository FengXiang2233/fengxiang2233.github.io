# API v1
API v1均可使用HTTP GET/POST请求

请在调用过程中多观察增强报错处理 考虑多种情况

统一调用地址
> https://cf-v1.uapis.cn/api
## 登录
- 接口
    > /login.php
- 请求参数

    Query:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |username|string|用户名/用户QQ号|
    |password|string|密码|
- 返回

    通常为两种情况 请注意分辨

    - 查询成功返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|状态码|
        |token|string|用户令牌|
        |userid|number|用户id|
        |usergroup|string|用户权限组|
        |term|string|用户权限组过期时间|
        |qq|string|用户绑定QQ号|
        |email|string|用户绑定邮箱|
        |tunnel|number|用户可开通的隧道数|
        |tunnelstate|number|用户已开通的隧道数|
        |message|string|返回信息|
        |userimg|string|用户头像url|
        |username|string|用户名称|
        |bandwidth|number|*用户带宽限制(Mdps)
        |realname|string|用户实名状态|
        |background_img|string/null|用户背景图片url|
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |error|string|错误信息|

    ```
    *用户带宽限制:
     国内带宽限制: bandwidth*1
     国外宽带限制: bandwidth*4
    ```
## 用户隧道信息
- 接口
    > /usertunnel.php
- 请求参数

   Query:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |token|string|用户令牌|
- 返回

    通常为两种情况 请注意分辨

    - 查询成功返回
    
        返回一个list内含诺干个Map

        每个Map代表一条隧道

        Map参数:
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |id|string|隧道识别id|
        |name|string|隧道名称|
        |node|string|节点名称|
        |type|string|隧道类型|
        |ap|string|frp额外参数|
        |ip|string|该隧道的连接地址|
        |localip|string|隧道本地IP|
        |nport|string|隧道本地端口|
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|状态码|
        |error|string|错误信息|
## 新建隧道
- 接口
    > /tunnel.php
- 请求参数

    Query:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |token|string|用户令牌|
    |userid|number|用户id|
    |type|string|隧道类型|
    |node|string|节点名称|
    |name|string|隧道名称|
    |ap|string|frp额外参数|
    |dorp|number|外网端口|
    |localip|string|内网地址|
    |nport|string|内网端口|
- 返回

    该接口无返回
## 重新设置隧道
- 接口
    > /cztunnel.php
- 请求参数
    ```
    tip:
    这个接口Query参数和上一个一样
    只是多了一个tunnelid
    ```

    Query:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |token|string|用户令牌|
    |userid|number|用户id|
    |type|string|隧道类型|
    |node|string|节点名称|
    |name|string|隧道名称|
    |ap|string|frp额外参数|
    |dorp|number|外网端口|
    |localip|string|内网地址|
    |nport|string|内网端口|
    |tunnelid|string|需要修改的隧道识别id|
- 返回

    该接口无返回
## 删除隧道
- 接口
    > /deletetl.php
- 请求参数

    Query:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |token|string|用户令牌|
    |userid|string|用户id|
    |nodeid|string|隧道识别id|
- 返回

    通常为两种情况 请注意分辨

    - 查询成功返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|状态码|
        |error|string|返回信息|
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|状态码|
        |error|string|错误信息|
        
<!-- TODO /tunnelinfo.php>