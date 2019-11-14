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


### [`virtualenvwrapper`](https://virtualenvwrapper.readthedocs.io/en/latest/)

I mostly use `virtualenvwrapper` to create more "system-level" environments. These typically isolate tools based on categories such as "devops tools" vs "scientific computing tools" or however you would like to organize cross-project shared dependency management. 

#### Setup 

For `virtualenvwrapper`, you need to install the package, as well as set up a few things in your shell environment. YMMV with the commands below, but the key one to potentially modify is the location of the virtualenvwrapper script. For Mac OS, these commands should work fine. 

```
$ pip install virtualenvwrapper
$ mkdir ~/.virtualenvs # Create directory to store virtualenvs
$ echo "export WORKON_HOME=~/.virtualenvs" >> ~/.zshrc
$ echo "VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3" >> ~/.zshrc # Making sure we are using python3 for default virtualenvs
$ echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.zshrc      # Sources the main script to initialize virtualenvwrapper
```

#### Usage

A typical workflow looks like such...

```
$ mkvirtualenv devops_tools -p python3
$ lsvirtualenvs # See all created virtualenvs
$ workon devops_tools
$ pip install requests
...
$ deactivate
$ rmvirtualenv devops_tools # You can remove when done
```

Here would be how to create a python2 virtualenv:

`$ mkvirtualenv old_school -p python2`

### [`pipenv`](https://pipenv.readthedocs.io/en/latest/)

I pretty much use Pipenv for all new larger software projects. I love Pipenvs approach to dependency management, and have been an advocate for a python-based lockfile approach for a while. It is best for specifying per-project dependencies with an eye towards ease of use for developers.

#### Setup

`$ pip install pipenv`

#### Usage

Just initialize and begin installing a package with it! It will handle creating all the required files for you. I run the following from the root of my project...

```
$ pipenv --python 3.7     # Start pipenv with python 3.7
$ pipenv install requests # Install any pip package you want
$ pipenv shell            # Expose pipenv environment to shell. "Sources" the virtualenv
$ pipenv sync             # Main command you want to run to sync with lockfile and not get new versions
$ pipenv sync --dev       # Same as above but installs development dependencies
```

Unless you have "assumed the pipenv shell", you can run python commands in the environment with 

`$ pipenv run python manage.py runserver` for example...

## Formatting and Style

### Use [Black](https://github.com/psf/black)

#### Installing

`pip install black` or `pipenv install black --dev`

I love Black to keep style arguments at bay and I enjoy its overall approach to formatting. I set up VSCode to "format on save" for Python code. Below is the snippet in my config file to enable that (note, this also enables PEP8 style gutters):

```
    "[python]": {
        "editor.formatOnSave": true,
        "editor.rulers": [
            79,
            120
        ]
    },
```

#### Additional Usage

I like to modify Black's behavior a bit to limit line length. The following file "pyproject.toml" can be placed in the root of your project directory to enable that:

`pyproject.toml`

```
[tool.black]
line-length = 79
```
