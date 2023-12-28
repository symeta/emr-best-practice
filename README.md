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
  - (2) in the case of flink application writing to s3, such writing is accomplished via flink-s3-fs-hadoop. Both cases can achieve writing to s3 bucket by simply pointing the output destination as s3 buket url
 

- flink log shutdown, auto rotate
  - **DO NOT RECOMMEND TO SHUTDOWM LOGS, SUGGEST TO ARCHIVE LOGS TO S3**
  - shutdown log via code
    ```java
    Log4jLoggerAdapter logger = (Log4jLoggerAdapter)LoggerFactory.getLogger(JobManager.class);
    Field loggerField = Log4jLoggerAdapter.class.getDeclaredField("logger");
    loggerField.setAccessible(true);
    Logger loggerObject = (Logger)loggerField.get(logger);
    Field repoField = Category.class.getDeclaredField("repository");
    repoField.setAccessible(true);
    LoggerRepository repoObject = (LoggerRepository)repoField.get(loggerObject);
    repoObject.setThreshold(Level.OFF);
    ```
  - shutdown log via config
    ```properties
    log4j.logger.my.app1=DEBUG
    log4j.logger.my.app2=WARN
    log4j.logger.my.app3=OFF
    ```
  - [auto rotate tool guidance](https://aws.amazon.com/cn/blogs/big-data/seven-tips-for-using-s3distcp-on-amazon-emr-to-move-data-efficiently-between-hdfs-and-amazon-s3/
)


- [zookeeper use case summary](https://zookeeper.apache.org/doc/r3.9.1/zookeeperUseCases.html)

## 2. emr specific terms explanation

  - primary nodes
  - core nodes
  - task nodes
  - instance group
  - instance fleet

  https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-master-core-task-nodes.html
  
  https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-group-configuration.html

  https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-purchasing-options.html

## 3. [emr cost optimization](https://aws.github.io/aws-emr-best-practices/cost_optimization/best_practices/)

   -[managed scaling metrics](https://docs.aws.amazon.com/emr/latest/ManagementGuide/managed-scaling-metrics.html)
   -[custom scaling deep dive](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-automatic-scaling.html)

## 4. [emr reliability](https://aws.github.io/aws-emr-best-practices/reliability/best_practices/)
  

## resources
  - https://aws.github.io/aws-emr-best-practices/
  - https://aws.amazon.com/cn/blogs/china/realize-emr-automatic-cluster-size-adjustment-with-eventbridge-and-lambda/
  - https://aws.amazon.com/cn/blogs/china/cost-optimization-application-practice-of-amazon-ec2-spot-instance-in-aws-emr-cluster/
  - https://aws.amazon.com/cn/blogs/china/best-practices-for-running-apache-spark-applications-using-amazon-ec2-spot-instances-with-amazon-emr/
  - https://aws.amazon.com/cn/blogs/china/best-practices-for-successfully-managing-memory-for-apache-spark-applications-on-amazon-emr-2/


