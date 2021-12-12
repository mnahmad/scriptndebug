
---
layout: page
title: Template for new blogs
tagline: Template
description: Template for new blogs
---

<a href="https://twitter.com/intent/tweet?text=<title with %20 for each space>%20https://mnahmad.github.io/scriptndebug/pages/<url-post>%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: --/--/----*

The issue of .filter instead of .get

{'unit_name': 'metersq'}
fetched <QuerySet [<Land_Size_Units: metersq>]>
{'subcounty_name': 'Saharti Samre', 'county': {'id': 5, 'county_name': 'Tigray', 'countryId': 2, 'country': {'id': 2, 'country_name': 'Ethiopia', 'currency': 'Br', 'code': 'ET', 'counties': []}, 'subCounties': []}}
{'county_name': 'Tigray', 'country': {'id': 2, 'country_name': 'Ethiopia', 'currency': 'Br', 'code': 'ET', 'counties': []}}
{'id': 2, 'country_name': 'Ethiopia', 'currency': 'Br', 'code': 'ET', 'counties': []}
{'country_name': 'Ethiopia', 'currency': 'Br', 'code': 'ET', 'counties': []}
{'country_name': 'Ethiopia', 'currency': 'Br', 'code': 'ET'}
{'country_name': 'Ethiopia', 'currency': 'Br'}
country fetched <QuerySet [<countries: Ethiopia>]>
fetched -  Tigray
fetched -  Saharti Samre
{'id': 2, 'name': 'CIUY', 'farmingEntityId': 1, 'hasCrops': False, 'fenced': False, 'estimatedSize': 12.0, 'calculatedSize': 0.02, 'subCountyId': 5}
{'name': 'CIUY', 'hasCrops': False, 'fenced': False, 'estimatedSize': 12.0, 'calculatedSize': 0.02}
Internal Server Error: /respi/treeplanting/
Traceback (most recent call last):
  File "/usr/local/lib/python3.9/site-packages/django/core/handlers/exception.py", line 34, in inner
    response = get_response(request)
  File "/usr/local/lib/python3.9/site-packages/django/core/handlers/base.py", line 145, in _get_response
    response = self.process_exception_by_middleware(e, request)
  File "/usr/local/lib/python3.9/site-packages/django/core/handlers/base.py", line 143, in _get_response
    response = response.render()
  File "/usr/local/lib/python3.9/site-packages/django/template/response.py", line 106, in render
    self.content = self.rendered_content
  File "/usr/local/lib/python3.9/site-packages/rest_framework/response.py", line 70, in rendered_content
    ret = renderer.render(self.data, accepted_media_type, context)
  File "/usr/local/lib/python3.9/site-packages/rest_framework_json_api/renderers.py", line 517, in render
    return self.render_errors(data, accepted_media_type, renderer_context)
  File "/usr/local/lib/python3.9/site-packages/rest_framework_json_api/renderers.py", line 502, in render_errors
    utils.format_errors(data), accepted_media_type, renderer_context
  File "/usr/local/lib/python3.9/site-packages/rest_framework_json_api/utils.py", line 425, in format_errors
    if len(data) > 1 and isinstance(data, list):
TypeError: object of type 'NoneType' has no len()
