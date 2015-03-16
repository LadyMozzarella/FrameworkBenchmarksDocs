The __TechEmpower Framework Benchmarks__ is a project that provides representative performance measures across a wide field of web application frameworks. With much help from the community, coverage is quite broad and we are happy to broaden it further with contributions. The project presently includes frameworks on many languages including `Go`, `Python`, `Java`, `Ruby`, `PHP`, `C#`, `Clojure`, `Groovy`, `Dart`, `JavaScript`, `Erlang`, `Haskell`, `Scala`, `Perl`, `Lua`, `C`, and others.  The current tests exercise plaintext responses, JSON seralization, database reads and writes via the object-relational mapper (ORM), collections, sorting, server-side templates, and XSS counter-measures. Future tests will exercise other components and greater computation.

#Results
View the [latest results](https://www.techempower.com/benchmarks/), or check out the [previous rounds](https://www.techempower.com/benchmarks/#section=previous-rounds).

#Motivation
Choosing a web application framework involves evaluation of many factors. While comparatively easy to measure, performance is frequently given little consideration. We hope to help change that. Application performance can be directly mapped to hosting dollars, and for companies both large and small, hosting costs can be a pain point. Weak performance can also cause premature and costly scale pain, user experience degradation, and penalties levied by search engines.

What if building an application on one framework meant that at the very best your hardware is suitable for one tenth as much load as it would be had you chosen a different framework? The differences aren't always that extreme, but in some cases, they might be. Especially with several modern high-performance frameworks offering respectable developer efficiency, __it's worth knowing what you're getting into__.

#Making improvements
We expect that all frameworks' tests could be improved with community input. For that reason, we are extremely happy to receive [pull requests](https://github.com/TechEmpower/FrameworkBenchmarks/pulls) from fans of any framework. We would like our tests for every framework to perform optimally, so we invite you to please join in.

#What's to come
Feedback has been continuous and we plan to keep updating the project in several ways, such as:

* Coverage of more frameworks. Thanks to community contributions to-date, the number of frameworks covered has already grown quite large. We're happy to add more if you submit a pull request.
* [Additional test types](https://github.com/TechEmpower/FrameworkBenchmarks/issues/133).
* Enhancements to this site, such as better rendering of error information and sorting within the data tables and charts. We would also like to add side-by-side comparison of data sets (to visualize the changes between rounds or test types) and to accept additional results files from the community. How does EC2 compare to, say, Rackspace Cloud? We don't have the data now, but if you have a Rackspace Cloud account and are willing to run the full test suite, we'd like to be able to render that here.