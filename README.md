# Performance Testing Project with JMeter

This repository contains the results of load tests carried out on an application using [Apache JMeter](https://jmeter.apache.org/). Each test was configured with different numbers of threads (100, 500, 1000, 2000, 2999, 3969), and the results are presented in aggregate graphs, latency graphs, and CSV files summarizing the metrics. The application used for the HTTP requests is [NextJS Login App](https://next-login-mocha.vercel.app).

## Test Description

The load tests were carried out to measure the application's performance at different stress levels, simulating multiple simultaneous users. Below is an overview of the results based on each number of threads.

| Threads | Average (ms) | Min. (ms) | Max. (ms) | Standard Deviation | % Error | Throughput (req/s) | KB per s | Sent KB/s  | Average Bytes |
|---------|--------------|-----------|-----------|--------------------|---------|--------------------|----------|------------|----------------|
| 100     | 3176         | 1586      | 5997      | 878.49             | 0.000%  | 15.71              | 107.72   | 4.05       | 7021.9         |
| 500     | 7888         | 2281      | 20703     | 2450.74            | 0.000%  | 23.72              | 162.67   | 6.12       | 7021.9         |
| 1000    | 6448         | 1190      | 36805     | 4039.88            | 0.000%  | 26.78              | 183.67   | 6.91       | 7021.9         |
| 2000    | 23858        | 1033      | 64463     | 12797.92           | 23.600% | 30.19              | 183.32   | 6.86       | 6219.0         |
| 2999    | 38732        | 2090      | 68345     | 17109.98           | 76.559  | 43.85              | 187.33   | 6.68       | 4374.3         |
| 3969    | 45890        | 5132      | 92566     | 5340.19            | 95.742% | 42.81              | 151.96   | 4.90       | 3635.1         |

### Graphs & Charts

#### Aggregated Graphs

The aggregate graphs show the average, minimum, maximum and standard deviation response times for each load test. These values help to identify performance variations and possible bottlenecks. 

#### Latency Graphs

The average response latency was also measured for each set of threads. These graphs visualize the time taken for requests to return to the client.

### CSV summaries

Each test generated a CSV file containing a detailed summary of the requests, such as response time, number of successful requests, failures, etc. These files can be downloaded and analyzed directly, just like their respective Charts.

## Performance Analysis

### Error Analysis

As the number of threads increases, we notice a significant increase in the percentage of errors:

- Up to 1000 threads, the system was able to handle the load without errors.
- From **2000 threads**, we observed **23.6% error**, which may indicate server saturation.
- At **2999 threads**, the error increased dramatically to **76.56%**, suggesting that the server is failing to cope with the volume of requests.
- In the test with **3969 threads**, the error reached **95.74%**, showing that the system practically collapsed under this load.
- In previous tests, the **100%** error seems to indicate a possible blocking of the application due to a suspected attack.

### Performance Analysis

1. **Average Response Time**: There is a significant increase in the average response time as the number of threads increases, going from **3,176 ms** to **45,890 ms** in the test carried out with 3969 threads, which indicates that the server faces difficulties in dealing with a high volume of simultaneous requests.

2. **Standard Deviation**: The standard deviation also shows a marked increase as the number of threads increases. For 3969 threads, the standard deviation was **5340 ms**, showing a substantial variation in response times.

3. **Throughput**: Interestingly, the throughput (requests per second) increased as the number of threads increased until it reached **2999 threads**, reaching **43.85 req/s**. However, there was a slight decrease to **42.81 req/s** in the test with **3969 threads**, which suggests that the server is beginning to show shortcomings in the efficiency of processing requests.

### Conclusions

The application evaluated performs satisfactorily with up to **1000 threads**, without registering any faults. However, when increasing to **2000 threads**, there is an increase in the number of errors, which reaches a maximum of **95.74%** of failures with **3969 threads**, indicating that the server's processing capacity has been exceeded. The increase in **latency** and **response time** reveals that the application is not adequately sized to deal with this high load.

These findings indicate that the application may need improvements, such as implementing load balancing, expanding server resources or adopting caching techniques in order to optimize its performance in situations of high simultaneous traffic.
