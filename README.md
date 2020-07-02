# fluentd-splunk-hec

A Fluentd Docker image with pre-installed and configured fluent-plugin-splunk-enterprise plugin.

## Notes

The included `fluent.conf` is for a specific use case and must be edited as it contains the Splunk HEC information and specific path values might also need attention.

## Build

```
$ docker build -t my-fluentd-splunk-hec:latest ./
```

## Run

This example starts Fluentd with the enabled Splunk HEC plugin, sets a volume for Fluent's logs, and also binds to the volume of a running Vault container with enabled file audit device log per the `fluent.conf`.

This example also joins a specific network and sets a static IP address as well.

```shell
$ docker run \
    -it \
    --rm \
    --name fluentd-splunk-hec \
    --volume $(pwd)/log:/fluentd/log \
    --volume $(pwd)/logs:/vault/logs \
    --network vss-network \
    --ip 10.0.42.101 \
    fluentd-splunk-hec:latest
```

Note, if the Vault container is not prepared with an enabled audit device log file at `/vault/logs/vault-audit.log` first, the Fluent container will error loop until it is present.

## Acknowledgments

- [Brian Shumate](https://github.com/brianshumate)
