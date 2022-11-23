# k3d (Ansible Role)

[![CI](https://github.com/averagebit/ansible-role-k3d/workflows/CI/badge.svg?event=push)](https://github.com/averagebit/ansible-role-k3d/actions?query=workflow%3ACI)

## Description

Ansible role to install [k3d](https://github.com/k3d-io/k3d").

## Requirements

The role was developed and tested with the following Ansible versions.

| Name                                                   | Version     |
| ------------------------------------------------------ | ----------- |
| [ansible](https://pypi.org/project/ansible-base/)      | `>= 2.9.13` |
| [ansible-base](https://pypi.org/project/ansible-base/) | `>= 2.10.1` |
| [ansible-core](https://pypi.org/project/ansible-core/) | `>= 2.11.2` |

## Platforms

The role was tested on the following distributions and releases.

| Name   | Version |
| ------ | ------- |
| Ubuntu | `jammy` |

## Installation

`ansible-galaxy install averagebit.k3d` will install the latest
stable release.

`ansible-galaxy install -r requirements.yml` will install the role
from a requirements file.

```yaml
# requirements.yml
---
roles:
  - name: averagebit.k3d
    version: 1.0.0
```

## Variables

- `k3d_os`
  - Default: `"linux"`
  - Description: The OS target for the binary.
- `k3d_version`
  - Default: `"latest"`
  - Description: The version of the binary can be a specific version such as: `"5.4.6"`.
- `k3d_owner`
  - Default: `"root"`
  - Description: The owner of the installed binary.
- `k3d_group`
  - Default: `"root"`
  - Description: The group of the installed binary.
- `k3d_mode`
  - Default: `"0755"`
  - Description: The permissions of the installed binary.
- `k3d_bin_dir_mode`
  - Default: `"0755"`
  - Description: The permissions of the binary directory.
- `k3d_bin_dir`
  - Default: `"/usr/local/share/k3d"`
  - Description: The directory to install the binary in.
- `k3d_bin_path`
  - Default: `"{{ k3d_bin_dir }}/k3d"`
  - Description: The full path to the binary.
- `k3d_link_path`
  - Default: `"/usr/local/bin/k3d"`
  - Description: The symlink path created to the binary.
- `k3d_repo_url`
  - Default: `"https://github.com/k3d-io/k3d"`
  - Description: The URL to the repository.
- `k3d_file_url`
  - Default: `"{{ k3d_repo_url }}/releases/download/v{{ k3d_version }}/k3d-{{ k3d_os }}-{{ k3d_architecture }}"`
  - Description: The URL to the file.
- `k3d_version_url`
  - Default: `"https://api.github.com/repos/k3d-io/k3d/releases/latest"`
  - Description: The URL to fetch the latest version from.
- `k3d_checksum_url`
  - Default: `n/a` - see https://github.com/k3d-io/k3d/issues/1048
  - Description: The URL to the checksum of the file.
- `k3d_architecture`
  - Default: `"{{ k3d_architecture_map[ansible_architecture] }}"`
  - Description: The architecture target for the binary.
- `k3d_architecture_map`
  - Default: `{"aarch": "arm64", "aarch64": "arm64", "amd64": "amd64", "arm64": "arm64", "armhf": "armhf", "armv7l": "armhf", "ppc64le": "ppc64le", "s390x": "s390x", "x86_64": "amd64"}`
  - Description: The architecture map used to set the correct name
    according to the repository binary naming.

## Usage

```yaml
# playbook.yml
- hosts: servers
  roles:
    - role: averagebit.k3d
      become: true # required unless specified at the playbooks top level
      tags: k3d # (optional) convenience tag
  vars:
    - k3d_version: latest # or a specific version such as: 5.4.6
```

## Legal

Copyright 2022 averagebit <[averagebit@pm.me](mailto:averagebit@pm.me)>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY k3d, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
