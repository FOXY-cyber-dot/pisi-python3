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
- [x] `coreutils.py` parse hatası giderildi
- [x] `api.py` geçersiz escape sequence düzeltildi (Python 3.12+ SyntaxWarning)
- [ ] `piksemel` → `lxml` ile değiştirilecek (`pisi/pxml/xmlext.py` ve 7 bağımlı dosya)
- [ ] Kapsamlı test yazılacak
- [ ] Pardus 25 üzerinde çalıştırılacak

## Kritik Engel: `piksemel`

`piksemel`, Pardus'a özgü bir C-extension XML kütüphanesidir. PyPI veya apt üzerinden
kurulumu mevcut değildir. `import pisi` çalışmaz hale getirmektedir.

**Çözüm:** `pisi/pxml/xmlext.py` dosyasındaki piksemel API'si `lxml.etree` ile ikame edilecek.
Etkilenen dosyalar (8 adet):

| Dosya | Bağımlılık |
| ----- | ---------- |
| `pisi/pxml/xmlext.py` | `import piksemel` — ana adaptör |
| `pisi/pxml/xmlfile.py` | xmlext üzerinden |
| `pisi/pxml/autoxml.py` | xmlext üzerinden |
| `pisi/db/packagedb.py` | doğrudan piksemel |
| `pisi/db/installdb.py` | doğrudan piksemel |
| `pisi/db/sourcedb.py` | doğrudan piksemel |
| `pisi/db/repodb.py` | doğrudan piksemel |
| `pisi/specfile.py` | doğrudan piksemel |

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