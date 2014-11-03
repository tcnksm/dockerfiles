# Dockerfile-h2o

This is Dockerfile for trying [h2o](https://github.com/h2o/h2o).

To Build,

```bash
$ docker build -t tcnksm/h2o .
```

To run,

```bash
$ docker run --rm -p <port>:<port> tcnksm/h2o examples/h2o.conf
```
