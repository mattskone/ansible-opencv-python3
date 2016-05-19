# ansible-opencv-python3
An Ansible playbook to install OpenCV and Python3 on Ubuntu Linux

### Motivation
As a graduate student in Georgia Tech's awesome [Online Master of Science in Computer Science (OMSCS) program](http://www.omscs.gatech.edu/), I recently completed CS 6476, Computer Vision.  The required software for the course was [Python 3.4+](https://www.python.org/) with [OpenCV 3.0+](http://opencv.org/), to which I added the desire to work on [Ubuntu 14.04](http://www.ubuntu.com/) using Python [virtual environments](https://virtualenv.pypa.io/en/latest/).  I found this to be pretty tricky to set up, but was fortunate enough to discover Adrian Rosebrock's [excellent blog post](http://www.pyimagesearch.com/2015/07/20/install-opencv-3-0-and-python-3-4-on-ubuntu/) explaining how to do it.

I wrote this [Ansible](https://www.ansible.com/) playbook in an effort to automate his steps in an easily repeatable way.

### Prerequisites
1. An installation of Ubuntu 14.04 Desktop edition (Server may also work)
2. Ansible 2.0 or higher.  See the [Ansible installation page](http://docs.ansible.com/ansible/intro_installation.html) for installation instructions.  It may be as simple as `$ sudo pip install ansible`.

### What do I do now?
1. Clone this repository to your Ubuntu machine.
2. Verify the contents of `group_vars/all` (discussed under Variables, below).
3. From the project root, run `$ ansible-playbook playbook.yml`.

### So, what will this playbook do?
This playbook contains all the steps from [Adrian's blog post](http://www.pyimagesearch.com/2015/07/20/install-opencv-3-0-and-python-3-4-on-ubuntu/) to:

1. Download OpenCV and its various dependencies.
2. Compile and install OpenCV.  (NOTE: OpenCV, and its dependency numpy, are install system-wide.  If you already have a system-wide installation of numpy, that's fine.)
3. Install Python virtualenv and virtualenvwrapper, create a virtual environment, and make OpenCV available in that virtual environment.

Some of the steps, especially cloning the OpenCV repository and compiling OpenCV, take quite a bit of time.  The whole playbook takes about 30 minutes to run on my 2-core Mac.

### Variables
Please verify the variables in the `group_vars/all` file have the values you want for your setup.  They are:

1. `download_dir` - this is the path to the directory where any downloaded files will be placed during installation.  If the directory doesn't exist, it will be created before use, and removed when the installation is complete.
2. `opencv_version` - this is the version of OpenCV that will be installed.  `3.1.0` is the current version.  This value can be a tag or a specific commit hash from the [OpenCV github project](https://github.com/Itseez/opencv).
3. `virtualenv_home` - this is the path to the directory where all of your virtual environments will be stored.
4. `virtualenv_name` - this is the name of the virtual environment that will be created for you, with OpenCV available in it.

### A note about virtual environments
Virtual environments are a Python best-practice technique for preventing dependency conflicts while developing multiple Python projects on the same machine.  If you're unfamiliar with them, [this guide](http://docs.python-guide.org/en/latest/dev/virtualenvs/) provides good coverage of the rationale and basic usage.

#### How do I use OpenCV in my new virtual environement?
Assuming the value of `virtualenv_home` is `cv`, just use

`$ workon cv`

to activate your virtual environment.  OpenCV will be available to your Python code with  `import cv2`.  Any other Python packages you install using `pip` while your virtual environment is active will only be installed in your virtual environment, and not system-wide.

When you want to exit your virtual environment, just use

`$ deactivate`

#### What if I don't want to use virtual environments?
No problem - you don't have to.  Since OpenCV is installed system-wide, it is available in your Python code with `import cv2` whether or not you are inside an active virtual environment.

### Using Vagrant
If you have [Vagrant](https://www.vagrantup.com/) installed (or if you install it), you can optionally spin up a vagrant virtual machine and run this playbook inside it.  Just run

`$ vagrant up`

and vagrant will create and provision the virtual machine with OpenCV installed.

### Contributions
I'm pretty new at Ansible.  If there's a smarter way to do any of this, please send me a pull request with an explanation of your propsed change.  If something doesn't work, please create a github issue against this project including specific steps to reproduce the problem.

### License
Use of this software is governed by the included MIT license.
