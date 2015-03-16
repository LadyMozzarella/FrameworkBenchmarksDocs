#Test type 6

The __Plaintext__ test is an exercise of the request-routing fundamentals only, designed to demonstrate the capacity of high-performance platforms in particular. Requests will be sent using HTTP pipelining. The response payload is still small, meaning good performance is still necessary in order to saturate the gigabit Ethernet of the test environment.

##Requirements

In addition to the requirements listed below, please note the [general requirements](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests#general-requirements) (listed on the [Framework Tests](https://github.com/LadyMozzarella/FrameworkBenchmarks/wiki/Framework-Tests) page) that apply to all implemented tests.

1. The recommended URI is __/plaintext__.
2. The response content type must be set to `text/plain`.
3. The response body must be `Hello, World!`.
4. This test is not intended to exercise the allocation of memory or instantiation of objects. Therefore it is acceptable but not required to re-use a single buffer for the response text (`Hello, World`). However, the response must be fully composed from this and its headers within the scope of each request and it is not acceptable to store the entire payload of the response, headers inclusive, as a pre-rendered buffer.
5. The response headers must include either `Content-Length` or `Transfer-Encoding`.
6. The response headers must include `Server` and `Date`.
7. gzip compression is not permitted.
8. Server support for HTTP Keep-Alive is strongly encouraged but not required.
9. Server support for HTTP/1.1 pipelining [is assumed](http://www-archive.mozilla.org/projects/netlib/http/pipelining-faq.html). Servers that do not support pipelining may be included but should downgrade gracefully. If you are unsure about your server's behavior with pipelining, test with the [wrk](https://github.com/wg/wrk) load generation tool used in our tests.
10. If HTTP Keep-Alive is enabled, no maximum Keep-Alive timeout is specified by this test.
11. The request handler will be exercised at 256, 1024, 4096, and 16,384 concurrency.
12. The request handler will be exercised using GET requests.

##Example request

```bash
GET /plaintext HTTP/1.1
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
Content-Length: 15
Content-Type: text/plain; charset=UTF-8
Server: Example
Date: Wed, 17 Apr 2013 12:00:00 GMT

Hello, World!
```