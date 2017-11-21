[![master](https://img.shields.io/travis/emc-mongoose/mongoose-storage-driver-atmos/master.svg)](https://travis-ci.org/emc-mongoose/mongoose-storage-driver-atmos)
[![downloads](https://img.shields.io/github/downloads/emc-mongoose/mongoose-storage-driver-atmos/total.svg)](https://github.com/emc-mongoose/mongoose-storage-driver-atmos/releases)
[![release](https://img.shields.io/github/release/emc-mongoose/mongoose-storage-driver-atmos.svg)]()
[![Docker Pulls](https://img.shields.io/docker/pulls/emcmongoose/mongoose-storage-driver-atmos.svg)](https://hub.docker.com/r/emcmongoose/mongoose-storage-driver-atmos/)

[Mongoose](https://github.com/emc-mongoose/mongoose-base)'s driver for
EMC Atmos cloud storage

# Introduction

The storage driver extends the Mongoose's [Abstract HTTP Storage Driver](https://github.com/emc-mongoose/mongoose-base/wiki/v3.6-Extensions#231-http-storage-driver)

# Features

* API version: ?
* Authentification:
    * Requests are signed with a secret key if configured
    * Using subtenant
* Filesystem access
* SSL/TLS
* Item types:
    * `data`
    * `token`
* Data item operation types:
    * `create`
    * `read`
        * full
        * random byte ranges
        * fixed byte ranges
        * content verification
    * `update`
        * full (overwrite)
        * random byte ranges
        * fixed byte ranges (with append mode)
    * `delete`
    * `noop`
* Token item operation types:
    * `create`
    * `read`
    * `delete`
    * `noop`

# Usage

Latest stable pre-built jar file is available at:
https://github.com/emc-mongoose/mongoose-storage-driver-atmos/releases/download/latest/mongoose-storage-driver-atmos.jar
This jar file may be downloaded manually and placed into the `ext`
directory of Mongoose to be automatically loaded into the runtime.

```bash
java -jar mongoose-<VERSION>/mongoose.jar \
    --storage-driver-type=atmos \
    ...
```

## Notes

* To specify a subtenant use the `storage-auth-token` configuration option

## Docker

### Standalone

```bash
docker run \
    --network host \
    --entrypoint mongoose \
    emcmongoose/mongoose-storage-driver-atmos \
    -jar /opt/mongoose/mongoose.jar \
    --storage-type=atmos \
    ...
```

### Distributed

#### Drivers

```bash
docker run \
    --network host \
    --expose 1099 \
    emcmongoose/mongoose-storage-driver-service-atmos
```

#### Controller

```bash
docker run \
    --network host \
    --entrypoint mongoose \
    emcmongoose/mongoose-base \
    -jar /opt/mongoose/mongoose.jar \
    --storage-driver-remote \
    --storage-driver-addrs=<ADDR1,ADDR2,...> \
    --storage-driver-type=atmos \
    ...
```

## Advanced

### Sources

```bash
git clone https://github.com/emc-mongoose/mongoose-storage-driver-atmos.git
cd mongoose-storage-driver-atmos
```

### Test

```
./gradlew clean test
```

### Build

```bash

./gradlew clean jar
```

### Embedding

```groovy
compile group: 'com.github.emc-mongoose', name: 'mongoose-storage-driver-atmos', version: '<VERSION>'
```

