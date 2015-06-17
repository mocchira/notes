## Benchmark LeoFS v1.2.2 with Watchdog

### Environment

* OS: CentOS release 6.5 (Final)
* Erlang/OTP: 17.4
* LeoFS: v1.2.2
* LeoFS cluster settings:

```
 [System Confiuration]
---------------------------------+----------
 Item                            | Value    
---------------------------------+----------
 Basic/Consistency level
---------------------------------+----------
                  system version | 1.2.2
                      cluster Id | leofs_1
                           DC Id | dc_1
                  Total replicas | 3
        number of successes of R | 1
        number of successes of W | 2
        number of successes of D | 2
 number of DC-awareness replicas | 0
                       ring size | 2^128
---------------------------------+----------
 Multi DC replication settings
---------------------------------+----------
      max number of joinable DCs | 2
         number of replicas a DC | 1
---------------------------------+----------
 Manager RING hash
---------------------------------+----------
               current ring-hash | 74fb0b34
              previous ring-hash | 74fb0b34
---------------------------------+----------

 [State of Node(s)]
-------+-----------------------------+--------------+----------------+----------------+----------------------------
 type  |            node             |    state     |  current ring  |   prev ring    |          updated at         
-------+-----------------------------+--------------+----------------+----------------+----------------------------
  S    | leofs14@192.168.100.14      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:01 +0900
  S    | leofs15@192.168.100.15      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:01 +0900
  S    | leofs16@192.168.100.16      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:01 +0900
  S    | leofs17@192.168.100.17      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:01 +0900
  S    | leofs18@192.168.100.18      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:01 +0900
  G    | leofs13@192.168.100.13      | running      | 74fb0b34       | 74fb0b34       | 2015-01-09 09:44:06 +0900
-------+-----------------------------+--------------+----------------+----------------+----------------------------

```

* basho-bench Configuration:
    * Duration: 154 minutes
    * # of concurrent processes: 64
    * # of keys: 100000
    * Value size groups(byte):
        *   1024..  10240: 24%
        *  10241.. 102400: 30%
        * 102401.. 819200: 30%
        * 819201..1572864: 16%
    * basho_bench driver: [basho_bench_driver_leofs.erl](https://github.com/leo-project/leofs/blob/develop/test/src/basho_bench_driver_leofs.erl)
    * Configuration file: [1m_r8w2_9999min.conf](20150109_094917/1m_r8w2_9999min.conf)

### OPS and Latency:

![ops-latency](20150109_094917/summary.png)

### Network Traffic
#### Chart of Each Nodes

* Gateway-1
![Gateway-1](leofs13_20150109_094916/sar_1_20150109_094916_p1p1-if1.png)

* Storage-1
![Storage-1](leofs14_20150109_094916/sar_3_20150109_094916_p1p1-if1.png)

* Storage-2
![Storage-2](leofs15_20150109_094916/sar_3_20150109_094916_p1p1-if1.png)

* Storage-3
![Storage-3](leofs16_20150109_094916/sar_3_20150109_094916_p1p1-if1.png)

* Storage-4
![Storage-4](leofs17_20150109_094916/sar_3_20150109_094916_p1p1-if1.png)

* Storage-5
![Storage-5](leofs18_20150109_094916/sar_2_20150109_094916_p1p1-if1.png)


### Disk
#### Chart of Each Nodes (Storage)

* Storage-1
![Storage-1](leofs14_20150109_094916/sar_3_20150109_094916_dev8-16-t1.png)
![Storage-1](leofs14_20150109_094916/sar_3_20150109_094916_dev8-16-t2.png)

* Storage-2
![Storage-2](leofs15_20150109_094916/sar_3_20150109_094916_dev8-16-t1.png)
![Storage-2](leofs15_20150109_094916/sar_3_20150109_094916_dev8-16-t2.png)

* Storage-3
![Storage-3](leofs16_20150109_094916/sar_3_20150109_094916_dev8-16-t1.png)
![Storage-3](leofs16_20150109_094916/sar_3_20150109_094916_dev8-16-t2.png)

* Storage-4
![Storage-4](leofs17_20150109_094916/sar_3_20150109_094916_dev8-16-t1.png)
![Storage-4](leofs17_20150109_094916/sar_3_20150109_094916_dev8-16-t2.png)

* Storage-5
![Storage-5](leofs18_20150109_094916/sar_2_20150109_094916_dev8-16-t1.png)
![Storage-5](leofs18_20150109_094916/sar_2_20150109_094916_dev8-16-t2.png)

