# ansible-k8s-node-on-premise
環境:VirtualBox  
OS:ubuntu server 2204　（osboxeのイメージで）  
https://www.osboxes.org/ubuntu-server/  

ネットワークは適当に
```
osboxes@osboxes:~$ cat /etc/netplan/00-installer-config.yaml
network:
  ethernets:
    enp0s3:
      dhcp4: true
  version: 2
```

macの公開鍵を入れて接続
```
vi ~/.ssh/authorized_keys
```

sudoがパスワードなしで実行できるように設定（ターゲットホスト側）
```
osboxes@osboxes:~$ sudo -i
[sudo] password for osboxes:
root@osboxes:~# echo "osboxes ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
```

疎通試験（Ping）
```
ansible all -i inventory.txt -m ping
```

実行
```
ansible-playbook -i inventory.txt k8s-node-setup_part.yaml
```

個別のプレイ毎に(-vは無くても)
```
ansible-playbook -i inventory.txt k8s-node-setup_part.yaml --tags "Containerd_setup" -v
```

