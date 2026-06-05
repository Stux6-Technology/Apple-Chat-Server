# Apple Chat Server

## Genel Bakış
Apple Chat Server, Apple tarafından geliştirilen ChatServer 409 platformunun gönüllüler tarafından sürdürülen bir türevidir. Bu repo, Mac OS X Server tabanlı Jabber/XMPP mesajlaşma altyapısının kaynak kodunu, Apple patchlerini, konfigürasyon şablonlarını ve yönetim araçlarını içerir.

## Kurumsal Amaç ve Kapsam
Bu belge, teknik ekiplerin projeyi hızlıca değerlendirmesi ve kullanımına başlaması için hazırlanmıştır. Reponun ana hedefleri:

- Apple tarafından yayımlanmış orijinal ChatServer kaynak kodunu korumak.
- jabberd2 tabanlı XMPP sunucu yapılandırması ve entegrasyonunu sağlamlaştırmak.
- Apple Server ekosistemine özgü konfigürasyon ve yedekleme/geri yükleme iş akışlarını belgelemek.
- APSL 2.0 lisans gereksinimlerine uyarak açık kaynaklı sürüm yönetimi sunmak.

## Mevcut İçerik

Ana dizin altındaki başlıca bileşenler:

- `Makefile` — ChatServer bileşenleri için Apple build sistemi üzerinden wrapper derleme kuralları.
- `CHATServer2.xcodeproj/` — Xcode projesi ve çalışma alanı dosyaları.
- `apple_patch/` — Apple tarafından sağlanan pre/post configure yama dizinleri.
- `cfg-apple/` — jabberd2, c2s/s2s, router ve sm modülleri için Apple uyumlu yapılandırma şablonları.
- `backup_restore/` — Apple Server yedekleme / geri yükleme servisi entegrasyonu ve plist tanımları.
- `jabber_od_auth/` — Open Directory / LDAP kimlik doğrulaması için Apple özel modüllerinin kaynakları.
- `jabber_autobuddy/` — otomatik kullanıcı ekleme, grup eşleme ve roster yönetimi araçları.
- `opensource_pkgs/` — bağımlı paket kaynak arşivleri; örneğin `jabberd-2.2.17.tar.gz` ve `libidn`.
- `migration/`, `tools/`, `restore_extras/`, `common_extras/` — geçiş, yönetim ve kurulum eklentileri.

## Teknik Özellikler

- Sunucu yazılımı: `jabberd2` tabanlı XMPP mesajlaşma altyapısı.
- Ek kütüphane: `libidn` statik olarak derlenerek jabberd2 ile bağlanır.
- Apple özgü entegre bileşenler: `jabber_od_auth`, `jabber_autobuddy`, `backup_restore`, `cfg-apple`.
- Derleme yaklaşımı: Apple iç yapı değişkenlerini ve `pb_makefiles` yapılarını kullanan Apple Server uyumlu Makefile.

## Derleme ve Kurulum Notları

### Gereksinimler

- Apple platformuna uygun Xcode ve komut satırı araçları.
- Apple iç ortamında tanımlı `$(MAKEFILEPATH)` ve `/AppleInternal/ServerTools/ServerBuildVariables.xcconfig` dosyaları.
- `opensource_pkgs/jabberd-2.2.17.tar.gz` ve `opensource_pkgs/libidn-0.6.14.tgz` gibi bağımlılık kaynakları.

### Örnek Derleme Akışı

1. Kaynak kök dizinine gidin.
2. `make` veya `make default` komutu ile derleme sürecini başlatın.
3. Gerekirse `OBJROOT` ve `ARCHS` değişkenlerini Apple build ortamına uygun şekilde yapılandırın.

> Not: Mevcut `Makefile`, Apple Server iç ortamında kullanılan `pb_makefiles` ve `ServerBuildVariables.xcconfig` referansları içerir. Bu referanslar olmadan yerel bir macOS ortamında doğrudan çalışmayabilir.

## Yapılandırma ve Dağıtım

- `cfg-apple/` dizinindeki XML dosyaları, c2s/s2s/route/sm bileşenleri için temel Apple-özgü yapılandırma şablonlarıdır.
- `backup_restore/` dizini Apple Server yedekleme/geri yükleme entegrasyonunu destekler.
- Dağıtım öncesi, sistem yolları, kullanıcı hesapları ve yetkilendirme modülleri ortamınıza göre yeniden uyarlanmalıdır.

## Lisans ve Uyum

- Bu repo, kök dizinde yer alan `LICENSE` dosyası ile Apple Public Source License (APSL) 2.0 altında lisanslanmıştır.
- `APSL 2.0`, orijinal Apple kodu ve ona yapılan değişikliklerin telif hakkı bildirimlerinin korunmasını ve dışa dağıtım halinde kaynak kodunun paylaşılmasını zorunlu kılar.

### APSL Uyum Analizi

1. Mevcut durumda bu repo zaten APSL 2.0 lisansına sahip görünüyor.
2. Apple kaynaklı kodun içeriği ve lisans bildirimi `LICENSE` dosyası ile belirtilmiş.
3. Eğer bu repoda değişiklik yapılıp harici olarak dağıtılırsa, değiştirilen kaynak dosyalarında:
   - Apple telif hakkı bildirimleri korunmalı,
   - değişiklikler ve değişiklik tarihleri açıkça belirtmeli,
   - dışa dağıtılan değişikliklerin kaynak kodu APSL 2.0 kapsamında erişilebilir olmalıdır.
4. `opensource_pkgs/` altında yer alan ek paketlerin kendi lisansları olabilir; bunların APSL ile çakışmadığı doğrulanmalıdır.

### Dikkat Edilmesi Gereken Hususlar

- `Makefile` içindeki Apple dahili dosya yolları, herkese açık macOS ortamında mevcut değildir.
- Bu repo Apple markalarını, ticari isimlerini veya logolarını kullanmaya izin vermez.
- APSL 2.0, kısıtlı bir açık kaynak lisansıdır; özellikle dışa dağıtımda kaynak kodu erişilebilir kılma yükümlülüğü bulunur.

## Katkıda Bulunma

- Reponun yukarıdaki lisans kapsamında yeniden dağıtılması veya değiştirilmesi planlanıyorsa, tüm değişiklikler APSL 2.0 şartlarına uygun şekilde yapılmalıdır.
- Orijinal Apple kaynak kodu ve lisans bildirimleri korunmalıdır.
- Gönüllü katkılarda bulunan kaynaklar ve değişiklik tarihleri belgelenmelidir.

## Özet

Bu repo, Apple ChatServer 409 kaynaklarını ve Apple Server uyumlu yapılandırma/paketleme yaklaşımlarını içerir. Lisans olarak APSL 2.0 belirlenmiş olup, uyumluluk için özellikle dışa dağıtılan modifikasyonların kaynak erişimi ve Apple telif hakkı bildirimlerinin korunması gereklidir.
