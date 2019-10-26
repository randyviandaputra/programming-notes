## Installing Flask
Install Flask framework and python vitual envoirement
### What is Flask?
According to wikipedia :D, Flask is a micro web framework written in Python. It is classified as a microframework because it does not require particular tools or libraries. It has no database abstraction layer, form validation, or any other components where pre-existing third-party libraries provide common functions. Flask official wesite is available in [**flask.pocoo.org**](http://flask.pocoo.org/) **.**

### Why Using Flask?
-   It's based on Python
    
-   The Flask "core" is simple
    
-   Flask is a lighter weight framework for Python
    
-   Excellent documentation
    
-   Actively maintained
## Installing Flask-Framework
Before install flask, make sure python is installed in your PC
#### 1. Install Virtualenv
Virtualenv allows you to manage separate package installations for different projects. It essentially allows you to create a “virtual” isolated Python installation and install packages into that virtual installation. Using virtualenv allows you to **avoid installing Python packages globally** which could break system tools or other projects. You can install virtualenv using pip.

**For Debian or Ubuntu**
```
$ sudo apt-get install python-virtualenv
```
**For Mac**
```
$ sudo pip install virtualenv
```
**For Windows**
```
> pip install virtualenv virtualenvwrapper-win
```
You can simply create a new virtual environment by follow these commands:

    $ mkdir my_flask_app
    $ cd my_flask_app
    $ virtualenv my_virtualenv_name

Example:
```
$ virtualenv venv
```
And to activating our virtual envoirement that we create recently with thise command bellow:
```
## unix
$  . ven/bin/activate

## windows
>  venv\Scripts\activate
```

#### Install  Flask
```
$ pip install Flask
```

[==> Read more...](https://emixbal.gitbook.io/workspace/) 

> kalo sempet nanti pindah sini semua :)

