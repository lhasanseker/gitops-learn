← [README'ye dön](../README.md)

# 1. Projenin Amacı

Bu projedeki temel amacım, bir Linux sunucusunun altyapısını mümkün olduğunca **kod ile yönetmeyi** öğrenmekti.

Normalde bir sunucu kurulduğunda elle yapılması gereken işler şunlardır:

- işletim sistemi hazırlanır,
- gerekli programlar kurulur,
- Docker yüklenir,
- web sunucusu yapılandırılır,
- güvenlik ayarları yapılır,
- uygulamalar çalıştırılır.

Bunların hepsini her sunucu için elle tekrar etmek yerine, aynı işlemleri **kod ile tekrar uygulanabilir** hale getirmeyi hedefledim.

## Kurduğum Yapı

| Adım | Araç / Kavram | Ne Yaptım |
|------|----------------|-----------|
| 1 | **Vagrant** | Ubuntu sanal sunucusunun tanımını (Vagrantfile) oluşturdum |
| 2 | **VirtualBox** | Vagrant'ın altında çalışan sanallaştırma sağlayıcısı |
| 3 | **Ansible** | Sunucu yapılandırmasını playbook'larla otomatikleştirdim |
| 4 | **Docker** | Uptime Kuma'yı container içinde çalıştırdım |
| 5 | **Nginx** | Uptime Kuma'ya reverse proxy ile erişimi yönettim |
| 6 | **UFW & Fail2ban** | Temel sunucu güvenliğini uyguladım |
| 7 | **GitHub Actions** | Altyapı kodlarını kontrol eden bir CI pipeline'ı kurdum |
| 8 | **Pull tabanlı GitOps** | Git'i tek doğruluk kaynağı (single source of truth) olarak kullandım |
| 9 | **Self-healing** | Bir servis bozulduğunda otomatik ayağa kalkmasını test ettim |
| 10 | **Disaster Recovery** | Sanal sunucuyu tamamen silip sıfırdan yeniden oluşturdum |

Bu çalışma sayesinde sadece araçları kullanmayı değil, **araçların birbiriyle nasıl bağlantılı çalıştığını** anlamaya çalıştım — bu da GitOps'un asıl özüdür: her bileşen kendi işini yapar, ama hepsi Git etrafında birleşir.

## Neden Bu Notları Tuttum?

- Öğrendiğim kavramları **kendi cümlelerimle** ifade etmek, bilgiyi kalıcı hale getiriyor.
- İleride benzer bir sorunla karşılaştığımda buraya geri dönüp bakabiliyorum.
- Aynı yolda ilerleyen başka biri için bir referans/rehber niteliğinde.

---
➡️ Sonraki: [2. Genel Mimari](02-mimari.md)
