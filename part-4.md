## IV. Compute Solutions

##### Read Time: ~10 mins

##### About: Compute Engine, App Engine

### > Planning Service Resources

Basically, you could use [this calculator](https://cloud.google.com/products/calculator/) for calculating resources.

### > Compute Solutions

#### I. Compute Engine

##### Product Basic Information

- **Compute Engine** is a basic VM products. Available in many options for flexibility.
- **Compute Engine** provides you with Linux and Windows VM.

##### Image

**Image** is the OS that you can use in your instance. You can use Linux-based or Windows-based OS. Cater it to your needs. You can see available images [here](https://cloud.google.com/compute/docs/images#os-compute-support).

To see images available to you. You could run this

```sh
# Get list of images
gcloud compute image list
```

##### Instances

**Instance** is basically the **Compute Engine** VM itself. You could create a VM and turn it on and off like your laptop. GCP let's you to easily create, configure, and delete instance with ease

###### Create an Instance

To create instance you could issue the command

```sh
# Create instance with:
# -> Instance Name "AyamVM"
# -> Image family "ubuntu-1804-lts"
# -> Image project "gce-uefi-images"
# -> Zone "europe-west1-b"
gcloud compute instances create AyamVM --zone europe-west1-b --image-family ubuntu-1804-lts --image-project gce-uefi-images
```

###### Accessing the Instance

You could ssh into your VM by using this command

```sh
# Accessing vm "AyamVM"
gcloud compute ssh AyamVM

# Or you could specify more details into the command. Like adding project id and zone information
gcloud compute ssh --project project-id-123 --zone europe-west1-b AyamVM
```

