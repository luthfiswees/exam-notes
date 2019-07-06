## I. Introduction to GCP

##### Read Time : ~5mins

### > Google Innovations 

- Google is all about Big Data and Huge Scalability
- Published a lot of **whitepapers**, Example:
  - _MapReduce_
  - _Google File System_
  - _Colosus_
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

### > Pricing

#### Schemes

- **Provision** -> _"Make sure you're ready to handle X amount of load"_
- **Usage** -> _"Charge me for what I use"_

#### Network Traffic

- **Free** on the way **in** (_ingress_)
- **Charge** on the way **out** (_egress_), calculated by how many GBs used
- Traffic between GCP services sometimes free