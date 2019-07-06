## I. Introduction to GCP

##### Read Time : ~5mins

### > Google Innovations 

- Google is all about Big Data and Huge Scalability
- Published a lot of **whitepapers**, Example:
  - _MapReduce_
  - _Google File System_
  - _Colossus_
- Released some of it's innovation as **open source tools**, Example:
  - _Kubernetes_, from project called _Borg_
- **Commercialize** some of it's internal tools, Example:
  - _BigTable_
  - _Spanner_
  - _Google Cloud Storage (GCS)_, built on _Colossus_
  -  _BigQuery_, built on _Dremel_
- **Acquire** some products, Example:
  - _Firebase_
  - _Stackdriver_
- Google hires _Site Reliability Engineer_ instead of _Operations people_ to manage their infrastructure. _Site Reliability Engineer_ are tasked to automate operation task and built reliability into the software.

### > Physical Infrastructure

#### Stacks

vCPU < Physical Server < Rack < Data Center < Zone < Region < Multi-Region < Global

#### Details

- Every _region_ are connected using _private global network_ that doesn't have to touch the internet traffic.
- **Points of Presence** : Network edge that connects Google's private network to the whole internet.
- **Points of Presence** could also be a CDN location.

#### Networks

- Normal Network : Routes traffic to edge location **closest to destination**
- Google Network : Routes traffic to enters from Internet **closest to source**
  - (+) Single global IP Address can load balance worldwide
  - (+) Sidesteps many DNS issues

### > Google Cloud Platform as a Product

Google Cloud Platform (GCP) are built with these things in mind.

#### Approach

- **GCP** was built from developers towards infra/ops
- **AWS** was built from infra/ops towards developers

#### Model

- **GCP** is intrinsically global
  - (+) Easier to handle latency in a global way
  - (-) More sensitive to multi-region/global failure
- **AWS** is intrisically region-scoped
  - (+) Simplifies data sovereignity
  - (-) Less availability across regions

#### Basic Products

##### Compute Products

- **Compute Engine** : VM with Disk connected to default Network
- **Kubernetes Engine (GKE)** : Managed Kubernetes/Containers
- **Cloud Functions** : _Event-driven_, _Serverless_ functions

##### Storage Products

- **Cloud Storage (GCS)** : Object Storage (like S3)
- **Nearline** : Archive, Occasional Access Storage
- **Coldline** : Archive, Rare Access Storage

##### Database Products

- **Cloud SQL** : Managed MySQL and PostgreSQL
- **Cloud Spanner** : Horizontally Scalable Relational DB
- **Cloud Datastore** : Horizontally Scalable Document DB 
- **Cloud Firestore** : Consistent, _Serverless_, Document DB

##### Networking Products

- **Virtual Private Cloud** : Private Network on the cloud
- **Cloud Load Balancing** : Multi-Region Load Distribution
- **Cloud CDN** : Content Distribution Network on the cloud
- **Cloud Armor** : DDoS Protection and WAF 

##### Data and Analytics Products

- **Cloud Pub/Sub** : Global Real-time Messaging
- **BigQuery** : _Serverless_, Data Warehouse & Analytics
- **Cloud Dataproc** : Managed Spark and Hadoop
- **Cloud Dataflow** : Stream/batch data processing

##### Machine Learning Products

- **Cloud TPU** : Tensorflow Processing Unit on the Cloud
- **Cloud Machine Learning Engine** : Managed Platform for ML
- **Cloud AutoML** : Configured ML Model. ready to use

##### Management Tools Product

- **Stackdriver Monitoring** : Infrastructure and Application Monitoring
- **Stackdriver Logging** : Centralized Logging
- **Cloud Deployment Manager** : Templated Infrastructure Deployment

### > Pricing

#### Schemes

- **Provision** -> _"Make sure you're ready to handle X amount of load"_
- **Usage** -> _"Charge me for what I use"_

#### Network Traffic

- **Free** on the way **in** (_ingress_)
- **Charge** on the way **out** (_egress_), calculated by how many GBs used
- Traffic between GCP services sometimes free