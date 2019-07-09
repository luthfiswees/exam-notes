## II. Manage Account

##### Read Time: ~5mins

##### About : Console, Projects, Services Basics

### > Principle of Least Privilege (PoLP)

- **Principle of Least Privilege (PoLP)**, or known as _Principle of minimal privilege_ enquires you to have minimal privilege possible to do a task in an abstract layer to ensure security.

- An **user**,  **program**, or **application** must be able to access **only** the resource it needed. Nothing more, nothing less.

- In building any apps, VM's, etc. Make sure to follow this approach thoroughly to ensure security. This approach is implemented in IAM Policy Management.

### > Basic Console Commands

To access Google Cloud console online, you could access [https://console.cloud.google.com](https://console.cloud.google.com/) and select Cloud Shell. Or if you want, you could also install the SDK in your local environment. It enables you to do GCP operations locally.

#### Installing Google Cloud SDK locally

##### Linux (Debian)

[Reference](https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu) 

```sh
# Add source for deb
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

# Install CA certificates library
apt-get install apt-transport-https ca-certificates

# Import Google Public Key
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

# Install the SDK
sudo apt-get update && sudo apt-get install google-cloud-sdk
```

##### MacOS

[Reference](https://cloud.google.com/sdk/docs/quickstart-macos) 

```sh
# Download file using curl
curl google-cloud-sdk-253.0.0-darwin-x86_64.tar.gz

# Unzip it using tar
tar -xvzf google-cloud-sdk-253.0.0-darwin-x86_64.tar.gz

# Enter the directory
cd google-cloud-sdk-253.0.0-darwin-x86_64

# Run the installation script
./google-cloud-sdk/install.sh
```

#### Initialize the SDK

```sh
# Init the command
gcloud init

# You will be prompted to login in the browser. Pick 'Y'
To continue, you must log in. Would you like to log in (Y/n)? Y

# Pick project you want to log on
Pick cloud project to use:
 [1] [my-project-1]
 [2] [my-project-2]
 ...
Please enter your numeric choice: 1
 
# Enter your preferred compute zone 
Which compute zone would you like to use as project default?
 [1] [asia-east1-a]
 [2] [asia-east1-b]
 ...
 [14] Do not use default zone
Please enter your numeric choice: 1

# It will be succeed if you see this kind of message
gcloud has now been configured!
You can use [gcloud config] to change more gcloud settings.

Your active configuration is: [default]
```

#### Core Google Cloud Commands

Most of this command are used to login and inquire basic needed info about config and credentials.

```sh
# Login to account
gcloud auth login

# To list account whose credentials are stored locally
gcloud auth list

# See config available locally
gcloud config list

# Set project used by current account in config
glcoud config set project myProject

# Set area/zone used by current account in config
gcloud config set compute/zone asia-east1-b

# Inquire help about gcloud commands
gcloud info

# You could also inquire info about specific command like this.
#
# Here, you want to know what `gcloud compute instances create` commands do
gcloud help compute instances create
```

### > Projects

##### What is a Project?

- A **project** is a **set** of Google Cloud Platform **resources**
  - A **project** could consist a set of users
  - A **project** could consist a set of billing
  - A **project** could consist a set of API's, and monitoring tools of that API's
- Example:
  - You could have a GCS, Compute Engine Instances, and all of it's monitoring peripherals in a same project.
  - You could have multiple billing accounts inside a project. For example, your company registered your CTOs and your VP of Engineering billing accounts to the projects. Both of them could pay the bills of that project.

##### Creating Project

```sh
# Create Projects with id "project-id-123" and name "luthfiswees"
gcloud projects create project-id-123 --name="luthfiswees"

# Create Projects with id "project-id-123", name "luthfiswees", and label with key "usage" and value "entertainment"
gcloud projects create project-id-123 --name="luthfiswees" --labels=usage=entertainment
```

##### List existing Projects

```sh
# List all existing project available to the account
gcloud projects list
```

##### Describe Project

```sh
# Describe project named "luthfiswees"
gcloud projects describe luthfiswees
```

##### Delete Project

```sh
# Delete Projects with id "project-id-123"
gcloud projects delete project-id-123
```

##### IAM Policy

It is used to **add**, **list**, and **remove** user access to the project.

```sh
# To add user "luthfi@gmail.com" with role "editor" to project "project-id-123"
gcloud projects add-iam-policy-binding "project-id-123" --member='user:luthfi@gmail.com' --role='roles/editor'

# To get iam policies for project "project-id-123"
gcloud projects get-iam-policy project-id-123

# To remove user "luthfi@gmail.com" with role "roles/editor" from project "project-id-123"
gcloud projects remove-iam-policy-binding "project-id-123" --member='user:luthfi@gmail.com' --role='roles/editor'
```

### > Service

**Service** are basically a general term for products. Such as GCS, BigQuery, GKE, etc.

##### Basic Commands

```sh
# List service available to you (enabled and available to be enabled)
gcloud services list --available

# List service enabled to you
gcloud services list --enabled

# Enabling PubSub (pubsub.googleapis.com)
gcloud services enable pubsub.googleapis.com

# Disabling PubSub (pubsub.googleapis.com)
gcloud services disable pubsub.googleapis.com
```

#### Cloud IAM Roles

Roles available to services

- `roles/viewer` : Could only view. Operations available:
  - get
  - list: `gcloud services list`
- `roles/editor` or `roles/owner`: Could edit and view. Operations available:
  - get
  - list: `gcloud services list`
  - disable: `gcloud services disable`
  - enable: `gcloud services enable`
- `roles/serviceusage.serviceUsageViewer`: Could edit and view. Operations available:
  - get
  - list: `gcloud services list` 
- `roles/serviceusage.serviceUsageAdmin`:  Could edit and view. Operations available:
  - get
  - list: `gcloud services list`
  - disable: `gcloud services disable`
  - enable: `gcloud services enable`
- `roles/servicemanagement.serviceConsumer`: Could bind. Operations available:
  - bind