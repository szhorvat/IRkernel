# Native R kernel for IPython

This is still experimental and unreliable. Your code should be safe,
since IPython handles saving and loading notebooks in another process, but
you'll lose all your variables if it crashes.

##Installing

You'll need zmq development headers to compile rzmq, as well curl headers for
R devtools. On a recent Ubuntu/Debian installation, you can get these
with:

```Shell
sudo apt-get install libzmq3-dev libcurl4-openssl-dev
```

or with homebrew:

```Shell
brew install zmq
# or upgrade
brew update
brew upgrade zmq
```

We need development versions of several packages from Github for now, due to
recent fixes. First, you need to make sure you have the `devtools` R package
available. If you don't, at the R console type:

```coffee
install.packages("devtools")
```

Then, you can install the necessary development dependencies with:

```coffee
library(devtools)
install_github("armstrtw/rzmq")
install_github("hadley/evaluate")
install_github("takluyver/IRdisplay")
install_github("takluyver/IRkernel")
```

You'll also need [IPython](http://ipython.org/). If you already have a Python
environment set up, install IPython using your preferred tools. If not,
installing [Anaconda](http://continuum.io/downloads) is the quickest way to get
everything you need.

# Running the notebook

```Shell
ipython notebook --KernelManager.kernel_cmd="['R', '-e', 'IRkernel::main(\'{connection_file}\')']"
```

You can also substitute 'qtconsole' or 'console' for 'notebook' in this command.
