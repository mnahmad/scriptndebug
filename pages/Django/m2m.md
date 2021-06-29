---
layout: page
title: Django app using M2M relationship models
description: Django M2M models
---
*Last update: 29/06/2021*

__This blog is an implementation of Djano many to many model.__

First install pip (if not already available), also know that you should always work with latest version of pip.

Install pip on mac by using the following commands  

```
sudo easy_install pip
$ sudo pip install --upgrade pip

```

the above commands were taken from [this](https://www.shellhacks.com/python-install-pip-mac-ubuntu-centos/) blog.


### Install Virtual environment
Virtual env is needed so that new package installations do not mess with mess with your environment.

```
sudo pip install virtualenv

result:
Successfully installed virtualenv-16.7.8


OR

sudo pip3 install virtualenv

results:
Successfully installed appdirs-1.4.4 distlib-0.3.2 filelock-3.0.12 virtualenv-20.4.7

```

One thing to note here, since I am using mac, usually on mac python is in /usr/local/lib/pythonx.x/ (like python2.7 or python3.9),  however on my machine it is in /Library/Python/2.7/ thus all packages are here.

Created folder to work from (I created agroforestry_app).

Now goto the folder and create the virtual env.

```
virtualenv env
```

The above command will create a folder called __env__.

Now start the virtual env by using the following command

```
source env/bin/activate

```
[reference](https://programwithus.com/learn-to-code/Pip-and-virtualenv-on-Mac/)

Once you activate virtual environment a folder is created in root folder (in our case it is agroforestry_app) with name __env__. All virtual environment settings are in this folder.

Now install the dependencies in virtual env. Since I am working with Django 1.11, as my other projects are in this version.

```
pip install Django==1.11.25
```

Django or any other package needs to be installed once, virtual env. will keep record of installed packages so next time when you will just start the virtual env. it will load all the packages.

Now Let create a django project

```
django-admin startproject af

```

After the above command, django will create the following files and folders

```
manage.py
af
  __init__.py
  settings.py
  urls.py
  wsgi.py


```

__Note__ Django creates a folder with same name as of project which contains project settings etc. According to Django tutorial "root directory is a container for your project. Its name doesn’t matter to Django; you can rename it  to anything you".

Now run the following command

```
django-admin startapp agroforestry
```

from the above command a new folder (agroforestry in our case) is created so the file and folder structure is now


```
manage.py
agroforestry
  __init__.py
  settings.py
  urls.py
  wsgi.py
  agroforestry
      __init__.py
      admin.py
      apps.py
      migrations
      models.py
      test.py
      views.py
```


Now add __agroforestry__ app to setting.py INSTALLED_APPS

```

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'agroforestry.apps.AgroforestryConfig',
]
```

Now lets crate tables in model.py, i created the following models

```

class state(models.Model):
    name = models.CharField(max_length=100)

    # optional
    class Meta:
        app_label = 'agroforestry'
        db_table = 'state'

    def __str__(self):
        return self.name


```

We have created tables in agroforestry/models.py but still there is no database till now. In order to create database we need to prepare migration file by using the following command.

Goto app folder (in our case agroforestry) and run the following command

If first time

```
python manage.py makemigrations agroforestry

```


and now run migration

```
python manage.py migrate
```

Now add the model to admin panel by registering model class to agroforestry/admin.py. This is done so that we can see the model(table) in admin panel.


```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.contrib import admin

from . import models

admin.site.register(models.state)

```

When all is done, we also need to create a new user (if not created before)

```
python manage.py createsuperuser

for this post my user is admin and password is

testpassword
```

Now run server to view the site + admin panel (make sure to goto folder where manage.py script is)


```
python manage.py runserver
```


If you visit http://127.0.0.1:8000/admin and login with above password then you will only see user and group tables (if you have not modified the models.py table)


Note, if you get error that port 8000 is already utilized , probably ur previous attempts left it in hanging thus use the following command to clear it


```
sudo lsof -t -i tcp:8000 | xargs kill -9
```

### SQL API


start sql shell


```
(env) ICTServicess-MacBook-Pro:af AMuhammad$ python manage.py shell
Python 2.7.10 (default, Feb 22 2019, 21:55:15)
[GCC 4.2.1 Compatible Apple LLVM 10.0.1 (clang-1001.0.37.14)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)
>>> import django
>>> django.setup()

>>> from agroforestry.models import crop
>>> crop.objects.all()
<QuerySet [<crop: maze>]>

>>> from agroforestry.models import crop, crop_district, tree, nursery
>>> crop_distric.objects.all()
<QuerySet [<crop_distric: crop_distric object>, <crop_distric: crop_distric object>]>

>>> crop_distric.date_de
<django.db.models.query_utils.DeferredAttribute object at 0x10231abd0>

>>> exit
Use exit() or Ctrl-D (i.e. EOF) to exit
>>> ^D
```

### how to implement M2M
What is M2M (image).

Many to Many relationship implementation in Django

Models/Tables are crop, district, landuse_type. Following are the steps.

1. Create table1 model (crop) in application's models.py file.

```
#crop table
class crop(models.Model):
    name = models.CharField(max_length=100)
    field_prep = models.TextField(max_length= 1000)
    planting_pethod = models.TextField(default='none')

    def __str__(self):
        return self.name
```

__Note:__ the method __str__ which will return name for admin module to show as list of items (in this case crop). If one uses __self__, then the method returns object and one will see a list of objects in admin module (when viewing the table).

2. Create table2 model (district) in application's models.py file.

```

class district(models.Model):
    name = models.CharField(max_length=100)
    state = models.ForeignKey(state, on_delete=models.CASCADE)
    crops = models.ManyToManyField(crop,related_name='districts',through='agroforestry.crop_distric', blank =False,)
    def __str__(self):
        return self.name
```

Note:
- related_name: metadata
- through: the m2m model/table , if not provided Dj will generate it automatically  (but then how we will refer it in admin.py without knowing the name)
- through_fields: specify fields as well otherwise automatically id field will be picked
- db_table: name of table to be created (if through parameter is not provided)

Notice
- we have added table1.returned field (crops in this case) in table2. So we are telling Django to also allow table2 to (while data entry) to link already added crops.

- we establied the link (to m2m model ) using the __through__ option as <through='m2m_model class name' >  

3. Create M2M model for table1 and table2 in application's models.py file.

```
class crop_distric(models.Model):
    district_id = models.ForeignKey(district, on_delete=models.CASCADE)
    crop_id = models.ForeignKey(crop, on_delete=models.CASCADE)
    date_de = models.DateField()

    def __self__(self):
        return '%s %s' % (self.district.name, self.crop.name)


```

Notice two things
- name of the table will appear as m2m section heading for data entry form in admin module  
- model contains ForeignKeys from both table1(crop) and table2(district), and table2 field will be shown as dropdown label so it should be proper.
- the use of __self__ as method
- return statement is returning 2 attributes/variables.


4. In application/admin.py , import models  crop, district,  crop_distric

```
from agroforestry.models import crop, district,  crop_distric
```

__Note:__ Any new model, regardless of relationship type, has to be imported if you want to see it in admin module.

5. Create inline class for m2m model/table. In the above exmaple, the m2m model is  crop_distric so we will create an inline claass for it.


```
class crop_inline_distric(admin.TabularInline):
    model = crop_distric
    extra = 1
```

Notice
- admin.TabularInline will show the options in tablular form.
- model tells Django which model will be used to add m2m data
- extra = 1 will show one option to save in admin module (otherwise you have to press add option , in this case, a district)

6. Register table1 (crop in this case)

```
@admin.register(crop)
```

and tell admin module to show the m2m option on a single screen for table 1 data entry/display. This is done by adding a class like below

```
@admin.register(crop)
class cropinline(admin.ModelAdmin):
    inlines = [crop_inline_distric]
```
the inlines option is tell Django to show district as One2Many option during data entry for crop.

__Note:__ If crop has m2m relationship with more than one table then use can add more inline classes like shown in inline statement below

```
@admin.register(crop)
class cropinline(admin.ModelAdmin):
    inlines = [crop_inline_distric,crop_inline_LU_type]
```

Now that we have added two inline classes, when one will add data to crop, two One2Many options will appear (1) for district and (2) for landuse_type

7. Register table2 (district in this case)

```
@admin.register(district)
class districtinline(admin.ModelAdmin):
    inlines = [crop_inline_distric]
```
Note that we also included crop_inline_distric as inlines option so that it crop can appear as One2Many in district data entry (we have alread done the same to table 1(crop) in point 6).

8. Run

```
python manage.py makemigrations agroforestry


and

python manage.py migrate
```

9. Run server to test

```
python manage.py runserver
```


### Templates


### Views
