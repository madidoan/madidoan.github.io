# Setting Up Wireguard for a VPN
## Pre: make sure docker is installed and use digital ocean terminal
## Make configuration directories
    mkdir -p ~/wireguard/
    mkdir -p ~/wireguard/config/
## Edit file with nano
    nano ~/wireguard/docker-compose.yml
## Enter the following (I had to change the version):
    version: '3.8'
    services:
      wireguard:
        container_name: wireguard
        image: linuxserver/wireguard
        environment:
          -   PUID=1000
          - PGID=1000
          - TZ=YOUR_TIME_ZONE
          - SERVERURL= YOUR_IP_ADDRESS
          - SERVERPORT=51820
          - PEERS=pc1,pc2,phone1
          - PEERDNS=auto
          - INTERNAL_SUBNET=10.0.0.0
        ports:
          - 51820:51820/udp
        volumes:
          - type: bind
          source: ./config/
          target: /config/
          - type: bind
          source: /lib/modules
          target: /lib/modules
        restart: always
        cap_add:
          - NET_ADMIN
          - SYS_MODULE
        sysctls:
          - net.ipv4.conf.all.src_valid_mark=1
## Save file and run Wireguard
    cd ~/wireguard/
#
    docker-compose up -d
# Find conf file and scp to local machine
# Activate wireguard
![2023-12-04](https://github.com/madidoan/madidoan.github.io/assets/124703457/ba183528-6b80-4859-a2ea-b8423101c46a)
# After activation
![2023-12-04 (2)](https://github.com/madidoan/madidoan.github.io/assets/124703457/4cf58f19-4810-4862-83c8-d9ea78c0ed29)

