Docker-registry
===============

Sources for [google/docker-registry](https://index.docker.io/u/google/docker-registry/), [Docker Registry](https://github.com/dotcloud/docker-registry) image to push/pull your [Docker](https://www.docker.io/) images to/from [Google Cloud Storage](https://cloud.google.com/products/cloud-storage/).

- Uses 'gcs' as a storage option
- Has OAuth2 support built in
- Works locally and on [Google Compute Engine] (https://cloud.google.com/products/compute-engine/)


### Building google/docker-registry image


    docker build -t google/docker-registry .


### Usage

After [google/docker-registry](https://index.docker.io/u/google/docker-registry) is built or pulled from the [public registry]( https://index.docker.io/u/google/docker-registry) you can push/pull docker images to/from your [Google Cloud Storage](https://cloud.google.com/products/cloud-storage/) bucket.

#### Locally

1. Start the registry and mount your credentials from a data container named gcloud-config. You also need to pass some environment variables to your container, i.e. GCS_BUCKET and BOTO_PATH (path to your .boto file with credentials). If you have logged in with [gcloud container](https://index.docker.io/u/google/cloud-sdk/), your credentials are in /.config/gcloud/legacy_credentials/{your email}/.boto. For more information about getting OAuth2 credentials please refer to [google/cloud-sdk](https://index.docker.io/u/google/cloud-sdk/) documentation.



        docker run -d -e GCS_BUCKET=yet-another-docker-bucket -p 5000:5000 \
        --volumes-from gcloud-config google/docker-registry



1. Now you can store your images on GCS!


        docker tag myawesomeimage localhost:5000/myawesomeimage
        docker push localhost:5000/myawesomeimage


#### Google Compute Engine

On [Google Compute Engine] (https://cloud.google.com/products/compute-engine/) instance you don't need to mount any volumes or pass BOTO_PATH. All necessary information will be received from Metadata Server:

    docker run -d -e GCS_BUCKET=yet-another-docker-bucket -p 5000:5000 google/docker-registry 


### Notes

Current image size: 257.4 MB

