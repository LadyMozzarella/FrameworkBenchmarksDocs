The setup file is responsible for starting and stopping the test. This script is responsible for (among other things):

* Modifying the framework's configuration to point to the correct database host
* Compiling and/or packaging the code (if impossible to do in `install.sh`)
* Starting the server
* Stopping the server

The setup file is a python script that contains a start() and a stop() function.  
The start function should build the source, make any necessary changes to the framework's 
configuration, and then start the server. The stop function should shutdown the server, 
including all sub-processes as applicable.

#### Configuring database connectivity in start()

By convention, the configuration files used by a framework should specify the database 
server as `localhost` so that developing tests in a single-machine environment can be 
done in an ad hoc fashion, without using the benchmark scripts.

When running a benchmark script, the script needs to modify each framework's configuration
so that the framework connects to a database host provided as a command line argument. 
In order to do this, use `setup_util.replace_text()` to make modifications prior to 
starting the server.

For example:

```python
setup_util.replace_text("wicket/src/main/webapp/WEB-INF/resin-web.xml", "mysql:\/\/.*:3306", "mysql://" + args.database_host + ":3306")
```

Note: `args` contains a number of useful items, such as `troot`, `iroot`, `fwroot` (comparable
to their bash counterparts in `install.sh`, `database_host`, `client_host`, and many others)

Note: Using `localhost` in the raw configuration file is not a requirement as long as the
`replace_text` call properly injects the database host provided to the benchmark 
toolset as a command line argument.

#### A full example

Here is an example of Wicket's setup file.

```python
import subprocess
import sys
import setup_util

##################################################
# start(args, logfile, errfile)
#
# Starts the server for Wicket
# returns 0 if everything completes, 1 otherwise
##################################################
def start(args, logfile, errfile):

# setting the database url
setup_util.replace_text(args.troot + "/src/main/webapp/WEB-INF/resin-web.xml", "mysql:\/\/.*:3306", "mysql://" + args.database_host + ":3306")

# 1. Compile and package
# 2. Clean out possible old tests
# 3. Copy package to Resin's webapp directory
# 4. Start resin
try:
  subprocess.check_call("mvn clean compile war:war", shell=True, cwd="wicket", stderr=errfile, stdout=logfile)
  subprocess.check_call("rm -rf $RESIN_HOME/webapps/*", shell=True, stderr=errfile, stdout=logfile)
  subprocess.check_call("cp $TROOT/target/hellowicket-1.0-SNAPSHOT.war $RESIN_HOME/webapps/wicket.war", shell=True, stderr=errfile, stdout=logfile)
  subprocess.check_call("$RESIN_HOME/bin/resinctl start", shell=True, stderr=errfile, stdout=logfile)
  return 0
except subprocess.CalledProcessError:
  return 1

##################################################
# stop(logfile, errfile)
#
# Stops the server for Wicket
# returns 0 if everything completes, 1 otherwise
##################################################
def stop(logfile):
try:
  subprocess.check_call("$RESIN_HOME/bin/resinctl shutdown", shell=True, stderr=errfile, stdout=logfile)
  return 0
except subprocess.CalledProcessError:
  return 1
```
