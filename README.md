[![CI](https://github.com/de-it-krachten/ansible-role-openssh/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-openssh/actions?query=workflow%3ACI)


# ansible-role-openssh

Installs & manages OpenSSH



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS
- Fedora 39
- Fedora 40

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# OpenSSH service
openssh_service: sshd

# Default OpensSH port
openssh_port: 22

# SELinux type
openssh_setype: ssh_port_t

# dict of key/values to be configured
openssh_daemon_options:
  - key: Port
    value: "{{ openssh_port }}"
  - key: Ciphers
    value: 'aes128-ctr,aes192-ctr,aes256-ctr'
    insertafter: "# Ciphers"
  - key: KexAlgorithms
    value: ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256
    insertafter: "# Ciphers"
  - key: PermitRootLogin
    value: 'no'

# Use predefined host keys
openssh_host_keys: []
# openssh_host_keys:
#   - files/openssh/host1/ssh_host_dsa_key
#   - files/openssh/host1/ssh_host_dsa_key.pub
#   - files/openssh/host1/ssh_host_ecdsa_key
#   - files/openssh/host1/ssh_host_ecdsa_key.pub
#   - files/openssh/host1/ssh_host_ed25519_key
#   - files/openssh/host1/ssh_host_ed25519_key.pub
#   - files/openssh/host1/ssh_host_rsa_key
#   - files/openssh/host1/ssh_host_rsa_key.pub
</pre></code>

### defaults/family-Debian.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh-server
  - openssh-client

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>

### defaults/family-RedHat.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh
  - openssh-server
  - openssh-clients

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>

### defaults/family-Suse.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh
  - openssh-server
  - openssh-clients

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>

### defaults/Ubuntu-24.yml
<pre><code>
# OpenSSH service
openssh_service: ssh
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'openssh'
  hosts: all
  become: 'yes'
  vars:
    openssh_port: 2222
  tasks:
    - name: Include role 'openssh'
      ansible.builtin.include_role:
        name: openssh
</pre></code>
