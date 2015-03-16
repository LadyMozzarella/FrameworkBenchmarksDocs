The simplest way to begin development is to set up [vagrant](https://www.vagrantup.com/). 

Here's a short example: 
    
```bash
# Clone the project, then move into the right directory 
$ cd ~/FrameworkBenchmarks/deployment/vagrant-development
# Turn on the VM. Takes at least 20 minutes
$ vagrant up
# Enter the VM, then run a test
$ vagrant ssh
vagrant@TFB-all:~$ cd ~/FrameworkBenchmarks
vagrant@TFB-all:~/FrameworkBenchmarks$ toolset/run-tests.py --install server --mode verify --test beego
```