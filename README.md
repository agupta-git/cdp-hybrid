# cdp-hybrid - ROUGH NOTES - WIP
Hybrid features that we support in this use case - 
- Develop once, run anywhere. Single code base, multiple uses.
- De-risk cloud migration. Migrate apps independently instead of doing whole lift & shift.
- Add cloud workloads/features to existing on-prem data pipelines. This prevents disruption to existing business. Avoids duplication of data pipelines.
- Enhancements - Add Denodo partner & build virtual views on on-prem & cloud tables.

## Design
Following diagram shows this data pipeline in private & public form factors.

![CDP Hybrid Design](https://user-images.githubusercontent.com/2523891/172304557-ccc8772b-afc6-4ce2-9683-24a27204ee34.png)

## Prerequisites
- A data pipeline in a private cloud environment. Please follow instructions provided in [cdp-pvc-data-pipeline](https://github.com/agupta-git/cdp-pvc-data-pipeline) to set one up.
