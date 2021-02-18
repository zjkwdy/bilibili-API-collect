# APP端剪贴板匹配模式

- [APP端剪贴板匹配模式](#app端剪贴板匹配模式)
  - [获取APP端剪贴板匹配模式](#获取app端剪贴板匹配模式)

---

## 获取APP端剪贴板匹配模式

> https://api.bilibili.com/x/share/clipboardRules

*请求方式：GET*

鉴权方式：APP

**url参数：**

| 参数名   | 类型 | 内容           | 必要性      | 备注        |
| -------- | ---- | -------------- | ----------- | ----------- |
| appkey   | str  | APP密钥        | APP方式必要 |             |
| platform | str  | 平台类型（？） | APP方式必要 | 可为android |
| ts       | num  | 当前时间戳     | APP方式必要 |             |
| sign     | str  | APP签名        | APP方式必要 |             |

**json回复：**

根对象：

| 字段    | 类型 | 内容     | 备注                                                 |
| ------- | ---- | -------- | ---------------------------------------------------- |
| code    | num  | 返回值   | 0：成功<br />-3：API校验密匙错误<br />-400：请求错误 |
| message | str  | 错误信息 | 默认为0                                              |
| ttl     | num  | 1        |                                                      |
| data    | obj  | 信息本体 |                                                      |

`data`对象：

| 字段            | 类型  | 内容     | 备注 |
| --------------- | ----- | -------- | ---- |
| clipboard_rules | array | 每条规则 |      |

`data`中的`clipboard_rules`数组：

| 项  | 类型 | 内容          | 备注 |
| --- | ---- | ------------- | ---- |
| 0   | obj  | 匹配模式1     |      |
| n   | obj  | 匹配模式(n+1) |      |
| ……  | obj  | ……            | ……   |

`list`数组中的对象：

| 字段               | 类型 | 内容          | 备注 |
| ------------------ | ---- | ------------- | ---- |
| id                 | num  | 匹配模式ID    |      |
| name               | str  | 匹配模式名url |      |
| priority           | num  | 权重（？）    |      |
| regex              | str  | 正则表达式    |      |
| start_pattern      | num  | 未知          |      |
| business           | str  | 说明（？）    |      |
| user_status        | num  |               |      |
| self_copied_active | bool | 未知          |      |
| popup_rule         | num  | 未知          |      |
| popup_mode         | num  | 未知          |      |
| url                | str  | 空            | 未知 |

**示例：**

```shell
curl -G 'https://api.bilibili.com/x/share/clipboardRules' \
--data-urlencode 'appkey=1d8b6e7d45233436' \
--data-urlencode 'ts=0' \
--data-urlencode 'platform=android' \
--data-urlencode 'sign=78a89e153cd6231a4a4d55013aa063ce'
```

<details>
<summary>查看响应示例：</summary>

```json
{
    "code": 0,
    "message": "0",
    "ttl": 1,
    "data": {
        "clipboard_rules": [
            {
                "id": 4,
                "name": "裂变分享口令",
                "priority": 150,
                "regex": "(.*)([gG][hH][aA][0-9a-zA-Z]{7})(.*)",
                "start_pattern": 3,
                "business": "FISSION_WORD",
                "user_status": 1,
                "self_copied_active": true,
                "popup_rule": 3,
                "popup_mode": 3,
                "url": ""
            },
            {
                "id": 30003,
                "name": "OGV春节活动",
                "priority": 104,
                "regex": "2233hcny\\$([0-9a-zA-Z]{6,8})\\$",
                "start_pattern": 3,
                "business": "OGV_DISH",
                "user_status": 1,
                "self_copied_active": false,
                "popup_rule": 4,
                "popup_mode": 3,
                "url": ""
            },
            {
                "id": 3,
                "name": "直播答题口令分享",
                "priority": 101,
                "regex": "b23\\$([0-9a-zA-Z]{6})\\$",
                "start_pattern": 3,
                "business": "ZHIBODATI_WORD",
                "user_status": 1,
                "self_copied_active": true,
                "popup_rule": 4,
                "popup_mode": 3,
                "url": ""
            },
            {
                "id": 2,
                "name": "直播答题复制链接",
                "priority": 100,
                "regex": "b23\\$([0-9a-zA-Z]{8})\\$",
                "start_pattern": 3,
                "business": "ZHIBODATI_LINK",
                "user_status": 1,
                "self_copied_active": true,
                "popup_rule": 4,
                "popup_mode": 3,
                "url": ""
            },
            {
                "id": 5,
                "name": "一起看口令邀请",
                "priority": 60,
                "regex": "2333freya([0-9a-zA-Z]{6,8})",
                "start_pattern": 3,
                "business": "FREYA",
                "user_status": 1,
                "self_copied_active": true,
                "popup_rule": 2,
                "popup_mode": 3,
                "url": ""
            },
            {
                "id": 1,
                "name": "bv匹配规则",
                "priority": 50,
                "regex": "^((http|https)://(www.bilibili.com/(video/)?|bilibili.com/|b23.tv/))?BV1[1-9A-NP-Za-km-z]{9}$",
                "start_pattern": 3,
                "business": "BV",
                "user_status": 1,
                "self_copied_active": true,
                "popup_rule": 4,
                "popup_mode": 1,
                "url": ""
            }
        ]
    }
}
```

</details>

