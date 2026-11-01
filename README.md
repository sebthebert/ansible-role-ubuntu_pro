# Ansible Role : ubuntu_pro

An Ansible Role that registers and configures host with [Ubuntu Pro](https://ubuntu.com/pro).

[![OpenSSF Baseline](https://www.bestpractices.dev/projects/14663/baseline)](https://www.bestpractices.dev/projects/14663)

## Requirements

This role uses [Role Argument Validation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#role-argument-validation) introduced with **Ansible 2.11**.

Ubuntu Pro is only available for every **Ubuntu LTS releases from 16.04 LTS**.

## Roles Variables

The only mandatory variable is `ubuntu_pro_token`.

| Variable                                   | Description                      | Type   | Mandatory | Default Value |
|--------------------------------------------|----------------------------------|--------|-----------|---------------|
| `ubuntu_pro_token`                         | Ubuntu Pro token                 | String | YES       | None          |
||||||
| `ubuntu_pro_config.http_proxy`             | HTTP Proxy                       | String | NO        | None          |
| `ubuntu_pro_config.http_proxy`             | HTTPS Proxy                      | String | NO        | None          |
| `ubuntu_pro_config.apt_http_proxy`         | APT HTTP Proxy                   | String | NO        | None          |
| `ubuntu_pro_config.apt_https_proxy`        | APT HTTPS Proxy                  | String | NO        | None          |
| `ubuntu_pro_config.ua_apt_http_proxy`      | UA APT HTTP Proxy                | String | NO        | None          |
| `ubuntu_pro_config.ua_apt_https_proxy`     | UA APT HTTPS Proxy               | String | NO        | None          |
| `ubuntu_pro_config.global_apt_http_proxy`  | Global APT HTTP Proxy            | String | NO        | None          |
| `ubuntu_pro_config.global_apt_https_proxy` | Global APT HTTPS Proxy           | String | NO        | None          |
| `ubuntu_pro_config.update_messaging_timer` | Update Messaging Timer           | Int    | NO        | `21600`       |
| `ubuntu_pro_config.update_status_timer`    | Update Status Timer              | Int    | NO        | `43200`       |
| `ubuntu_pro_config.metering_timer`         | Metering Timer                   | Int    | NO        | `14400`       |

You can find more information about `ubuntu_pro_config.*` variables on [Ubuntu Pro Client README](https://github.com/canonical/ubuntu-advantage-client#readme).

## Dependencies

None.

## Example Playbook

```shell
ansible-playbook -i inventory.ini -e ubuntu_pro_token=<your_token> ubuntu_pro.yml
```

with `ubuntu_pro.yml` :

```yaml
# ubuntu_pro.yml
- hosts: ubuntu_servers
  
  roles:
    - sebthebert.ubuntu_pro
```

## Docker Test Matrix

The [tests/docker-compose.yml](tests/docker-compose.yml) file defines test containers for **every supported Ubuntu LTS release from 16.04 through 26.04**.

```shell
docker compose -f tests/docker-compose.yml build
docker compose -f tests/docker-compose.yml up --detach
```

The container hostnames are `ubuntu1604`, `ubuntu1804`, `ubuntu2004`, `ubuntu2204`, `ubuntu2404`, and `ubuntu2604`.

Stop and remove the test containers with `docker compose -f tests/docker-compose.yml down`.

The test playbook uses the Docker connection plugin. From the repository root, prepare the test virtualenv with Python 3.9 using `uv`, then install the required Ansible collection:

```shell
uv python install 3.9
rm -rf tests/.venv-ansible-tests
uv venv --python 3.9 tests/.venv-ansible-tests
. tests/.venv-ansible-tests/bin/activate
uv pip install --python tests/.venv-ansible-tests/bin/python -r tests/requirements.txt
tests/.venv-ansible-tests/bin/python --version  # should report Python 3.9.x
tests/.venv-ansible-tests/bin/ansible --version  # should report Ansible Core 2.12.x
tests/.venv-ansible-tests/bin/ansible-galaxy collection install -r tests/requirements.yml
```

Set an Ubuntu Pro token, start the test containers, and launch the playbook while the virtualenv is active:

```shell
export UBUNTU_PRO_TOKEN=<your_ubuntu_pro_token>

docker compose -f tests/docker-compose.yml build

docker compose -f tests/docker-compose.yml up --detach

ANSIBLE_ROLES_PATH="$PWD" tests/.venv-ansible-tests/bin/ansible-playbook -i tests/inventory.yml tests/playbook.yml
```

The test controller is pinned to **Ansible Core 2.12 because Ubuntu 16.04 uses Python 3.5**, which is not supported by newer Ansible module wrappers.

Deactivate the virtualenv after testing with `deactivate`.

## License

MIT / BSD

## Author Information

This role was created in October 2022 by [Sebastien Thebert](https://github.com/sebthebert).
