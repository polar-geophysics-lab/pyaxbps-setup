# Setting up PyAXBPS

## Set up Python Environment
PyAXBPS is fairly old and no longer appears to be maintained. Installing it requires Python 3.8 (3.7 may work also).

Since these are older versions of python they are generally not available on current systems without installing in addition to the Python versions native to the system.

Pyenv is used to install a specific version of python and them the python `venv` module is used to create an isolated python environment for a PyAXBPS project.

### 1. Install pyenv (if you haven't already)
**This has been done on JKB.**

Linux: `curl https://pyenv.run | bash`

### 2. Set up User environment (assumes Bash)
Add to .bashrc:

`export PYENV_ROOT="$HOME/.pyenv"`
`[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"`
`eval "$(pyenv init - bash)"`

### 3. Install Pythin Build dependencies

`sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev`

### 4. Install/Build desired python version 

Log out and back in or `source ~/.bashrc`

We want to use Python v3.8.20:

`pyenv install 3.8.20`

Set the default environment in the project directory root:

### 5. Set Default Pyenv Python Version

Do this in the root directory of your project:

`pyenv local 3.8.20`

This creates the file `.python-version` in the project directory.

### 6. Create isolated python/pip environment with venv

In the root dir of your project create a local venv environment into which you will install the project's python package dependencies. 

`python -m venv venv`

For convenience, add the following to your `.bashrc` file:

`alias sa='source venv/bin/activate'`

and run on command line:
`alias sa='source venv/bin/activate'`

By using the `venv` module you can have separate projects all using the Pyenv python v3.8.20 while keeping the specific python dependencies (typically installed with `pip`) completely isolated. This avoids version and dependency conflicts between seprate projects.

