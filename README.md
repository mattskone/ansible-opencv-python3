# ansible-opencv-python3
An Ansible playbook to install OpenCV and Python3 on Ubuntu Linux

### Motivation
As a graduate student in Georgia Tech's awesome [Online Master of Science in Computer Science (OMSCS) program](http://www.omscs.gatech.edu/), I recently completed CS 6476, Computer Vision.  The required software for the course was [Python 3.4+](https://www.python.org/) with [OpenCV 3.0+](http://opencv.org/), to which I added the desire to work on [Ubuntu 14.04](http://www.ubuntu.com/) using Python [virtual environments](https://virtualenv.pypa.io/en/latest/).  I found this to be pretty tricky to set up, but was fortunate enough to discover Adrian Rosebrock's [excellent blog post](http://www.pyimagesearch.com/2015/07/20/install-opencv-3-0-and-python-3-4-on-ubuntu/) explaining how to do it.

In an effort to automate his steps in an easily repeatable way, I wrote this [Ansible](https://www.ansible.com/) playbook.  If you have a standard installation of Ubuntu 14.04...
