---
title: curl命令使用
date: 2017-08-15 17:04:22
tags:
---

# curl 基本使用

1. 最简单的直接请求页面 ` curl "https://www.baidu.com" `
2. 请求保存页面 ` curl "https://www.baidu.com" > /path/name.html` 
3. `-o` 保存页面 ` curl -o /path/name.html "https://www.baidu.com" ` `--progress ` 显示进度条
4. `-s` 加入这个就不会出现进度条,安静模式
5. `-A` 参数用来指定 USER-AGENGT ` curl -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_2) AppleWebKit/537.17 (KHTML, like Gecko) Chrome/24.0.1312.52 Safari/537.17" http://localhost/learing-curl/show-server-info.php `
6. `-e` 指定 referer 来源网址 ` curl -e "https://www.google.com/"  http://localhost/learing-curl/show-server-info.php `
7. `-d` post 请求 ` curl -d "name=1" "http://localhost:6666/post" `
8. `-G` 轻质指定表单以 GET 方法提交
9. `-I` 只展示 Header ` curl -I  http://www.baidu.com `
10. `-D` 保存 Header 到文件里 ` curl -D header.txt http://www.alibaba.com `
11. `-L` 跟随重定向过去 ` curl -L http:localhost:6666/red `
12. `-F` 提交文件 ` curl -F upload_file=@test.data url`
13. `-c` 保存 cookie ` curl -c cookie.txt https://www.baidu.com `
14. `-b` 带 coolie 访问 ` curl -b "name=data" url ` ` curl -b cookie.txt url `
15. `-H` 设置请求头
16.  `-m` 设置最大传输时间 seconds 
17. `-u` 设置服务器用户名和密码 ` curl -u name:password url `


```bash
curl 'https://oapi.dingtalk.com/robot/send?access_token=6fb5741248b308d1eb616f993fddf0fb3459f42cb6b4eb86078e33042b5bc4e0' \
   -H 'Content-Type: application/json' \
   -d \
  '{"msgtype": "text", 
    "text": {
        "content": "我就是我, 是不一样的烟火"
     }
  }'
```

```bash
curl 'http://www.ferryvip.com/v1/me/webhook' \
   -H 'Content-Type: application/json ' \
   -H 'x-coding-event: push ' \
   -d \
  '{"ref":"refs/heads/master","before":"fbec0e3aa41f1364587c5d62df9032bcc5406afd","commits":[{"committer":{"name":"chencangshan","email":"chencangshan@huaxiweiying.com"},"web_url":"https://coding.net/u/ferryVip/p/lostwebserver/git/commit/90360e33395e3bb1e1b844b4b85de08d2a559152","short_message":"测试 hook\n","sha":"90360e33395e3bb1e1b844b4b85de08d2a559152"}],"after":"90360e33395e3bb1e1b844b4b85ded2a559152","event":"push","repository":{"owner":{"path":"/u/ferryVip","web_url":"https://coding.net/u/ferryVip","global_key":"ferryVip","name":"ferryVip","avatar":"https://dn-coding-net-production-static.qbox.me/82b7ce57-96ef-4faf-a480-bb0645ab2a1a.jpg?imageMogr2/auto-orient/format/jpeg/crop/!200x200a0a0"},"https_url":"https://git.coding.net/ferryVip/lostwebserver.git","web_url":"https://coding.net/u/ferryVip/p/lostwebserver","project_id":"1219048","ssh_url":"git@git.coding.net:ferryVip/lostwebserver.git","name":"lostwebserver","description":"react webpack node mongodb express\n\n失物招领b server"},"user":{"path":"/u/ferryVip","web_url":"https://coding.net/u/ferryVip","global_key":"ferryVip","name":"ferryVip","avatar":"https://dn-coding-net-production-static.qbox.me/82b7ce57-96ef-4faf-a480-bb0645ab2a1a.jpg?imageMogr2/auto-orient/format/jpeg/crop/!200x200a0a0"},"token":"https://oapi.dingtalk.com/robot/send?access_token=6fb5741248b308d1eb616f993fddf0fb3459f42cb6b4eb86078e33042b5bc4e0"}'

```