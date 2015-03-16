#Test type 5
The __Database Updates__ test is a variation of [Test #3](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Multiple-Database-Queries.md) that exercises the ORM's persistence of objects and the database driver's performance at running `UPDATE` statements or similar. The spirit of this test is to exercise a variable number of read-then-write style database operations.

##Requirements

In addition to the requirements listed below, please note the [general requirements](/ProjectInformation/FrameworkTests/Framework-Tests.md#general-requirements) (listed on the [Framework Tests](/ProjectInformation/FrameworkTests/Framework-Tests.md) page) that apply to all implemented tests.

1. The recommended URI is __/updates__.
2. For every request, an integer `query` string parameter named queries must be retrieved from the request. The parameter specifies the number of rows to fetch and update in preparing the HTTP response (see below).
3. The `queries` parameter must be bounded to between 1 and 500. If the parameter is missing, is not an integer, or is an integer less than __1__, the value should be interpreted as 1; if greater than 500, the value should be interpreted as __500__.
4. The request handler must retrieve a set of __World__ objects, equal in count to the `queries` parameter, from the __World__ database table.
5. Each row must be selected randomly using one query in the same fashion as the single database query test (Test #2 above). As with the read-only multiple-query test type (#3 above), use of `IN` clauses or similar means to consolidate multiple queries into one operation is not permitted.
6. At least the `randomNumber` field must be read from the database result set.
7. Each __World__ object must have its `randomNumber` field updated to a new random integer between 1 and 10000.
8. Each __World__ object must be persisted to the database with its new `randomNumber` value.
9. Use of batch updates is acceptable but not required.
10. Use of transactions is acceptable but not required. If transactions are used, a transaction should only encapsulate a single iteration, composed of a single read and single write. Transactions should not be used to consolidate multiple iterations into a single operation.
11. For raw tests (that is, tests without an ORM), each updated row must receive a unique new `randomNumber` value. It is not acceptable to change the `randomNumber` value of all rows to the same random number using an `UPDATE ... WHERE id IN (...)` clause.
12. Each __World__ object must be added to a list or array.
13. The list or array must be serialized to JSON and sent as a response.
14. The response content type must be set to `application/json`.
15. The response headers must include either `Content-Length` or `Transfer-Encoding`.
16. The response headers must include `Server` and `Date`.
17. Use of an in-memory cache of __World__ objects or rows by the application is not permitted.
18. Use of prepared statements for SQL database tests (e.g., for MySQL) is encouraged but not required.
19. gzip compression is not permitted.
20. Server support for HTTP Keep-Alive is strongly encouraged but not required.
21. If HTTP Keep-Alive is enabled, no maximum Keep-Alive timeout is specified by this test.
22. The request handler will be exercised at 256 concurrency only.
23. The request handler will be exercised with query counts of 1, 5, 10, 15, and 20.
24. The request handler will be exercised using GET requests.

##Example request
```bash
GET /updates?queries=10 HTTP/1.1
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