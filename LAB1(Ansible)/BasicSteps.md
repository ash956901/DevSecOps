# BASIC STEPS TO BEGIN

## INSTALL ANSIBLE ON YOUR OS

- Ubuntu:
  
```bash
 sudo apt update
 sudo apt install software-properties-common
 sudo add-apt-repository --yes --update ppa:ansible/ansible
 sudo apt install ansible
```
- Mac:
  
```bash
  brew install ansible
```

- Windows: use wsl and run linux one

## START SSH 

```bash
sudo systemctl restart ssh
```

## CONNECT 

```bash
ssh user@remote-ip
```

user: is your remote user login ( name before @ in ubuntu terminal. In cselab3 its just cselab3)
remote-ip:ip of the remote machine you want to connect to (get this by ip a running in ubuntu)

If this step runs succesfully, then ctrl + D to get out for the next step
Else uh will have to generate keys using ssh keygen and copy them to the remote machine , also check the user and the ip

## MAKE inventory.ini and run playbook

```bash
mkdir ansible-proj
cd ansible-proj
nano inventory.ini
```

-make inventory.ini

```bash
[servers]
remoteip ansible_user=user(before @ in ubuntu terminal) 
```
- make playbook
  
```bash
 nano playbook.yml
```
- paste this there
  
```yml
- name: Ensure directory and file exist 
  hosts: servers
  become: true
  tasks:
    - name: Create directory if not exists
      file:
        path: "/home/{{ ansible_user }}/testdir"
        state: directory
        mode: '0755'

    - name: Create file if not exists
      file:
        path: "/home/{{ ansible_user }}/testdir/testfile.txt"
        state: touch
        mode: '0644'

    - name: Copy some thing
      copy: 
        dest : "/home/{{ansible_user}}/testdir/testfile.txt"
        content: "sdfkljdskljflkdsjlkfjlksdjlkfjdlsjlkjfklds"
        mode: '0644'
        force: yes 
```

- run the play book

```bash
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass
```
But after this if you get this error:(By Ankit Singh)
```bash
TASK [Gathering Facts] ************************************************************
fatal: [10.20.19.137]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: bkarthik@10.20.19.137: Permission denied (publickey,password).", "unreachable": true}

PLAY RECAP ************************************************************************
10.20.19.137               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0   
```

Then start doing these steps:
```bash
ssh-keygen -t rsa
ssh-copy-id user_name@remoteip
ssh -v user_name@remoteip
```
After this now use the previous ansible run command :)
You are ready to go.

Enter password of remote machine on being asked
