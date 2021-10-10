---
layout: page
title: Solve Pip error "No module named helpers" on mac
tagline: pip error helpers
description: Solve Pip error "No module named helpers" on mac
---

<a href="https://twitter.com/intent/tweet?text=<Solve%20Pip%20 error%20"No%20module%20named%20helpers"%20on%20mac>https://mnahmad.github.io/scriptndebug/pages/python/pip-issue.md%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: 10/10/2021*

Its been some time that when ever I install a python package (after getting python3) using pip, i get the error "No module named helpers" and when I try to install "helpers" I get the same message. I Googled the issue and found this [post](https://stackoverflow.com/questions/55069451/pip-error-importerror-no-module-named-helpers) but it was linux related, thus, required some work to fix the issue on mac.

Firts I tried to see where python2.7 is on my system so I ran the following command

```
whereis python2.7
```

I was pointed to `/usr/bin/python`, and when i checked the path, I see the following.


```
ls -l python

python     -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
pythonw2.7 -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/pythonw2.7
python2    -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
python2.7  -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
```

__Note:__Some items removed from the list above.  

Since the [post](https://stackoverflow.com/questions/55069451/pip-error-importerror-no-module-named-helpers) was talking about site+packages, I tried to look for the folder but could not find it. Then i tried the command `which python` (and also confirmed the python site-package folder path from [stackoverflow](
https://stackoverflow.com/questions/122327/how-do-i-find-the-location-of-my-python-site-packages-directory) as well), it s was

```
which python

/usr/local/bin/python

```

and the site-packages path is `/usr/local/lib/python2.7/site-packages`. Now I modifed the provided/accepted solutoin in this [post](https://stackoverflow.com/questions/55069451/pip-error-importerror-no-module-named-helpers) according to my paths.

```
rm -rf /usr/local/lib/python2.7/site-packages
python2.7 -m ensurepip
pip install --upgrade pip

```

When I tried to insatll packages again with pip, it worked. 

Icon references:<br>
<a href="https://icon-library.net/icon/twiter-icon-15.html">Twiter Icon #268986</a>
