## Introduction

This guide provides instructions for developers to build Flowgate from source code.

## Step 1: Prepare for a build environment for Flowgate

Flowgate is deployed as several Docker containers and most of the code is written in Java language. The build environment requires Docker, Docker Compose. Please install the below prerequisites:

Software              | Required Version
----------------------|--------------------------
docker                | 17.05 +
docker-compose        | 1.11.0 +
git                   | 1.9.1 +

## Step 2: Getting the source code

   ```sh
      $ git clone git@github.com:vmware/flowgate.git
   ```

## Step 3: Building and installing Flowgate
### Compile code with your own environment, then build Flowgate

*  Build Flowgate:

   ```sh
      $ cd flowgate/
      $ bash build.sh all -version v1.0
   ```

### Verify your installation

If everything worked properly, you can get the below message:

   ```sh
      ...
      build success.
   ```
Also, you can execute below command to verify your installation:

   ```
      $ sudo docker images
      REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
      flowgate/labsdb-worker     v1.0                b751b1e55ec9        5 hours ago         228MB
      flowgate/nlyte-worker      v1.0                4c1b5c0c1893        5 hours ago         226MB
      flowgate/aggregator        v1.0                a6ada87420a8        5 hours ago         229MB
      flowgate/poweriq-worker    v1.0                b1d6997bd8c8        5 hours ago         226MB
      flowgate/vro-worker        v1.0                6910c721130c        5 hours ago         231MB
      flowgate/vc-worker         v1.0                81c255461862        5 hours ago         255MB
      flowgate/redis             v1.0                b0d6035edaf6        5 hours ago         102MB
      flowgate/api               v1.0                0b71d1eea75b        5 hours ago         238MB
      flowgate/mongodb           v1.0                a56dcb8f1dad        5 hours ago         271MB
      flowgate/infoblox-worker   v1.0                227b8304775d        5 hours ago         221MB
      flowgate/management        v1.0                939197e11efe        5 hours ago         249MB
      photon                     2.0                 c3c18145a8cd        13 days ago         32.4MB
      maven                      3.3.9-jdk-8         9997d8483b2f        2 years ago         653MB
   ```

## Appendix
* Using the build.sh

The `build.sh` contains these configurable parameters:

Variable           | Description
-------------------|-------------
ui                 | only build ui.
jar                | build jar package. (You must execute the above orders.)
image              | build all docker images. (You must execute the above orders.)
save               | save all of the docker images to a tar. (You must execute the above orders.)
all                | build all above steps.
version            | Specify a version number for Flowgate.

#### EXAMPLE:

#### execute build script

   ```sh
      $ bash build.sh
      eg. 'bash build.sh ( ui | jar | image | save | copy2server | all ) -version v1.0'
   ```
