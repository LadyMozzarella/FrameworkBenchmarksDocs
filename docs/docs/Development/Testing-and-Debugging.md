## Listing Tests

You can easily list all available tests

```bash
$ toolset/run-tests.py --list-tests
activeweb
activeweb-raw
aspnet
aspnet-jsonnet
aspnet-mongodb-raw
aspnet-mono
aspnet-mono-jsonnet
aspnet-mono-mongodb-raw
<snip>
```

## Running Tests

There are a number of options that can be specified: 

```bash
# Run a verification for test beego
$ toolset/run-tests.py --test beego --mode verify

# Run the default benchmark for the beego test
$ toolset/run-tests.py --test beego

# Specify which test types are run during benchmark
$ toolset/run-tests.py --test beego --type json
$ toolset/run-tests.py --test beego --type db
$ toolset/run-tests.py --test beego --type fortune

# Specify a number of options for how the load is generated
$ toolset/run-tests.py --test beego --max-concurrency 24 --max-threads 24 --duration 20 --max-queries 200

# Run a tiny benchmark
$ toolset/run-tests.py --test beego --max-threads 2 --max-concurrency 2 
```

## Finding output logs

Logs file locations use the format `results/ec2/latest/logs/wt/err.txt`. 
The general structure is `results/<run name>/<timestamp>/logs/<test name>/<file>`
You can use the `--name` flag to change the `<run name>`
If you re-run the same test multiple times, you will get a different folder
for each `<timestamp>`, although the `latest` folder will be kept up to date. 
The `<test name>` is simply the name of the test type you ran, and `<file>` is either `out.txt`
or `err.txt` (these are the `logout` and `logerr` arguments passed into each 
`setup.py` file. 


Note: If you're looking for logs from our official benchmark rounds, see 
[Round 9](https://github.com/TechEmpower/TFB-Round-9) and 
[Round 8](https://github.com/TechEmpower/TFB-Round-8)