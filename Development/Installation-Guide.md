If you're looking to quickly get started developing using the vagrant development environment, consider the [vagrant development environment guide](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Vagrant-Development-Environment). 

Take a look at the [Summary of Script Directories section](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Summary-of-Script-Directories) to figure out which directory has scripts relevant to your use case (development or benchmarking).

#Installation Basics

In order for SSH to work appropriately, the user on **each machine** will need to be 
set up to have passwordless sudo access.

**Setting up the `user`**

```bash
sudo vim /etc/sudoers
```

You will need to change the line that reads `%sudo   ALL=(ALL:ALL) ALL` to 
`%sudo   ALL=(ALL:ALL) NOPASSWD: ALL`. You should be able to exit your shell, ssh 
back in and perform `sudo ls` without being prompted for a password.

**NOTE** Again, you will have to do this on every machine: server, database, client.

**Setting up SSH**

You will need to also be able to SSH onto each of the 3 machines from any of the
3 machines and not be prompted for a password. We use an identity file and authorized_keys
file to accomplish this.

```bash
ssh-keygen -t rsa
```

This will prompt you for various inputs; leave them all blank and just hit 'enter'.
Next, you will want to allow connections identified via that key signature, so add
it to your authorized keys.

```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

Next, you will need these exact same files to exist on the other 2 machines.
If you properly set up your user account on all 3 machines, then this will not prompt
you for a password (if it does, go back to "Setting up the `user`" and fix it).

```bash
# Export some variables so you can copy/paste the rest.
export TFB_SERVER_USER=[your server user]
export TFB_SERVER_HOST=[your server ip]
export TFB_DATABASE_USER=[your database user]
export TFB_DATABASE_HOST=[database ip]
export TFB_CLIENT_USER=[your client user]
export TFB_CLIENT_HOST=[client ip]
# Set up the database machine for SSH
cat ~/.ssh/id_rsa.pub | ssh $TFB_DATABASE_USER@$TFB_DATABASE_HOST 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
scp ~/.ssh/id_rsa $TFB_DATABASE_USER@$TFB_DATABASE_HOST:~/.ssh/id_rsa
scp ~/.ssh/id_rsa.pub $TFB_DATABASE_USER@$TFB_DATABASE_HOST:~/.ssh/id_rsa.pub
# Set up the client machine for SSH
cat ~/.ssh/id_rsa.pub | ssh $TFB_CLIENT_USER@$TFB_CLIENT_HOST 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
scp ~/.ssh/id_rsa $TFB_CLIENT_USER@$TFB_CLIENT_HOST:~/.ssh/id_rsa
scp ~/.ssh/id_rsa.pub $TFB_CLIENT_USER@$TFB_CLIENT_HOST:~/.ssh/id_rsa.pub
```

Now, test it all out, you should be able to execute all of the following without
being prompted for a password. **NOTE** The first time you SSH to these machines
(read: in this step) you will be prompted to accept the signature - do it.

```bash
# Test your database SSH setup
ssh $TFB_DATABASE_HOST
# Accept the signature
# You are connected to the database machine!
sudo ls
# This should NOT prompt for a password and list the directory's contents
# If this is not true, go back to "Setting up the `user`" and fix it
exit
# Test your client SSH setup
ssh $TFB_CLIENT_HOST
# Accept the signature
# You are connected to the client machine!
sudo ls
# We also need to test that we can SSH back to the server machine
ssh [enter your server ip again]
# Accept the signature
# You are connected to the server machine!
sudo ls
# If this works, you are golden!
exit
# Back on client
exit
# Back on initial ssh connection to server machine
```

Last, the benchmarks require that every framework test be run under a different
user than the one who executes the `run-tests.py` script. Creating a `runner_user` named "testrunner" is simple:

```bash
# Change this value to whatever username you want
export RUNNER=testrunner
# Get your primary user
export ME=$(id -u -n)
# Create the new testrunner user
sudo useradd $RUNNER
# Give him a home dir
sudo mkdir /home/$RUNNER
# Make testrunner the owner of his home dir
sudo chown $RUNNER:$RUNNER /home/$RUNNER
# Add the testrunner user to every group that the travis user is in
sudo sed -i 's|:'"$ME"'|:'"$ME"','"$RUNNER"'|g' /etc/group
# Add the testrunner user to the travis group specifically
sudo sed -i 's|'"$ME"':x:\(.*\):|'"$ME"':x:\1:'"$RUNNER"'|g' /etc/group
# Add the travis user to the testrunner group
sudo sed -i 's|'"$RUNNER"':x:\(.*\):|'"$RUNNER"':x:\1:'"$ME"'|g' /etc/group
# Add testrunner to the sudoers group
echo "$RUNNER ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers
# Set the default shell for testrunner to /bin/bash
sudo sed -i 's|/home/'"$RUNNER"':.*|/home/'"$RUNNER"':/bin/bash|g' /etc/passwd
```

**Setting up prerequisites**

The suite requires that a few libraries and applications are installed in order to run.
First, clone our repository.

```bash
git clone https://github.com/TechEmpower/FrameworkBenchmarks.git
cd FrameworkBenchmarks
source toolset/setup/linux/prerequisites.sh
sudo apt-get install -y python-pip
sudo pip install -r config/python_requirements.txt
```

To install TFB components onto the various servers, you must provide
basic login details for each server (e.g. usernames, IP addresses, 
private key files). While these details can all be passed 
using command line flags, it's easier to use a configuration 
file and avoid having huge flag lists in your commands. 

```bash
cp benchmark.cfg.example benchmark.cfg
vim benchmark.cfg
```

You will need to change, at a minimum, the following:

* `client_host` Set this to the IP address of your client machine
* `client_identity_file` Set to `/home/[username]/.ssh/id_rsa`
* `client_user` Set to your username
* `runner_user` Set to your runner's username
* `database_host` Set this to the IP address of your database machine
* `database_identity_file` Set to `/home/[username]/.ssh/id_rsa`
* `database_user` Set to your username
* `server_host` Set this to the IP address of your server machine

At this point, you should be ready to install the suite.

We use the `--install-only` flag in our examples to 
prevent launching tests at this stage. All of these commands 
should be run from the `app server` - it will SSH into other
hosts as needed. For more information on how TFB installation 
works, see [here](deployment). 

**Setting up the `load server`**

```bash
toolset/run-tests.py --install client --install-only
```

**Setting up the `database server`**

```bash
toolset/run-tests.py --install database --install-only
```

**Setting up the `app server`**

At this point, you should be able to run a benchmark of the entire
suite or selectively run individual benchmarks. Additionally, you
can test your setup by running a verification on one of the stable
frameworks. Since we wrote it, we tend to test with `gemini`:

```bash
toolset/run-tests.py --mode verify --test gemini
```

You can find the results for this verification step under the directory:
`results/ec2/latest/logs/gemini`. There should be an `err` and an `out`
file.

You can choose to selectively install components by using the 
`--test` and `--exclude` flags. 

```bash
# Install just the software for beego (as an example)
toolset/run-tests.py --install server --test beego --verbose --install-only

# Install all php software but php-fuel (as another example)
toolset/run-tests.py --install server --test php* --exclude php-fuel --verbose install-only

# Install *all* framework software. Expect this to take hours!
# If running on a remote server, use `screen` or `tmux` or `nohup` to 
# prevent the installation from being terminated if you are disconnected
$ toolset/run-tests.py --install server --verbose --install-only
```
