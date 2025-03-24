# Some observations

## inventory.ini FILE LAYOUT

```ini
[servers]
172.1.58.96 ansible_user=cselab3 ansible_ssh_pass=cselab3

[all:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

- the 96 is the remote system ip btw

## SSHPASS ERROR

```bash
172.1.58.95 | FAILED! => {
    "msg": "to use the 'ssh' connection type with passwords, you must install the sshpass program"
}
```

- if you get this error on running  ansible -i inventory.ini servers -m ping , execute this and it will go away 

```bash
sudo apt-get install sshpass
```



## PASSWORD FLAG FOR ANSIBLE COMMAND TO EXECUTE SCRIPT

```bash
ansible-playbook -i inventory.ini uptime_check.yml -K
```

- add -K flag here so that password access is on , when asked enter cselab3 

## SUDO PASSWORD ERROR

- Use the flag --ask-become-pass while running playbook if u get the following error:

```bash
fatal: [10.20.9.51]: FAILED! => {"msg": "Missing sudo password"}
```

```bash
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass
```

## CREATE DIR FILES , INSIDE CREATE custom_index.html

```bash
mkdir files
cd files
touch index.html
nano index.html
```

- Copy this content inside it 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to My Nginx Server</title>
</head>
<body>
    <h1>Welcome to Nginx!</h1>
    <p>Your custom index page is successfully deployed.</p>
</body>
</html>
```

