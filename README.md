# MaggieBol_infra
MaggieBol Infra repository

bastion_IP = 130.193.36.41
someinternalhost_IP = 10.130.0.23

testapp_IP = 130.193.39.175
testapp_port = 9292


yc compute instance create   --name reddit-app   --hostname reddit-app   --memory=4   --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604-lts,size=10GB   --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4   --metadata serial-port-enable=1  --metadata-from-file user-data=metadata.yml

------------------------------
1. Дополнительное задание

Set jump-host configuration in /etc/ssh/ssh_config.
Example:

Host *
 User appuser
 StrictHostKeyChecking no
 IdentityFile /home/test/.ssh/appuser
 AddKeysToAgent no
 IgnoreUnknown UseKeychain
 UseKeychain yes
 ForwardAgent yes

Host bastion
 HostName 130.193.36.41
 ForwardAgent yes

Host someinternalhost
 HostName 10.130.0.23
 ProxyJump bastion

Result output:
test@test-VirtualBox:~$ ssh someinternalhost
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-142-generic x86_64)
appuser@someinternalhost:~$

---------------------------------
2. Дополнительное задание (Сертификаты)

#use certbot certonly command

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
 /etc/letsencrypt/live/130.193.36.41.sslip.io/fullchain.pem
 Your key file has been saved at:
 /etc/letsencrypt/live/130.193.36.41.sslip.io/privkey.pem
 Your certificate will expire on 2021-06-28. To obtain a new or
 tweaked version of this certificate in the future, simply run
 certbot again. To non-interactively renew *all* of your
 certificates, run "certbot renew"

# Set new SSL server cert:
pritunl set app.server_cert "$(cat /path/to/cert.pem)"

# Set new SSL server key:
pritunl set app.server_key "$(cat /path/to/privkey.pem)"
