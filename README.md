# A Voting Website using React and Django 用 Django 和 React 实现的投票网站

## Introduction 简介

This website allows the user to vote for their choices and shows the voting result as a bar chart.
The end of this documentation contains some screenshot.

观众可以用该网站投票，然后用柱状图统计投票结果。
文档尾部有一些截图。

## Features 功能

Useful features includes:

* A database editing page that is accessable in web browsers, implemented with Django administration
* A REST API that can both interact with a React UI or used directly through browser with Django REST Framework
* A voting page that automatically synchronize the choice with the back end
* An interactive result page using Chart.js
* Generating unique URLs for each user that can be embedded on a ticket's QR code

主要功能包括：

* 用 Django 管理界面实现的数据库管理网页
* 实现了 REST API，可以用前端 UI 访问，或通过 Django REST Framework 直接在浏览器中交互
* 投票界面自动与服务器同步
* 用 Chart.js 实现的交互式结果界面
* 为每个用户生成独立的 URL，可以作为二维码嵌入门票

## How to Use 使用说明

Please refer to the documentation for [client](https://github.com/LouYu2015/voting-client#readme) and [server](https://github.com/LouYu2015/voting-server#readme) on how to deploy them.
Replace `api.example.com` below with the domain of your back end and `example.com` below with the domain of your front end.

关于如何部署网站，请参阅子目录的说明。
以下用 `api.example.com` 表示后端域名，`example.com` 表示前端域名，请替换为自己的域名。

### Adding Voters 添加投票人

Each user should be assigned a random serial number to check their identity.
You can generate random numbers with a script (not provided in this project).

你需要给每个用户生成一个序列码，来验证用户身份。
你可以用脚本生成随机数（项目中不包含该程序）。

Go to `api.example.com/enable/`, log in as superuser, and submit the serial numbers as an JSON array of string.

打开 `api.example.com/enable/`，用管理员帐户登陆，然后以 JSON 数组格式提交所有序列码。序列码需要转为字符串。

You can also stop certain serial numbers from voting by going to `api.example.com/disable/`.

你也可以用 `api.example.com/disable/` 撤销某些序列号的投票权。

![Result Page Screenshot](pic/rest_admin.png)

### Adding Choices 添加选项

You can edit the database by going to `api.example.com/admin/`.
Edit `Questions` table to add and enable questions.
When a question is disabled (not enabled), users can't continue to submit any vote for it.
Edit `Choices` table to add choices and link each choice to a question.

你可以在 `api.example.com/admin/` 中修改数据库。
若要添加/启用提问，请修改 `Questions` 表。
提问不启用时，用户不能再给该提问投票。
若要添加选项，请修改 `Choices` 表，把每个选项连接到对应提问下。

![Admin Screenshot](pic/django_admin.png)

### Accessing Voting Page 投票

Each voter can access their voting page by going to `example.com/qr_code/<serial number>` where `<serial number>` is their assigned serial number.
You can embed this URL in their ticket's QR code for convenient access.

投票人可以前往 `example.com/qr_code/<serial number>` 投票，其中 `<serial number>` 是用户的序列码。
你可以把此 URL 用二维码嵌入门票，以便扫码打开。

![Voting Page Screenshot](pic/voting_page.png)

### Accessing Result Page 查看结果

You can access the result page by going to `example.com/view_result/<question id>` where `<question id>` is the ID in `Questions` table.

你可以前往 `example.com/view_result/<question id>` 查看投票结果，其中 `<question id>` 是某个提问在 `Question` 表中的编号。

![Result Page Screenshot](pic/voting_result_page.png)
