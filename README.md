# 🌈17wanxiaoCheckin-Actions

**🚀2021.01.08：增加一些代码注释方便大家看懂代码，编写Wiki方便提供帮助**

**🤺2020.12.04：缝缝补补又几天，欢迎fork使用，感谢反馈，好用别忘记点个star✨**

**🦄2020.12.02：更新校内打卡，（健康打卡，校内打卡）我全都要！**

**💫2020.11.23：支持多人打卡，重写了一下代码**

**⚡2020.11.16：本项目已更新，使用本项目，你不需要抓包就可以使用（理论上大概......）**

------


------

## 🌟功能介绍

1. 完美校园模拟登录获取 token
2. 自动获取上次提交的打卡数据
3. 自动化任务分三次运行（ps：没有校内打卡就不会校内打卡，没有晚上打卡也不会晚上打卡的）
   - `上午六点`：健康打卡，上午校内打卡
   - `中午十二点`：健康打卡，下午校内打卡
   - `下午五点`：健康打卡，晚上校内打卡
4. 微信推送打卡消息

## 💢使用方法

1. 请先确保手机app或支付宝小程序进入健康打卡界面，信息能够正确的自动填写（没有自动填写的项，可以自行修改代码）

2. 点击右上角的 `fork`，`fork` 本项目到自己仓库中

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/click_fork.png)

   

3. 开启 `Actions`

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/start_action.png)

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/end_actions.png)

   

4. 设置三个 `secrets`  字段：`USERNAME`、`PASSWORD`、`SCKEY`（对应就是账号，密码以及 Server 酱）

   1. 如果是多人打卡的话：
      - USERNAME字段：手机号1,手机号2,......（与下面密码对应），例如：`1737782***,13602***`
      - PASSWORD字段：密码1,密码2,......  （与上面账号对应），例如：`123456,456789`
      - SCKEY字段：填写一个即可，例如：`SCU90543*******`，没有请前往 [Server酱](https://sc.ftqq.com/3.version) 注册获取

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/new_secrets.png)

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/secrets_details.png)

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/end_secrets.png)

   

5. 修改 `README.md` 选第一个就好，不要选第二个Create a new branch***（为什么教着做都不听话，泪目），测试一次

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/modify_readme.png)

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/end_modify.png)

   

6. 查看 `Actions` 运行情况，以及微信推送情况，**至此每日六点多将会自行打卡**

   

   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/check_status.png)

   



   ![](https://cdn.jsdelivr.net/gh/ReaJason/17wanxiaoCheckin-Actions/Pictures/end_check.png)


## ✅Q&A

### 1、怎么图片都无法加载出来，看了个寂寞？

可以前往我的博客查看 [使用方法](https://zik05.cn/archives/82.html)

### 2、fork之后，修改README.md并没有触发actions？

请进入 Actions，Enable workflow

![enable](https://cdn.jsdelivr.net/gh/LingSiKi/images/img/enable.png)

### 3、我们学校要求打卡的时间不一样，这个自动运行的时间该怎么修改？

进入 `.github/workflows/run.yml `修改时间，请不要搁那掐着秒算程序运行，你设置好了，明天就一定能好好运行，Giuhub Actions大概会有10~20分钟的延迟

```python
"""
这里的cron就是脚本运行时间，22,4,9对应的时间是UTC时，对应北京时间早上六点，中午十二点，下午五点
详细对应关系请查看：http://timebie.com/cn/universalbeijing.php

只有健康打卡的小伙伴可以只留着22就可以了，这样其余两个时间就不会打卡
如果害怕程序报错导致上午健康打卡没打，可设置6点和7点各运行一次即：0 22,23 * * *
"""
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
  schedule:
    - cron: 0 22,4,9 * * *
```

### 4、程序报错显示密码错误，还有 * 次机会？

请立马修改 secrets 的密码再尝试运行

