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

Sane Curtin defaults are set in the variables, see [defaults/main.yml/curtin_defaults](./defaults/main.yml)

Variables can extended and overrided like this in variables:
```yaml
curtin_userdata_enabled:
  - image: "ubuntu_18_custom_image"

curtin_userdata_templates:
  ubuntu_18_custom_image:
    package:
      upgrade: "True"
    commands:
      early:
        - '10_foobar: ["curtin", "in-target", "--", "echo", "bar"]'
      late:
        - '20_remove_netplan_default: ["curtin", "in-target", "--", "rm", "-rf", "/etc/netplan/01-netcfg.yaml"]'
        - '30_generate_netplan_config: ["curtin", "in-target", "--", "sh", "-c", "netplan --debug generate"]'
        - '40_enable_systemd_networkd: ["curtin", "in-target", "--", "sh", "-c", "systemctl enable systemd-networkd"]'
      final:
        - '10_foobaz: ["curtin", "in-target", "--", "echo", "baz"]'
    networking:
      renderers:
        - netplan
        - eni
      interfaces:
      # cloud-init format
        network:
          version: 1
          config:
            - type: physical
              name: eth0
              mtu: 1500
              subnets:
                - type: static
                  control: auto
                  address: 192.168.10.250/24
                  gateway: 192.168.10.1
                  dns_nameservers: []
                  routes: []
            - type: nameserver
              address:
                - 192.168.10.254
              search:
                - foobar.lan
            - type: route
              destination: 10.22.98.0/24
              gateway: 192.168.10.1
              metric: 0
```

## Playbook Example

Use default configuration, means that nothing will be done.

```yaml
- hosts: localhost
  roles:
    - ansible-maas-curtin
```

## Dependencies

- ansible-maas-regiond

## Limitations

So far, this is compatible with Debian and derivatives.

## Development

Please read carefully CONTRIBUTING.md before making a merge request.

[contributing-img]: https://img.shields.io/badge/contributing--grey.svg
