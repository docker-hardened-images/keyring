# Docker Hardened Images - Keyring

Repository containing public signing keys for Docker Hardened Images (DHI)

## Versions

| Version | Status |                        |
|---------| -------|------------------------|
| 1       | active | [dhi-1.pub](dhi-1.pub) |

## Usage

To verify images and attestations, customer can run the following command:

```
$ cosign verify dhi/golang:1-dev \
  --key https://raw.githubusercontent.com/docker-hardened-images/keyring/refs/heads/main/dhi.pub
```
