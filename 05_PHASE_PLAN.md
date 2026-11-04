# Faz planı

Bu belge fazların kapsamını tanımlar. Güncel çalışma ve kabul durumu yalnız [09 — Handoff](09_CODEX_HANDOFF.md) içinde tutulur.

## Faz sırası

- **00 — Bootstrap:** Laravel kökü, ortam, DB/migration/test/route doğrulaması, mimari ve dokümantasyon.
- **01 — Corporate Core:** marka, ofis, broker, danışman, model, üyelik ve aktivasyon.
- **02 — Customer & Service Core:** CRM, Data Havuzu, görüşme, Talep/Hizmet Dosyası.
- **03 — Governance, Commercial Policy & UX:** marka yönetimi, ofis/danışman yönetimi, ticari plan/ücret/hak, sözleşme, yetki, model ve paylaşım politikaları. Tahakkuk final fatura değildir.
- **04 — Property Core:** gayrimenkul, portföy, ilan ve tek pazaryeri.
- **05 — Lead, Appointment & Transaction:** lead, randevu, gösterim, teklif ve İşlem.
- **06 — Finance & Revenue Pool:** fatura, tahsilat, dağıtım, hakediş, ödeme ve Kazanç Havuzu.
- **07 — Final Test ve Kabul:** uçtan uca akış, yetki, veri bütünlüğü, performans ve ürün sahibi kabulü.

## Faz kapısı

**ADR-078 — Güncel kodlama öncesi paket (3 Kasım):** Yalnız mevcut dokümantasyon güncellenir; ADR-077 Marka/Broker sınırı değişmez. Sıra: üç kuruluş seçeneği ve hazırlık sorumlusu → hesap/davet/ofis ilişkisi ve SETUP sınırlı erişimi → resmî ilişkiyle unvan → ana ofis sözleşmesinde ofis temsil/imzası ve ayrı Broker şahsi kabulü → Marka ticari onayı/kanıt doğrulaması → 02 bölüm 8.4.3'ün dokuz koşuluyla READY/ACTIVE. Sonra aynı yürürlükte tek aktif Broker değişimi/atama eki ve sözleşme sonundaki derhal yetki kapanışı ile ayrı kapanış işlerinin hedefi ele alınır. Mevcut Office/Professional/Commercial/belge-kanıt/erişim/audit katmanları korunur; ayrı zorunlu Broker sözleşmesi veya yeni mimari kurulmaz.

13 yeni yaşam döngüsü kabul hedefi 02 bölüm 8.10'dadır; çalıştırılmamıştır. Hukukçu imza incelemesi DQ-002, müdahale/itiraz/geçici yönetici/başarısız devir usulü DQ-014/020/021, mali takvim/tasfiye DQ-022'de kalır. Broker değişiminde ana sözleşmenin devamı ve ilişki sonundaki unvan/erişim artık açık soru değildir. Kadro/ilk ilan veya kararsız ödeme şartı eklenmez. 03C.4 KISMİ kapısı, kodlama/test/build/veritabanına geçmeme sınırı korunur; eski tarihli plan hükümlerinin önünde ADR-078 geçerlidir.

**3 Kasım ADR-077 çalışma sınırı:** Yalnız mevcut dokümantasyonun kurumsal yetki/sorumluluk tutarlılığı güncellenir. Marka kurumsal yönetişim/denetim, Broker ofis işletmesi, danışman yetkili dosya çalışması, ortak sözleşmeli görev ve müşteri kendi karar alanındadır (02 bölüm 8.2). İlgili mevcut alanlar Office/Professional/Commercial, Customer/Service/Transaction ve hedef Finance/RevenuePool'dur; bunlar bu görevde kodlanmaz. Açık 03C.4 KISMİ kapısı ve finans fazı koşulları korunur.

Sonraki değerlendirme sırası: **(1)** Marka–Ofis matrisi; **(2)** üç kuruluş başlangıcının tutarlı kurumsal/ticari sonucu; **(3)** Broker hazırlık erişimi, sözleşme taraf kabulleri/imza kanıtı ve aktivasyon; **(4)** üç ayrı mali kaynaktan yükümlülük/vade/tahakkuk/fatura/tahsilat/mutabakat; **(5)** değişiklik/askı/sonlandırmada hizmet devamı, otomatik yönetim devri ve mali hak/tasfiye. İlk üç başlık birbirine bağlıdır. Matris kesin sınırları taşır; kalan müdahale/itiraz usulü DQ-014/020/021, franchise takvimi/tasfiye DQ-022'dir. Bu sıra onaylanmamış ticari koşulu kesinleştirme, kodlama veya ALFA panelinin ayrıntılı tasarımını başlatma talimatı değildir. Eski tarihli plan ifadelerinin önünde ADR-075/076/077 geçerlidir.

1. İlgili kapsamın kod/test kanıtı.
2. Gereken gerçek ortam ve tarayıcı kabulü.
3. Açık kararların ve kabul eksiklerinin handoff'ta kaydı.
4. Ürün sahibinin açık geçiş kararı.

Kodun varlığı, prototip veya başarılı test tek başına fazı onaylamaz. Eski belgelerdeki 3C/4B gibi paket etiketleri yukarıdaki faz sırasını değiştirmez. Sonraki faza yalnız belgenin tarihine veya numarasına bakarak geçilmez.

## Ana iş akışının geliştirme sırası — öneri, 29 Ekim 2026

30 Ekim ürün sahibi kurumsal kayıtları, bağımsız panel adreslerini ve müşteri hizmet akışını uygulama talimatı verdi. Bu paket bu açık kapsamın geliştirmesidir; geçmiş 03C.4 kabulünü kapatmaz, bütün ileri fazları tamamlandı ilan etmez. İlk teslim: giriş düzeltmesi, ofis başvurusu/görev bağı, müşteri hizmet teklifi kararı ve havale kontrolüne bağlı peşin paket dönemi. Tüm ilan/işlem kapanışı, genel finans ve kalan iki panelin kabulü ayrıca izlenir. Ürün sahibi Stratejik İş Ortağı/Yatırımcı panellerini sonraki adıma bıraktı.

Önce mevcut test hazırlığı ve açık kabul sorunları; sonra gayrimenkul danışmanı temeli/broker görevi, panel bağlamı ve ofisten model tutarlılığı. Ardından 02'deki bir tam iş yolculuğu ilgili faz kapıları içinde uygulanır. Standart ilanla satış ilk adaydır; seçim kesinleştirilmeden zorunlu sıra sayılmaz.

Açık artırma hedef kapsamına eklenmiştir; yöntem/katılım/teklif/sonuç kuralları kesinleştirilip ilgili ilan ve işlem fazları ayrıca açılmadan uygulaması başlatılmaz. İş ortağı ve yatırımcı paketleri için de görev, veri ve mali kapsam kararı gerekir. Bu sıra 03C.4 KISMİ kapısını veya faz 04–06 geçiş şartlarını kaldırmaz.

## Marka Paneli ürün tanımından uygulamaya — 1 Kasım 2026

ADR-071 ve [02, bölüm 8](02_BUSINESS_RULES.md#8-marka-paneli--ürün-ve-işleyiş-sözleşmesi) güncel hedefi ve 16 kabul ölçütünü tanımlar. Kullanıcının "başla" talimatıyla ürün tanımı mevcut belgelere işlendi. Kaynak metin açık kuralların uygulama talimatından önce netleşmesini ister; bu kayıt uygulama değişikliği, geçmiş faz kabulü veya altı panelin tamamlanması değildir.

1. **Tanım ve karar hazırlığı:** marka aktörleri/sınırlar, dashboard-liste eşitliği, audit bağlamı, üç kuruluş yolu, iki ayrı kabul ve mali ayrımlar kaydedilir. ADR-072 ile DQ-005/015/016 ana kararları kapandı: ofis türü değişmez, broker aynı ofiste danışman devam eder, ofis şartı aktivasyon ve danışman anlaşması operasyon içindir. ADR-073 ile otomatik 24 saat bırakma, görüşme sonrası 3 gün koruma, son görüşmeden itibaren aynı danışmanı kapsayan 15 gün aramama; yıllık en yüksek işlem cirosu, iki brokerın bedel anlaşması ve hedef talebi/kaynak kabulü kesinleşti. DQ-017/018 yalnız kalan istisna/hesap kanıtı ayrıntılarıdır. DQ-010/014/019 devir/sorumluluk, yetki matrisi ve mesleki kanıt; DQ-012/013 iş ortağı/yatırımcı sınırlarını taşır.
2. **Kurumsal/yetki uygulama paketi:** kapsam açıldığında panel bağlamını aşan yetki istisnaları, gerçek aktör/sıfat ve konu kapsamı audit'i, tutarlı aktivasyon/operasyon kapıları ve dashboard sorguları ele alınır. Marka görevlerinin teknik izin modeli kesinleştirilir. Ürün tanımı tek başına migration veya kullanıcı yetkilerini topluca değiştirme talimatı değildir.
3. **İlişki yaşam döngüsü paketi:** ofis türünün mevcut kayıtta değiştirilememesi, broker görevi bitişinde profesyonel kimliğin korunması ve yönetim yetkilerinin kapanması ADR-072/076 esas alınarak ele alınır. Olağan transfer hedef ofis talebi ve kaynak ofis kabulüyle ilerler (ADR-073); eski dosya sorumluluğu ve yürürlük korunur. Eski model/dosya snapshot'ları değişmez; yerinde tür dönüşüm akışı kurulmaz. Havuzun 24 saat/3 gün/15 gün kararları uygulanırken çalışma koruması ve aramama ayrı denetlenir. Brokerların anlaşılmış transfer bedeli sistem tarafından seçilmez veya ödenmiş sayılmaz. Devir/marka yönetimi, tek aktif üyelik ve kalan istisna/kanıt koşulları kendi kararlarına bağlıdır. ADR-072’nin eski danışman unvanına dönüş ifadesi tarihsel kayıttır; mesleki çalışma için dönüş şartı yoktur (ADR-075/076).
4. **İlgili fazların sonuçları:** iş ortağı/yatırımcı, işlem kapanışı ve mali hareketler kendi açık kapsam/karar/kabul kapılarında sürer. Finansal göstergeye veri kaynağı uygulanmadan gerçekleşmiş gelir/hakediş sayısı eklenmez.

Her uygulama paketinde izin, çoklu sıfat, çapraz-ofis, kabul sürümü, tarihçe, hata/geri alma ve tekrar çağrı güvenliği somut kanıtla değerlendirilir. 02'deki kabul ölçütleri 09'daki güncel kanıtla kapatılır; tanımın yazılması ölçütün geçtiği anlamına gelmez.

## MAXIMUM panel tasarımı — 2 Kasım 2026 çalışma sınırı

Kullanıcı bu aşamada yalnız mevcut belgelerde tasarım/entegrasyon istedi; uygulama, veritabanı, migration, seed ve test dosyası değiştirilmeyecek. 02 bölüm 9'da 13 hedef menü, mevcut ekran farkları, M1–M6 karşı panel matrisi ve 21 temel ve 14 ek kabul senaryosu tutulur. ADR-075 yedi hedef panel/Broker unvanını günceller; bu yeni yazılım mimarisi veya UserRole/veri modeli talimatı değildir. 03C.4 KISMİ kapısı korunur.

ADR-076 ile Brokerın Marka onaysız kişisel havuz çalışması, dağıtımı/sorumluları belirleme ve ayrılıkta otomatik yönetim devri kesindir. DQ-020/021 yalnız inceleme/itiraz/acil kısıt/geçici yönetici ve devir hata/bildirim usulünü taşır. Kaynak farkları 02 bölüm 9.9, 14 ek kabul ölçütü 9.10'dadır; hiçbiri çalıştırılmış test değildir. MAXIMUM belge entegrasyonu tamamlanır; 03C.4 KISMİ kapısı ve ALFA tasarımına geçmeme sınırı korunur.
