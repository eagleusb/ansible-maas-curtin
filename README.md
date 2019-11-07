# ansible-maas-curtin

[![contributing][contributing-img]](CONTRIBUTING.md)

1. [Overview](#overview)
1. [Description](#description)
1. [Requirements](#requirements)
1. [Setup](#setup)
1. [Role Variables](#role-variables)
1. [Playbook Example](#playbook-example)
1. [Dependencies](#dependencies)
1. [Limitations](#limitations)
1. [Development](#development)

## Overview

[MAAS](https://maas.io/docs/what-is-maas) is Metal As A Service. It lets you treat physical servers like virtual machines (instances)
in the cloud. Rather than having to manage each server individually, MAAS turns your bare metal
into an elastic cloud-like resource.

## Description

This role install and configure [Curtin installer](https://curtin.readthedocs.io/en/latest/)
specifically for MAAS usage.

## Requirements

- [ansible-maas-regiond](https://github.com/eagleusb/ansible-maas-regiond)

## Setup

Use `ansible-galaxy` or download the role in your `roles` directory.

## Role Variables

```yaml
```

## Playbook Example

Use default configuration, means that nothing will be done.

```yaml
- hosts: localhost
  roles:
    - ansible-maas-curtin
```

## Dependencies

None.

## Limitations

So far, this is compatible with Debian and derivatives.

## Development

Please read carefully CONTRIBUTING.md before making a merge request.

[contributing-img]: https://img.shields.io/badge/contributing--grey.svg
