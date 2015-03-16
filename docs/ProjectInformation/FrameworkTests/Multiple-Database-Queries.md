#Test Type 3

The __Multiple Database Queries__ test is a variation of [Test #2](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Single-Database-Query) and also uses the __World__ table. Multiple rows are fetched to more dramatically punish the database driver and connection pool. At the highest queries-per-request tested (20), this test demonstrates all frameworks' convergence toward zero requests-per-second as database activity increases.

##Requirements

In addition to the requirements listed below, please note the [general requirements](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests#general-requirements) (listed on the [Framework Tests](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests) page) that apply to all implemented tests.

1. For every request, an integer `query` string parameter named queries must be retrieved from the request. The parameter specifies the number of database queries to execute in preparing the HTTP response (see below).
2. The recommended URI is __/queries__.
3. The `queries` parameter must be bounded to between 1 and 500. If the parameter is missing, is not an integer, or is an integer less than 1, the value should be interpreted as 1; if greater than 500, the value should be interpreted as __500__.
4. The request handler must retrieve a set of __World__ objects, equal in count to the `queries` parameter, from the __World__ database table.
5. Each row must be selected randomly in the same fashion as the single database query test (Test #2 above).
6. Since this test is designed to exercise multiple queries, each row must be selected individually by a query. It is not acceptable to retrieve all required rows using a `SELECT ... WHERE id IN (...`) clause.
7. Each __World__ object must be added to a list or array.
8. The list or array must be serialized to JSON and sent as a response.
9. The response content type must be set to `application/json`.
10. The response headers must include either `Content-Length` or `Transfer-Encoding`.
11. The response headers must include `Server` and `Date`.
12. Use of an in-memory cache of __World__ objects or rows by the application is not permitted.
13. Use of prepared statements for SQL database tests (e.g., for MySQL) is encouraged but not required.
14. gzip compression is not permitted.
15. Server support for HTTP Keep-Alive is strongly encouraged but not required.
16. If HTTP Keep-Alive is enabled, no maximum Keep-Alive timeout is specified by this test.
17. The request handler will be exercised at 256 concurrency only.
18. The request handler will be exercised with query counts of 1, 5, 10, 15, and 20.
19. The request handler will be exercised using GET requests.

##Example request
```bash
GET /queries?queries=10 HTTP/1.1
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
Content-Length: 315
Content-Type: application/json; charset=UTF-8
Server: Example
Date: Wed, 17 Apr 2013 12:00:00 GMT

[{"id":4174,"randomNumber":331},{"id":51,"randomNumber":6544},{"id":4462,"randomNumber":952},{"id":2221,"randomNumber":532},{"id":9276,"randomNumber":3097},{"id":3056,"randomNumber":7293},{"id":6964,"randomNumber":620},{"id":675,"randomNumber":6601},{"id":8414,"randomNumber":6569},{"id":2753,"randomNumber":4065}]
```