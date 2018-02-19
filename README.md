# Personal gocd infrastructure setup

Ansible playbook to manage my personal gocd systems.

```
ansible 2.4.3.0
```

## Step 1: Copy SSH private key

Copy the SSH `ansible.pem` file to the `ssh` folder.

```shell
$ cp ??/ansible.pem ssh/ansible.pem
```

## Step 2: Update inventory

Update `inventory/production.yml` to point to our webserver.

```shell
$ vim inventory/production.yml
```

## Step 3: Update Cloudflare credentails

Update `group_vars/vault/secrets.yml` with Cloudflare info.

```shell
$ vim group_vars/vault/secrets.yml
```

## Step 4: Run playbook!

To update all the systems you can run,

```shell
$ ansible-playbook gocd-infra.yml
```

To update just the server,

```shell
$ ansible-playbook gocd-server.yml
```

To update all the agents,

```shell
$ ansible-playbook gocd-agents.yml
```
