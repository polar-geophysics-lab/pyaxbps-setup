# Setting up PyAXBPS on JKB.UCSD.EDU (Alma Linux 9)

## Set up Python Environment
PyAXBPS is fairly old and no longer appears to be maintained. Installing it requires Python 3.8 (3.7 may work also). Having to use Python 3.8 means that you may need to older versions of other pythin packages used in your application. Use the requirements.txt file (see below) to do this.

Python version 3.8 and older are not usually available on current systems without installing them *in addition to* the Python versions native to the system.

The approach outlined below is to use Pyenv to install a specific version (3.8) of python. The python `venv` module is used to create an isolated python environment for the individual project.

## 1. Install pyenv Python Build dependencies (if you haven't already)
**THIS HAS BEEN DONE ON JKB.**

`curl https://pyenv.run | bash`

This is for Alma Linux 9. Package manager and library names may differ on other linux distributions.

Install dependencies:
**THIS HAS BEEN DONE ON JKB.**

`sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev`

## 2. Set up Your User environment (assumes Bash)
**EACH USER MUST DO THIS**
Add to your ~/.bashrc file:

```
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"
```

Log out and back in or `source ~/.bashrc`

## 3. Install/Build desired python version 
**THIS HAS BEEN DONE ON JKB.**

Install Python v3.8.20:

```
pyenv install 3.8.20`
```

## 4. Set Default Pyenv Python Version

In the root directory of your project tell `pyenv` that you want to base all work on Python v 3.8.20.

```
cd <project-dir>
pyenv local 3.8.20
```

This creates the file `.python-version` in the project directory.

### 5. Create isolated python/pip environment with venv

By using the `venv` module you can have separate projects all using the Pyenv python v3.8.20 while keeping the specific python dependencies (typically installed with `pip`) completely isolated. This avoids version and dependency conflicts between seprate projects.

In the root dir of your project create a local venv environment into which you will install the project's python package dependencies. 

`python -m venv venv`

For convenience, add the following to your `.bashrc` file:

`alias sa='source venv/bin/activate'`

Log out and back in or run on command line:
`alias sa='source venv/bin/activate'`

Now you can you the bash `sa` alias to activate the project `venv` environment.

`sa` should then add "(venv)" to your bash prompt.

## 6. Install PyAXBPS & Dependencies into Local Environment

Copy the requirements.txt file from this repo into the root folder of your project. 

When adding additional dependencies to requirements.txt you may need to pin each to a specific older version that is compatible with Python 3.8 and the older `numpy`. 

Install the dependencies with `pip` as follows from the root folder of your project:

`pip install -r requirements.txt`

You can now reference the `PyAXBPS` package and modules in your python code.
