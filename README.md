# ansible-role-mikrotik

Deploys a complete configuration to a MikroTik RouterOS device:

1. renders `<filespath>/<inventory_hostname>/config.rsc` (Jinja template) locally
2. uploads it and the key/certificate files to `/flash` on the device (sftp)
3. shreds the rendered file locally
4. resets the device configuration and runs `flash/config.rsc` after the reset

**Warning:** step 4 replaces the whole device configuration.

## Requirements

- collections `community.routeros`, `ansible.netcommon`
- `sshpass` on the control node
- host vars: `ansible_network_os: community.routeros.routeros`, `ansible_host`, `ansible_user`,
  `ansible_ssh_pass`

## Variables

```yaml
mikrotik:
  filespath: /srv/ansible/files/<inventory>   # contains one directory per inventory host
```

Files per host in `<filespath>/<inventory_hostname>/`: `config.rsc`, `ssh_host_rsa`, `www-ssl.key`,
`www-ssl.crt`, `ca.crt`.

## Example

```yaml
- hosts: routeros
  gather_facts: false
  roles:
    - role: ansible-role-mikrotik
```

## License

Apache-2.0

Created with the help of AI
