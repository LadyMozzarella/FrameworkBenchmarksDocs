When adding a new framework or new test to an existing framework, please follow these steps:

* Update/add a [benchmark_config](../Codebase/Framework-Benchmark-Config-File.md)
* Update/add a [setup file](../Codebase/Framework-Setup-File.md)
* Update/add an [install.sh file](../Codebase/Framework-Install-File.md)
* When creating a database test, use the table/collection `hello_world`. Our database setup scripts are stored inside the `config/` folder if you need to see the database schema

### Testing on both Windows and Linux

If your framework and platform can execute on both Windows and Linux, we encourage you to specify tests for both operating systems.  This increases the amount of testing you should do before submitting your pull-request, however, so we understand if you start with just one of the two. Travis-CI cannot automatically verify Windows-based tests, and therefore you should verify your code manually. 

The steps involved are:

* Assuming you have implemented the Linux test already, add a new test permutation to your `benchmark_config` file for the Windows test.  When the benchmark script runs on Linux, it skips tests where `os` in `Windows` and vice versa. 
* Add the necessary tweaks to your [setup file](../Codebase/Framework-Setup-File.md) to start and stop on the new operating system.  See, for example, [the script for Go](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/frameworks/Go/go/setup.sh).
* Test on Windows and Linux to make sure everything works as expected.