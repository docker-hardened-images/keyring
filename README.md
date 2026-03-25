<img alt="dhi-banner" src="https://github.com/user-attachments/assets/fc0ca203-3f25-4ae5-aa8e-e3918bbcc31f" />

# Docker Hardened Images - Keyring

This repository contains the public signing keys for [**Docker Hardened Images**](https://dhi.io). These keys are used to verify the authenticity and integrity of Docker Hardened Images and their attestations.

## 🎯 Overview

The keyring provides cryptographic verification for Docker Hardened Images, ensuring:

- **Supply chain security**: Verify image signatures and provenance
- **Attestation validation**: Confirm authenticity of SBOMs and VEX metadata
- **Trust**: Ensure images haven't been tampered with

## 🔑 Signing Keys

| Status   | Key File                                                                                                 | URL 
|----------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| active   | [dhi-latest.pub](publickey/dhi-2.pub)                                                                    | https://dhi.io/keyring/latest.pub                                  |
| active   | [dhi-2.pub](publickey/dhi-2.pub)                                                                         | https://dhi.io/keyring/2.pub                                       |
| inactive | [dhi-1.pub](publickey/dhi-1.pub)                                                                         | https://dhi.io/keyring/1.pub                                       |
| active   | [dhi-apk@docker-0F81AD7700D99184.rsa.pub](publickey/dhi-dhi-apk@docker-0F81AD7700D99184.rsa.pub)         | https://dhi.io/keyring/dhi-apk@docker-0F81AD7700D99184.rsa.pub     |
| active   | [dhi-apk-sec@docker-0F81AD7700D99184.rsa.pub](publickey/dhi-dhi-apk-sec@docker-0F81AD7700D99184.rsa.pub) | https://dhi.io/keyring/dhi-apk-sec@docker-0F81AD7700D99184.rsa.pub |
| active   | [dhi-apk-els@docker-0F81AD7700D99184.rsa.pub](publickey/dhi-dhi-apk-els@docker-0F81AD7700D99184.rsa.pub) | https://dhi.io/keyring/dhi-apk-els@docker-0F81AD7700D99184.rsa.pub |
| active   | [dhi-deb-gpg.D46852F6925E9F71.key](publickey/dhi-dhi-deb-gpg.D46852F6925E9F71.key)                       | https://dhi.io/keyring/dhi-deb-gpg.D46852F6925E9F71.key            |   
| active   | [dhi-deb-sec-gpg.D46852F6925E9F71.key](publickey/dhi-dhi-deb-sec-gpg.D46852F6925E9F71.key)               | https://dhi.io/keyring/dhi-deb-sec-gpg.D46852F6925E9F71.key        |   
| active   | [dhi-deb-els-gpg.D46852F6925E9F71.key](publickey/dhi-dhi-deb-els-gpg.D46852F6925E9F71.key)               | https://dhi.io/keyring/dhi-deb-els-gpg.D46852F6925E9F71.key        |   
 
## 🚀 Getting Started

### Verifying Images and Attestations

To verify images and attestations, you can run the following commands:

```bash
# log into dhi.io
$ docker login dhi.io

# verify the signature on the image index
$ cosign verify dhi.io/alpine-base:3.22 \
  --key https://dhi.io/keyring/latest.pub \
  --experimental-oci11
```

```bash
# list all available attestations
$ regctl artifact list dhi.io/golang:1-debian12-dev \
  --platform linux/arm64

# verify the signature on any of the provided attestations
$ cosign verify dhi.io/golang@sha256:... \
  --key https://dhi.io/keyring/latest.pub \
  --experimental-oci11
```

### Installing Docker Hardened Packages

#### Alpine

##### Main Package Respository

```bash
$ cd /etc/apk/keys && curl -O https://dhi.io/keyring/dhi-apk@docker-0F81AD7700D99184.rsa.pub
$ echo "https://dhi.io/apk/alpine/v3.23/main" >> /etc/apk/repositories
$ apk update
```

##### Enterprise Package Repository

```bash
$ cd /etc/apk/keys && curl -O https://dhi.io/keyring/dhi-apk-sec@docker-0F81AD7700D99184.rsa.pub
$ echo "https://dhi.io/apk/alpine/v3.23/security" >> /etc/apk/repositories
$ apk update
```

##### ELS Package Repository

```bash
$ cd /etc/apk/keys && curl -O https://dhi.io/keyring/dhi-apk-els@docker-0F81AD7700D99184.rsa.pub
$ echo "https://dhi.io/apk/alpine/v3.23/els" >> /etc/apk/repositories
$ apk update
```

The Enterprise and ELS package repositories require authentication and DHI entitlements. 
You can authenticate using the `dhictl` by running the following command:

```bash
$ docker run -it -e HTTP_AUTH="$(dhictl auth apk)" dhi.io/alpine-base:3.23-dev
```

#### Debian

```bash
$ curl -s https://dhi.io/keyring/dhi-deb-gpg.D46852F6925E9F71.key | gpg --dearmor >> /usr/share/keyrings/docker-dhi-deb.gpg
$ echo "deb [signed-by=/usr/share/keyrings/docker-dhi-deb.gpg] https://dhi.io/deb/debian trixie main" >> /etc/apt/sources.list.d/docker-dhi.list
$ echo "deb-src [signed-by=/usr/share/keyrings/docker-dhi-deb.gpg] https://dhi.io/deb/debian trixie main" >> /etc/apt/sources.list.d/docker-dhi.list
$ apt-get update
```

## 📄 License

This project is licensed under the Apache License 2.0. See [LICENSE.txt](LICENSE.txt) for details.

## 🔗 Links

- **Docker Hardened Images Catalog**: [dhi.io](https://dhi.io)
- **Docker Hardened Images**: [docker.com/products/hardened-images](https://docker.com/products/hardened-images/)
- **Catalog Repository**: [github.com/docker-hardened-images/catalog](https://github.com/docker-hardened-images/catalog)
- **Commercial Support**: [docker.com/support](https://docker.com/support/)
- **Issue Tracker**: [GitHub Issues](https://github.com/docker-hardened-images/keyring/issues)
- **Discussions**: [GitHub Discussions](https://github.com/orgs/docker-hardened-images/discussions)

---

**Docker Hardened Images** - Building secure containers, together.
