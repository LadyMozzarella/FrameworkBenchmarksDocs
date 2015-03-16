### How do I run the benchmark myself? 

If you plan to run the benchmark and compare results, you need to run in *benchmark* 
mode. We recommend having a minimum of three distinct computers with a fast network 
connection in between, all of which you should be comfortable installing a large amount
of additional software on. One of these computers (the `app server`) must have passwordless
SSH access to the other two ([search Google for help](https://www.google.com/#hl=en&q=passwordless%20SSH%20access), yielding references such as these: [article 1](http://hortonworks.com/kb/generating-ssh-keys-for-passwordless-login/) [article 2](http://superuser.com/questions/336226/how-to-ssh-to-localhost-without-password) [article 3](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)), and on every computer 
you will need to have passwordless sudo access ([Google for help](https://www.google.com/#hl=en&q=passwordless%20sudo)).
Once you have cloned our repository, run `toolset/run-tests.py --help` for detailed help
on running in *benchmark* mode. 

If you wish to benchmark on Amazon EC2, see [our scripts](deployment/vagrant-production) for 
launching a benchmark-ready Amazon environment. 

If you are not an expert, please ensure your setup can run in *verify* mode before 
attempting to run in *benchmark* mode. 
