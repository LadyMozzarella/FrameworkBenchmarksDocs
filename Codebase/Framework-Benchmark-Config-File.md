The `benchmark_config` file is used by our scripts to identify available tests - it should exist at the root of the framework directory.

Here is an example `benchmark_config` from the `Compojure` framework. There are two different tests listed for the `Compojure` framework.

    {
      "framework": "compojure",
      "tests": [{
        "default": {
          "setup_file": "setup",
          "json_url": "/compojure/json",
          "db_url": "/compojure/db/1",
          "query_url": "/compojure/db/",
          "fortune_url": "/compojure/fortune-hiccup",
          "plaintext_url": "/compojure/plaintext",
          "port": 8080,
          "approach": "Realistic",
          "classification": "Micro",
          "database": "MySQL",
          "framework": "compojure",
          "language": "Clojure",
          "orm": "Micro",
          "platform": "Servlet",
          "webserver": "Resin",
          "os": "Linux",
          "database_os": "Linux",
          "display_name": "compojure",
          "notes": "",
          "versus": "servlet"
        },
        "raw": {
          "setup_file": "setup",
          "db_url": "/compojure/dbraw/1",
          "query_url": "/compojure/dbraw/",
          "port": 8080,
          "approach": "Realistic",
          "classification": "Micro",
          "database": "MySQL",
          "framework": "compojure",
          "language": "Clojure",
          "orm": "Raw",
          "platform": "Servlet",
          "webserver": "Resin",
          "os": "Linux",
          "database_os": "Linux",
          "display_name": "compojure-raw",
          "notes": "",
          "versus": "servlet"
        }
      }]
    }

* `framework:` Specifies the framework name.
* `tests:` A list of tests that can be run for this framework. In many cases, this contains a single element for the "default" test, but additional tests can be specified.  Each test name must be unique when concatenated with the framework name. Each test will be run separately in our Rounds, so it is to your benefit to provide multiple variations in case one works better in some cases.
  * `setup_file:` The location of the [python setup file](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Setup-File) that can start and stop the test, excluding the `.py` ending. If your different tests require different setup approachs, use another setup file. 
  * `json_url (optional):` The URI to the JSON test, typically `/json`
  * `db_url (optional):` The URI to the database test, typically `/db`
  * `query_url (optional):` The URI to the variable query test. The URI must be set up so that an integer can be applied to the end of the URI to specify the number of queries to run.  For example, `/query?queries=`(to yield `/query?queries=20`) or `/query/` (to yield `/query/20`)
  * `fortune_url (optional):` the URI to the fortunes test, typically `/fortune`
  * `update_url (optional):` the URI to the updates test, setup in a manner similar to `query_url` described above.
  * `plaintext_url (optional):` the URI of the plaintext test, typically `/plaintext`
  * `port:` The port the server is listening on
  * `approach (metadata):` `Realistic` or `Stripped` (see [here](http://www.techempower.com/benchmarks/#section=code&hw=peak&test=json) for a description of all metadata attributes)
  * `classification (metadata):` `Full`, `Micro`, or `Platform`
  * `database (metadata):` `MySQL`, `Postgres`, `MongoDB`, `SQLServer`, or `None`
  * `framework (metadata):` name of the framework
  * `language (metadata):` name of the language
  * `orm (metadata):` `Full`, `Micro`, or `Raw`
  * `platform (metadata):` name of the platform
  * `webserver (metadata):` name of the web-server (also referred to as the "front-end server")
  * `os (metadata):` The application server's operating system, `Linux` or `Windows`
  * `database_os (metadata):` The database server's operating system, `Linux` or `Windows`
  * `display_name (metadata):` How to render this test permutation's name on the results web site.  Some permutation names can be really long, so the display_name is provided in order to provide something more succinct.
  * `versus (optional):` The name of another test (elsewhere in this project) that is a subset of this framework.  This allows for the generation of the framework efficiency chart in the results web site. For example, Compojure is compared to "servlet" since Compojure is built on the Servlets platform.

The [requirements section](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests#requirements) explains the expected response for each URL as well all metadata options available. 
