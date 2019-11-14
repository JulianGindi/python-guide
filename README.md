# Python Guide

This is an attempt to document how I develop with Python with some tips and tricks along the way.

*Note: Always develop with Python3*

## Installing Python

#### Mac OSX

`brew install python3`


Any other reasonable development environment should have a working version.

## Dependency Management/Packages

**Use python virtual environments**

There are a few schools of thought here, but I primarily follow a two-tier approach to virtualenv creation using both virtualenvwrapper and pipenv. 


### ```virtualenvwrapper```

I mostly use ```virtualenvwrapper``` to create more "system-level" environments. These typically isolate tools based on categories such as "devops tools" vs "scientific computing tools" or however you would like to organize cross-project shared dependency management. 

#### Setup 

More here about setup...

#### Usage

A typical workflow looks like such...

```
$ mkvirtualenv devops_tools -p python3
$ workon devops_tools
$ pip install requests
...
$ deactivate
```
