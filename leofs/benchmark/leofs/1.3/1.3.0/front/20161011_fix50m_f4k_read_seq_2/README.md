## Benchmark LeoFS v1.3.0

### Purpose
We check Performance with LeoFS when files are put/get sequentially

### Issues
* https://github.com/leo-project/notes/issues/20

### Summary
- Put/Get 4000 50MB files in key order
- Throughput in loading is limited by single thread client
    - Stable around 200MB/s
- During reading phase, performance decreases over time, with occasional large drops
    - Start with 200MB/s, slowly decrease to 150MB/s
    - Large drops to 50MB/s
    - Similar pattern is observed when files are read in reverse order

### Next Action
- Close monitoring during read to find out the case of large drops
- Check possibilties to improve single thread performance

### Environment

* OS: Ubuntu Server 14.04.3
* Erlang/OTP: 17.5
* LeoFS: 1.3.0
* CPU: Intel Xeon E5-2630 v3 @ 2.40GHz
* HDD (node[36~50]) : 4x ST2000LM003 (2TB 5400rpm 32MB) RAID-0 are mounted at `/data/`, Ext4
* SSD (node[36~50]) : 1x Crucial CT500BX100SSD1 mounted at `/ssd/`, Ext4

```
 [System Confiuration]
-----------------------------------+----------
 Item                              | Value
-----------------------------------+----------
 Basic/Consistency level
-----------------------------------+----------
                    system version | 1.3.0
                        cluster Id | leofs_1
                             DC Id | dc_1
                    Total replicas | 3
          number of successes of R | 1
          number of successes of W | 2
          number of successes of D | 2
 number of rack-awareness replicas | 0
                         ring size | 2^128
-----------------------------------+----------
 Multi DC replication settings
-----------------------------------+----------
        max number of joinable DCs | 2
           number of replicas a DC | 1
-----------------------------------+----------
 Manager RING hash
-----------------------------------+----------
                 current ring-hash | 4adb34e4
                previous ring-hash | 4adb34e4
-----------------------------------+----------

 [State of Node(s)]
-------+------------------------+--------------+----------------+----------------+----------------------------
 type  |          node          |    state     |  current ring  |   prev ring    |          updated at
-------+------------------------+--------------+----------------+----------------+----------------------------
  S    | S1@192.168.100.37      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:38:50 +0900
  S    | S2@192.168.100.38      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:38:50 +0900
  S    | S3@192.168.100.39      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:38:50 +0900
  S    | S4@192.168.100.40      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:38:50 +0900
  S    | S5@192.168.100.41      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:38:49 +0900
  G    | G0@192.168.100.35      | running      | 4adb34e4       | 4adb34e4       | 2016-10-11 14:39:05 +0900
-------+------------------------+--------------+----------------+----------------+----------------------------

```

* basho-bench Configuration:
    * Duration: 30 minutes
    * # of concurrent processes: 1
    * # of keys: 4000 (sequential, reverse-sequential)
    * Value size groups(byte):
        * 52428800..52428800: 100%
    * basho_bench driver: [basho_bench_driver_leofs.erl](https://github.com/leo-project/basho_bench/blob/master/src/basho_bench_driver_leofs.erl)
    * Configuration file: 
        * [fix50m_f4k_load_seq.conf](load_seq/fix50m_f4k_load.conf)
        * [fix50m_f4k_read_seq.conf](read_seq/fix50m_f4k_read_seq.conf)
        * [fix50m_f4k_read_seq_rev.conf](read_seq/fix50m_f4k_read_seq_rev.conf)

* LeoFS Configuration:
    * Manager_0: [leo_manager_0.conf](conf/G0/leo_manager.conf)
    * Gateway  : [leo_gateway.conf](conf/G0/leo_gateway.conf)
        * Disk Cache: 0
        * Mem Cache:  0
    * Storage  : [leo_storage.conf](conf/S0/leo_storage.conf)
        * Container Path: /ssd/avs

### Results:
* Loading
    ![ops-latency](load_seq/summary.png)
    ![monitoring-results](grafana_load_seq.png)

* Reading
    ![ops-latency](read_seq/summary.png)
    ![monitoring-results](grafana_read_seq.png)

* Reading (Reverse)
    ![ops-latency](read_seq_rev/summary.png)
    ![monitoring-results](grafana_read_seq_rev.png)