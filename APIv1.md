# API v1
API v1均可使用HTTP GET/POST请求

请在调用过程中多观察增强报错处理 考虑多种情况

统一调用地址
> https://cf-v1.uapis.cn/api

## 登录
- 接口
    > /login.php
- 请求参数

    Query/JSON:
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
        |background_img|string|用户背景图片url|
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |error|string|错误信息|

    ```
    用户带宽限制:
    国内带宽限制: bandwidth*1
    国外宽带限制: bandwidth*4
    ```

## 节点信息
- 接口
    > /unode.php
- 返回
    返回一个list内含诺干个Map

    每个Map代表一条节点

    Map参数:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |apitoken|string|节点frp-api token|
    |nodetoken|string|节点frp token|
    |id|number|节点id|
    |ip|string|节点地址|
    |name|string|节点名称|
    |area|string|节点所属地区|
    |china|string|是否是国内节点<yes/no>|
    |fangyu|string|是否有防御<true/false>|
    |http_port|number|节点http端口|
    |https_port|number|节点https端口|
    |nodegroup|string|节点可使用用户组|
    |notes|string|节点简介|
    |port|number|节点frp端口|
    |rport|string|节点frp端口限制|
    |udp|string|节点是否可以使用upd<true/false>|
    |wed|string|节点是否可以建站<yes/no>|


## 用户隧道信息
- 接口
    > /usertunnel.php
- 请求参数

   Query/JSON:
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

## 隧道信息
- 接口
    > /tunnelinfo.php
- 请求参数

    Query/JSON:
    |属性|说明|
    |:--:|:--:|
    |id|隧道识别id|
- 返回

    通常为两种情况 请注意分辨

    此接口可以使用返回的code参数识别

    - 查询成功返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|值为200|
        |area|string|节点所在地|
        |ip|string|节点的地址|
        |iparea|string|隧道连接地址|
        |name|string|节点名称|
        |tunnel_id|string|隧道识别id|
        |tunnel_name|string|隧道名称|
        |tunnel_type|string|隧道类型|
        |tunnel_ap|string|frp额外参数|
        |tunnel_localip|string|隧道本地IP|
        |tunnel_nport|string|隧道本地端口|
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |code|number|状态码|
        |error|string|错误信息|

## 新建隧道
- 接口
    > /tunnel.php
- 请求参数

    Query/JSON:
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
    这个接口Query/JSON参数和上一个一样
    只是多了一个tunnelid
    ```

    Query/JSON:
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

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |token|string|用户令牌|
    |userid|string|用户id|
    |nodeid|string|隧道识别id|
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |code|number|状态码 200为成功|
    |error|string|返回信息|

## frp配置文件生成
- 接口
    > /frpconfig.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |usertoken|string|用户令牌|
    |node|string|节点名称|
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |status|number|状态码 200为成功|
    |success|boolean|状态 true为成功|
    |message|string|该节点all隧道的frp配置文件|

## 重置令牌
- 接口
    > /resusertoken.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |usertoken|string|用户令牌|
- 返回

    通常为两种情况 请注意分辨

    - 查询成功
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |newToken|string|新的用户令牌|
    - 查询失败
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |error|string|错误信息|

## 签到
- 接口
    > /qiandao.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |usertoken|string|用户令牌|
    |g_recaptcha_response|string|人机验证返回值|
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |status|string|状态 true为成功|
    |message|string|返回信息|
    |points|number|获得积分|
    |total_sign_ins|number|累计签到次数|
    |total_points|number|累计积分|

## 签到信息
- 接口
    > /qdxx.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |userid|string|用户id|
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |code|number|状态码|
    |is_signed_in_today|boolean|今天是否签到|
    |last_sign_in_time|string|最后签到时间|
    |total_points|number|累计积分|
    |count_of_matching_records|number|今天签到人数|
    |total_sign_ins|string|累计签到次数|

## 用户信息
- 接口
    > /userinfo.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |userid|string|用户id|
- 返回

    通常为两种情况 请注意分辨
    - 查询成功返回

        ```
        tip:
        和/login接口成功时返回基本一样
        只是少了token,code,background_img
        ```

        |属性|类型|说明|
        |:--:|:--:|:--:|
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
    - 查询失败返回
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |status|number|状态码|
        |success|boolean|状态 值为false|
        |message|string|错误信息|

    ```
    用户带宽限制:
    国内带宽限制: bandwidth*1
    国外宽带限制: bandwidth*4
    ```

## 用户流量消耗
- 接口
 > /flow_zong.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |usertoken|string|用户令牌|
- 返回

    通常为两种情况 请注意分辨

    此接口可以使用返回的status参数识别
    - 查询成功
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |status|string|值为success|
        |userid|string|用户id|
        |data|list|*流量数据|
    - 查询失败
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |status|string|查询状态|
        |message|string|错误信息|
    
    流量数据:
    ```json
    [
        {
            "time": "08-25",
            "traffic_in": 0,
            "traffic_out": 0
        },
        {
            "time": "08-26",
            "traffic_in": 0,
            "traffic_out": 0
        },
        {
            "time": "08-27",
            "traffic_in": 0,
            "traffic_out": 0
        }
    ]
    ```
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |time|string|日期|
    |traffic_in|number|下载数据|
    |traffic_out|number|上传数据|

## 用户节点数据
- 接口
    > /confignode.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |userid|string|用户id|
- 返回
    通常为两种情况 请注意分辨
    - 查询成功
        
        返回一个list内含诺干个Map

        每个Map代表一条隧道

        Map:
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |id|string|节点id|
        |name|sting|节点名称|
        |data|list|*所属节点隧道|

        所属节点隧道:
        ```json
        [
            {
                "tunnel_id": "404",
                "tunnel_name": "KAgTHYe"
            },
            {
                "tunnel_id": "48888",
                "tunnel_name": "barf5BRF"
            }
        ]
        ```
        |属性|类型|说明|
        |:--:|:--:|:--:|
        |tunnel_id|string|隧道id|
        |tunnel_name|srting|隧道名称|
    - 查询失败
        空返回

## 面板设置
- 接口
    > /usersetup.php
- 请求参数

    Query/JSON:
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |usertoken|string|用户令牌|
    |url|string|详见下表|
    |meg|string|详见下表|
    |isTrusted|boolean|值为true|

    url/meg:
    |url|meg|
    |:-:|:-:|
    |透明度|Element_transparency|
    |用户背景图片url|background_img|
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |code|number|状态码|
    |error|string|返回信息|

## 面板信息
- 接口
    > /sinfo.php
- 返回
    |属性|类型|说明|
    |:--:|:--:|:--:|
    |user_count|string|总用户数|
    |tunnel_count|string|总隧道数|
    |node_count|string|总节点数|
    |blogroll|Map|友链|
