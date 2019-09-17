# Ansible-AWS-EC2

### Work-Flow

**1)**

```
[hkothari@hema-linux Ansible(EC2)]$ ansible -i /deploy/hosts all -m ping -e 'ansible_python_interpreter=/usr/bin/python3'
ec2-instance | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
[hkothari@hema-linux Ansible(EC2)]$ 
```

**2)**

**Error:**

```
[hkothari@hema-linux Ansible(EC2)]$ ansible-playbook deploy/java_install.yml -e 'ansible_python_interpreter=/usr/bin/python3'

PLAY [prod] *****************************************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************************
ok: [ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com]

TASK [Update and upgrade apt packages] **************************************************************************************************************************************
fatal: [ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com]: FAILED! => {"changed": false, "failed": true, "module_stderr": "Shared connection to ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com closed.\r\n", "module_stdout": "\r\n  File \"/tmp/ansible_t_ewfta6/ansible_module_apt.py\", line 382\r\n    except Exception, e:\r\n                    ^\r\nSyntaxError: invalid syntax\r\n", "msg": "MODULE FAILURE", "rc": 0}
	to retry, use: --limit @/home/hkothari/Desktop/Muruga/Everest/Ansible(EC2)/deploy/java_install.retry

PLAY RECAP ******************************************************************************************************************************************************************
ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com : ok=1    changed=0    unreachable=0    failed=1   

[hkothari@hema-linux Ansible(EC2)]$
```


**Changed python version in command**

```
[hkothari@hema-linux Ansible(EC2)]$ ansible-playbook deploy/java_install.yml -e 'ansible_python_interpreter=/usr/bin/python2.7'

PLAY [prod] *****************************************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************************
ok: [ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com]

TASK [Update and upgrade apt packages] **************************************************************************************************************************************
ok: [ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com]

TASK [Install jdk] **********************************************************************************************************************************************************
ok: [ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com]

PLAY RECAP ******************************************************************************************************************************************************************
ec2-3-0-92-33.ap-southeast-1.compute.amazonaws.com : ok=3    changed=0    unreachable=0    failed=0   

[hkothari@hema-linux Ansible(EC2)]$ 
```
**Installed python-pip**
```bash
[hkothari@hema-linux Ansible(EC2)]$ ansible-playbook deploy/google_keep_main.yml -e 'ansible_python_interpreter=/usr/bin/python2'
 [WARNING]: Ignoring invalid attribute: restarted


PLAY [prod] ************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************
fatal: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]: FAILED! => {"changed": false, "failed": true, "module_stderr": "Shared connection to ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com closed.\r\n", "module_stdout": "\r\n/bin/sh: 1: /usr/bin/python2: not found\r\n", "msg": "MODULE FAILURE", "rc": 0}
        to retry, use: --limit @/home/hkothari/Desktop/Muruga/Everest/Ansible(EC2)/deploy/google_keep_main.retry

[hkothari@hema-linux Ansible(EC2)]$ 

```
```bash
[hkothari@hema-linux Ansible(EC2)]$ ansible-playbook deploy/google_keep_main.yml -e 'ansible_python_interpreter=/usr/bin/python2.7'
 [WARNING]: Ignoring invalid attribute: restarted


PLAY [prod] ************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************
ok: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Set release variable] ********************************************************************************************************************************************************
ok: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Retrieve current release folder] *********************************************************************************************************************************************
changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Create new folder for new release] *******************************************************************************************************************************************
changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Copy Private Key] ************************************************************************************************************************************************************
ok: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Clone the repository] ********************************************************************************************************************************************************
changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Update and upgrade apt packages] *********************************************************************************************************************************************
changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

TASK [Install docker] **************************************************************************************************************************************************************
changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com] => (item=[u'docker.io', u'docker-compose'])

TASK [Run docker compose] **********************************************************************************************************************************************************

changed: [ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com]

PLAY RECAP *************************************************************************************************************************************************************************
ec2-52-76-140-63.ap-southeast-1.compute.amazonaws.com : ok=9    changed=6    unreachable=0    failed=0   

[hkothari@hema-linux Ansible(EC2)]$

```