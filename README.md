# PiHole-VPN
Deploy your own Ad-blocking VPN  
Script for automating [Pi-Hole](pi-hole.net) and [HWDSL2/IPSec VPN Docker](https://github.com/hwdsl2/docker-ipsec-vpn-server)

# Step
1. Spin up a vps (Use a VPS with a static IP)
2. Install docker [here](https://docs.docker.com/engine/install/ubuntu/)
3. (Optional) Run post installation step [here](https://docs.docker.com/engine/install/linux-postinstall/)
4. Clone this github
5. Run these commands as root (`sudo su`)
```
systemctl disable systemd-resolved.service
systemctl stop systemd-resolved
nano /etc/resolv.conf
```
6. Change the content to
```
nameserver 127.0.0.1
```
7. Create the containers
```
docker compose up
```
8. Done
```
# Access pi-hole url in http://[vps_public_ip]/admin
```

# Manage IKEv2 Clients
## List clients
```
docker exec -it ipsec-vpn-server ikev2.sh --listclients
```
## Create new client
```
docker exec -it hwdsl2-vpn ikev2.sh --addclient [client name]
docker cp hwdsl2-vpn:/etc/ipsec.d/[client name].p12 ./
```
