# LBRY

### Introduction
* Originally adapted from: [https://github.com/lbryio/lbrycrd/tree/v17_master/packaging/docker-for-binary](https://github.com/lbryio/lbrycrd/tree/v17_master/packaging/docker-for-binary)
* lbrycrd releases can be found here: [https://github.com/lbryio/lbrycrd/releases](https://github.com/lbryio/lbrycrd/releases)

### Build image
```
docker build -t [docker repo]:[version] --build-arg release_url=[url of linux zip] .
```

### Run image
```
docker run -ti --rm \
-v [path to host data dir]:/lbry/data \
-v [path to host keys dir]:/lbry/keys \
-v [path to conf file]:/lbry/lbrycrd.conf \
. -conf=/lbry/lbrycrd.conf
```
