# homelab
Collection for reproducing my homelab setup. Contained are docker compose setups for all of my hosted applications.


### nas mounting

**cli**
```bash
sudo mount -t nfs [nas-ip]:volume1/shared /mnt/nas
```

**/etc/fstab**
```bash
[nas-ip]:/volume1/shared   /mnt/nas   nfs   defaults,_netdev   0   0
```

### adguard home setup
**ubuntu systemd resolve issue fix:**
https://adguard-dns.io/kb/adguard-home/faq/#bindinuse


### tailscale setup

https://tailscale.com/kb/1031/install-linux

- enable ip forwarding (ubuntu 24.0.4 - see tailscale docs for other versions)
```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

- run tailscale, set as exit node and configure to not override resolv.conf so adguard continues to work
```bash
sudo tailscale up \
  --advertise-routes=192.168.1.0/24 \
  --advertise-exit-node \
  --accept-dns=false
```
