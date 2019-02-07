# Making Jupyter work with your virtual environment

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

## Step 2 - Creating your a folder in Jupyter's configuration directory for your kernel:

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
What we are interested in here is the first path under `data:` specifically `/home/username/.local/share/jupyter` a thiss is where Jupyter will look for kernels,

Make the folder for your kernel:
```
$ mkdir /home/username/.local/share/jupyter/kernels/venv
```
If you enter the kernels folder you can see your new kernel folder:
```
$ cd /home/username/.local/share/jupyter/kernels
$ ls
python2 python3 venv
```

## Step 3 - Making your virtual environment kernel available in Jupyter 

Inside the folder for each kernel inside the `kernels` folder, you will notice a file called kernel.json

*Note: If at this point you are unaware what JSON is, don't worry, you can just copy in below and leave it at that.*

The `kernel.json` file specifies the information that Jupyter needs to start up your custom kernel. If you would like to know more about how the kernel.json folder works, read this helpful guide from the [Jupyter documentation](https://jupyter-client.readthedocs.io/en/stable/kernels.html).


Navigate now into the folder for your virtual environment kernel, create a `kernel.json` file, and open it for editing
```
$ cd venv
$ touch kernel.json
$ nano kernel.json
```
Then enter the following:
For you will need the location of your python installation in your virtual environment, which we noted down at the end of step 1, enter it as the first item in the "argv" tree.
```
{
 "argv": [
  "/home/username/.../venv/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "venv",
 "language": "python"
}
```
Save and exit the file.
Navigate back to your home directory using `cd` and launch Jupyter regularly using `jupyter notebook`.

Create a new notebook and click on the kernel selector in the top right hand corner, you should now see a kernel named after whatever you chose to name the kernel in the `kernel.json` file.

If everything is working fine, the kernel will be ready to go!

Common errors include not have the structure of the JSON file correct (missing brackets, double quotes, e.t.c.). Another issue is that the ipykernel you installed isnt the right one for the version of Python you are using. Make sure to use the `pip3` command in your virtual environment.

## An arguably easier method of using Jupyter with your virtual environment...

You could install jupyter directly in your virtual environment and each virtual environment you create. Therefore running `jupyter notebook` from the virtual environment will create an instance of jupyter using the python installation for that specific virtual environment. 

Personally, I like the flexibility of being able to switch between different virtual environments from one place. It's up to you.

Thanks for reading!



