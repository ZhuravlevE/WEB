```
Запуск инстансов: dotnet run --urls=http://localhost:5001/
```

###Доступ к апи сервера напрямую

```
zhyra@zhyra:~$ ab -c 10 -n 10000 http://localhost:5001/api/Ad
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 1000 requests
Completed 2000 requests
Completed 3000 requests
Completed 4000 requests
Completed 5000 requests
Completed 6000 requests
Completed 7000 requests
Completed 8000 requests
Completed 9000 requests
Completed 10000 requests
Finished 10000 requests


Server Software:
Server Hostname:        localhost
Server Port:            5001

Document Path:          /api/Ad
Document Length:        0 bytes

Concurrency Level:      10
Time taken for tests:   52.076 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      0 bytes
HTML transferred:       0 bytes
Requests per second:    192.03 [#/sec] (mean)
Time per request:       52.076 [ms] (mean)
Time per request:       5.208 [ms] (mean, across all concurrent requests)
Transfer rate:          0.00 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       5
Processing:     1    1   0.5      1      21
Waiting:        0    0   0.0      0       0
Total:          1    2   0.6      2      21

Percentage of the requests served within a certain time (ms)
  50%      2
  66%      2
  75%      2
  80%      2
  90%      2
  95%      3
  98%      3
  99%      3
 100%     21 (longest request)
```

###Доступ к апи сервера напрямую, когда развернуто на 3х портах

```
zhyra@zhyra:~$ ab -c 10 -n 10000 http://localhost:5002/api/Ad
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 1000 requests
Completed 2000 requests
Completed 3000 requests
Completed 4000 requests
Completed 5000 requests
Completed 6000 requests
Completed 7000 requests
Completed 8000 requests
Completed 9000 requests
Completed 10000 requests
Finished 10000 requests


Server Software:        Kestrel
Server Hostname:        localhost
Server Port:            5002

Document Path:          /api/Ad
Document Length:        260 bytes

Concurrency Level:      10
Time taken for tests:   7.757 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      3990000 bytes
HTML transferred:       2600000 bytes
Requests per second:    1289.18 [#/sec] (mean)
Time per request:       7.757 [ms] (mean)
Time per request:       0.776 [ms] (mean, across all concurrent requests)
Transfer rate:          502.33 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    3   5.9      2      77
Processing:     1    4   6.9      2     101
Waiting:        0    3   4.9      2      67
Total:          2    7   9.2      4     102

Percentage of the requests served within a certain time (ms)
  50%      4
  66%      5
  75%      5
  80%      6
  90%     14
  95%     26
  98%     42
  99%     50
 100%    102 (longest request)
```

###Без балансировки

```
zhyra@zhyra:~$ ab -c 10 -n 9000 http://localhost/api/v1/Ad
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 900 requests
Completed 1800 requests
Completed 2700 requests
Completed 3600 requests
Completed 4500 requests
Completed 5400 requests
Completed 6300 requests
Completed 7200 requests
Completed 8100 requests
Completed 9000 requests
Finished 9000 requests


Server Software:        myserver
Server Hostname:        localhost
Server Port:            80

Document Path:          /api/v1/Ad
Document Length:        166 bytes

Concurrency Level:      10
Time taken for tests:   8.065 seconds
Complete requests:      9000
Failed requests:        0
Non-2xx responses:      9000
Total transferred:      2826000 bytes
HTML transferred:       1494000 bytes
Requests per second:    1115.94 [#/sec] (mean)
Time per request:       8.961 [ms] (mean)
Time per request:       0.896 [ms] (mean, across all concurrent requests)
Transfer rate:          342.19 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    2   5.6      2     200
Processing:     3    7   6.6      6     328
Waiting:        2    7   4.2      6     135
Total:          3    9   8.6      8     329

Percentage of the requests served within a certain time (ms)
  50%      8
  66%      8
  75%      9
  80%      9
  90%     11
  95%     12
  98%     13
  99%     15
 100%    329 (longest request)
```

###С балансировкой

```
zhyra@zhyra:~$ ab -c 10 -n 9000 http://localhost/api/v1/Ad
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 900 requests
Completed 1800 requests
Completed 2700 requests
Completed 3600 requests
Completed 4500 requests
Completed 5400 requests
Completed 6300 requests
Completed 7200 requests
Completed 8100 requests
Completed 9000 requests
Finished 9000 requests


Server Software:        myserver
Server Hostname:        localhost
Server Port:            80

Document Path:          /api/v1/Ad
Document Length:        166 bytes

Concurrency Level:      10
Time taken for tests:   10.480 seconds
Complete requests:      9000
Failed requests:        0
Non-2xx responses:      9000
Total transferred:      2826000 bytes
HTML transferred:       1494000 bytes
Requests per second:    858.80 [#/sec] (mean)
Time per request:       11.644 [ms] (mean)
Time per request:       1.164 [ms] (mean, across all concurrent requests)
Transfer rate:          263.34 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    5   6.9      2      75
Processing:     1    6   8.1      3      76
Waiting:        0    5   7.5      2      75
Total:          2   11  10.7      5      78

Percentage of the requests served within a certain time (ms)
  50%      5
  66%     10
  75%     15
  80%     17
  90%     27
  95%     33
  98%     46
  99%     49
 100%     78 (longest request)
```
