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

## Implementation
Below are the steps to replicate a data pipeline from private cloud (**PVC**) to public cloud (**PC**) -
### Replication Manager
- Prior to creating replication policies, register private cloud cluster in the public cloud environment. Go to Classic Clusters in CDP PC Management Console and add PVC cluster. In the Cluster Details dialog, select CDP Private Cloud Base option and fill out all the details. If you have Knox enabled in your PVC cluster, check "Register KNOX endpoint (Optional)" box and add the KNOX IP address & port.  
  For detailed information on adding & managing classic clusters, please visit [Managing classic clusters](https://docs.cloudera.com/management-console/cloud/classic-clusters/topics/mc-managing-classic-clusters.html).
  <img width="1402" alt="Screen Shot 2022-06-07 at 12 17 09 AM" src="https://user-images.githubusercontent.com/2523891/172319541-76adca08-5c1b-432e-9b18-ede0d588c7b1.png">

- Once the PVC cluster is added, proceed to creating policies in Replication Manager.
- Following replication policies need to be created to support this exercise - 
  * HDFS Policy  
    <img width="1123" alt="Screen Shot 2022-06-08 at 11 58 43 AM" src="https://user-images.githubusercontent.com/2523891/172695444-4fd10057-f113-44d0-808d-64add87952fe.png">

  * Hive Policy
  * HBase Policy


### NiFi

### Spark

### Hive

### HBase

### Data Catalog

## FAQs
Document common challenges / not-so-best cases
