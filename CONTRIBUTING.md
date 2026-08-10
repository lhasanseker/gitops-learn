# Katkıda Bulunma Rehberi

Bu repo öncelikle kişisel bir öğrenme günlüğü olsa da, düzeltme ve önerilere açığım. 🙌

## Nasıl Katkıda Bulunabilirsiniz?

1. **Yazım/anlatım hatası** gördüyseniz → doğrudan bir issue açın veya küçük bir PR gönderin.
2. **Eksik/yanlış bir teknik detay** fark ettiyseniz → lütfen kaynak da paylaşın (resmi dokümantasyon, güvenilir makale vb.).
3. **Yeni bir konu önerisi** (örn. "Sealed Secrets üzerine bir bölüm eklenebilir") → issue şablonlarından `Doküman önerisi`ni kullanın.

## Pull Request Süreci

1. Repoyu fork'layın ve bir branch açın: `docs/konu-adi` veya `fix/kisa-aciklama`
2. Değişikliğinizi yapın.
3. `examples/` altında bir YAML değiştiyseniz, mümkünse yerel olarak doğrulayın:
   ```bash
   kustomize build examples/kustomize/overlays/dev
   yamllint examples/
   ```
4. PR açarken **neyi neden değiştirdiğinizi** kısaca özetleyin.
5. CI (markdown lint, link check, yaml validate) yeşil olmalı.

## Stil Rehberi

- Türkçe yazım kurallarına uyun; teknik terimleri (GitOps, reconciliation, drift vb.) olduğu gibi bırakmak, çevirmeye çalışmaktan daha anlaşılır.
- Her `docs/*.md` dosyası, önceki/sonraki bölüme bağlantı vermeli (dosyaların en üst ve en alt kısmına bakın).
- Kod blokları için dil belirtimini unutmayın (` ```yaml `, ` ```bash ` vb.).

Katkınız için şimdiden teşekkürler!
