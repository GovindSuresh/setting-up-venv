# Why use virtual environments

Virtual Environments are an effective way of managing the varying dependencies projects you are working on may have. Rather than installing all the latest versions of various libraries directly into your main python directory; installing using virtual environments will help you to keep each project 'clean'. Most importantly you will not run into issues whereby you have installed a new version of a certain library and your older projects will no longer work properly. This can easily occur when using languages such as Python, where a number of older projects may be written in Python 2.7. 

This guide is written  for Python 3. If you haven't yet installed Python please see install from (INSERT PYTHON LINK)

## Step 1: Installing  pip

To install the required libraries, we will use the python installer pip. You can check you have this by typing:

``` $ pip3 --version ```

*note: As I am using Ubuntu which came with python 2.7 installed, I generally have to add a 3 to end of calls such as python 3 and pip3 to ensure I run the python 3 version*

You should see something like this:
``` $pip3 --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
```

## Step 2: Installing virtualenv:

Virtualenv is used to create isolated python environments. In other words, you create a seperate instance of python which exists standalone from python installed in your main directory. This allows you to install packages only for that specific environment .

To install virtualenv using pip:

``` $ pip3 install virtualenv ```

You can then test this using:

``` $ virtualenv --version ```

You should see output such as:

``` 16.3.0 ```

### Step 2.1 Creating a virtual environment:

First, navigate to where you would like to create the virtual environment. This will likely be the folder in which you plan on keeping all related project documents 

``` 
$ cd coding_projects\myproject
$ virtualenv venv
```

This will create a Python virtual environment in whichever directory you ran the command and place it in a folder named whatever you named your virtual environment, in our case this was `venv`

To use your virtual environment you must activate it using the following:

```
$ source venv/bin/activate
```

What you will see now is that the name of your virtual environment will appear on the left hand side of the prompt

```
(venv) test&test:~ path/to/directory$ 
```
You're now running inside your virtual environment. Anything installed in here will only be installed to this virtual environment.

You can exit the virtual environment by typing:

```
$ deavtivate
```
You will notice that the (venv) on the left hand side has gone.

Lets now take a step back and look into the directory that contains your virtual environment. For ease of use I recommend just using the file browser here.

As mentioned before, if you navigate to where you created the virtual environment you will notice a new folder named after your virtual environment. If you open it up, you will see various folders containing the files for whatever package you install in this virtual environment. It also contains the files used to make the virtual environment run. If you look in the **bin** folder you will see a file called **activate** which is what we navigate to when activating the virtual environment.

(insert pic showing venv files)

### 2.2 Installing into your virtual environment  

Installing packages into your virtual environment is very similar to installing packages regularly. First we need to activate our virtual environment:

``` $ venv\bin\activate
```
Then install whatever package you want using pip. We are going to install the great numpy package

``` $ pip install numpy
```
*NOTE: As my virtual environment was installed only using Python 3, I no longer need to call pip3. Using pip3 will work however*

Doing this will install the numpy package into your virtual environment's folder. If you now run any Python script from within your virtual environment which imports numpy it will execute correctly. To check this you can deactivate your virtual environment and then attempt to run the same script.  

## Conclusion

Congrats! You have now successfully created your own virtual environment and intalled packages directly into it. You can now begin creating seperate environments for new projects to ensure that you do not break dependencies. There are numerous different commands for virtual environments for which I recommend that you read the [virtualenv](https://pypi.org/project/virtualenv/) documentation. There are also a number of other packages such as [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/index.html) which can be used to streamline your virtual env use.
