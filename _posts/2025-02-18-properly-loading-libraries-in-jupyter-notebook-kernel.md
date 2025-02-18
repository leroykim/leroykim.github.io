---
layout: post
title: Properly Loading Libraries In Jupyter Notebook
categories: [Large Language Models (LLMs), AWS]
tags: [Jupyter Notebook, IPython, Python]
author: Dae-young Kim
comment: true
---

When a Jupyter Notebook kernel starts, it loads the libraries into the kernel's memory space. This means that when you import a library, the kernel keeps it in memory for subsequent use within the same session. If the kernel is restarted, the libraries will need to be loaded again.

The code is particulary helpful when you are using your custom libraries which needs frequent code modification:
```python
import IPython

IPython.Application.instance().kernel.do_shutdown(restart=True)
```

Otherwise, you have to manually click `Restart` button before you run the code after code modification.