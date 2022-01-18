```
$ docker build -t hellonode .
$ docker run --rm -d \
  -p 60000:8080 \
  hellonode
```