# Libpostal REST Docker

[libpostal](https://github.com/openvenues/libpostal) is a C library for parsing and normalizing street addresses. Using libpostal requires compiling a C program that downloads ~2GB of training data.

This Dockerfile automates that compilation and creates a container with libpostal and [libpostal-rest](https://github.com/fphgov/libpostal-rest) which allows for a simple REST API that makes it easy interact with libpostal.

## Build image and start up container

```
docker build -t libpostal-rest .
docker run -d -p 8080:8080 libpostal-rest
```

## Environments

|Name                   |Default value                            |
|-----------------------|-----------------------------------------|
|LIBPOSTAL_UPSTREAM     |github.com/openvenues/libpostal          |
|LIBPOSTAL_REST_UPSTREAM|github.com/johnlonganecker/libpostal-rest|
|LIBPOSTAL_COMMIT       |master                                   |
|LIBPOSTAL_REST_RELEASE |1.1.0                                    |
|LOG_LEVEL              |info                                     |
|LOG_STRUCTURED         |true                                     |
|PROMETHEUS_ENABLED     |false                                    |
|PROMETHEUS_PORT        |9090                                     |
|LISTEN_PORT            |8080                                     |

## Build image from specific libpostal git hash

```
docker build -t libpostal-rest --build-arg COMMIT=68cc0dd7f5bef9189481a44d87391cb7fa841285 .
```

**Works with branch names as well**
```
docker build -t libpostal-rest --build-arg COMMIT=parser-data .
```

If a commit/hash is not specified it defaults to the **master** branch

## Documentation

See REST API [here](https://github.com/johnlonganecker/libpostal-rest)
