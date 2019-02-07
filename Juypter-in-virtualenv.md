#Making Jupyter work with your virtual environment

Jupyter is a very useful tool for programming in Python and is commonly used in areas such as data science. You can read more about Jupyter [here](https://jupyter.org/).

In this walk-through I will go through how I got Jupyter to work with my virtual environment. This is something that can be replicated for any number of virtual environments that you create, allowing you to effortlessly switch between different virtual environments when using Jupyter. This guide assumes some familiarity with Jupyter and how it works. You will also need to have installed Jupyter which you can find [here](https://jupyter.org/install).

## Step 1 - Installing IPYkernel in your virtual environment
Jupyter works by running a kernel which processes your code and creates the output. It has different Kernels for Python 2 and Python 3, as well as others. You can easily select to switch between kernels to change to one which matches the language you have written your code in.

The first step here is to install the IPython kernel into your virtual environment. This is the Python backend for Jupyter.

First navigate to where your virtual environment is and then activate it:
```
$ source venv/bin/activate 
```
We then install the ipykernel using pip
```
$ python3 -m ipykernel install --user
```
Once this is done you can check that you have installed the kernel correctly by calling:
```
$ pip3 list
```
The command should then list all packages you have installed in this virtual environment, scroll through and you should see ipython

While still in your virtual environment, run the folliwng:
```
$ which python
```
You will recieve output which shows you the path to your python installation folder in your virtual environment similar to:
```
/home/username/path/to/venv/bin/python
```
Keep a note of this for later!
Deactivate your virtual environment using the deactivate command shown in the previous guide.

## Step 2 - Creating your new Jupyter Python kernel:

In this step we will need to insert a file into Jupyter's configuration files which points to your virtual environment.

First you need the location of your Jupyter configuration files:
```
$ jupyter --paths
```
Your output will look like this
```
config:
    /home/username/.jupyter
    /usr/etc/jupyter
    /usr/local/etc/jupyter
    /etc/jupyter
data:
    /home/username/.local/share/jupyter
    /usr/local/share/jupyter
    /usr/share/jupyter
runtime:
    /run/user/1000/jupyter
```
What we are interested in here is the first path under `data:` specifically `/home/username/.local/share/jupyter` 
    

