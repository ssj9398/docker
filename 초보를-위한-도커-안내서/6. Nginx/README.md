```
$ docker build -t lab02/exam1 .
$ docker run -d --rm \
  -p 50000:80 \
  lab02/exam1
```