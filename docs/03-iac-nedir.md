← [README'ye dön](../README.md) | [◀ Önceki: Genel Mimari](02-mimari.md)

# 3. Infrastructure as Code (IaC) Nedir?

**Infrastructure as Code (IaC)**, sunucu ve altyapı ayarlarının elle yapılması yerine **kod dosyalarıyla tanımlanması**dır.

## Elle Yönetim vs. IaC

**Elle (manuel) yöntemde**, yeni bir sunucu aldığımda tek tek:

- Ubuntu kurarım,
- kullanıcıları ayarlarım,
- Docker kurarım,
- Nginx kurarım,
- güvenlik ayarlarını yaparım,
- uygulamaları çalıştırırım.

Bunları elle yapmak mümkündür — ama sunucu silinirse veya aynı yapıdan başka bir sunucu kurmak istersem, **aynı işlemleri tekrar hatırlayıp tek tek yapmam gerekir.** Bu hem zaman kaybı hem de hataya açık bir süreçtir (insan faktörü, unutulan adımlar, versiyon farkları).

**IaC yaklaşımında** ise altyapının nasıl olması gerektiğini kod dosyalarında tanımlarım:

```text
Elle yapılan işlem  →  Kod dosyasında tanım
────────────────────────────────────────────
"Ubuntu 22.04 kur"  →  Vagrantfile
"Docker kur"         →  Ansible playbook / role
"Nginx yapılandır"   →  Ansible template (Jinja2)
"Port 80/443 aç"     →  UFW task (Ansible)
```

## IaC'nin Getirdiği Avantajlar

| Özellik | Açıklama |
|---------|----------|
| **Tekrarlanabilirlik** | Aynı kodu çalıştırdığımda her seferinde aynı sonucu alırım |
| **Versiyon kontrolü** | Altyapı değişiklikleri Git geçmişinde izlenebilir |
| **Hızlı kurtarma** | Sunucu bozulursa/silinirse dakikalar içinde yeniden oluşturulabilir |
| **Dokümantasyon = Kod** | Kodun kendisi, sunucunun nasıl kurulduğunun belgesidir |
| **İnsan hatasını azaltma** | Elle yapılan adımlarda unutulan/yanlış yazılan komutlar ortadan kalkar |

## İki Farklı IaC Yaklaşımı

Bu projede ikisini de kullandım, ama farklı katmanlarda:

- **Declarative (bildirimsel) – Vagrant:** "Sonuç ne olsun" tanımlanır, nasıl ulaşılacağı araca bırakılır.
- **Imperative/Declarative karışık – Ansible:** Adımlar sırayla tanımlanır ama *idempotent* çalışır (aynı playbook'u tekrar çalıştırmak sistemi bozmaz, sadece eksik olanı tamamlar).

> 💡 GitOps, aslında IaC'nin bir adım ötesidir: IaC "altyapı kod ile tanımlanır" der, GitOps ise "bu kodun **tek doğruluk kaynağı Git'tir** ve sistem sürekli bu kaynakla senkronize tutulur" der. Detay için: [`09-gitops-pull-based.md`](09-gitops-pull-based.md)

---
➡️ Sonraki: [4. Vagrant & VirtualBox](04-vagrant-virtualbox.md)
