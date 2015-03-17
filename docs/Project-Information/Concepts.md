##Servers

The full benchmark requires at least three computers:

* `app server`: The computer that your framework will be launched on.
* `load server`: The computer that will generate client load. Also known as the `client machine`.
* `database server`: The computer that runs all the databases. Also known as the `DB server`.

This codebase (`TechEmpower/FrameworkBenchmarks` aka `TFB`) must be run on 
the `app server`. The codebase contains a number of `framework directories`, each 
of which contains one or more `framework test implementations`. While our current setup has 
many directories, we are working to consolidate related code into fewer directories  
with more tests per directory. 

When run, `TFB` will: 
* select which framework tests are to be run based on command-line arguments you provide
* install the necessary software (both on the `app server` and other servers)
* launch the framework
* access the urls listed in [the requirements](http://www.techempower.com/benchmarks/#section=code) and verify the responses
* launch the load generation software on the `load server`
* gather the results
* halt the framework

