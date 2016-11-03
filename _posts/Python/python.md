# 确定python的site-packages位置
```
from distutils.sysconfig import get_python_lib
print get_python_lib()
```

# ipython
- IPython itself is focused on **interactive Python**, part of which is providing a Python kernel for Jupyter.
- Support for interactive data visualization and use of GUI toolkits.
- Flexible, embeddable interpreters to load into your own projects.
- Easy to use, high performance tools for parallel computing.

## how to install ipython on unbuntu?
```
pip install ipython # to make the version newer
sudo apt-get install ipython
```
## Jupyter notebook or IPython notebook
- Code can produce rich output such as images, videos, LaTeX, and JavaScript.
- has support for over 40 programming languages
- Leverage big data tools

# install sciPy
```
sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
```