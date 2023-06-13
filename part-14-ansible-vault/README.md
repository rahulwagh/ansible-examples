
## SSH to EC2 instance

```
ssh -i /Users/rahulwagh/.ssh/aws_ec2_terraform ubuntu@18.198.3.146
```

## 1. Ansible vault Commands

### a. Create new vault

```bash
ansible-vault create group_vars/my_vault.yml
```

Set the password for the vault 

```yaml
my_message: "This is test message from vault"
```

You can't view the file if you run the following command

```bash
cat groups_vars/my_vault.yml 
```

### b. Edit the encrypted file 


```bash
ansible-vault edit group_vars/my_vault.yml
```

Enter the password for the vault


### c. View the encrypted file

```bash
ansible-vault view group_vars/my_vault.yml 
```

### d. Encrypt existing file

```bash
ansible-vault encrypt group_vars/plain_text_secret_file.txt 
```
Set the password for the vault

<br/>

## 2. Run the playbook with vault using `--ask-vault-pass`

### a. Run the playbook
```bash
# Vault file - my_vault.yml
ansible-playbook --inventory inventory/ansible-vault/hosts ansible-vault-playbook.yml -e @group_vars/my_vault.yml --ask-vault-pass
```
`-e @group_vars/my_vault.yml` - associate extra variables to the playbook

<br/>

## 3. Encrypting the vault with base64 generated password

### a. Generate the base64 password file `pass_file/ansible-vault.pass`
```
openssl rand -base64 2048 > pass_file/ansible-vault.pass
```


### b. Create vault with `pass_file/ansible-vault.pass`

```bash
ansible-vault create group_vars/my_vault_with_bas64_pass.yml --vault-password-file=pass_file/ansible-vault.pass
```

### c. View the content of the vault with pass file 

```bash
ansible-vault view group_vars/my_vault_with_bas64_pass.yml --vault-password-file=pass_file/ansible-vault.pass
```

``` 
# Vault file - my_vault_with_bas64_pass.yml
ansible-playbook --inventory inventory/ansible-vault/hosts ansible-vault-playbook.yml -e @group_vars/my_vault_with_bas64_pass.yml --vault-password-file=pass_file/ansible-vault.pass
```

<br/>

## 3. Reading the ansible password from the environment variable - `ANSIBLE_VAULT_PASSWORD_FILE`

a. Set the following the `Environment Variable` - 

```bash
export ANSIBLE_VAULT_PASSWORD_FILE=/Users/rahulwagh/Documents/Documents-Rahul-MacBook-Pro/jhooq/ansible-examples/part-14-ansible-vault/pass_file/ansible-vault.pass
```


b. Run the playbook 

```bash
ansible-playbook --inventory inventory/ansible-vault/hosts ansible-vault-playbook.yml -e @group_vars/my_vault_with_bas64_pass.yml
```

Reference - https://gist.github.com/xoyabc/4ab27d181808affa6450ee481e0ff9b2
