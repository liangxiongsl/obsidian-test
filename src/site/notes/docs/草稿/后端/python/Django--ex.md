---
{"dg-publish":true,"permalink":"/docs///python/django-ex/"}
---


### 参考


进阶内容 => [使用 Django](https://docs.djangoproject.com/zh-hans/5.0/topics/)
api => [API 参考](https://docs.djangoproject.com/zh-hans/5.0/ref/)


### 配置
> topic：[Django 配置](https://docs.djangoproject.com/zh-hans/5.0/topics/settings/)
> ref：[django-admin 和 manage.py](https://docs.djangoproject.com/zh-hans/5.0/ref/django-admin/), [配置](https://docs.djangoproject.com/zh-hans/5.0/ref/settings/)


| 配置           | 用途    |
| ------------ | ----- |
| ROOT_URLCONF | 设置根路由 |
|              |       |


### 应用(app)
> ref：[应用程序](https://docs.djangoproject.com/zh-hans/5.0/ref/applications/), [Django 实用程序](https://docs.djangoproject.com/zh-hans/5.0/ref/utils/), [contrib 包](https://docs.djangoproject.com/zh-hans/5.0/ref/contrib/), 


一个 Django app 由 `urls`, `views`, `template`, `static`, `model`, `migration`, `database` 等组成

`urls`, `views` => 实现 前端 和 后端 的交互
`template`, `static` => 主要实行前端功能 => 可以交给前端框架实现前后端分离
`model`, `migration`, `database` => 主要实行后端功能
### 路由(urls)
> topic：[URL调度器](https://docs.djangoproject.com/zh-hans/5.0/topics/http/urls/)
> ref：[django.urls 实用函数](https://docs.djangoproject.com/zh-hans/5.0/ref/urlresolvers/), [URLconfs 中使用的 django.urls 函数](https://docs.djangoproject.com/zh-hans/5.0/ref/urls/), [URLconfs 中使用的 django.urls 函数](https://docs.djangoproject.com/zh-hans/5.0/ref/urls/#module-django.conf.urls), [跨站请求伪造保护](https://docs.djangoproject.com/zh-hans/5.0/ref/csrf/)

路由在 django 中被称为 **URLconfs**

涉及的包和模块：
=> `django.urls` => `path()`, `re_path()`, 
=> `django.http` => `HttpRequest`, `HttpResponse`

#### url 调度器

Django 处理请求的工作方式：
=> 根据 `HttpRequest` 对象的 `urlconf` 属性，或者 `ROOT_URLCONF` 确定**根路由器**
=> 根据 `HttpRequest` 的 `path_info` 部分匹配路由器模块中 `urlpatterns` 里的一条路由，并转入下一条**路由器**，或者一个**视图**；若匹配不到路由，则 Django 调用适当的错误处理视图，参见 [[docs/草稿/后端/python/Django--ex#安全\|安全->异常]]
=> 例子
```python
urlpatterns = [
    path("articles/2003/", views.a),
    path("articles/<int:year>/", views.b),
    path("articles/<int:year>/<int:month>/", views.c),
    path("articles/<int:year>/<int:month>/<slug:slug>/", views.d),
]
```
- `/articles/2005/03/` => 匹配第三项，调用 `views.c(request, year=2005, month=3)`
- `/articles/2003/` => 匹配第一项，调用 `views.a(request)`
- `/articles/2003` => 匹配不到
- `/articles/2003/03/building-a-django-site/` => 匹配第四项，调用 `views.d(request, year=2005, month=3, slug='building-a-django-site')`

**路径转换器** => 在 path 的 `route` 参数中用于指定 `path-params`
- `<str:path_param>` => 匹配 `[^/]+` 并传递给 `path_param: str` 参数
- `<int:path_param>` => 匹配自然数 `\d+` 并传递给 `path_param: int` 参数
- `<slug:path_param>` => 匹配 `[^\x00-\xFF]+`（ASCII 字母、下划线、连字符）并传递给 `path_param: str` 参数
- `<uuid:path_param>` => 匹配一个格式化的 [UUID](https://docs.python.org/3/library/uuid.html#uuid.UUID)
- `<path:path_param>` => 匹配 `.+` 并传递给 `path_param: str` 参数
=> 例子：

**自定义路径转换器** => 定义一个类，其具有 `regex` 属性，`to_python()` 和 `to_url()` 方法 => 然后用 `register_converter(ExampleConverter: class, converter_name: str)` 注册转换器
- `regex: str` => 指定匹配的模式
- `to_python(self, value: str): any` => 指定路径参数传递给视图函数形参时的数据
- `to_url(self, value: any): str` => 指定数据转换为 url 中的路径参数时得到的字符串（即 `to_python()` 的逆变换），通常在调用 `reverse()` 时触发
=> 例子：
```python
class ExampleConverter:
	regex = "\d{4}"
	def to_python(self, value):
		return int(value)
	def to_url(self, value):
		return "%04d" % value

from django.urls import path, register_converter
register_converter(ExampleConverter, "yyyy")
urlpatterns = [
	path("<yyyy:param>", ...)
]
```


正则路由 => `re_path()` => 使用 `(?P<path-param>pattern)` 或 `(pattern)` 进行分组（或者说指定路径参数）
=> 例子： `re_path(r'^email/(?P<param>\w+@\w+\.\w+)/$', ...)`
- 嵌套参数 => 





#### 附录

| urls 的函数                                                                                                | 用途                      | 参数解释                                   |
| ------------------------------------------------------------------------------------------------------- | ----------------------- | -------------------------------------- |
| path(route: str, view: (req: HttpRequest, **path_params) => HttpResponse, args?: dict, name?: str)      | 获取一条匹配规则 => 将匹配的路由转发到视图 | args => 传递给视图的额外数据<br>name => 路由规则的标识符 |
| re_path(route: regex, view: (req: HttpRequest, **path_params) => HttpResponse, args?: dict, name?: str) |                         |                                        |


### 视图(views)
> topic：[编写视图](https://docs.djangoproject.com/zh-hans/5.0/topics/http/views/), [视图装饰器](https://docs.djangoproject.com/zh-hans/5.0/topics/http/decorators/), [文件上传](https://docs.djangoproject.com/zh-hans/5.0/topics/http/file-uploads/), [Django 便捷函数](https://docs.djangoproject.com/zh-hans/5.0/topics/http/shortcuts/), [通用视图](https://docs.djangoproject.com/zh-hans/5.0/topics/http/generic-views/), [中间件](https://docs.djangoproject.com/zh-hans/5.0/topics/http/middleware/), [如何使用会话](https://docs.djangoproject.com/zh-hans/5.0/topics/http/sessions/)
> topic2：[基于类的视图](https://docs.djangoproject.com/zh-hans/5.0/topics/class-based-views/intro/), [内置的基于类的通用视图](https://docs.djangoproject.com/zh-hans/5.0/topics/class-based-views/generic-display/), [使用基于类的视图处理表单](https://docs.djangoproject.com/zh-hans/5.0/topics/class-based-views/generic-editing/), [在基于类的视图中使用混入](https://docs.djangoproject.com/zh-hans/5.0/topics/class-based-views/mixins/), 
> topic3：[条件视图处理](https://docs.djangoproject.com/zh-hans/5.0/topics/conditional-view-processing/), [分页](https://docs.djangoproject.com/zh-hans/5.0/topics/pagination/)
> ref：[内置基于类的视图 API](https://docs.djangoproject.com/zh-hans/5.0/ref/class-based-views/), [内置视图](https://docs.djangoproject.com/zh-hans/5.0/ref/views/), [请求和响应对象](https://docs.djangoproject.com/zh-hans/5.0/ref/request-response/), [中间件](https://docs.djangoproject.com/zh-hans/5.0/ref/middleware/)


### 模板(template)
> topic：[模板](https://docs.djangoproject.com/zh-hans/5.0/topics/templates/), [使用表单](https://docs.djangoproject.com/zh-hans/5.0/topics/forms/)
> ref：[模板](https://docs.djangoproject.com/zh-hans/5.0/ref/templates/), [TemplateResponse 和 SimpleTemplateResponse](https://docs.djangoproject.com/zh-hans/5.0/ref/template-response/), [表单](https://docs.djangoproject.com/zh-hans/5.0/ref/forms/), [分页器](https://docs.djangoproject.com/zh-hans/5.0/ref/paginator/)


### 静态资源(static)


### 模型(models)
> topic：[模型](https://docs.djangoproject.com/zh-hans/5.0/topics/db/models/), [执行查询](https://docs.djangoproject.com/zh-hans/5.0/topics/db/queries/), [聚合](https://docs.djangoproject.com/zh-hans/5.0/topics/db/aggregation/), [搜索](https://docs.djangoproject.com/zh-hans/5.0/topics/db/search/), [管理器](https://docs.djangoproject.com/zh-hans/5.0/topics/db/managers/), [原生sql](https://docs.djangoproject.com/zh-hans/5.0/topics/db/sql/), [数据库事务](https://docs.djangoproject.com/zh-hans/5.0/topics/db/transactions/), [模型关联 API 用法示例](https://docs.djangoproject.com/zh-hans/5.0/topics/db/examples/), [序列化 Django 对象](https://docs.djangoproject.com/zh-hans/5.0/topics/serialization/)
> ref：[模型](https://docs.djangoproject.com/zh-hans/5.0/ref/models/), [信号](https://docs.djangoproject.com/zh-hans/5.0/ref/signals/), [验证器](https://docs.djangoproject.com/zh-hans/5.0/ref/validators/), 

主要涉及 `django.db.models.Model` 类


Django 中只有 `app` 才拥有自己的 `model`，其定义在 `<app>.models` 下（可以是 `.py` 的模块文件，也可以是包的 `__init__.py` 文件）

注册模型 => 首先要注册 app => 即 `INSTALLED_APPS` 添加一条表示 `model` 所属 app 的配置
定义模型 => 定义字段 => **字段类型**、**字段选项**

字段类型的作用
- 指定字段在数据库中的类型
- 渲染表单字段时默认使用 html 表单进行渲染

####  模型类

1. `<app>.models` 下的 `django.db.models.Model` 的子类总是对应一张数据库表（两个模型之间也可能有一张中间表）
2. `Model` 子类的属性与对应的数据库表的字段一一映射





#### 模型字段
> 外链：[模型字段参考 -> 字段类型](https://docs.djangoproject.com/zh-hans/5.0/ref/models/fields/#field-types)

普通字段： => 包括整数、浮点数、二进制、bool、字符串、邮箱、url、时间、文件、IP地址、slug、uuid等有关原始数据的字段

| 字段类型                                                                                                       | 解释                               | 表单部件                                                            | 相关验证                                  | 补充                                   |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------- | --------------------------------------------------------------- | ------------------------------------- | ------------------------------------ |
| SmallIntegerField                                                                                          | 用于存储 16 位整数                      |                                                                 | MinValueValidator, MaxValueValidator  |                                      |
| IntegerField                                                                                               | 用于存储 32 位整数                      |                                                                 |                                       |                                      |
| BigIntegerField                                                                                            | 用于存储 64 位整数                      |                                                                 |                                       |                                      |
| PositiveSmallIntegerField                                                                                  | 用于存储 16 位正整数                     |                                                                 |                                       |                                      |
| PositiveIntegerField                                                                                       | 用于存储 32 位正整数                     |                                                                 |                                       |                                      |
| PositiveBigIntegerField                                                                                    | 用于存储 64 位正整数                     |                                                                 |                                       |                                      |
| SmallAutoField                                                                                             | 根据可用的 id 自动递增的 SmallIntegerField |                                                                 |                                       |                                      |
| AutoField                                                                                                  | 根据可用的 id 自动递增的 IntegerField      |                                                                 |                                       |                                      |
| BigAutoField                                                                                               | 根据可用的 id 自动递增的 BigIntegerField   |                                                                 |                                       |                                      |
| FloatField                                                                                                 | 用于存储 float                       | `localize=Ture` => TextInput<br>`localize=False` => NumberInput |                                       |                                      |
| DecimalField(max_digits: int, decimal_places: int)                                                         | 用于存储 Decimal                     | `localize=Ture` => TextInput<br>`localize=False` => NumberInput | DecimalValidator                      |                                      |
| BinaryField(max_length: int)                                                                               | 用于存储二进制数据                        |                                                                 | MaxLengthValidator                    |                                      |
| BooleanField                                                                                               | 用于存储 bool                        | CheckboxInput                                                   |                                       |                                      |
| CharField(max_length: int, db_collation?)                                                                  | 用于存储 str                         | TextInput                                                       | MaxLengthValidator                    |                                      |
| TextField(max_length: int, db_collation?)                                                                  | 用于存储大文本 str                      | TextInput                                                       |                                       |                                      |
| EmailField(max_length=254)                                                                                 | 存储邮箱的 CharField                  |                                                                 | EmailValidator                        |                                      |
| URLField                                                                                                   | 存储 url 的 CharField               |                                                                 | URLValidator                          |                                      |
| DateField(auto_now?: bool, auto_now_add?: bool)                                                            | 用于存储 datetime.date               | DateInput                                                       |                                       | auto_now, auto_now_add, default 三者互斥 |
| TimeField(auto_now=False, auto_now_add=False)                                                              | 用于存储 datetime.time               |                                                                 |                                       |                                      |
| DateTimeField(auto_now?: bool, auto_now_add?: bool)                                                        | 用于存储 datetime.datetime           | DateTimeInput                                                   |                                       |                                      |
| DurationField                                                                                              | 用于存储 datetime.timedelta          |                                                                 |                                       |                                      |
| FileField(upload_to='', storage=None, max_length=100)                                                      | 用于存储文件                           |                                                                 |                                       | FieldFile？                           |
| ImageField(upload_to=None, height_field=None, width_field=None, max_length=100)                            | 用于验证有效的图像的 FileField             | ClearableFileInput                                              |                                       | 需要 pillow 库                          |
| FilePathField(path='', match=None, recursive=False, allow_files=True, allow_folders=False, max_length=100) |                                  |                                                                 |                                       |                                      |
| GenericIPAddressField(protocol='both', unpack_ipv4=False)                                                  |                                  |                                                                 |                                       |                                      |
| JSONField(encoder: json.JSONEncoder, decoder: json.JSONDecoder)                                            |                                  |                                                                 |                                       |                                      |
| SlugField(max_length=50)                                                                                   |                                  |                                                                 | validate_slug 或 validate_unicode_slug |                                      |
| UUIDField                                                                                                  | 用于存储通用唯一标识符的字段                   |                                                                 |                                       |                                      |
| GeneratedField(expression, output_field, db_persist=None)                                                  | 数据库底层中由其他字段计算的字段                 |                                                                 |                                       |                                      |


##### 表间关系

定义模型间的关系的三个**特殊字段**：


| 表间关系 | 对应字段类型                                                           | 补充                                               |
| ---- | ---------------------------------------------------------------- | ------------------------------------------------ |
| 多对一  | ForeignKey(model: Model \| str, ...)                             | 支持**自关联关系**                                      |
| 多对多  | ManyToManyField(model: Model \| str, through: Model \| str, ...) | 1. 建议使用复数形式<br>2. 只能设置在两个多对多模型之一<br>3. 总是会产生中间模型 |
| 一对一  | OneToOneField(model: Model \| str, ...)                          |                                                  |
注：
- model => **关联模型**
- through => 自定义**中间模型** => 用于给多对多关系**添加额外字段**

多方的相关方法：
```python
<model1>.<model2>_set.add(model: Model2, through_defaults: dict)
<model1>.<model2>_set.create(opt1, ..., through_defaults: dict)
<model1>.<model2>_set.set(model: Model2[], through_defaults: dict)
<model1>.<model2>_set.remove(model: Model2)
<model1>.<model2>_set.clear()
```

注：字段有命名限制 => 不能是关键字，不能有**下划线**，不能**以下换线结尾**


#### 模型字段的构造参数
> 外链：[模型字段参考 -> 字段选项](https://docs.djangoproject.com/zh-hans/5.0/ref/models/fields/#field-options)



| 字段参数                              | 解释                        | 表单？        | 补充                                          |
| --------------------------------- | ------------------------- | ---------- | ------------------------------------------- |
| null: bool                        | 数据库中若字段为空，则将字段设置为 NULL    |            |                                             |
| blank: bool                       | 字段可为空                     |            |                                             |
| choices: 2-tuple[] \| map \| enum | 枚举字段（key为后端数据，value为前端数据） | `<select>` | 为 `model` 添加新字段时，该选项应与 `default` 选项配合使用     |
| default: any \| func              | 字段默认值                     |            |                                             |
| help_text: str                    |                           |            |                                             |
| primary_key: bool                 | 表的唯一主键（该字段只读）             |            | 若表中没有该字段，则 django 将添加 IntegerField 字段，并设为主键 |
| unique: bool                      |                           |            |                                             |
| verbose_name: str                 | **人类可读**的字段名              |            |                                             |

| 字段参数                   | 解释                   |
| ---------------------- | -------------------- |
| db_column: str         | 数据库底层中该字段对应的列名       |
| db_comment: str        | 数据库底层中对该字段的注释        |
| db_default: any        | 字段默认值，可以是字面量，或者数据库函数 |
| db_index: bool         | 数据库底层中对该字段创建索引       |
| db_tablespace: bool    |                      |
| editable               |                      |
| error_messages         |                      |
| unique_for_date: bool  |                      |
| unique_for_month: bool |                      |
| unique_for_year: bool  |                      |
| validators:            | 验证器列表                |

#### 模型字段的属性

| 普通属性               | 解释      |
| ------------------ | ------- |
| auto_created: bool |         |
| concrete: bool     |         |
| hidden: bool       |         |
| is_relation: bool  | 是否为特殊字段 |
| model              | 当前模型    |

| 特殊字段的属性            | 解释     |
| ------------------ | ------ |
| many_to_many: bool |        |
| many_to_one: bool  |        |
| one_to_many: bool  |        |
| one_to_one: bool   |        |
| related_model      | 相关联的模型 |

注：特殊字段 => 用于定义两个模型之间的关系的字段（ForeignKey, ManyToManyField, OneToOneField 其中之一）

#### Meta 内部类
> 外链：[模型 | Django 文档 | Django (djangoproject.com)](https://docs.djangoproject.com/zh-hans/5.0/topics/db/models/#meta-options), [模型 Meta 选项 | Django 文档 | Django (djangoproject.com)](https://docs.djangoproject.com/zh-hans/5.0/ref/models/options/)

`ordering: str[]` => 指定排序的字段
`verbose_name_plural` => 
`abstract: bool` => 指定当前模型是否为**抽象基类** => 若为 true，那么该模型不会创建任何数据库表
`indexes: models.Index[]` => 用于创建数据库索引，参见 [[docs/草稿/后端/python/Django--ex#模型索引\|#模型索引]]

#### 模型自定义方法

模型中的方法可以执行**表级操作**（这些定义**不需要迁移**）

例子：
```python
class User(models.Model):
    username = models.CharField("user's name",max_length=20)
    password = models.CharField("user's password",max_length=20)

    def func(self):
        return f'{self.username} {self.password}'

    @property
    def virtual_attr(self):
        return f'{self.username} {self.password}'
```

两个常用的自定义方法：
- `__str__()` => 用于交互式控制台或后台中现实某个模型本身的内容
- `get_absolute_url()` => 告诉 Django 如何计算对象的 url


可以重写 `save()`，`delete()` 等 `Model` 方法 => 
例子：
```python
def save(self, *args, **kwargs):
	# do something ...
	super().save(args,kwargs)
	# do something else ...
```

#### 模型类继承

抽象基类 => **模型基类**在 `Meta` 子类上定义字段 `abstract = True` => 该模型不会创建任何表，仅用于继承
多表继承 => **模型基类**在 `Meta` 子类上定义字段 `abstract = False` => 继承链中的每个模型都会创建表
代理模型 => **模型子类**在 `Meta` 子类上定义字段 `proxy = True` => 该模型不会创建任何表，但是可以操作基类的字段和方法

#### 模型索引
> 外链：[模型索引参考 | Django 文档 | Django (djangoproject.com)](https://docs.djangoproject.com/zh-hans/5.0/ref/models/indexes/#index-options)

[[docs/草稿/后端/python/Django--ex#Meta 内部类\|#Meta 内部类]] 中定义的 indexes 用于给模型创建多条索引

| models.Index 构造器选项 | 解释  |
| ------------------ | --- |
| expressions        |     |
| fields             |     |
| name               |     |
| db_tablespace      |     |
| opclasses          |     |
| condition          |     |

### 模型查询

数据库查询相关的包或类
=> `django.db.models` => `Model`, `ForeignKey`, `ManyToManyField`, `QuerySet`, `F`, `AVG`, `MIN`, `MAX`
=> `django.db.models.manager` => `Manager`
=> `django.db.models.fields.json` => `KT`

#### 执行查询

创建或保存对象 =>
- `<Model>.save(**opts)` => 保存模型对象
- `<Manager>.create(**attr_opts)` => 创建并保存对象
=> 例子：
```python
# 例1
user_model = UserModel(username='150',password='62')
user_model.save()
# 例2
UserModel.objects.create(username='150',password='62') # => 会返回对应模型
```

修改对象 => 
- `<Model>.<attr> = new_val` => 直接修改
- `<Model>.<func>()` => 间接修改
- `<Model>.<many-Model>_set.add(<many-Model1>, ...)` => 添加一个`多方模型`的记录
- `<Model>.<one-Model> = <one-Model>` => 覆盖一个`一方模型`的记录


检索对象 => 用到 QuerySet 类 => 通常通过 `<Model>.objects.all()` 得到
=> 通过 `get()` 获取单个对象
=> 通过 `filter()`, `exclude()` 过滤或排除检索到的对象集合
注：QuerySet 是**惰性的** => 每次过滤都只是在添加限制条件，并非真正执行了 sql，只会在你 “要使用” 时才会执行
=> 支持**切片**极其**step**语法 => 例如：`<QuerySet>[0]`, `<QuerySet>[0:5]`, `<QuerySet>[::2]`, `<QuerySet>[1::2]`
注：指定步长后会执行 sql

其中 `filter()`, `exclude()` 等方法支持如下形式的可选参数：
- `<attr>` => 模型的属性
- `<attr>__<lookup_type>` => 指定模型属性的各种复杂查询 => `lookup_type` 的常见类型 => `lte`, `gte`. `lt`, `gt`, `exact`, `iexact`, `regex`, `iregex`, `contains`, `icontains`, `startswith`, `endswith`, `istartswith`, `iendswith`, `in`
- `<one-model>_id` => 关联的表模型的 id
- `<one-model>__<one-model-attr>` => 指定 `一方模型` 的属性的限制条件
- `<one-model>__<one-model-attr>__<lookuptype>` => 
- `<many-model>__<many-model-attr>` => 指定**至少满足一个** `多方模型` 的属性的限制条件
- `<many-model>__<many-model-attr>__<lookuptype>` => 
参数值：
- 常量
- F 表达式 => `F(attr: str)` => 可以引用当前模型的字段，并进行相关运算
- 可以使用 `Min`, `Max`, `AVG` 等

缓存问题 => [执行查询 | Django 文档 | Django (djangoproject.com)](https://docs.djangoproject.com/zh-hans/5.0/topics/db/queries/#caching-and-querysets)

#### 异步查询

#### json 查询

json 字段在 `filter()`, `exclude()` 等方法中的参数的组成：
- 前缀 `<json-attr>`
- `__<int>` => 索引 json 数组的第 `<int>` 个 json 对象
- `__<key>` => 索引 json 对象 key 为 `<key>` 的 json 对象

`KT(lookup: str)` => 针对于 json 字段的类似于 `F(lookup: str)` 的函数

json 字段还支持更多的 `lookup_type`：
- `contains` => 
- `contained_by` => 
- `has_key: str` => 含有对应的 key
- `has_keys: str[]` => 含有给定 key 数组中的所有 key
- `has_any_keys: str[]` => 含有给定 key 数组中的一个 key

#### 通过 Q 对象完成复杂查询
[执行查询 | Django 文档 | Django (djangoproject.com)](https://docs.djangoproject.com/zh-hans/5.0/topics/db/queries/#complex-lookups-with-q-objects)



#### 附录

注：下面的方法加上前缀 `a` 总是可以得到异步版本

| Model 的类属性       | 用途  |
| ---------------- | --- |
| objects: Manager |     |
|                  |     

| Model 的方法                                                                                      | 用途   |
| ---------------------------------------------------------------------------------------------- | ---- |
| save(force_insert=False, force_update=False, using=DEFAULT_DB_ALIAS, update_fields=None): void | 保存记录 |
|                                                                                                |      |

| Manager 的方法             | 用途          |
| ----------------------- | ----------- |
| all(): QuerySet         |             |
| create(**kwargs): Model | 创建一个对象并保存记录 |
|                         |             |
注：Manager 实例通常通过 `Model.objects` 获取

| QuerySet 的方法                     | 用途     |
| -------------------------------- | ------ |
| get(**kwargs): Model             | 检索单个对象 |
| filter(**lookup_args): QuerySet  | 过滤对象   |
| exclude(**lookup_args): QuerySet | 排除对象   |
| values(): QuerySet               |        |
| annotate(): QuerySet             |        |


### 迁移(migrations)
> topic：[迁移](https://docs.djangoproject.com/zh-hans/5.0/topics/migrations/), [管理文件](https://docs.djangoproject.com/zh-hans/5.0/topics/files/), 
> ref：[迁移操作](https://docs.djangoproject.com/zh-hans/5.0/ref/migration-operations/), [SchemaEditor](https://docs.djangoproject.com/zh-hans/5.0/ref/schema-editor/), 

### 数据库(database)
> topic：[多数据库](https://docs.djangoproject.com/zh-hans/5.0/topics/db/multi-db/), [表空间](https://docs.djangoproject.com/zh-hans/5.0/topics/db/tablespaces/), [数据库访问优化](https://docs.djangoproject.com/zh-hans/5.0/topics/db/optimization/), [数据库工具](https://docs.djangoproject.com/zh-hans/5.0/topics/db/instrumentation/), [辅助工具](https://docs.djangoproject.com/zh-hans/5.0/topics/db/fixtures/), 
> ref：[数据库](https://docs.djangoproject.com/zh-hans/5.0/ref/databases/)

### 测试(test)
> topic：[编写并运行测试](https://docs.djangoproject.com/zh-hans/5.0/topics/testing/overview/), [测试工具](https://docs.djangoproject.com/zh-hans/5.0/topics/testing/tools/), [进阶测试主题](https://docs.djangoproject.com/zh-hans/5.0/topics/testing/advanced/)

### 信号
> topic：[信号](https://docs.djangoproject.com/zh-hans/5.0/topics/signals/)

### 文件
> ref：[文件处理](https://docs.djangoproject.com/zh-hans/5.0/ref/files/)


### 安全
> topic：[Django中的用户认证](https://docs.djangoproject.com/zh-hans/5.0/topics/auth/)，[加密签名](https://docs.djangoproject.com/zh-hans/5.0/topics/signing/), [发送邮件](https://docs.djangoproject.com/zh-hans/5.0/topics/email/), [Django 的安全性](https://docs.djangoproject.com/zh-hans/5.0/topics/security/), [系统检查框架](https://docs.djangoproject.com/zh-hans/5.0/topics/checks/)
> ref：[点击劫持保护](https://docs.djangoproject.com/zh-hans/5.0/ref/clickjacking/), [系统检查框架](https://docs.djangoproject.com/zh-hans/5.0/ref/checks/),[Django 异常](https://docs.djangoproject.com/zh-hans/5.0/ref/exceptions/)

#### 认证




### 性能
> topic：[Django 缓存框架](https://docs.djangoproject.com/zh-hans/5.0/topics/cache/), [性能和优化](https://docs.djangoproject.com/zh-hans/5.0/topics/performance/)


### 其他
> topic：[国际化和本地化](https://docs.djangoproject.com/zh-hans/5.0/topics/i18n/), [日志](https://docs.djangoproject.com/zh-hans/5.0/topics/logging/), [扩展包](https://docs.djangoproject.com/zh-hans/5.0/topics/external-packages/), [异步支持](https://docs.djangoproject.com/zh-hans/5.0/topics/async/)
> ref：[日志](https://docs.djangoproject.com/zh-hans/5.0/ref/logging/), [Unicode 数据](https://docs.djangoproject.com/zh-hans/5.0/ref/unicode/)




