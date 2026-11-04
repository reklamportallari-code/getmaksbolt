# GETMAKS360 V2 — Proje bağlamı

Getmaks, gayrimenkul sektöründe franchise ve ofis organizasyonu temelli bir marka yapılanmasıdır. Getmaks360 bu organizasyonun ticari, operasyonel ve finansal süreçlerini yöneten dijital ekosistemdir. Dijital pazaryeri, yetkili ofis ve profesyonel portföylerini yayınlayan, nihai müşteri taleplerini organizasyonla buluşturan ayrı fakat ekosistemle bütünleşik kanaldır; bugünkü işletme modelinin yerine geçmez. Standart veya açık artırma ilanları aracılık sürecine hizmet eder. Yetkili uygulama kaynağı bu depodur; legacy yalnız referanstır.

## Ürün ve organizasyon

**Ofis/Broker yaşam döngüsü — ADR-078 (3 Kasım):** Kuruluş mevcut Broker, yeni Broker daveti veya atamayı erteleme yoluyla ilerler. Ertelemede hazırlığı Marka, atama sonrası günlük hazırlık/işletmeyi Broker yürütür. Broker unvanı resmî franchise/ofis ilişkisi veya geçerli Marka atamasına bağlıdır; davet/hazırlık erişimi tek başına unvan vermez. Ana sözleşme Getmaks A.Ş. ile ofis tüzel kişiliğinin **Getmaks Ofis Franchise ve İşletme Sözleşmesi**dir; ofis temsil/imzası ile Broker şahsi kabulü ayrıdır, ayrı Broker sözleşmesi zorunlu değildir. Değişimde ana sözleşme sürer, eski/yeni yetki aynı yürürlükte el değiştirir. Sözleşme sonu ilgili Broker yetkisi/işletme erişimini derhal kapatır; başka geçerli Broker ilişkisi yoksa kişi danışman statüsündedir. TERMINATED terminaldir; ayrı kapanış yükümlülükleri yetkiyi uzatmaz. Dokuz aktivasyon koşulu, kabul sırası ve açık hukuk/mali usuller [02 bölüm 8.4](02_BUSINESS_RULES.md#84-ofis-kuruluşu-modeli-ve-yaşam-döngüsü) ve 07'dedir. Bu hedef, teknik uygulama veya test kabulü değildir.

**3 Kasım 2026 — ADR-077:** Marka franchise/kurumsal politika ve sözleşme koşullarını belirler; ofisi kurar, Brokerı yetkilendirir, kurumsal statüleri ve ticari yükümlülükleri yönetir, tüm ağı denetler. Broker kendi ofisinin günlük işletmesini, ekibini ve müşteri/portföy/dosya dağıtımını yönetir. Markanın sözleşme, güvenlik ve kurumsal yükümlülük kapsamında müdahale edebilmesi günlük müşteri işinin sorumlusu olması değildir. Müdahale/itiraz usulü DQ-014/020/021'deki açık sınırları aşmaz. Aktör/karar matrisi tek yerde [02 bölüm 8.2](02_BUSINESS_RULES.md#82-marka-aktörleri-ve-yetki-ayrımı); mevcut modüllerin uygulama hedefi 01'de, finans kaynakları 03'tedir. Kod veya faz kabulü değildir.

**Son entegrasyon — ADR-076 (2 Kasım):** Broker kendi ofisinin operasyonunu ve müşteri/portföy dağıtımını yönetir; standart düzeni değiştirebilir. Kendi MAXIMUM havuzunda Broker unvanıyla çalışması için ayrıca Marka onayı gerekmez. Marka bütün ofislerin istatistiklerini izler, Brokerdan açıklama ister. Broker değişiminde açık işlerin yönetimi yeni Broker/yetkili yöneticiye; danışman ayrılığında ofis yönetimine otomatik geçer. Broker işi kendisi yürütür, atar veya yönetiminde bekletir. Yönetim devri fiilî çalışanı ve geçmiş kazancı otomatik değiştirmez; belge/tercih/sözleşme/geçmiş korunur. Ayrıntılar 02 bölüm 9 ve 07'dedir; uygulama kabulü değildir.

Organizasyon: GETMAKS markası → Ofis → aktif Broker yöneticisi ve Danışman üyeleri.

Tek marka altında birden fazla ofis yönetilebilir; her ofiste aynı anda tek aktif broker bulunur. Danışman brokerın alt hesabı değildir, ofisin profesyonel üyesidir. İlk tek-ofis kurulum örneği kalıcı ofis sayısı sınırı değildir.

**28 Ekim 2026 ürün sahibi kararı:** MAXIMUM ve ALFA hem ofis türü hem danışmanın çalışma modelidir. Danışman hangi ofisi seçerse o modeli seçmiş olur. Ofis ve danışman için birbirinden bağımsız veya çelişen model seçimi yapılmaz. Geçmiş dosya/model snapshot'ları korunur; bu belge düzenlemesi veriyi dönüştürmez.

**1 Kasım ek kararı (ADR-072):** Kurulmuş ofisin türü değişmez. Broker devir sonrası yönetim yetkilerini bırakır; diğer tür için ayrı Ofis Başvurusu yapar. Yönetim görevinin bitişi profesyonel kimliği bitirmez. Ofis şartı öz kabulü aktivasyonu, danışman anlaşması öz kabulü operasyonu açan ayrı koşullardır. Ayrıntılar ve yeni havuz/iki taraf danışmanı kuralları 02/03'tedir; kararların yazılması uygulanmış kod veya kabul değildir. ADR-078 ayrımı geçerlidir: aktif Brokerın mesleki işi için unvan dönüşü gerekmez; ilgili resmî ilişki bitince başka geçerli Broker ilişkisi yoksa kişi danışman statüsüne döner, işletme erişimi sürmez.

Her hesap temel Üye/Müşteri alanını korur. Profesyonel kimlik, ofis üyeliği, broker görevi ve müşteri dosya tarafı ayrı kavramlardır. **2 Kasım ADR-075:** Broker ofise atanmasıyla Broker unvanını taşır; ilan, müşteri ilişkisi, portföy ve işlemi kendi Broker unvanıyla yürütebilir. Danışman unvanına dönmesi veya ayrıca danışman statüsü alması gerekmez. Yönetim yetkisi ile kendi mesleki çalışma hakkı ayrıdır; yönetici olmak başkasının aktif müşteri/portföy hakkını veya kazancını kendiliğinden vermez. Temel profesyonellik korunur; Broker ve Danışman aynı mesleki unvan sayılmaz.

**Güncel hedef yedi paneldir (ADR-075):** Marka, MAXIMUM Ofis, ALFA Ofis, Danışman, Stratejik İş Ortakları, Marka Yatırımcı ve Nihai Müşteri. Standard Member bütün kullanıcıların ortak temel üyeliğidir; Nihai Müşteri/Standart görünümünden ayrı sekizinci ticari panel değildir. Önceki altı panel sayımı, Ofis Panelini MAXIMUM/ALFA olarak ayıran bu hedefle güncellenmiştir. Aynı kişi geçerli ilişkileriyle birden fazla panel kullanabilir; hedef yedi panelin mevcut kodda hazır olduğu iddia edilmez. MAXIMUM ekran tasarımı tarihsel ayrı kapsamdadır; ADR-078 ortak ofis yaşam döngüsünü netleştirir, ALFA ekranlarını geliştirme veya yedi panelin tamamlandığı anlamına gelmez.

## Operasyon omurgası

Tek ana iş akışı ve sorumluluklar [02 — İş kuralları](02_BUSINESS_RULES.md) içindedir. Ofis modeli, hizmet paketi, işlem türü ve ilan yöntemi birbirinden ayrı seçimlerdir.

Talep tarafı: Üye/Müşteri → Talep Dosyası → atama ve hizmet süreçleri.

Mülk sahibi tarafı: Müşteri → hizmet teklifi/kabul → Hizmet Dosyası → sözleşme ve yetkilendirme → gayrimenkul/portföy/ilan.

Hedef devam: eşleşme → randevu/gösterim → teklif → İşlem → Finans. Bu zincirin belgelenmesi tüm adımların uygulandığı veya kabul edildiği anlamına gelmez.

Data Havuzu MAXIMUM ofisindeki müşteri, talep ve portföy çalışmalarının operasyonel alanıdır; kaynağın ortak görünmesi bütün sorumluluk ve kazançların devri değildir. Kazanç Havuzu MAXIMUM finansal katkı ve dönemsel dağıtım mekanizmasıdır. ALFA'da bu ortak havuzlar varsayılmaz. Atanmamış üye Talep Dosyası da ayrı kaynak kaydıdır. Üç mali kaynak korunur: ofis–Marka ticari ilişki/sözleşmesi, gerçekleşmiş İşlem Dosyası hizmet geliri ve peşin müşteri hizmet satın alma/ödeme kaydı. İlan ücreti veya pazaryeri komisyonu bugün kararlaştırılmış sayılmaz (03; DQ-022).

## Kapsam ve çalışma disiplini

- MVP tek pazaryeri hedefler; public tanıtım/landing ve çoklu pazaryeri kapsam dışıdır.
- Güncel çalışma sınırı ve açık kabul kapıları [handoff](09_CODEX_HANDOFF.md) içindedir.
- Bir fazın testleri geçse de ürün sahibi kabulü olmadan sonraki faz açılmaz.
- Oran, fiyat ve finansal sonuçlar kod içine gömülmez.
- Legacy dosyaları açık yeniden kullanım kararı olmadan kopyalanmaz.
- Zorunlu başlangıç sırası: 00, 01, 02, 03, 05, 07, 09.

Ayrıntılı belge yönlendirmesi: [rehber](README.md).
