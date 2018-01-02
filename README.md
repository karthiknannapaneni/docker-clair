# Container scrubbing with Clair

Clair is an image scrubbing service used for detecting vulnerabilities within containers.
[Read more on Clair by the CoreOS team](https://github.com/coreos/clair)

## Fire it up!

Before you start Clair, edit `docker-compose.yml` and set your own postgres database password. Use this password in `data/clair/config/config.yml` too.
Now, your ready to go!

`
docker-compose up -d
`

## Using Clair with Klar

Using Clair to scrubb an image is super simple with the command line tool [Klar](https://github.com/optiopay/klar).
Build Klar as a docker container is the easiest way to use Klar:

```
git clone https://github.com/optiopay/klar
cd klar
docker build --rm -t klar .
```

Now, to scrubb an image from the hub, you would run:

```
docker run -e CLAIR_ADDR="http://<clair_host>:6060" \
           -e CLAIR_OUTPUT=Unknown \
           -e CLAIR_THRESHOLD=10 \
           klar centos:7
```

If you want to scrubb an image in some other registry, you would run:

```
docker run -e CLAIR_ADDR="http://<clair_host>:6060" \
           -e CLAIR_OUTPUT=Unknown \
           -e CLAIR_THRESHOLD=10 \
           -e DOCKER_USER=myuser \
           -e DOCKER_PASSWORD=mypassword \
           klar registry.example.com/centos:7
```



