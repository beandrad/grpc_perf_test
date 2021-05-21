# Basic Performance Test

This project contains a [Locust](https://locust.io/) script with a simple test to measure the performance of the [grpcio](https://github.com/grpc/grpc/tree/master/src/python/grpcio) library. In particular, the output files contain the performance results [before](./output/old_version) and [after](./output/new_version) applying [this change](https://github.com/grpc/grpc/pull/26058).

## System info

Tests run inside an Ubuntu Docker container (see [.devcontainer](.devcontainer)) with the following resource limits:

- 8 cores
- 10GB of memory
- 2GB of swap

The underlying machine is a MacBook Pro:
- 2.3 GHz 8-Core Intel Core i9
- 32 GB of memory

## Test result

Running the test script for 20s with only one "user" sending requests at a particular point in time:

```bash
locust -f locust/locustfile.py --html locust/output/<version_name>/<version_name>.html --csv locust/output//<version_name>/<version_name> -u 1 -t 20s --headless
```

The metrics (RPS and response times) are very similar; the change doesn't seem to affect the performance of the library. 
