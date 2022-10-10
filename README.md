# Ansible Role : ubuntu_pro

An Ansible Role that registers host on [Ubuntu Pro](https://ubuntu.com/pro).

## Requirements

Ansible Pro is only available for every Ubuntu LTS releases from 16.04 LTS.

## Roles Variables

The only mandatory variable for this role is `ubuntu_pro_token`.

```yaml
ubuntu_pro_token: <ubuntu_pro_token>
```

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