# Ansible-pi
Experimentation with Ansible to configure Raspberry Pi nodes from scratch

First install the latest raspbian jessie lite image from https://www.raspberrypi.org/downloads/raspbian/. 
On first boot it will resize the SD card and reboot. Watch to get the IP address and then copy in your public SSH key

```shell
ssh-copy-id pi@192.0.2.1
```
You may need to clean up any existing known-hosts entries if you've had a different machine at that IP address before.
Next, log in as 'pi' and change the default password from 'raspberry' (this also verifies that your SSH key is working
```shell
laptop $> ssh pi@192.0.2.1
pi@raspberrypi:~ $ passwd
Changing password for pi.
(current) UNIX password:
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
pi@raspberrypi:~ $ logout
Connection to 192.0.2.1 closed.
laptop $>
```

Add the IP address to your ansible hostlist

```ini
[pies]
192.0.2.1

[pies:vars]
ansible_ssh_user = pi
```

And now you should be able to ping it:
```shell
laptop $> ansible all -m ping
192.0.2.1 | SUCCESS => {
        "changed": false,
            "ping": "pong"
}
```
