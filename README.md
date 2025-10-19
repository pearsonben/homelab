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