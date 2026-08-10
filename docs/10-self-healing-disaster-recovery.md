← [README'ye dön](../README.md) | [◀ Önceki: GitOps Pull Mantığı](09-gitops-pull-based.md)

# 10. Self-Healing & Disaster Recovery

## Self-Healing Testi

Bir servisin (Uptime Kuma container'ı) beklenmedik şekilde durmasını simüle ettim:

```bash
docker kill uptime-kuma
```

**Beklenti:** `restart_policy: always` sayesinde Docker, container'ı otomatik olarak yeniden başlatmalı.

**Sonuç:** Birkaç saniye içinde container tekrar `running` durumuna geçti, Uptime Kuma arayüzü erişilebilir hale geldi. Bu, sistemin **istenen durumdan (desired state) sapmayı kendi kendine düzeltmesi** anlamına geliyor — GitOps'un "self-healing" ilkesinin en basit hali.

| Test Adımı | Komut | Gözlem |
|------------|-------|--------|
| Container'ı durdur | `docker kill uptime-kuma` | Container `exited` durumuna geçti |
| Bekle | `sleep 5` | Docker restart policy tetiklendi |
| Durumu kontrol et | `docker ps` | Container tekrar `running`, uptime sıfırlandı |
| Servisi test et | `curl http://localhost:3001` | Arayüz normal şekilde yanıt verdi |

## Disaster Recovery Testi

Daha büyük bir senaryo olarak, sanal sunucuyu **tamamen sildim** ve sıfırdan yeniden oluşturdum:

```bash
vagrant destroy -f
vagrant up
ansible-playbook -i inventory.ini ansible/site.yml
```

**Amaç:** "Elimde sadece Git repository kalsa, kaç adımda ve ne kadar sürede aynı sistemi yeniden ayağa kaldırabilirim?" sorusuna cevap bulmak.

**Sonuç:** VM'in oluşturulmasından (Vagrant) yapılandırmanın tamamlanmasına (Ansible) kadar geçen süre yaklaşık **[X dakika]** sürdü ve elle hiçbir müdahale gerekmedi — tüm adımlar kod üzerinden otomatik işledi.

> ✍️ *Not: Kendi ölçtüğünüz gerçek süreyi buraya ekleyin — bu, projenizin somut bir başarı metriği olur.*

## Bu Testlerden Çıkardığım Sonuç

Bir altyapının **gerçekten IaC/GitOps ile yönetildiğini kanıtlayan en iyi test**, onu kasıtlı olarak bozmak veya yok etmektir. Eğer sistem, elle müdahale gerektirmeden veya minimum müdahaleyle kendini toparlayabiliyorsa, "kod olarak tanım" gerçekten işe yarıyor demektir. Bu prensip, production ortamlarında **chaos engineering** (örn. Netflix'in Chaos Monkey'i) pratiğinin de temelini oluşturuyor.

## Sınırlılıklar (dürüstçe not ediyorum)

- Testler tek düğümlü (single-node) bir ortamda yapıldı; çok düğümlü/dağıtık senaryolarda (örn. Kubernetes cluster) network partition, quorum kaybı gibi ek karmaşıklıklar devreye girer.
- Veri kalıcılığı (Uptime Kuma'nın geçmiş verileri) bu testte volume üzerinden korundu, ama gerçek bir felaket senaryosunda **backup/restore stratejisi** ayrıca ele alınmalı.

---
➡️ Sonraki: [11. Referans Projeler & İleri Seviye Konular](11-referans-projeler.md)
