# Django最佳实践

# django生态

## drf



## django-debug-toolbar

> [github](https://github.com/jazzband/django-debug-toolbar)
>
> document

# 问题处理



## 解决Vue与Django冲突

### 方法一 

[官方说明](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#verbatim)

```django
{% verbatim %}
	{{ message }}
{% endverbatim %}
```

### 方法二 

[官方说明](https://cn.vuejs.org/v2/api/#delimiters)

```django
<div id='app'>
[[ message ]]
</div>
<script>
    var app = new Vue({
        el: '#app',
        delimiters: ['[[', ']]'] 
        data: {
        message: "Hello, 世界!"
    }
    })
</script>
```

```javascript
new Vue({
  delimiters: ['${', '}']
})

// 分隔符变成了  模板字符串的风格
```

## shell

```bash
django-admin shell -i python
```

## [测试工具](https://docs.djangoproject.com/zh-hans/3.0/topics/testing/tools/) - Test Tools

> 使用命令行查看 request 

```bash
>>> c = Client()
>>> response = c.post('/login/', {'username': 'john', 'password': 'smith'})
>>> response.status_code
200
>>> response = c.get('/customer/details/')
>>> response.content

```



## 使用httpx查看Request/Response

```python
import httpx
r = httpx.get('http://www.baidu.com')
r.headers

response = httpx.request('GET', 'https://www.baidu.com')
response.request
```

## 解决admin中中文末尾出现s

> verbose_name_plural='配置字典'





## django与vue.js整合

> - https://cloud.tencent.com/developer/article/1005607
> - https://docs.djangoproject.com/zh-hans/3.2/ref/class-based-views/base/#templateview

将html作为模板渲染, 同时需要注意静态文件目录

将静态文件放在 静态文件目录的`static`目录下可以使得相对目录与绝对目录保持一致



## 类视图中的类变量不应该依赖数据库中的数据

一次开发中, 将类变量 config=Config.objects.get(config_id=1). 结果在删除数据库, 重新生产迁移文件时, 出现了错误, 提示 notifications_config表不存在. 显然是 对models产生了依赖, 导致无法初始化该变量, 而导致了严重错误.

# 工程结构

> project structure

## 应用规划

### 什么是一个应用

- 实现的功能某种集合
- 博客系统
- 投票应用
- 数据库模型

# 返回响应

## 接口概览

```python
render_to_string(template_name, context=None, request=None, using=None)
```

# 模型和数据库

```python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute("select * from test")
```



# 官方指南



# 常见需求

## 官方指南

[官方文档](https://docs.djangoproject.com/zh-hans/3.2/howto/)

> howto, 操作指南

## 搜索

工具 : elasticsearch 

## 返回json的几种方法

[简书链接](https://www.jianshu.com/p/f97f73b96443)



## 开启事务



## 初始化数据

> [官方文档](https://docs.djangoproject.com/zh-hans/2.2/howto/initial-data/)[1](https://docs.djangoproject.com/zh-hans/2.2/howto/initial-data/)



项目初始化

# 常见问题

## 解决 django项目 python console 错误

```bash
File >> Settings >> Languages & Frameworks >> Django
```

# 视图接口 - Views

## request

## HttpResponse

## JsonResponse

## StreamingHttpResponse

流处理

The [`StreamingHttpResponse`](https://docs.djangoproject.com/en/3.0/ref/request-response/#django.http.StreamingHttpResponse) class is used to stream a response from Django to the browser. You might want to do this if generating the response takes too long or uses too much memory. For instance, it’s useful for [generating large CSV files](https://docs.djangoproject.com/en/3.0/howto/outputting-csv/#streaming-csv-files).

## `FileResponse`

*class* `FileResponse`(*open_file*, *as_attachment=False*, *filename=''*, ***kwargs*)[¶](https://docs.djangoproject.com/en/3.0/ref/request-response/#django.http.FileResponse)

```bash
>>> from django.http import FileResponse
>>> response = FileResponse(open('myfile.png', 'rb'))
```

## render()

```python
from django.shortcuts import render
```

## TemplateResponse - 一般不需要, render即可

[Templates and SimpleTemplateRespones](https://blog.csdn.net/boyun58/article/details/89500164)



# JSON交互

- [Django之AJAX传输JSON数据](https://www.cnblogs.com/open-yang/p/11222430.html)
- 

```js
// js
var myEvent = {id: calEvent.id, start: calEvent.start, end: calEvent.end,
               allDay: calEvent.allDay };
$.ajax({
    url: '/event/save-json/',
    type: 'POST',
    contentType: 'application/json; charset=utf-8',
    data: $.toJSON(myEvent),
    dataType: 'text',
    success: function(result) {
        alert(result.Result);
    }
});
```

```python
# request.body

# request.raw_post_data
def save_events_json(request):
    if request.is_ajax():
        if request.method == 'POST':
            print 'Raw Data: "%s"' % request.body   
    return HttpResponse("OK")


# 
```



# 常见需求



### 秒杀系统



## 单点登录(single Sign On)

多个系统中, 只需要登录一次,就可以访问其他相互信任的系统.





### 相同域名下的单点登录

将cookie的域名设置为顶级的域名(域名相同), 在三个系统中共享session方案

### 登录认证

完成登录和密码验证后, session中标记登录状态为yes. 同时在浏览器中写入cookie, cookie 是用户的唯一标识.

### 不同域名下的单点登录

CAS流程 SSO登录系统



### 中心认证服务(Central Authentication Service, CAS)



