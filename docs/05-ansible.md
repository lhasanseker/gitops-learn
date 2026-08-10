← [README'ye dön](../README.md) | [◀ Önceki: Vagrant & VirtualBox](04-vagrant-virtualbox.md)

# 5. Ansible ile Konfigürasyon Yönetimi

Vagrant VM'i "var ettikten" sonra, sunucunun içini doldurma işini **Ansible** üstlendi.

## Neden Ansible?

- **Agentless**: hedef sunucuya ek bir ajan kurmaya gerek yok, SSH yeterli.
- **Idempotent**: aynı playbook'u 10 kez çalıştırsam da sonuç değişmiyor — sadece eksik/farklı olan uygulanıyor.
- **İnsan tarafından okunabilir**: YAML formatı, ne yapıldığını kod okumadan bile anlamaya yardımcı oluyor.

## Playbook Yapım

```text
ansible/
├── inventory.ini
├── site.yml
└── roles/
    ├── docker/
    │   └── tasks/main.yml
    ├── nginx/
    │   ├── tasks/main.yml
    │   └── templates/uptime-kuma.conf.j2
    └── security/
        └── tasks/main.yml   # UFW + Fail2ban
```

Örnek bir görev (Docker kurulumu):

```yaml
- name: Docker paketini kur
  ansible.builtin.apt:
    name: docker.io
    state: present
    update_cache: true

- name: Docker servisinin çalıştığından emin ol
  ansible.builtin.service:
    name: docker
    state: started
    enabled: true
```

## Idempotency'i Neden Önemsiyorum?

GitOps zihniyetinin temel taşlarından biri **"istenen durum" (desired state)** kavramıdır. Ansible playbook'u her çalıştığında sunucuyu "olması gereken hale" getirmeye çalışır, mevcut durumdan bağımsız olarak. Bu, ileride Argo CD/Flux gibi araçların Kubernetes üzerinde yaptığı **reconciliation** mantığının basit bir ön provasıdır.

## Karşılaştığım Sorun

`apt` cache güncel olmadığında paket kurulumları bazen "not found" hatası veriyordu. Çözüm: her `apt` görevine `update_cache: true` eklemek yerine, playbook'un başında tek seferlik bir `apt update` task'ı koymak (performans açısından daha doğru yaklaşım).

---
➡️ Sonraki: [6. Docker & Nginx](06-docker-nginx.md)
