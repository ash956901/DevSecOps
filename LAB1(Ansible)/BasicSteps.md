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
-name: Ensure directory and file exist
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

Enter password of remote machine on being asked
