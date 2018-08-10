# Ansible

with vagrant
`cd /vagrant/ansible`

```ansible
ansible-playbook -C -i inventories/infrastructure/hosts -u deployer --vault-password-file=~/.vaultpass base.yml --limit jenkins-master -C
```

## in session variable

read -s VAULT_PASS
_Type Secret_
export VAULT_PASS

-C = dry run
-i = identity

check `vi ~/.ssh/config` make sure desired servers are allowed

ansible-playbook -i inventories/infrastructure/hosts -u deployer --vault-password-file=~/.vaultpass jenkins.yml --limit jenkins-master -C

remove -C when ready
