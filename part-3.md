## III. Storage Solutions

##### Read Time: ~10mins

##### About: GCS

### > Planning Service Resources

Basically, you could use [this calculator](https://cloud.google.com/products/calculator/) for calculating resources.

### > Storage Solutions

#### I. Google Cloud Storage (GCS)

##### Product Basic Information

- _Google Cloud Storage (GCS)_ is an _unstructured database_ provided by GCP.
- _Unstructured Database_ usually used to store files (media files, executables, etc).
- To operate GCS, you could use **gsutil** command line tool.
- Default storage class available:
  - `multi_regional`
  - `regional`
  - `nearline` (Occasional Archival Data)
  - `coldline` (Rare Archival Data)

##### Command Line Basics (gsutil)

###### Create Bucket

```sh
# Create bucket named "ayam-pop-enak" in region "northamerica-northeast1"
gsutil mb -l northamerica-northeast1 gs://ayam-pop-enak

# Create bucket named "ayam-bakar" in region "northamerica-northeast1" with storage class "coldline" and project name "project-ayam"
gsutil mb -p project-ayam -l northamerica-northeast1 -c coldline gs://ayam-bakar
```

###### List Bucket

```sh
# List available bucket
gsutil ls

# List content of bucket called "ayam"
gsutil ls gs://ayam

# List everything inside bucket called "ayam"
gsutil ls gs://ayam/**
```

###### Delete Bucket

```sh
# Delete bucket named "ayam"
gsutil rm -r gs://ayam/
```

###### Upload and Download Object

```sh
# Upload local file called "fotosaya.jpg" to bucket "ayam"
gsutil cp fotosaya.jpg gs://ayam/

# Upload everything in local directory "foto" to bucket "ayam"
gsutil cp foto/** gs://ayam/

# Download files "fotosaya.jpg" from bucket "ayam" to local Desktop
gsutil cp gs://ayam/fotosaya.jpg Desktop/fotosaya.jpg

# Move file from bucket "ayam" to bucket "sapi"
gsutil cp gs://ayam/** gs://sapi/
```

###### Delete Object

```sh
# Delete file "fotosaya.jpg" in bucket "ayam"
gsutil rm gs://ayam/fotosaya.jpg
```

###### Enable Object Versioning

Basically make object uploaded to bucket versioned. So if you delete something accidentally. You could revert the state to make it back.

```sh
# Find out if versioning is turned on or not in bucket "ayam"
gsutil versioning get gs://ayam/

# Enable versioning
gsutil versioning set on gs://ayam/

# Disable versioning
gsutil versioning set off gs://ayam/

# Fetch list with active versioning in bucket "ayam"
gsutil ls -a gs://ayam/
```

###### Object Access Control

```sh
# Give public read access to file "fotosaya.jpg" in bucket "ayam"
gsutil acl ch -u AllUsers:R gs://ayam/fotosaya.jpg

# To delete public permission of file "fotosaya.jpg" in bucket "ayam"
gsutil acl ch -d AllUsers gs://ayam/fotosaya.jpg
```

###### Labels

```sh
# Add label with key "ayam" with value "bakar" to bucket "opor"
gsutil label ch -l ayam:bakar gs://opor/

# View labels on bucket "opor"
gsutil ls -L -b gs://opor/

# Remove label with key "ayam" on bucket "opor"
gsutil label ch -d ayam gs://opor/
```

