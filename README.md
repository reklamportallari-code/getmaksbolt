# GETMAKS360 V2 — Belge rehberi

Güncelleme: 3 Kasım 2026. Başlangıç noktası bu sayfadır. Yeni proje belgesi eklenmedi; karar, davranış, mali dayanak ve uygulama kanıtı aşağıdaki mevcut kaynaklarda ayrı tutulur.

## Hızlı okuma

- Projeyi anlamak: [Proje bağlamı](00_PROJECT_CONTEXT.md).
- Güncel ofis/Broker yaşam döngüsü: [02 bölüm 8.4](02_BUSINESS_RULES.md#84-ofis-kuruluşu-modeli-ve-yaşam-döngüsü), 13 çalıştırılmamış kabul hedefi [8.10'da](02_BUSINESS_RULES.md#810-ofisbroker-yaşam-döngüsü-kabul-hedefleri--adr-078). ADR-078; üç kuruluş seçeneği, sınırlı SETUP hazırlığı, resmî ilişkiye bağlı unvan, tek ana sözleşme/ayrı şahsi kabul, dokuz aktivasyon koşulu ve yetki sonu günceldir. Hukuk/imza ve kalan mali/usul açıkları 07'de korunur; uygulama kabulü değildir.
- Marka–Ofis kurumsal yetki/operasyon matrisi, aktörler ve on hak ayrımı: [02 bölüm 8.2](02_BUSINESS_RULES.md#82-marka-aktörleri-ve-yetki-ayrımı). ADR-077 günceldir; müdahale/itiraz usulü ve ticari takvim açıkları [07'de](07_DECISIONS.md) kalır. Ofis sözleşmesi, İşlem Dosyası ve peşin paket kaynakları [03'te](03_FINANCE_RULES.md) ayrıdır.
- Ana iş akışı ve yedi hedef panelin sorumluluğu: [İş kuralları](02_BUSINESS_RULES.md). Mevcut kod ile hedef panel sayımı farklıdır (ADR-075).
- Marka Paneli ürün tanımı, 16 temel ve 15 kurumsal sınır kabul ölçütü: [İş kuralları, bölüm 8](02_BUSINESS_RULES.md#8-marka-paneli--ürün-ve-işleyiş-sözleşmesi). Yazılmış hedeflerdir; çalıştırılmış test veya uygulama kabulü değildir. Durum 09'dadır.
- MAXIMUM Ofis Paneli: [İş kuralları, bölüm 9](02_BUSINESS_RULES.md#9-maximum-ofis-paneli--tasarım-ve-belge-entegrasyonu); 13 menü sözleşmesi, mevcut/hedef ekranlar, altı karşı panel etkileşimi ve 21 temel ve 14 ek kabul ölçütü; kesin yönetim/devir kararları ADR-076, kalan prosedürler DQ-020/021'dedir; ALFA tasarımı bu kapsamda değildir.
- Nasıl çalışmalı: [İş kuralları](02_BUSINESS_RULES.md) ve [finans kuralları](03_FINANCE_RULES.md).
- Nerede kaldık: [Güncel durum ve kabul](09_CODEX_HANDOFF.md).
- 28 Ekim belge sadeleştirmesi: [Revizyon raporu](REVIZYON_RAPORU.md).

Geliştirme oturumunda zorunlu sıra değişmedi: 00 → 01 → 02 → 03 → 05 → 07 → 09. Yalnız yapılacak işle ilgili ayrıntılar için referans belgeye gidilir.

## Her belgenin tek sorumluluğu

1. [00 — Proje bağlamı](00_PROJECT_CONTEXT.md): amaç, kapsam ve kavramlar.
2. [01 — Mimari ve veri sahipliği](01_ARCHITECTURE.md): teknik sınırlar, temel veri grupları, legacy disiplini.
3. [02 — İş kuralları](02_BUSINESS_RULES.md): kimlik, ofis, danışman, dosya ve panel davranışları.
4. [03 — Finans kuralları](03_FINANCE_RULES.md): ticari politika, gelir, tahakkuk, fatura ve ödeme ayrımı.
5. [05 — Faz planı](05_PHASE_PLAN.md): faz sırası ve geçiş koşulları.
6. [07 — Kararlar](07_DECISIONS.md): güncel kararlar ve açık karar listesi.
7. [09 — Handoff](09_CODEX_HANDOFF.md): çalışma sınırı, sonraki adım ve kabul kanıtı.
8. [Revizyon raporu](REVIZYON_RAPORU.md): bu düzenlemenin kapsamı ve doğrulaması.

04, 06 ve 08 numaraları yeniden kullanılmadı: veri modeli ve legacy kaydı 01'e; kabul özeti 09'a birleştirildi. DECISIONS_REQUIRED içeriğinin güncel durumu 07'dedir.

## Gerektiğinde başvurulacak kaynaklar

- [Birleştirilmiş ürün şartnameleri](reference/PRODUCT_SPECIFICATIONS.md): on kaynak; içindekilerden ilgili bölüme gidilir.
- [Dilim 03 v1.3 prototipi](reference/PROTOTYPE_v1.3.html) ve [üyelik/unvan görseli](reference/UYELIK_UNVAN_v1.3.png): görsel referans; çalışan Laravel uygulamasının kanıtı değildir.
- [Revizyon öncesi arşiv](archive/docs-2026-10-28-oncesi.zip): özgün 29 dosya, eski ADR'ler, test raporları, v1.1/v1.2 sürümleri ve eski docs değişiklik günlüğü.
- [Tek değişiklik günlüğü](../CHANGELOG.md): yeni kayıtlar yalnız buraya eklenir.

## Kaynak önceliği ve bakım

Kullanıcının açık güncel kararı ve kalıcı proje talimatı esas alınır. İş kuralları 02/03'te, karar gerekçesi 07'de, uygulama/kabul durumu 09'da tutulur. Referans ve arşivdeki eski ifadeler bu özetlerin önüne geçmez. Çözümlenmemiş çelişki 07'de görünür bırakılır; tarih veya sürüm numarası tek başına faz onayı değildir.

Yeni bir iş için yeni sürümlü ana belge açmak yerine ilgili mevcut belge güncellenir. Kalıcı karar değişirse 07, ilgili kural, handoff ve kök CHANGELOG aynı değişiklikte hizalanır. Tam test çıktıları ve oturum günlükleri güncel handoff'a yığılmaz.
