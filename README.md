# Ansible Role : ubuntu_pro

An Ansible Role that registers and configures host with [Ubuntu Pro](https://ubuntu.com/pro).

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

`ansible-playbook -i inventory.ini -e ubuntu_pro_token=<your_token> ubuntu_pro.yml` 

with `ubuntu_pro.yml` :

```yaml
# ubuntu_pro.yml
- hosts: ubuntu_servers
  
  roles:
    - sebthebert.ubuntu_pro

```

## License

MIT / BSD

## Author Information

This role was created in October 2022 by [Sebastien Thebert](https://github.com/sebthebert).
