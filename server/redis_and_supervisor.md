# Install Redis & Supervisor
## Install Redis
```bassh
sudo apt update
sudo apt install redis-server -y
```

Setelah install, lakukan update pada conf redis.
```bash
sudo nano /etc/redis/redis.conf

# Ubah value supervised menjadi systemd
supervised systemd
```

Simpan dan restart service.
```bash
sudo systemctl restart redis-server
```

Enable service saat boot.
```bash
sudo systemctl enable redis-server
```

Test redis.
```bash
redis-cli ping
# Output: PONG
```
