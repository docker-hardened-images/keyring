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
$ cosign verify dhi/golang:1-dev \
  --key https://registry.scout.docker.com/publickey/latest
```
