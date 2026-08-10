← [README'ye dön](../README.md) | [◀ Önceki: IaC Nedir?](03-iac-nedir.md)

# 4. Vagrant & VirtualBox

## Vagrant Ne İşe Yarar?

Vagrant, sanal makineleri **kod ile tanımlamamı ve yönetmemi** sağlayan bir araç. Bir `Vagrantfile` içinde:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "gitops-node"
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end
end
```

tanımını yaptım. `vagrant up` komutu ile bu tanım okunur ve VirtualBox üzerinde otomatik olarak bir Ubuntu sunucusu ayağa kalkar.

## VirtualBox'ın Rolü

VirtualBox, Vagrant'ın **arkasında çalışan gerçek hypervisor**. Vagrant kendisi VM oluşturmaz; VirtualBox'a (veya VMware, Hyper-V, libvirt gibi başka bir "provider"a) talimat verir. Bu ayrım önemli çünkü:

- Vagrant = **orkestrasyon / tanım katmanı**
- VirtualBox = **sanallaştırma / yürütme katmanı**

## Öğrendiğim Pratik Komutlar

| Komut | Ne Yapar |
|-------|----------|
| `vagrant up` | VM'i tanıma göre oluşturur/başlatır |
| `vagrant ssh` | VM'e SSH ile bağlanır |
| `vagrant halt` | VM'i kapatır (diski korur) |
| `vagrant destroy` | VM'i tamamen siler |
| `vagrant reload --provision` | VM'i yeniden başlatıp provizyon adımlarını tekrar çalıştırır |

## Karşılaştığım Sorun

İlk kurulumda private network IP'si host makinedeki başka bir sanal adaptörle çakıştı ve VM ağa çıkamadı. Çözüm: `VBoxManage list hostonlyifs` ile mevcut host-only network'leri listeleyip çakışmayan bir IP aralığı seçmek oldu.

---
➡️ Sonraki: [5. Ansible ile Konfigürasyon](05-ansible.md)
