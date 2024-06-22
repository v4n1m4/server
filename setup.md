## Install & Start Firewall
- dnf install firewalld
- systemctl start firewall-cmd

## Setup sub-account with wheel permission group. 
- adduser *user*
- password *user*
- usermod -aG wheel *user*

## Setup SSH-Auth-Only
- mkdir .ssh
- add ssh keys that you wish to have root access to *nano /.ssh/authorized_keys* *(dnf install nano if nano is not installedm you can also use pre-installed vi editor)*
- *mkdir /home/team/.ssh* & *nano /home/team/.ssh/authorized_keys* to add keys to the team account. 
- *nano /etc/ssh/sshd_config* and uncomment "Port", change default ssh port from "22" to an open port within port range. *PasswordAuthentication* and blank passwords set to "No". Ensure pubkey authentication is enabled and set to the /.ssh/authorized_keys file.
- ctrl+o to save on nano (:wq on vi) & *systemctl restart sshd* to restart the SSH daemon.
- Ensure that you whitelist the ssh port: *firewall-cmd --permanent --zone-public --add-port=1234/tcp* & restarted daemon *firewall-cmd --reload*
- Do not logout of your terminal. To ensure you've done this correctly, make a new tab: *ssh -p *port* root@*serverip* & *ssh -p *port* team@*serverip*. If you setup this up correctly, it will ask to add the server to known_hosts for the first time & successully sign you in to either user thereafter. 

// Documenting further hardening configurations as they're applied.
