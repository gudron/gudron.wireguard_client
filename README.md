gudron.wireguard_client
=======================

Ansible role for install wireguad and create client config

Role Variables
--------------

### General variables
  * `boot_via: string`
    Startup wireguard via init system. Supported `systemd`, `interfaces`, `manual`
    
  * `interfaces: dict` 
    The dictionary with wireguard network interfaces. Like `wg0`, `wg1`.

    * `server_params: dict` 
      Parameters of wireguard server.
      
      * `address: string` 
        Domain name or IP address of wireguard server.

      * `port: string` 
        Wireguard server port

    * `peer_params: dict` 
      Parameters of wireguard server.
      
      * `address: string` 
        Peer IP address

      * `mask: string` 
        Peer IP-mask. In short-notation like `24`.

      * `private_key: string` 
        Private key path.

      * `public_key: string` 
        Public key path.

      * `preshared_key: string` 
        Public key path.

  Full example: [defaults/main.yml](defaults/main.yml).

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
