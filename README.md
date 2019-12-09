gudron.wireguard_client
=======================

Ansible role for install wireguad and create client config

Instalation
-----------

Add **gudron.wireguard_client** role to your *requirements* file.

```yaml
  - src: git@github.com:gudron/gudron.wireguard_client.git
    scm: git
    version: master
```

Install roles via **ansible-galaxy** tool.

```bash
ansible-galaxy install -p roles -r requirements.yml
```

Example Playbook
----------------

    - hosts: example_vpn_server
      any_errors_fatal: "{{ any_errors_fatal | default(true) }}"
      gather_facts: yes

      roles:
        - name: gudron.wireguard_client
          vars: 
            boot_via: systemd
            interfaces:
              wg0:
                server_params:
                  address: 10.8.0.1
                  mask: 24
                  port: 51820
                  save_config: true
                peer_params:
                  address: 10.8.0.2
                  mask: 24
                  private_key: /path/to/private/key
                  public_key: /path/to/public/key
                  preshared_key: /path/to/preshared/key
                  allowed_ips:
                    - 10.8.0.2/32

              wg1:
                server_params:
                  address: 10.8.0.1
                  mask: 24
                  port: 51820
                  save_config: true
                peer_params:
                  address: 10.8.0.3
                  mask: 24
                  private_key: /path/to/private/key
                  public_key: /path/to/public/key
                  preshared_key: /path/to/preshared/key
                  allowed_ips:
                    - 10.8.0.3/32

License
-------

Apache 2.0
