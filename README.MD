# About

This is an Ansible playbook to setup a Docker powered [Buildkite](http://buildkite.com) agents. It installs and configures Docker, docker-compose and Buildkite Agent.

It includes two different playbooks;

- bootstrap.yml -> To setup users and few security updates on a fresh server
- buildkite.yml -> Setup everything else

# Requirements

1 or more servers running Ubuntu 16.04

# Configuration

There are few steps to be done before running the playbook.

- Make sure you have SSH access to root user on the server(s).
- Edit `hosts` with server ip adresses. You can add more than one.
- Update the `user_name`, `user_pass` in bootstrap.yml; use `mkpasswd --method=sha-512` to generate an encrypted password.
- Update `remote_user`(same as `user_name` from `bootstrap.yml`), `buildkite_agent_token` and `buildkite_agent_count` in `buildkite.yml`
- Generate ssh key inside ssh-keys (ssh-keygen -f ./ssh-keys/id_rsa). Add generated id_rsa.pub key to GitHub as a deploy key. Playbook uploads private key to the server.

# Running

`
# Run bootstrap playbook first
ansible-playbook bootstrap.yml -i hosts
# It will give errors related to SSH at the end because SSH has been restarted. Other than that, if everything okays run buildkite playbook
ansible-playbook buildkite.yml -i hosts
`
