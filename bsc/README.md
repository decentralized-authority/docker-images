# BSC

## Build image
```bash
docker build -t [docker repo]:[version] --build-arg RELEASE_URL=[url of linux zip] .
```

## Run image
```bash
docker run -ti --rm \
-v [path to data folder]:/blockchain/data \
-v [path to wallets folder]:/blockchain/keys \
-v [path to config file]:/blockchain/config.toml \
. --config=/blockchain/config.toml
```
