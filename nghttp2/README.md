# Dockerfile-nghttp2

This is Dockerfile for trying [nghttp2](https://github.com/tatsuhiro-t/nghttp2).

Build it,

```bash
$ docker build -t tcnksm/nghttp2 .
```

Run it,

```bash
$ docker run --rm -it -p <port>:<port> nghttp2 <port>
```
