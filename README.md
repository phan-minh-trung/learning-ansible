# centos7-ansible
# learning-ansible

# hosts of ansible

[ubuntu-dev]
192.168.33.100 ansible_ssh_pass=vagrant ansible_ssh_user=vagrant

# try to ping all hosts

ansible all -m ping --private-key=.vagrant/machines/default/virtualbox/private_key -u vagrant

192.168.33.100 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

# ssh command

$ ssh vagrant@192.168.33.100 -i --private-key=.vagrant/machines/default/virtualbox/private_key
Warning: Identity file --private-key=.vagrant/machines/default/virtualbox/private_key not accessible: No such file or directory.
vagrant@192.168.33.100's password:  ?

# play book yml to install packages

```command
$ ansible-playbook provisioning/playbook.yml -i hosts

PLAY [Configure server] ********************************************************

TASK [setup] *******************************************************************
ok: [192.168.33.100]
TASK [java : Package are present] **********************************************
changed: [192.168.33.100] => (item=packages)
TASK [docker : Add Docker repository and update apt cache] *********************
changed: [192.168.33.100]
TASK [docker : Docker is present] **********************************************
changed: [192.168.33.100]
TASK [docker : Python-pip is present] ******************************************
changed: [192.168.33.100]
TASK [docker : Debian docker-py is present] ************************************
changed: [192.168.33.100]

TASK [docker : Files are present] **********************************************
changed: [192.168.33.100]

TASK [docker : Docker service is restarted] ************************************
changed: [192.168.33.100]

TASK [git : install git] *******************************************************
ok: [192.168.33.100]

TASK [install packages] ********************************************************
changed: [192.168.33.100] => (item=[u'mcrypt', u'nginx', u'php5-cli', u'php5-curl', u'php5-fpm', u'php5-intl', u'php5-json', u'php5-mcrypt', u'php5-sqlite', u'sqlite3'])

PLAY RECAP *********************************************************************
192.168.33.100             : ok=10   changed=8    unreachable=0    failed=0
```

h3. install Jenkins role from remote repo

# install Jenkins role

ansible-galaxy install geerlingguy.jenkins -p ./roles/

$ add this role to your playbook:

roles:
    - git
    - geerlingguy.jenkins



