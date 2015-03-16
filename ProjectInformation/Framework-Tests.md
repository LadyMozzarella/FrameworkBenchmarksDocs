We invite fans of frameworks and especially authors or maintainers of frameworks to join us in expanding the coverage of this project by implementing tests and contributing to the GitHub repository. The following are specifications for each of the test types we have included to-date in this project. Do not be alarmed; the specifications read quite verbose, but that's because they are specifications. The implementations tend to be quite easy in practice.

This project is evolving and we will periodically add new test types. As new test types are added, we encourage but do not require contributors of previous implementations to implement tests for the new test types. Wholly new test implementations are also encouraged to include all test types but are not required to do so. If you have limited time, we recommend you start with the easiest test types (1, 2, 3, and 6) and then continue beyond those as time permits.

#Requirements

##General Requirements
The following requirements apply to all test types below.

1. All test implementations __should be production-grade__. The particulars of this will vary by framework and platform, but the general sentiment is that the code and configuration should be suitable for a production deployment. The word should is used here because production-grade is our goal, but we don't want this to be a roadblock. If you're submitting a new test and uncertain whether your code is production-grade, submit it anyway and then solicit input from other subject-matter experts.

2. All test implementations __must disable all disk logging__. For many reasons, we expect all tests will run without writing logs to disk. Most importantly, the volume of requests is sufficiently high to fill up disks even with only a single line written to disk per request. Please disable all forms of disk logging. We recommend but do not require disabling console logging as well.

3. Specific characters and character case matter. Assume the client consuming your service's JSON responses will be using a case-sensitive language such as JavaScript. In other words, if a test specifies that a map's key is id, use id. Do not use Id or ID. This strictness is required not only because it's sensible but also because our automated validation checks are picky.

##Test Types & Specific Requirements

Each test type has their own requirements and specifications. Visit their pages for more details and complete requirements.

1. [__JSON Serialization__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/JSON-Serialization): Exercises the framework fundamentals including keep-alive support, request routing, request header parsing, object instantiation, JSON serialization, response header generation, and request count throughput.
2. [__Single Database Query__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Single-Database-Query): Exercises the framework's object-relational mapper (ORM), random number generator, database driver, and database connection pool.
3. [__Multiple Database Queries__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Multiple-Database-Queries): A variation of [Test #2](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Single-Database-Query) and also uses the __World__ table. Multiple rows are fetched to more dramatically punish the database driver and connection pool. At the highest queries-per-request tested (20), this test demonstrates all frameworks' convergence toward zero requests-per-second as database activity increases.
4. [__Fortunes__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Fortunes): Exercises the ORM, database connectivity, dynamic-size collections, sorting, server-side templates, XSS countermeasures, and character encoding.
5. [__Database Updates__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Database-Updates): A variation of [Test #3](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Multiple-Database-Queries) that exercises the ORM's persistence of objects and the database driver's performance at running `UPDATE` statements or similar. The spirit of this test is to exercise a variable number of read-then-write style database operations.
6. [__Plaintext__](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Plaintext): An exercise of the request-routing fundamentals only, designed to demonstrate the capacity of high-performance platforms in particular. Requests will be sent using HTTP pipelining. The response payload is still small, meaning good performance is still necessary in order to saturate the gigabit Ethernet of the test environment.