

Following [this](https://shiny.posit.co/py/docs/install-create-run.html) tutorial for Shiny python app development. 


When I ran `pip install shiny`, i got the following error

```bash
Installing collected packages: appdirs, uvicorn, uc-micro-py, python-multipart, prompt-toolkit, mdurl, htmltools, asgiref, watchfiles, starlette, questionary, markdown-it-py, linkify-it-py, mdit-py-plugins, shiny
  Attempting uninstall: prompt-toolkit
    Found existing installation: prompt-toolkit 3.0.42
    Uninstalling prompt-toolkit-3.0.42:
      Successfully uninstalled prompt-toolkit-3.0.42
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
ipython 8.24.0 requires prompt-toolkit<3.1.0,>=3.0.41, but you have prompt-toolkit 3.0.36 which is incompatible.
Successfully installed appdirs-1.4.4 asgiref-3.8.1 htmltools-0.5.3 linkify-it-py-2.0.3 markdown-it-py-3.0.0 mdit-py-plugins-0.4.2 mdurl-0.1.2 prompt-toolkit-3.0.36 python-multipart-0.0.9 questionary-2.0.1 shiny-1.1.0 starlette-0.38.5 uc-micro-py-1.0.3 uvicorn-0.30.6 watchfiles-0.24.0
```

Probably I will update prompt-toolkit from 3.0.36 to 3.0.41

Next, i rand `pip install --upgrade shiny htmltools` 

The tutorial suggests installing [python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) VSCode extension that I already had and [Shiny](https://marketplace.visualstudio.com/items?itemName=posit.shiny) that I installed. 

All set, next I created a new python file using VSCode option file -> new file -> python file. 

I copied the code from tutorial and ran by pressing the arrow button, it worked , see below 

![shiny\_test1|900](Pasted%20image%2020240920120953.png)


Since I wanted to use plotly, thus, had to install shinywidgets, I copied following command from [this](https://shiny.posit.co/py/docs/jupyter-widgets.html) page to 

```python
pip install shinywidgets
```


