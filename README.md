## Ansible Role Create Users
# This role is to manage users specifically on linux. Manage users in the user list config file. 
# Features include: adding users with specific uids, change passwords, lock and unlock user accounts, manage sudo access, add ssh keys based on authentication, set users primary group, gid, add user to specific group, create groups. 

# Ansible group is set for a server in the inventory file. 

# Prerequisites:
- Install Ansible
- Create keys
- ssh to client to add entry to known hosts file
- configure client server authorized keys

## Use Ansible-Vault 

cat vars/secret

ansible-vault encrypt vars/secret

ansible-vault edit vars/secret

vi .vaultpass
-Enter password for Ansible vault

chmod 600 .vaultpass

vi ansible.cfg * add the following lines
[defaults]
vault_password_file= ./.vaultpass

## Make sure to add the following to your .gitignore file

vi .gitignore
.vaultpass
.retry
.secret
*.secret

## Generting a password

on Ubuntu install whois package
mkpasswd --method=SHA-512

on REDHAT -Use Python

python -c 'import crypt,getpass; print(crypt(getpass.getpass(), crypt.mksalt(crypt.METHOD_SHA512)))'

##Example Playbook Create-User.yml

---
- hosts:'{{inventory}}'
  vars_files:
    - vars/secret
  become: yes
  roles: 
  - create-users

