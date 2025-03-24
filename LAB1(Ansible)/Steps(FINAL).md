## Steps For ansible

```sh
mkdir ansible_dir
cd ansible_dir
nano inventory.ini
```

- inventory.ini file
  
```sh
[servers]
remote_ip ansible_user=remote_user
```


```sh
nano ansible.yml
```

-ansible.yml file

```yml
- name: Jai mata di
  hosts: servers
  become: true 
  tasks:
      - name: Uptime
        command: uptime
        register: uptime_output

      - name: Display uptime
        debug: 
           msg: "UPTIME:{{uptime_output.stdout}}"
```

```sh
ssh-keygen -t rsa
ssh-copy-id remote_user_name@remote_ip
ansible-playbook -i inventory.ini ansible.yml --ask-become-pass
```
