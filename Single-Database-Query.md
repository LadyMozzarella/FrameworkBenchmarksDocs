#Test Type 2
The __Single Database Query__ test exercises the framework's object-relational mapper (ORM), random number generator, database driver, and database connection pool.

##Requirements

In addition to the requirements listed below, please note the [general requirements](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests#general-requirements) (listed on the [Framework Tests](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests) page) that apply to all implemented tests.

1. For every request, a single row from a __World__ table must be retrieved from a database table.
2. The recommended URI is __/db__.
3. The schema for __World__ is __id__ (int, primary key) and __randomNumber__ (int), except for MongoDB, wherein the identity column is <strong>_id</strong>, with the leading underscore.
4. The __World__ table is known to contain 10,000 rows.
5. The row retrieved must be selected by its id using a random number generator (ids range from 1 to 10,000).
6. The row should be converted to an object using an object-relational mapping (ORM) tool. Tests that do not use an ORM will be classified as "raw" meaning they use the platform's raw database connectivity.
7. The object (or database row, if an ORM is not used) must be serialized to JSON.
8. The response content length should be approximately 32 bytes.
9. The response content type must be set to `application/json`.
10. The response headers must include either Content-Length or Transfer-Encoding.
11. The response headers must include `Server` and `Date`.
12. Use of an in-memory cache of __World__ objects or rows by the application is not permitted.
13. Use of prepared statements for SQL database tests (e.g., for MySQL) is encouraged but not required.
14. gzip compression is not permitted.
15. Server support for HTTP Keep-Alive is strongly encouraged but not required.
16. If HTTP Keep-Alive is enabled, no maximum Keep-Alive timeout is specified by this test.
17. The request handler will be exercised at concurrency levels ranging from 8 to 256.
18. The request handler will be exercised using GET requests.

##Example request
```bash
GET /db HTTP/1.1
Host: server
User-Agent: Mozilla/5.0 (X11; Linux x86_64) Gecko/20130501 Firefox/30.0 AppleWebKit/600.00 Chrome/30.0.0000.0 Trident/10.0 Safari/600.00
Cookie: uid=12345678901234567890; __utma=1.1234567890.1234567890.1234567890.1234567890.12; wd=2560x1600
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Connection: keep-alive
```

##Example response
```bash
HTTP/1.1 200 OK
Content-Length: 32
Content-Type: application/json; charset=UTF-8
Server: Example
Date: Wed, 17 Apr 2013 12:00:00 GMT

{"id":3217,"randomNumber":2149}
```