# xadmin 使用方法

## 安装xadmin

### 注意：切勿pip install 方式安装！不然同步数据库会因缺失log表引发错误

1. 下载对应Django版本的xadmin，解压并将其中的xadmin文件夹全部复制到自己的项目下（app同级目录），然后在 settings.py文件的INSTALLED_APPS内添加以下代码：
```
INSTALLED_APPS = [
    'xadmin',
    'crispy_forms',
]
```

2. 在根urls.py内修改为如下代码：

```
import xadmin

urlpatterns = [
    url(r'^xadmin/', xadmin.site.urls),
```

3. 使用pip install安装以下依赖库：
```
six
future
httplib2
django-reversion
django-formtools
django-crispy-forms
django-import-export
requests
```

如果还提示缺少某个模块，安装即可。

4. 生成并同步表

> python manage.py makemigrations

> python manage.py migrate

启动项目，打开 ```127.0.0.1:8000/xadmin``` 进入后台登录页面，输入用户名和密码进入后台


## 配置xadmin

### 配置后台主题

首先需要在创建好的app中新建一个adminx.py的文件，然后添加代码
```
# _*_ coding: utf-8 _*_
import xadmin
from xadmin import views

# 配置后台主题
class BaseSetting(object):
    enable_themes = True    # 启动主题功能
    use_bootswatch = True   # 启用更多主题


xadmin.site.register(views.BaseAdminView, BaseSetting)
```

### 配置后台系统名称和页脚版权、菜单样式

```
# _*_ coding: utf-8 _*_
import xadmin
from xadmin import views

class GlobalSetting(object):
    site_title = 'xx后台管理系统'     # 后台系统名称
    site_footer = 'XXXX xxxx.com'    # 页脚版权信息
    menu_style = 'accordion'         # 设置后台菜单为收缩样式


xadmin.site.register(views.CommAdminView, GlobalSetting)
```

### 设置app的中文名称

更改apps.py文件
```
# _*_ coding: utf-8 _*_
from django.apps import AppConfig

class UsersConfig(AppConfig):
    name = 'users'
    verbose_name = "中文名称"
    verbose_name = u"中文名称"  # Python2

```
更改 \_\_init\_\_.py 文件
```
default_app_config = "users.apps.UsersConfig"  # users为当前app名称
```

更多详细： https://xadmin.readthedocs.io/en/latest/index.html
