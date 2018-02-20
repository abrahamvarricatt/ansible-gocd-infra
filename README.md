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

## Step 4: Create authentication file for go-server

We'll setup go-server to use file-based authentication. The authentication file
needs to be created with the following command,

```shell
$ htpasswd -B -c roles/gocd-server/files/authentication admin
```

In the above line, `admin` is the name of the user that we are creating. You'll
be asked to enter a password for the user. To add more users you need to run,

```shell
$ htpasswd -B roles/gocd-server/files/authentication next_user
```

If `htpasswd` utility is missing, on an Ubuntu system you can install it with,

```shell
$ sudo apt-get install apache2-utils
```

After gocd-server is installed, you'll need to use the GUI to setup the password
file. By default, anyone can do anything. Open up the web interface and from the
top menu select, Admin > Security > Authorization Configurations. On the new
screen select Add. For the id field type in `file_authentication` and for
password file path give `/etc/go/authentication`. Click the check button to
verify that gocd can access the file, finally click Save. You'll be asked to
login with the new credentials.

## Step 5: Run playbook!

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
