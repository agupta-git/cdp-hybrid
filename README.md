# WIP
# ROUGH NOTES
Hybrid features that we support in this use case - 
- Develop once, run anywhere. Single code base, multiple uses.
- De-risk cloud migration. Migrate apps independently instead of doing whole lift & shift.
- Add cloud workloads/features to existing on-prem data pipelines. This prevents disruption to existing business. Avoids duplication of data pipelines. Issue - airflow service needs to be available in both pvc and pc for hybrid to work in this context. 
- Enhancements - Add Denodo partner & build virtual views on on-prem & cloud tables.

## Use Case - How Cloudera Data Platform (CDP) delivers the best of private and public cloud
TBD

## Design
Following diagram shows a data pipeline in private & public form factors -
![CDP Hybrid Design](https://user-images.githubusercontent.com/2523891/172304557-ccc8772b-afc6-4ce2-9683-24a27204ee34.png)

## Prerequisites
- A data pipeline in a private cloud environment. Please follow instructions provided in [cdp-pvc-data-pipeline](https://github.com/agupta-git/cdp-pvc-data-pipeline) to set one up.
- Cloudera Data Platform (CDP) on Amazon Web Services (AWS). To get started, visit [AWS quick start](https://docs.cloudera.com/cdp/latest/aws-quickstart/topics/mc-aws-quickstart.html).

## Implementation
Below are the steps to replicate a data pipeline from private cloud base (**PVC**) cluster to public cloud (**PC**) environment -
### Replication Manager
- Prior to creating replication policies, register private cloud cluster in the public cloud environment. Go to Classic Clusters in CDP PC Management Console and add PVC cluster. In the Cluster Details dialog, select CDP Private Cloud Base option and fill out all the details. If you have Knox enabled in your PVC cluster, check "Register KNOX endpoint (Optional)" box and add the KNOX IP address & port.
- To ensure PVC cluster works with Replication Manager in PC environment, please follow instructions given in [Adding CDP Private Cloud Base cluster for use in Replication Manager](https://docs.cloudera.com/management-console/cloud/classic-clusters/topics/mc-register-cdpdc-cm-option.html).
- For more details on adding & managing classic clusters, please visit [Managing classic clusters](https://docs.cloudera.com/management-console/cloud/classic-clusters/topics/mc-managing-classic-clusters.html).
  <img width="1402" alt="Screen Shot 2022-06-07 at 12 17 09 AM" src="https://user-images.githubusercontent.com/2523891/172319541-76adca08-5c1b-432e-9b18-ede0d588c7b1.png">
- Once the PVC cluster is added, proceed to creating policies in Replication Manager.
- Create HDFS Policy  
  - Add all the code to HDFS directory of your choice. This includes NiFi flow definitions and PySpark program in this exercise.
  - Now, go to Replication Manager and create an HDFS policy. While creating the policy, you will be asked to provide source cluster, source path, destination cluster, destination path, schedule and few other additional settings. If you need help during any step in the process, please visit [Using HDFS replication policies](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-on-premise-to-amazon-s3-replication-in-hdfs.html) and [Creating HDFS replication policy](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-replication-of-data-on-premise-to-amazon-s3-data-in-hdfs.html).
  - Sample replication policy for reference -  
     <img width="1123" alt="Screen Shot 2022-06-08 at 11 58 43 AM" src="https://user-images.githubusercontent.com/2523891/172695444-4fd10057-f113-44d0-808d-64add87952fe.png">

- Create Hive Policy
  - While creating the policy, you will be asked to provide source cluster, destination cluster, database & tables to replicate, schedule and few other additional settings. In additional settings, ensure "Metadata and Data" is checked under Replication Option. If you need help during any step in the process, please visit [Using Hive replication policies](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-on-premise-to-cloud-in-hive.html) and [Creating Hive replication policy](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-replication-of-data-on-premise-to-amazon-s3-in-hive.html)
  - Sample replication policy for reference -  
    <img width="1119" alt="Screen Shot 2022-06-08 at 1 59 01 PM" src="https://user-images.githubusercontent.com/2523891/172716002-1fa93ca3-f728-4723-9f8f-0c5f22773b2f.png">
  
- Create HBase Policy
  - While creating the policy, you will be asked to provide source cluster, source tables, destination cluster and few other initial snapshot settings. If you need help during any step in the process, please visit [Using HBase replication policies](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-pc-hbase-replication-policy.html) and [Creating HBase replication policy](https://docs.cloudera.com/replication-manager/cloud/operations/topics/rm-pc-hbase-create-policy.html)
  - Sample replication policy for reference -  
    <img width="1114" alt="Screen Shot 2022-06-08 at 2 06 44 PM" src="https://user-images.githubusercontent.com/2523891/172718505-bf993a60-4723-477b-84a8-ec5a2faaa547.png">
    _Please ignore status message in the screen capture. Upon successful setup, it should say Active/Expired._

### NiFi
- Download NiFi flow definition from PVC cluster on your local machine.
- Go to Cloudera DataFlow (CDF) on PC environment and import the flow defintion.
- **Update the NiFi flow to use PutS3Object processor instead of PutHDFS processor.** Update properties in this processor to use desired S3 bucket. With this change, you will start storing incoming files in AWS S3 bucket instead of PVC HDFS directory. For any help with PutS3Object processor, please see [cdp-data-pipeline nifi flow](https://github.com/agupta-git/cdp-data-pipeline#step-1---setup-nifi-flow).
- Once updates are done, re-import NiFi flow as a newer version and deploy it.

### Spark
- Update the PySpark program to use AWS S3 bucket instead of PVC HDFS directory.
- Go to Cloudera Data 

### Hive

### HBase

### Data Catalog

## FAQs
Document common challenges / not-so-best cases
