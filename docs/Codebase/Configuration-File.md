TFB takes a large number of command-line arguments, and it can become tedious to 
specify them repeatedly. We recommend you create a `benchmark.cfg` file by 
copying the example `benchmark.cfg.example` file and modifying as needed. 
See `toolset/run-tests.py --help` for a description of each flag. 

For running in *verify* mode, you can set the various hosts to `localhost`. 
For running in *benchmark* mode, you will need all of the servers' IP addresses.

*Note: environment variables can also be used for a number of the arguments.*
