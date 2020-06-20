# Ansible Role: molecule

Ansible role for installing [`molecule`](https://molecule.readthedocs.io/) into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-molecule.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-molecule)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                           | Description                                                                   | Default Value        |
|------------------------------------|-------------------------------------------------------------------------------|----------------------|
| `molecule_version`                 | Use a specific version of molecule, eg. `2.22.0`. Specify `false` for latest. | `false`              |
| `molecule_install_dir`             | Installation directory to put molecule virtual environments.                  | `$HOME/.virtualenvs` |
| `molecule_current_dirname`         | Name for the currently active molecule Virtualenv.                            | molecule             |
| `molecule_venv_site_packages`      | Allow venv to inherit packages from global site-packages.                     | `false`              |
| `molecule_install_venv_helper`     | Install a venv helper to launch venv executables from a "bin" directory.      | `true`               |
| `molecule_bin_dir`                 | "bin" directory to install venv-helpers to.                                   | `$HOME/bin`          |
| `molecule_install_os_dependencies` | Allow role to install OS dependencies.                                        | `false`              |
| `molecule_python3_path`            | Specify a path to a specific python version to use in virtualenv.             | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: molecule_hosts
  roles:
     - { role: xanmanning.molecule, molecule_version: 2.22.0 }
```

Example playbook for installing the latest molecule version globally:

```yaml
---
- hosts: molecule_hosts
  become: true
  vars:
    molecule_install_os_dependencies: true
    molecule_install_dir: /opt/molecule/bin
    molecule_bin_dir: /usr/bin
    molecule_current_dirname: current
  roles:
    - role: xanmanning.molecule
```

### Activating the molecule venv

You need to activate the python3 virtual environment to be able to access `az`.
This is done as per the below:

```bash
source {{ molecule_install_dir }}/{{ molecule_current_dirname }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/molecule/bin/current/bin/activate
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
