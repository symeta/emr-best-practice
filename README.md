# emr-best-practice-discussion

## 1. flink@emr

- EMR Component Distribution Diagram


<img width="1056" alt="image" src="https://github.com/symeta/emr-best-practice/assets/97269758/82d1f310-3d61-40cf-afd6-666b6ff8f510">


- YARN Architecture


![image](https://github.com/symeta/emr-best-practice/assets/97269758/6702aeab-f0e0-4387-ae81-c2fdfa7f6d89)


- Flink Architecture


![image](https://github.com/symeta/emr-best-practice/assets/97269758/dcd909fc-adc8-476e-a5d0-e08f45cf8074)


- a typical data flow diagram of flink application having kafka as the source, hdfs/s3 and the destination

  - [architecture diagram](https://github.com/symeta/realtime-dw-prototype/tree/architecture-overview)
  - [sample code](https://github.com/symeta/realtime-dw-prototype/tree/Validate-the-connection-between-MSK-cluster-and-Hudi-(MSK-consumer-via-flink%40emr))
  - Note: (1) in the case that emr hive/spark application writes to s3, such writing is accomplished via EMRFS;
    (2) in the case of flink application writing to s3, such writing is accomplished via flink-s3-fs-hadoop. Both cases can achieve writing to s3 bucket by simply pointing the output destination as s3 buket url


1. flink, flink jobs, hdfs, s3, hive,hadoop,yarn,zk 这些组件的关系与关联方式。
2. 数据流向，kafka flink jobs 的数据分别是如何写到 hdfs和s3。
3. flink jobs 的 taskmanager的out 和 log如何关闭或自动rotate。
4. EMR, primary, core, instance group 的具体区别与用法。
5. 节点资源消耗 成本控制与高可用。



https://aws.github.io/aws-emr-best-practices/applications/spark/best_practices/

https://aws.amazon.com/cn/blogs/big-data/seven-tips-for-using-s3distcp-on-amazon-emr-to-move-data-efficiently-between-hdfs-and-amazon-s3/

https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-group-configuration.html

https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-purchasing-options.html


https://aws.amazon.com/cn/blogs/china/best-practices-for-successfully-managing-memory-for-apache-spark-applications-on-amazon-emr-2/


