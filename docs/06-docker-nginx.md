← [README'ye dön](../README.md) | [◀ Önceki: Ansible](05-ansible.md)

# 6. Docker & Nginx

## Uptime Kuma'yı Container İçinde Çalıştırma

**Uptime Kuma**, servislerin ayakta olup olmadığını izleyen açık kaynak bir monitoring aracı. Bunu doğrudan sunucuya kurmak yerine **Docker container** içinde çalıştırdım çünkü:

- İzole bir ortamda çalışır, host sistemi kirletmez.
- Güncelleme/geri alma tek bir `docker pull` + `docker run` kadar basit.
- Ansible ile "container çalışıyor mu" kontrolü, paket kurulu mu kontrolünden daha güvenilir.

```yaml
- name: Uptime Kuma container'ını çalıştır
  community.docker.docker_container:
    name: uptime-kuma
    image: louislam/uptime-kuma:1
    restart_policy: always
    ports:
      - "3001:3001"
    volumes:
      - uptime-kuma-data:/app/data
```

`restart_policy: always` burada kritik — sunucu yeniden başladığında veya container çökerse Docker'ın kendisi container'ı otomatik ayağa kaldırıyor. Bu, ileride bahsedeceğim [self-healing](10-self-healing-disaster-recovery.md) davranışının en temel seviyesi.

## Nginx ile Reverse Proxy

Uptime Kuma'yı doğrudan `3001` portundan dışarı açmak yerine **Nginx**'i önüne koydum:

```nginx
server {
    listen 80;
    server_name status.example.local;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

Bunu neden yaptım:

- **Tek giriş noktası**: ileride başka servisler eklesem hepsi 80/443 üzerinden, path veya subdomain bazlı yönlendirilebilir.
- **WebSocket desteği**: Uptime Kuma canlı güncellemeler için WebSocket kullanıyor; `Upgrade`/`Connection` header'ları olmadan arayüz donuk kalıyordu — bu, karşılaştığım ve çözdüğüm bir sorundu.
- **SSL termination noktası**: TLS sertifikasını (Let's Encrypt) tek bir yerden yönetmek mümkün oluyor.

---
➡️ Sonraki: [7. Sunucu Güvenliği](07-guvenlik.md)
