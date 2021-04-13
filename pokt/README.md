# POKT

## Build image
```bash
docker build -t [docker repo]:[version] --build-arg BRANCH_NAME=[version branch name] .
```

## Run image
```bash
docker run -ti --rm \
-v [path to data folder]:/root/.pocket \
. start
```
