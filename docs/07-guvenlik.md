← [README'ye dön](../README.md) | [◀ Önceki: Docker & Nginx](06-docker-nginx.md)

# 7. Sunucu Güvenliği: UFW & Fail2ban

## UFW (Uncomplicated Firewall)

Sunucuyu dışarı açmadan önce hangi portların açık olması gerektiğini netleştirdim:

| Port | Servis | Neden Açık |
|------|--------|-------------|
| 22 | SSH | Yönetim erişimi |
| 80 | HTTP | Nginx |
| 443 | HTTPS | Nginx (TLS) |

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp
ufw allow 80/tcp
ufw allow 443/tcp
ufw enable
```

**Önemli ders:** UFW'yi aktif etmeden önce SSH portunun (22) kesinlikle izinli listede olduğundan emin olmak gerekiyor — aksi halde sunucudan kendinizi dışarıda bırakabilirsiniz. Bunu Vagrant/VirtualBox test ortamında bir kez yaşayıp `vagrant reload` ile toparladım; production'da bu hata çok daha maliyetli olurdu.

## Fail2ban

Fail2ban, log dosyalarını izleyip **başarısız giriş denemelerini** tespit ederek ilgili IP'yi geçici olarak banlıyor. SSH için:

```ini
[sshd]
enabled = true
port = ssh
maxretry = 5
bantime = 1h
findtime = 10m
```

Bu ayarla, 10 dakika içinde 5 başarısız giriş denemesi yapan bir IP, 1 saat boyunca engellenmiş oluyor. Brute-force saldırılarına karşı basit ama etkili bir ilk savunma katmanı.

## Bu Katmanın GitOps'taki Yeri

Güvenlik ayarları da Ansible playbook'unun bir parçası olduğu için, **her yeni sunucu aynı güvenlik temeliyle** ayağa kalkıyor. Elle kurulumda kolayca unutulabilecek bu adımlar, kod olarak tanımlandığı için hiçbir sunucuda eksik kalmıyor.

---
➡️ Sonraki: [8. CI ile Kod Kontrolü](08-ci-cd.md)
