## III. Storage Solutions

##### Read Time: ~10mins

##### About: GCS, Spanner, Firestore

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

##### Basic Concepts

- **Object** stored inside a **bucket**
- **Object** named with **/** are directories. It could contain multiple **objects** inside it. Ex: `ayam/bakar.jpg` object consist of directory `ayam` and file object named `bakar.jpg`. If other object uploaded like `ayam/goreng.jpg`, it will create a `goreng.jpg` file inside `ayam` directory. Where `goreng.jpg` file stored in the same directory as `bakar.jpg`.
- **Object** naming conventions follows filesystem rules. You **cannot** create an object like `ayam//goreng` since it's not a valid filepath name.
- **Bucket** have access control (usually abbreviated as `acl`). It could be set to `public` (everyone could see the content) or the owner could set it as it fits.

##### Command Line Basics (gsutil)

[Source](https://cloud.google.com/storage/docs/quickstart-gsutil)

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

#### II. Cloud Spanner

##### Product Basic Information

- **Spanner** is a relational database that is **horizontally scalable** 
- **Spanner** is compatible with **SQL** operations

##### Basic Concepts

- **Spanner** applies **Relational Database** concepts

- **Object** are represented inside **tables**. **Table** have **column** that represents that object properties and **rows** that represent a single instance of that object. Every row represent a single set of data that is called **tuples**.

  - Example of table **User**

    | id   | name          | occupation | age  |
    | ---- | ------------- | ---------- | ---- |
    | 1    | Luthfi Kurnia | Student    | 17   |
    | 2    | Luthfi Putra  | Engineer   | 25   |

    We could say that **User** object have four properties. That is _id_, _name_, _occupation_, and _age_.

- A **Table** could be related to other tables to represent something as a whole.

  - Example of table **Transaction**. This table is related to table **User** presented above.

    | id   | amount | payment_type | user_id |
    | ---- | ------ | ------------ | ------- |
    | 1    | 50000  | cash         | 2       |
    | 2    | 300000 | credit_card  | 2       |
    | 3    | 20000  | cash         | 1       |
    | 4    | 1000   | cash         | 1       |

    Property _user_id_ is related to **User** tables. Which means that user with id `1` is creating transaction with id `3` and `4`.

  - The tables could be related in any way as you like. As long as it makes sense to you. That's why it called _relational_. Tables could relate to each other in some ways.

##### Command Line Basics

[Source](https://cloud.google.com/spanner/docs/create-manage-instances)

###### Creating Instances

```sh
# Create an instance with name "ayam goreng" and id "project-id-123", cluster type would be "regional" in "us-central1" and node needed will be "2"
gcloud spanner instances create project-id-123 --config=regional-us-central1 --description="ayam goreng" --nodes=2
```

Available value for cluster type is:

- `regional`
- `multi-region`

###### List Instances

```sh
# List spanner instances
gcloud spanner instances list
```

###### Editing an Instance

```sh
# Change instance name to "bebek sawah" to instance "project-id-123"
gcloud spanner instances update project-id-123 --description="bebek sawah"

# Change node count to 3 to instance "project-id-123"
gcloud spanner instances update project-id-123 --nodes=3
```

###### Delete an Instance

```sh
# Delete an instance with instance id "project-id-123"
gcloud spanner instances delete project-id-123
```

###### Executing Query 

```sh
# Perform SQL query in instance "project-id-123" in db "ayam"
gcloud spanner databases execute-sql ayam --instance=project-id-123 \
--sql="INSERT Singers (SingerId, FirstName, LastName) VALUES (1, 'Marc', 'Richards')"
```

#### III. Cloud Firestore

##### Product Basic Information

- **Firestore** is a **Non-SQL**, Realtime database that is scalable
- **Firestore** have offline support. Ideal for realtime client interactions.

##### Basic Concepts

- **Data** stored inside **collections**

- **Collections** store instances of objects called **documents**.

  - **User** collections store instances of **user** documents.

- **Documents** store data in **JSON**-like format.

  ```json
  {
     "name":"Luthfi Putra",
     "age":25,
     "occupation":"Engineer",
     "address":{
        "street":"Kenanga St.",
        "number":"10",
        "city":"Jakarta",
        "province":"DKI Jakarta"
     }
  }
  ```

##### Firestore Operations

[Source](https://firebase.google.com/docs/firestore/quickstart)

Basically, you could use other programming language to interact with **Firestore**. Here, I will use **Ruby** to demonstrate some capabilities. For me, it's simpler this way. 

###### Setup Development Environment

Setup your env variable to your Google Credentials JSON files

```sh
export GOOGLE_APPLICATION_CREDENTIALS="path/to/your/keyfile.json"
```

It is not needed in production environment if you run your production environment in the same project where the **Firestore** is enabled.

Then add the SDK to your `Gemfile`

```ruby
gem "google-cloud-firestore"
```

And install your dependencies

```sh
bundle install
```

###### Initialize Firestore

```ruby
require "google/cloud/firestore"

firestore = Google::Cloud::Firestore.new project_id: project_id

puts "Created Cloud Firestore client with given project ID."
```

###### Add Data

```ruby
# Add document "alovelace" to "users" collection 
doc_ref = firestore.doc "users/alovelace"

doc_ref.set(
  first: "Ada",
  last:  "Lovelace",
  born:  1815
)
```

###### Read Data

```ruby
# Read data in "users" collection
users_ref = firestore.col "users"
users_ref.get do |user|
  puts "#{user.document_id} data: #{user.data}."
end
```

###### Update Data

```ruby
# Update document "frank" in "users" collection
frank_ref = firestore.doc "users/frank"
frank_ref.set(
  name:      "Frank",
  favorites: {
    food:    "Pizza",
    color:   "Blue",
    subject: "Recess"
  },
  age:       12
)

# Update document "frank" age and favorite color
frank_ref.update age: 13, "favorites.color": "Red"
```

###### Delete Data

```ruby
# Delete "alanturing" documents in "users" collection
users_ref = firestore.doc "users/alanturing"
users_ref.delete
```

###### Write a Transaction

A **transaction** is basically a set of operations tied together. If one operation in a transaction fails. It will fail altogether.

It exist to implement **Atomic** operations concept.

```ruby
def return_info_transaction project_id:
  # project_id = "Your Google Cloud Project ID"

  firestore = Google::Cloud::Firestore.new project_id: project_id

  city_ref = firestore.doc "cities/SF"

  updated = firestore.transaction do |tx|
    new_population = tx.get(city_ref).data[:population] + 1
    if new_population < 1_000_000
      tx.update city_ref, population: new_population
    else
      false
    end
  end

  if updated
    puts "Population updated!"
  else
    puts "Sorry! Population is too big."
  end
end
```

###### Batch Write

You could use batch write if you **don't need to do any read operations**. It's basically a transaction without any read commands in it.

```ruby
firestore.batch do |b|
  # Set the data for NYC
  b.set "cities/NYC", name: "New York City"

  # Update the population for SF
  b.update "cities/SF", population: 1_000_000

  # Delete LA
  b.delete "cities/LA"
end
```

