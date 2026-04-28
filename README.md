# 🐍 PiSi - Python 3 Port

Pardus'un efsane paket yöneticisi **PiSi**'nin Python 3'e taşınma projesi.

## Hakkında

PiSi (Packages Installed Successfully as Intended), TÜBİTAK tarafından 
geliştirilen ve Pardus Linux'ta kullanılan özgün paket yöneticisidir.
2013'te Pardus'un Debian'a geçmesiyle birlikte terk edilmiştir.

Bu proje, PiSi'nin [pisilinux fork'unu](https://github.com/pisilinux/pisi) 
Python 3'e taşımak amacıyla başlatılmıştır.

## Durum

- [x] Python 3 uyumluluk analizi yapıldı
- [x] `fissix` ile otomatik dönüşüm uygulandı (13 dosya)
- [x] `eval()` ve `bytes/str` güvenlik açıkları düzeltildi (`pisi/cli/__init__.py`)
- [x] `coreutils.py` parse hatası giderilecek
- [ ] Kapsamlı test yazılacak
- [ ] Pardus 25 üzerinde çalıştırılacak

## Kurulum (Geliştirici)

```bash
git clone https://github.com/FOXY-cyber-dot/pisi-python3.git
cd pisi-python3
git checkout python3-port
```

## Orijinal Proje

- [pisilinux/pisi](https://github.com/pisilinux/pisi)
- [Pardus-Linux/pisi](https://github.com/Pardus-Linux/pisi)

## Katkı

Bu proje aktif geliştirme aşamasındadır.
Katkıda bulunmak isteyenler PR açabilir. 🚀

## Lisans
GPL-2.0