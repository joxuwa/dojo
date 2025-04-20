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

## Install Supervisor
```bassh
sudo apt update
sudo apt install supervisor -y
```

Setelah install, buat config baru. Ubah **[app_name]** dan juga **[app_container]**.
```bash
sudo nano /etc/supervisor/conf.d/[app_name]-worker.conf

# [app_name]-worker.conf
[program:[app_name]-worker]
process_name=%(program_name)s_%(process_num)02d
command=docker exec [app_container] php artisan queue:work redis --sleep=3 --tries=3
autostart=true
autorestart=true
numprocs=1
user=root
redirect_stderr=true
stdout_logfile=/var/log/supervisor/[app_name]-worker.log
```

Simpan dan reload.
```bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start [app_name]-worker:*
```
