---
published: false
---
## Copy file through scp PHP

Предварительно установить библиотеку:
[PHP script using ssh2_scp_send Fails to create remote file](https://stackoverflow.com/questions/35331318/php-script-using-ssh2-scp-send-fails-to-create-remote-file "PHP script using ssh2_scp_send Fails to create remote file")

```
$connection = ssh2_connect('host', 22);
ssh2_auth_password($connection, 'user', 'passwd');

ssh2_scp_send($connection, '/var/tmp/README.md', '/home/README.md', 0777);
```


