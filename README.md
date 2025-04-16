# Docker Hardened Images - Keyring

Repository containing public signing keys for Docker Hardened Images (DHI)

## Versions

| Version | Status      |                        |
|---------| ------------|------------------------|
| 2       | enabled     | [dhi-2.pub](dhi-2.pub) |
| 1       | disabled    | [dhi-1.pub](dhi-1.pub) |

## Usage

To verify images and attestations, customer can run the following command:

```
# log into the OCI referrer registry
$ docker login registry.scout.docker.com

# list all available attestations
$ regctl artifact list dhi/golang:1-debian12-dev \
  --external registry.scout.docker.com/dhi/golang \
  --platform linux/arm64

# verify the signature on any of the provided attestations
$ cosign verify registry.scout.docker.com/dhi/golang@sha256:... \
  --key https://registry.scout.docker.com/publickey/latest
```
