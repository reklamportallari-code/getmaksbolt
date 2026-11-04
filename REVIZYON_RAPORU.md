# Dokümantasyon revizyon raporu

**Tarih:** 28 Ekim 2026  
**Sonuç:** Belge sayısı azaltıldı, güncel okuma yolu sadeleştirildi ve ofis–danışman modeli kararı hizalandı.

## Sayısal sonuç

- docs ana dizini: **29 → 9 dosya**; yaklaşık %69 azalma.
- Alt klasörler dahil fiziksel dosya sayısı: **29 → 13**. Bunlar 9 ana belge, 1 birleşik referans, 1 HTML prototipi, 1 görsel ve 1 ZIP arşividir.
- Zorunlu yedi çalışma belgesinin toplam UTF-8 boyutu: **98.708 → 32.832 bayt**; %66,7 azalma. Bu ölçüm okuma süresi veya token hesabı değildir.
- On ayrıntılı ürün kaynağı tek referans belgesinde birleşti.
- Özgün 29 dosyanın tamamı arşivde korunuyor. ZIP içindeki dosyalar fiziksel dosya sayısına tek tek dahil edilmedi.

## Düzeltilen sorunlar

**Model çelişkisi çözüldü.** Kullanıcının kesin kararı ADR-061 olarak kaydedildi: MAXIMUM/ALFA hem ofis türü hem danışman çalışma modelidir; danışman ofisini seçince modeli de belirlenir. AGENTS.md, iş/finans kuralları ve Boost üzerinden kaydedilen ortak proje kuralı aynı ifadeye getirildi. Geçmiş snapshot ve model tarihçesi korunur.

**Faz geçmişi güncel durumdan ayrıldı.** Eski handoff'taki 03C.3 COMPLETED, 03C.4 KISMİ ve 4B.1 başlıkları tek ilerleme durumu gibi okunmuyordu. Güncel handoff son açık kabul kapısını 03C.4 KISMİ olarak koruyor; yeni faz onayı vermiyor.

**Eski kanıtlar tarihlendirildi.** Test sayıları, migration durumları ve “henüz yok” ifadeleri güncel sonuç olarak taşınmadı. Örneğin 19 Ekim'in sonraki migration kontrolü, aynı günün önceki “uygulanmadı” notundan ayrıldı. Prototip kontrolü ile gerçek Laravel kabulü açıkça ayrıldı.

**Tek-ofis çelişkisi giderildi.** Tek marka altında yönetilebilir ofisler ve ofis başına tek aktif broker kuralı esas alındı; ilk kurulumun tek ofis olması kalıcı ürün sınırı olarak bırakılmadı.

**Tek değişiklik günlüğü belirlendi.** Yeni kayıtlar yalnız kök CHANGELOG.md dosyasına yazılacak. Eski docs/CHANGELOG.md kaybolmadı; arşivde duruyor.

## Eski içerikler nereye gitti?

- 04_DATA_MODEL ve 08_LEGACY_MAPPING → [01 — Mimari](01_ARCHITECTURE.md).
- 06_ACCEPTANCE_TESTS güncel kabul özeti → [09 — Handoff](09_CODEX_HANDOFF.md); eski ayrıntılı test listeleri arşiv.
- DECISIONS_REQUIRED → [07 — Kararlar](07_DECISIONS.md); eski “uygulama yok” tespitleri tarihsel olarak ayrıldı.
- Eski ADR-001–060 tam metni → arşiv; güncel karar özeti ve yeni ADR-061/062 → 07.
- 10_SYSTEM_BEHAVIOR_CONTRACT, 11_CROSS_MODULE_INTERACTION_MATRIX, 12_BUSINESS_MODEL_VALIDATION → tarihsel inceleme arşivi.
- 10_PANEL_TALEP, 13 panel şartnamesi, 14 blueprint ve yedi güncel sürümlü ürün metni → [tek referans](reference/PRODUCT_SPECIFICATIONS.md).
- Eski v1.1 talimatı ve v1.2 prototipi → arşiv.
- Güncel v1.3 prototipi ve üyelik/unvan görseli → reference klasörü.

Birleştirilen kaynakların gövdesi değiştirilmedi; kaynak adları ve bölüm bağlantıları korunuyor. Eski model ifadelerinin ADR-061'in önüne geçmediği referansın başında açıklandı. Arşiv özgün metinleriyle saklandığı için geçmişteki çelişkiler tarihsel incelemede görülebilir.

## Doğrulama

- Arşivdeki **29 dosya**, değişiklik öncesi özgün dosyalarla tek tek SHA-256 karşılaştırmasından geçti.
- Ana dizinden kaldırılan **22 eski dosya**, kaldırılmadan önce arşivle yeniden hash karşılaştırmasından geçti.
- Birleştirilen **10 kaynak gövdesinin** tam metni referans belgesinde doğrulandı.
- Güncel HTML ve PNG'nin arşivdeki özgün dosyalarla SHA-256 eşitliği doğrulandı.
- Güncel Markdown dosyalarındaki yerel bağlantılar ve referansın on bölüm bağlantısı kontrol edildi.
- Zorunlu yedi belge yolu korundu; AGENTS.md yeni model kararıyla hizalandı.
- Uygulama PHP/Blade/JS kodu ve veritabanı değiştirilmedi. PHPUnit, build veya migration çalıştırılmadı; eski sonuçlar yeni test sonucu olarak sunulmadı.

## Devam ederken açık kalanlar

Bu revizyon belge karışıklığını giderir; uygulamanın bütün kararlarla uyumlu olduğunu kanıtlamaz. Ofis–danışman model uyumsuzlukları, eski NULL kayıtlar, profesyonel onboarding, broker kapsamı, scheduler ve tarayıcı kabulü [07](07_DECISIONS.md) ve [09](09_CODEX_HANDOFF.md) içinde açık tutuldu.

Eski panel şartnamesinin atıf yaptığı iki ana kaynak özgün docs envanterinde bulunmadığından içerikleri varsayılmadı. Finansal/hukuki eksik koşullar belge düzenlemesi sırasında üretilmedi.

## Kullanım

Önce [belge rehberi](README.md), sonra [güncel durum](09_CODEX_HANDOFF.md). Günlük çalışmada ayrı eski rapor ve sürümleri taramak gerekmiyor; yalnız konuya bağlı ayrıntı için birleşik referansa gidiliyor.

[Özgün belgelerin arşivi](archive/docs-2026-10-28-oncesi.zip) · [Değişiklik günlüğü](../CHANGELOG.md)
