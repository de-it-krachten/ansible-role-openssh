[![CI](https://github.com/de-it-krachten/ansible-role-openssh/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-openssh/actions?query=workflow%3ACI)


# ansible-role-openssh

Installs & manages OpenSSH


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

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

### vars/family-Debian.yml
<pre><code>
# list of packages
openssh_packages:
  - openssh-server
  - openssh-client

# ssh-server config file
opensshd_config: /etc/ssh/sshd_config
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'openssh'
  hosts: all
  vars:
    openssh_port: 2222
  tasks:
    - name: Include role 'openssh'
      include_role:
        name: openssh
</pre></code>
