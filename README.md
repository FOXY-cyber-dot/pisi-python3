# 🐍 PiSi - Python 3 Port

Pardus'un efsane paket yöneticisi **PiSi**'nin Python 3'e taşınma projesi.

## Hakkında

PiSi (Packages Installed Successfully as Intended), TÜBİTAK tarafından 
geliştirilen ve Pardus Linux'ta kullanılan özgün paket yöneticisidir.
2013'te Pardus'un Debian'a geçmesiyle birlikte terk edilmiştir.

Bu proje, PiSi'nin [pisilinux fork'unu](https://github.com/pisilinux/pisi) 
Python 3'e taşımak amacıyla başlatılmıştır.

## Durum

### Tamamlananlar

- [x] Python 3 uyumluluk analizi yapıldı
- [x] `fissix` ile otomatik dönüşüm uygulandı (13 dosya)
- [x] `eval()` ve `bytes/str` güvenlik açıkları düzeltildi (`pisi/cli/__init__.py`, `scripts/check-newconfigs.py`)
- [x] `coreutils.py` parse hatası giderildi
- [x] `api.py` geçersiz escape sequence düzeltildi (Python 3.12+ SyntaxWarning)
- [x] **DÜZELTİLDİ:** `import formatter` kaldırıldı — Python 3.12'de silinmiş modül; `_Writer` ve `_AbstractFormatter` sınıfları ile değiştirildi (`pisi/pxml/autoxml.py`)
- [x] **DÜZELTİLDİ:** `base64.encodestring()` → `base64.encodebytes()` — Python 3.9'da kaldırılmıştı (`pisi/fetcher.py`)
- [x] **DÜZELTİLDİ:** `os.tmpfile()` → `tempfile.TemporaryFile()` — Python 3'te kaldırılmıştı (`scripts/package-signing/pisign.py`)
- [x] **DÜZELTİLDİ:** Binary arşiv dosyaları text modda açılıyordu → `"wb"` modu ile düzeltildi (`pisi/archive.py`: Bzip2, Gzip, Lzma)
- [x] **DÜZELTİLDİ:** `_LZMAProxy.buf` string yerine bytes olarak başlatıldı (`pisi/archive.py`)
- [x] **DÜZELTİLDİ:** `distutils` → `setuptools` geçişi yapıldı — Python 3.12'de kaldırılmıştı (`setup.py`, `pisi/db/historydb.py`)
- [x] **DÜZELTİLDİ:** `bytes/str` karışıklığı kapsamlı düzeltildi (`pisi/db/sourcedb.py`, `scripts/package-signing/pisign.py`, `scripts/make-changelog.py`)
- [x] **DÜZELTİLDİ:** Geçersiz regex escape dizileri `SyntaxWarning` üretiyordu → raw string yapıldı (`pisi/index.py`, `pisi/operations/build.py`, `pisi/actionsapi/kerneltools.py`, `pisi/pxml/autoxml.py`)
- [x] **DÜZELTİLDİ:** `pisi/db/repodb.py` tanımsız `repo` değişkeni → `repo_name` ile düzeltildi
- [x] **DÜZELTİLDİ:** `from pisi.delta import` → `from pisi.operations.delta import` (`scripts/createdelta.py`)
- [x] **DÜZELTİLDİ:** `importlib.reload(sys)` Python 2 hack'i kaldırıldı (`pisi/__init__.py`)
- [x] **DÜZELTİLDİ:** `Config::CONFIG` → `RbConfig::CONFIG` — eski Ruby API (`pisi/actionsapi/rubymodules.py`)
- [x] **DÜZELTİLDİ:** `python setup.py` → `python3 setup.py` (`pisi/actionsapi/pythonmodules.py`)
- [x] **DÜZELTİLDİ:** `locale.getdefaultlocale()` → Python 3.11'de deprecated; `locale.setlocale()` ile değiştirildi (`pisi/pxml/autoxml.py`)
- [x] **DÜZELTİLDİ:** `is ""` → `== ""` SyntaxWarning giderildi (`pisi/pxml/autoxml.py`)

### Bekleyenler

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