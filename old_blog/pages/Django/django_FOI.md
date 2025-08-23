---
layout: page
title: Django Frequently Occurred Errors (FOE)
tagline: Django Errors
description: Django Frequently Occurred Errors (FOE)
---

<a href="https://twitter.com/intent/tweet?text=<title with %20 for each space>%20https://mnahmad.github.io/scriptndebug/pages/<url-post>%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: --/--/----*


Error:

SyntaxError: positional argument follows keyword argument unpacking

Issue:
ownership_obj = Land_OwnershipType.objects.create(**ownership_json,plot_obj)

Solution:
the foreign key has be like `key_name=json_object`


-------

Error:
Model.objects does not appear


Issue:
the djanog was not even creating the model , why because the class was not inhering from models.Model

[ref](https://stackoverflow.com/questions/24912173/django-1-7-makemigrations-not-detecting-changes)

Solution:
Check model and make sure it is inheriting from models.Model


Error:
Incorrect assumption about max_value and max_precision value

Issue:
if max_digit=3 and max_preision=2 then the max value one c an have is 9.99

Solution:
the max_digit means all digits before and after the decimal  
