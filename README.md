\# GitOps \& IaC Öğrenme Notlarım



Bu repository, geliştirdiğim \*\*GitOps \& Infrastructure as Code (IaC)\*\* projesinde

öğrendiğim kavramları kendi cümlelerimle açıklamak ve öğrenme sürecimi

belgelemek amacıyla hazırlanmıştır.



Bu repo çalışan projenin kendisi değildir.  

Burada projenin nasıl çalıştığını, kullandığım teknolojilerin ne işe yaradığını,

karşılaştığım sorunları ve yaptığım testleri notlarım şeklinde açıklıyorum.



\## Çalışan Proje



Uygulamasını yaptığım asıl proje:



\*\*\[gitops-iac-project](https://github.com/lhasanseker/gitops-iac-project)\*\*



\---



\# 1. Projenin Amacı



Bu projedeki temel amacım bir Linux sunucusunun altyapısını mümkün olduğunca

kod ile yönetmeyi öğrenmekti.



Normalde bir sunucu kurulduğunda:



\- işletim sistemi hazırlanır,

\- gerekli programlar kurulur,

\- Docker yüklenir,

\- web sunucusu yapılandırılır,

\- güvenlik ayarları yapılır,

\- uygulamalar çalıştırılır.



Bunların hepsini her sunucu için elle yapmak yerine,

aynı işlemleri kod ile tekrar uygulanabilir hale getirmeyi öğrendim.



Projede genel olarak şu yapıyı kurdum:



1\. \*\*Vagrant\*\* ile Ubuntu sanal sunucusunun nasıl oluşturulacağını tanımladım.

2\. \*\*VirtualBox\*\* üzerinde Ubuntu sanal makinesi çalıştırdım.

3\. \*\*Ansible\*\* ile sunucunun yapılandırılmasını otomatikleştirdim.

4\. \*\*Docker\*\* kullanarak Uptime Kuma'yı container içerisinde çalıştırdım.

5\. \*\*Nginx\*\* ile Uptime Kuma'ya erişimi yönettim.

6\. \*\*UFW ve Fail2ban\*\* ile temel sunucu güvenliği uyguladım.

7\. \*\*GitHub Actions\*\* ile altyapı kodlarını kontrol eden CI sistemi oluşturdum.

8\. \*\*Pull tabanlı GitOps\*\* mantığını uyguladım.

9\. Bir servis bozulduğunda tekrar ayağa kaldırılmasını sağlayan

&#x20;  \*\*self-healing\*\* mantığını test ettim.

10\. Sanal sunucuyu tamamen silip tekrar oluşturarak

&#x20;   \*\*disaster recovery\*\* senaryosunu test ettim.



Bu çalışma sayesinde sadece araçları kullanmayı değil,

araçların birbirleriyle nasıl bağlantılı çalıştığını anlamaya çalıştım.

