[ ![Download](https://api.bintray.com/packages/qaware-oss/registry/base%3Aalpine-k8s-ibmjava8/images/download.svg) ](https://bintray.com/qaware-oss/registry/base%3Aalpine-k8s-ibmjava8/_latestVersion)

# Alpine with IBM Java8 (Small Footprint) and DNS and Bash

This repository contains the `Dockerfile` for the `alpine-k8s-ibmjava8` image. It
is based on the latest IBM Java8 Alpine image and installs DNS and Bash. Thanks to
Jan Broer <janeczku@yahoo.com> for the Alpine image with proper DNS support.

## Build instructions

We use Gradle to build the Docker images. Of course you can also use the Docker
CLI commands to create and upload the image.
```shell
$ ./gradlew buildDockerImage
```

Next we need to squash the image size. For this we will export a container based
on the image and import it as image again using plain Docker commands.
```shell
docker run -d <IMAGE_ID>
docker export <CONTAINER_ID> | docker import - qaware-oss-docker-registry.bintray.io/base/alpine-k8s-ibmjava8:<VERSION>
```

`<IMAGE_ID>` - The created image ID name.
`<CONTAINER_ID>` - The container ID echoed after the Docker run command.
`<VERSION>` - Should be the actual Java version, like 8.0-3.10. When not specified
"latest" will be used as the Bintray version name.

## Pushing image to Bintray

Tag the latest image according to the following convention by running the following command:
```shell
docker tag <IMAGE_ID> qaware-oss-docker-registry.bintray.io/base/alpine-k8s-ibmjava8
```
`<IMAGE_ID>` - The image ID from the latest versioned image previously created.

Use the Docker client push command to upload and publish your images (please use
Docker v1.6 and above):
```shell
docker push qaware-oss-docker-registry.bintray.io/base/alpine-k8s-ibmjava8:<VERSION>
```
`<VERSION>` - Should be the actual Java version, like 8.0-3.10. When not specified
"latest" will be used as the Bintray version name.

Alternatively you can also use Gradle to upload the Docker images to Bintray.
```shell
$ ./gradlew pushDockerImage -PbintrayApiKey=<<INSERT API KEY>>
```

## Downloading image from Bintray

The images are hosted at the QAware OSS Bintray Docker repository. Use the Docker
client pull command to download an image (please use Docker v1.6 and above):
```shell
docker pull qaware-oss-docker-registry.bintray.io/base/alpine-k8s-ibmjava8:<VERSION>
```
`<VERSION>` - Optional. Should be the actual Java version like 8.0-3.10. When not specified
"latest" will be used as the Bintray version name.

## License

This software is provided under the MIT open source license, read the `LICENSE`
file for details.
