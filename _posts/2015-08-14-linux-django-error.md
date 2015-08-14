---
layout: post
category: ["linux", "django"]
title: "Django报错：ImportError: No module named 'pysqlite2'"
tags: ["Linux", "Django"]
---

运行环境：Cent OS6.5，Python3.4.3，Django1.8.3  

执行如下命令时报错：  

    python manage.py runserver

错误信息如下：  

    Traceback (most recent call last):
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/backends/sqlite3/base.py", line 31, in <module>
        from pysqlite2 import dbapi2 as Database
    ImportError: No module named 'pysqlite2'
    
    During handling of the above exception, another exception occurred:
    
    Traceback (most recent call last):
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/backends/sqlite3/base.py", line 33, in <module>
        from sqlite3 import dbapi2 as Database
      File "/usr/local/python3/lib/python3.4/sqlite3/__init__.py", line 23, in <module>
        from dbapi2 import *
    ImportError: No module named 'dbapi2'
    
    During handling of the above exception, another exception occurred:
    
    Traceback (most recent call last):
      File "manage.py", line 10, in <module>
        execute_from_command_line(sys.argv)
      File "/usr/local/python3/lib/python3.4/site-packages/django/core/management/__init__.py", line 338, in execute_from_command_line
        utility.execute()
      File "/usr/local/python3/lib/python3.4/site-packages/django/core/management/__init__.py", line 312, in execute
        django.setup()
      File "/usr/local/python3/lib/python3.4/site-packages/django/__init__.py", line 18, in setup
        apps.populate(settings.INSTALLED_APPS)
      File "/usr/local/python3/lib/python3.4/site-packages/django/apps/registry.py", line 108, in populate
        app_config.import_models(all_models)
      File "/usr/local/python3/lib/python3.4/site-packages/django/apps/config.py", line 198, in import_models
        self.models_module = import_module(models_module_name)
      File "/usr/local/python3/lib/python3.4/importlib/__init__.py", line 109, in import_module
        return _bootstrap._gcd_import(name[level:], package, level)
      File "<frozen importlib._bootstrap>", line 2254, in _gcd_import
      File "<frozen importlib._bootstrap>", line 2237, in _find_and_load
      File "<frozen importlib._bootstrap>", line 2226, in _find_and_load_unlocked
      File "<frozen importlib._bootstrap>", line 1200, in _load_unlocked
      File "<frozen importlib._bootstrap>", line 1129, in _exec
      File "<frozen importlib._bootstrap>", line 1471, in exec_module
      File "<frozen importlib._bootstrap>", line 321, in _call_with_frames_removed
      File "/usr/local/python3/lib/python3.4/site-packages/django/contrib/auth/models.py", line 41, in <module>
        class Permission(models.Model):
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/models/base.py", line 139, in __new__
        new_class.add_to_class('_meta', Options(meta, **kwargs))
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/models/base.py", line 324, in add_to_class
        value.contribute_to_class(cls, name)
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/models/options.py", line 250, in contribute_to_class
        self.db_table = truncate_name(self.db_table, connection.ops.max_name_length())
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/__init__.py", line 36, in __getattr__
        return getattr(connections[DEFAULT_DB_ALIAS], item)
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/utils.py", line 240, in __getitem__
        backend = load_backend(db['ENGINE'])
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/utils.py", line 111, in load_backend
        return import_module('%s.base' % backend_name)
      File "/usr/local/python3/lib/python3.4/importlib/__init__.py", line 109, in import_module
        return _bootstrap._gcd_import(name[level:], package, level)
      File "<frozen importlib._bootstrap>", line 2254, in _gcd_import
      File "<frozen importlib._bootstrap>", line 2237, in _find_and_load
      File "<frozen importlib._bootstrap>", line 2226, in _find_and_load_unlocked
      File "<frozen importlib._bootstrap>", line 1200, in _load_unlocked
      File "<frozen importlib._bootstrap>", line 1129, in _exec
      File "<frozen importlib._bootstrap>", line 1471, in exec_module
      File "<frozen importlib._bootstrap>", line 321, in _call_with_frames_removed
      File "/usr/local/python3/lib/python3.4/site-packages/django/db/backends/sqlite3/base.py", line 36, in <module>
        raise ImproperlyConfigured("Error loading either pysqlite2 or sqlite3 modules (tried in that order): %s" % exc)
    django.core.exceptions.ImproperlyConfigured: Error loading either pysqlite2 or sqlite3 modules (tried in that order): No module named 'dbapi2'

待解决...  

原因：  
需要安装sqlite-devel  

    yum install sqlite-devel

此时又出现错误信息：  

      File "/usr/bin/yum", line 30
        except KeyboardInterrupt, e:
                                ^
    SyntaxError: invalid syntax

此时原因可能是python3和python2语法规则不同导致，更新yum到最新版本：

    wget http://yum.baseurl.org/download/3.4/yum-3.4.3.tar.gz
    tar -xvf yum-3.4.3.tar.gz
    cd yum-3.4.3.tar.gz
    python yummain.py install yum

参考：  
centos安装和更新yum的方法：<http://blog.163.com/plawsh@126/blog/static/162925927201379566299>  






