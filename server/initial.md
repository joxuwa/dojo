# Initial Server Setup
Connect to the server using ssh, create a new user and give sudo access and setting up basic firewall.
```sh
# Connect to server using ssh
ssh root@[YOUR_SERVER_IP]

# Create a new user and give sudo access
adduser [NEW_USERNAME]
usermod -aG sudo [NEW_USERNAME]

# Setting up basic firewall
ufw app list
ufw allow OpenSSH
ufw enable
ufw status
```
