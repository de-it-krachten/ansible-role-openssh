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

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- SUSE Linux Enterprise<sup>1</sup>
- openSUSE Leap 15
- Debian 10 (Buster)<sup>1</sup>
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 37
- Fedora 38

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
  Port: "{{ openssh_port }}"

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


### vars/family-Debian.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh-server
  - openssh-client

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>

### vars/family-RedHat.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh
  - openssh-server
  - openssh-clients

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'openssh'
  hosts: all
  become: "yes"
  vars:
    openssh_port: 2222
  tasks:
    - name: Include role 'openssh'
      ansible.builtin.include_role:
        name: openssh
</pre></code>
