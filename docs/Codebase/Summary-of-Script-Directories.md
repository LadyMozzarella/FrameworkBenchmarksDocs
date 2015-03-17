Each script directory has a README, which will contain specific instructions related to seting up the relevant deployment/development environment.

| Directory Name | Summary |
| -------------- | :-------- |
[azure](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/azure)  | Scripts to help deploy onto Microsoft Azure
[common](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/common) | Common-use scripts that could be used in many environments
[vagrant-common](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/vagrant-common) | The core directory for vagrant-based setups. Currently only supports deplconfiguring Linux-based environments
[vagrant-aws](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/vagrant-aws) | Setup scripts for configuring Amazon such that you can use `vagrant-development` and `vagrant-production`. Also outlines Amazon-specific options, such as instance type, you can use with `vagrant-development` and `vagrant-production`
[vagrant-virtualbox](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/vagrant-virtualbox) | A readme defining all the Virtualbox-specific options you can use with `vagrant-development` and `vagrant-production`, such as amount of RAM per virtual machine
[vagrant-development](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/vagrant-development) | Sets up a development environment using a single Virtual Machine. Can use either Virtualbox (for a free, locally run virtual machine) or Amazon EC2 (for a `$1/day` remote virtual machine)
[vagrant-production](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/deployment/vagrant-production) | Sets up a 3-virtual machine environment in either Amazon or Virtualbox. If Amazon is used, this is intended to be an environment you could run an official `TechEmpower` round with. A 3-VM VirtualBox setup is mainly used to test-run in a free environment before launching into a paid environment
