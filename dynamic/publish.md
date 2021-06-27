# 发布动态

## 为图片动态（相簿）上传图片

> http://api.vc.bilibili.com/api/v1/drawImage/upload

*请求方式：POST*

认证方式：Cookie（SESSDATA）

~~这是图床？（滑稽保命）~~

注意：非日常类型像素宽高必须大于420

**正文参数（multipart/form-data）：**

| 参数名   | 类型 | 内容               | 必要性 | 备注                                                                  |
| -------- | ---- | ------------------ | ------ | --------------------------------------------------------------------- |
| file_up  | file | 需要上传的图片文件 | 必要   | 格式仅支持jpg  png  gif                                               |
| category | str  | 图片类型           | 必要   | daily：日常（动态）<br />draw：绘画（画友）<br />cos：摄影（COSPLAY） |

**json回复：**

根对象：

| 字段    | 类型 | 内容     | 备注                                                                                                           |
| ------- | ---- | -------- | -------------------------------------------------------------------------------------------------------------- |
| code    | num  | 返回值   | 0：成功 <br />-1：未添加图片<br />-2：参数错误<br />-3：图片尺寸过小<br />-4：账号未登录<br />-7：图片信息错误 |
| message | str  | 错误信息 | 默认为success                                                                                                  |
| data    | obj  | 信息本体 | 仅在正确时既`code=0`时为有效信息                                                                               |

`data`对象：

| 字段         | 类型 | 内容           | 备注 |
| ------------ | ---- | -------------- | ---- |
| image_url    | str  | 已上传图片url  |      |
| image_width  | num  | 已上传图片宽度 | 像素 |
| image_height | num  | 已上传图片高度 | 像素 |

示例：

上传了一张图片`test.png`类型为`日常`

```shell
curl 'http://api.vc.bilibili.com/api/v1/drawImage/upload' \
-F 'file_up=@test.png' \
-F 'category=daily'
-b 'SESSDATA=xxx'
```

<details>
<summary>查看响应示例：</summary>

```json
{
    "code":0,
    "message":"success",
    "data":{
     "image_url":"http:\/\/i0.hdslb.com\/bfs\/album\/13f9523efe186a8066b2d72e80283cea2437eb62.png",
        "image_width":1225,
        "image_height":850
    }
}
```

</details>

## 发送动态

> https://api.vc.bilibili.com/dynamic_svr/v1/dynamic_svr/create

*请求方式：POST*

认证方式：Cookie（SESSDATA）


**正文参数（multipart/form-data）：**

| 参数名            | 类型 | 内容                       | 必要性                        | 备注                                                                                          |
| ----------------- | ---- | -------------------------- | ----------------------------- | --------------------------------------------------------------------------------------------- |
| content           | str  | 动态文本                   | 非必要                        |                                                                                               |
| csrf              | str  | csrf校验信息（位于cookie） | 必要                          |                                                                                               |
| dynamic_id        | num  | 0                          | 非必要                        | 未知                                                                                          |
| type              | num  | 4                          | 非必要                        | 貌似任何数都行                                                                                |
| rid               | num  | 0                          | 非必要                        | 未知                                                                                          |
| at_uids           | str  | 非必要                     | 接@的人的uid,多个人用逗号隔开 | 这个可以脱离content独立存在，~~可以做出通篇找不到【@】却给对方发了【你被@了】消息的诡异效果~~ |
| ctrl              | arr  | 特殊效果控制，见下表       | 非必要                        |                                                                                               |
| up_close_comment  | num  | 0或1                       | 是否关闭评论区（？）          | ~~我没权限试不了~~，欢迎有权限的人测试一下                                                    |
| up_choose_comment | num  | 0或1                       | 是否精选评论（？）            | 同上                                                                                          |

`ctrl`数组:

| 项  | 类型 | 内容             | 备注 |
| --- | ---- | ---------------- | ---- |
| 0   | obj  | 特殊效果，如下表 |      |
| 0+1 | obj  | 同上             |      |
| ... | obj  | 同上             |      |

`ctrl`数组中的项：

| 项       | 类型 | 内容           | 备注                      |
| -------- | ---- | -------------- | ------------------------- |
| location | num  | 特殊文本起始点 |
| type     | num  | 特殊文本类型   | 1为at                     |
| length   | num  | 特殊文本长度   | 例如`@I__Min`就是7        |
| data     | str  | 根据`type`决定 | `type`为1时该项为@人的uid |


**json回复：**

根对象：

| 字段    | 类型 | 内容     | 备注                                                                                                           |
| ------- | ---- | -------- | -------------------------------------------------------------------------------------------------------------- |
| code    | num  | 返回值   | 0：成功 |
| message | str  | 错误信息 | 默认为空                                                                                                       |
| msg     | str  | 错误信息 | 默认为空                                                                                                       |
| data    | obj  | 信息本体 | 仅在正确时既`code=0`时为有效信息                                                                               |

`data`对象：

| 字段           | 类型 | 内容           | 备注                                      |
| -------------- | ---- | -------------- | ----------------------------------------- |
| create_result  | num  | 发送结果       | 1为成功                                   |
| dynamic_id     | num  | 动态id         |                                           |
| dynamic_id_str | str  | 动态ID(字符串) | 和上面的并不一样，这个是在url里看到的那个 |
| errmsg         | str  | 没看懂         | 难道是回调？                              |

示例：

较为复杂,就不写了~~其实是我懒~~

```shell
较为复杂,就不写了其实是我懒
```

<details>
<summary>查看响应示例：</summary>

```json
{
    "code": 0,
    "msg": "",
    "message": "",
    "data": {
        "result": 0,
        "errmsg": "; Create dynamic:540855482010245647, res:0, result:1; Push create kafka:0; Push create databus:0; Register comment result:0; Add outbox result:1; Send at_msg result:0",
        "dynamic_id": 540855482010245647,
        "create_result": 1,
        "dynamic_id_str": "540855482010245647",
        "_gt_": 0
    }
}
```

</details>
