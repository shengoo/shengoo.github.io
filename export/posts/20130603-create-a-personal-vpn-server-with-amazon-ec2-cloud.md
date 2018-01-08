title: Create a Personal VPN Server with Amazon EC2 Cloud
link: http://www.sheng00.com/581.html
author: admin
description: 
post_id: 581
created: 2013/06/03 23:06:02
created_gmt: 2013/06/03 15:06:02
comment_status: open
post_name: create-a-personal-vpn-server-with-amazon-ec2-cloud
status: publish
post_type: post

<!--Create a Personal VPN Server with Amazon EC2 Cloud-->

# Create a Personal VPN Server with Amazon EC2 Cloud

`# sudo apt-get install pptpd # sudo vi /etc/pptpd.conf : uncomnt remote put on local put private IP > local # sudo vi /etc/ppp/pptpd-options : uncomnt ms-dns add google # sudo vi /etc/sysctl.conf : uncomnt net.ipv4.ip_forward=1 # sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE # sudo vi /etc/rc.local : paste iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE # sudo vi /etc/ppp/chap-secrets`