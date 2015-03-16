The `install.sh` file for each framework starts the bash process which will 
install that framework. Typically, the first thing done is to call `fw_depends` 
to run installations for any necessary software that TFB has already 
created installation scripts for. TFB provides a reasonably wide range of 
core software, so your `install.sh` may only need to call `fw_depends` and 
exit. Note: `fw_depends` does not guarantee dependency installation, so 
list software in the proper order e.g. if `foo` depends on `bar`
use `fw_depends bar foo`.

Here are some example `install.sh` files

```bash
#!/bin/bash

# My framework only needs nodejs
fw_depends nodejs
```

```bash
#!/bin/bash

# My framework needs nodejs and mono and go
fw_depends nodejs mono go
```

```bash
#!/bin/bash

# My framework needs nodejs
fw_depends nodejs

# ...and some other software that there is no installer script for.
# Note: Use IROOT variable to put software in the right folder. 
#       You can also use FWROOT to refer to the project root, or 
#       TROOT to refer to the root of your framework
# Please see guidelines on writing installation scripts
wget mystuff.tar.gz -O mystuff.tar.gz
untar mystuff.tar.gz
cd mystuff
make --prefix=$IROOT && sudo make install
```

To see what TFB provides installations for, look in `toolset/setup/linux`
in the folders `frameworks`, `languages`, `systools`, and `webservers`. 
You should pass the filename, without the ".sh" extension, to fw_depends. 
Here is a listing as of July 2014: 

```bash
$ ls frameworks                                                                
grails.sh  nawak.sh  play1.sh  siena.sh     vertx.sh  yesod.sh
jester.sh  onion.sh  play2.sh  treefrog.sh  wt.sh
$ ls languages
composer.sh  erlang.sh   hhvm.sh   mono.sh    perl.sh     pypy.sh     racket.sh   urweb.sh
dart.sh      go.sh       java.sh   nimrod.sh  python2.sh  ringojs.sh  xsp.sh
elixir.sh    haskell.sh  jruby.sh  nodejs.sh  php.sh      python3.sh  ruby.sh 
$ ls systools
leiningen.sh  maven.sh
$ ls webservers
lapis.sh  mongrel2.sh  nginx.sh  openresty.sh  resin.sh  weber.sh  zeromq.sh
```
