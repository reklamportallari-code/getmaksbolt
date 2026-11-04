# Finans kuralları

Bu belge ticari/finansal anlamları tanımlar. Finans uygulamasının açılması ve kabulü [faz planı](05_PHASE_PLAN.md) ile [handoff'a](09_CODEX_HANDOFF.md) bağlıdır.

## Birbirinden ayrı kayıtlar

**3 Kasım 2026 — ADR-077, üç kaynak akışı:** Marka ticari koşulları ve yetkili mali takibi yönetir; Broker kendi ofisinin yükümlülüklerini/sonuçlarını, müşteri kendi paket/işlem koşullarını görür; hak sahipliği görüntüleme veya yönetim yetkisinden türemez. Etkilenen mevcut alanlar Commercial/Office, Transaction, ServicePurchase/ServicePaymentReceipt ve hedef Finance/RevenuePool'dur; yeni muhasebe mimarisi veya uygulama kabulü değildir.

| Akış | Dayanak / ilgili aktör | Ayrı tutulacak sonuç ve sınır |
| --- | --- | --- |
| A — Franchise ve ofis ticari ilişkisi | Ofis–Marka ticari ilişkisi, sözleşme/sürüm/koşullar; Marka ve ilgili ofis/Broker | Açılış, aylık/yıllık ve kararlaştırılmış diğer yükümlülükler. Tutar alanı veya ACTIVE sözleşme tahsilat değildir. Doğum/vade/iade/yenileme/yaptırım DQ-022'de açıktır. |
| B — Gayrimenkul aracılık hizmeti | Gerçekleşmiş İşlem Dosyası ve geçerli sözleşme/politika; müşteri tarafları ve gerçek hak sahipleri | Hizmet bedeli; ayrı marka/ofis/profesyonel hakları ve MAXIMUM Kazanç Havuzu katkısı. Paylaşım aynı hizmet bedelini ikinci kez gelir üretmez. İşlem açılması gelir/kapanış/ödeme değildir; DQ-008/011 sürer. |
| C — Peşin müşteri hizmet paketi | Kabul edilen paket/hizmet satın alma ve ayrı ödeme kaydı; müşteri ve yetkili banka kontrolü | ServicePurchase/ServicePaymentReceipt. Dekont yüklemesi tahsilat değildir; doğrulanmış ödeme ve geçerli dönem süreli hakkı açar (ADR-069/070). Ofis franchise borcunu veya B akışını otomatik kapatmaz. |

Tahakkuk, fatura, tahsilat, hakediş, dağıtım ve ödeme birbirinin yerine gösterilmez; her sonuç kendi dayanağına bağlanır. **Data Havuzu** müşteri/talep/portföy çalışmalarının operasyonel alanıdır; mali katkı ve dönemsel dağıtım **Kazanç Havuzudur**. ALFA'ya MAXIMUM ortak havuz/dağıtımı taşınmaz. İlan ücreti veya pazaryeri komisyonu kararlaştırılmış gelir kalemi değildir. Muhasebe görevi/panel kapsamı ve ikinci onay DQ-014; mali uygulama kapısı 05/09'dadır. Brokerın iş dağıtımı yetkisi marka ana fiyatını veya geçmiş kazanılmış tutarı değiştirme yetkisi değildir.

**ADR-076 — Yönetim devri mali devir değildir:** Broker değişiminde veya danışmanın ofis/çalışma ilişkisinin bitişinde açık işler otomatik yönetim sorumluluğuna geçer. Brokerın kendisinin yürütmesi, başka danışmana ataması veya yönetiminde bekletmesi geçmiş hakedişi, tamamlanmış işlem tarafını veya kazanılmış tutarı değiştirmez. Müşteri ilişkisi/portföy devri, fiilî çalışma ve kazanç hakkı ayrı izlenir. Devir yeni oran, üçüncü bireysel pay, otomatik borç veya ödeme üretmez; belge, sözleşme ve mali geçmiş korunur. Bu mali koruma uygulama/hakediş kabulü değildir.

SubscriptionPlan ürün/kapsam; Subscription dönem/atama; ChargePolicy ücret kuralı; PlanEntitlement erişim/kota; UsageEvent kullanım; ChargeAccrual bekleyen tahakkuktur.

Plan, tahakkuk, hakediş, fatura, tahsilat ve ödeme ayrı kayıtlardır. Tahakkuk veya ACTIVE sözleşme ödeme kanıtı değildir. Ücretsiz/hediye/indirim/waiver/özel şart ana fiyatı değiştirmez; standart şart snapshot'ı korunur.

## Ofis ve danışman ticari şartları

**ADR-078 — Ana sözleşme ve kapanışın mali sınırı:** Kaynak A'nın ana sözleşmesi Getmaks A.Ş. ile ilgili ofis tüzel kişiliği arasındaki Getmaks Ofis Franchise ve İşletme Sözleşmesidir. Broker şahsi görev/yükümlülüklerini aynı sözleşmede ayrı sıfatla kabul eder; ayrı Broker sözleşmesi zorunlu değildir. Bu kabul kendi başına yeni maaş/komisyon/borç veya geçmiş mali hakkın devri değildir. Broker değişiminde ana ofis sözleşmesi yürürlükte kalır; gerekli atama/ek kayıtları izlenir. Sözleşme iptal/sonunda Broker yetkisi/işletme erişimi derhal kapanır; başka geçerli Broker ilişkisi yoksa kişi danışman statüsündedir. Mali hesaplaşma ve teslim/kapanış tutanakları ayrı süreçtir, unvanı veya işletme erişimini uzatmaz. Geçmiş alacak/hakedişler korunur. Tutar/doğum/vade/yenileme/yaptırım/tasfiye ayrıntıları DQ-022, hukuk/imza incelemesi DQ-002'de açıktır; dokuz aktivasyon koşuluna belirsiz ödeme zorunluluğu eklenmez. Üç kaynak ve Data/Kazanç Havuzu ayrımı değişmez; uygulama veya muhasebe kabulü değildir.

- Marka aylık sistem bedeli, yıllık lisans, ofis bedeli, doğrudan broker/danışman ilişki bedeli, gerçekleşmiş işlem paylaşımı ve müşteri hizmet geliri ayrı ticari başlıklardır (ADR-071). Aylık/yıllık bedeller MAXIMUM/ALFA modelini seçtiren iki üyelik planı olarak sunulmaz; model ofisten gelir. Bu başlıklar yeni tutar veya uygulanmış tahsilat/fatura modülü tanımlamaz.
- Ofis–Marka franchise ilişkisi, ana ofis sözleşmesindeki beş yıllık franchise çerçevesi ve varsa aylık/yıllık ek yükümlülükleri taşır. Broker bu sözleşmede tanımlı görev/şahsi kabul sıfatıdır; ayrı zorunlu sözleşme/bedel değildir (ADR-078). Tutarlar sözleşme/politika kaydından okunur; yeni ödeme şartı üretilmez.
- Danışman ticari planı ayrı kavramdır. Ofis sözleşmesi danışman planına dönüştürülmez.
- Broker marka ana fiyatını değiştiremez; plan atama, indirim, ücretsiz hak ve limit aşımı yalnız etkin BrokerCommercialAuthority sınırındadır.
- Franchise ve aylık/yıllık ofis yükümlülükleri işlem hizmet bedeli dağılımına dahil değildir.
- Yapılandırılmış sözleşme formu şart snapshot'ı üretir; tahsilat üretmez.

Marka Panelinin hedef mali görünümü beklenen sabit gelir, tahakkuk, fatura, tahsilat, gecikmiş alacak, gerçekleşmiş işlem geliri, danışman/ofis hakedişi, MAXIMUM katkı/dağıtımı, ALFA işlem paylaşımı ve iptal/iade/düzeltmeyi ayrı gösterir. Koşul → tahakkuk → fatura → tahsilat → hakediş → dağıtım kavramsal ayrımdır; her olayın aynı sırada veya otomatik doğacağı varsayılmaz. İade/iptal önceki mali sonucu ilişkilendirilmiş düzeltmeyle izler. Sözleşmenin aktifliği kazanılmış tutar değildir. Vergi, tahsilat ve dağıtım kararı olmadan yeni varsayılan oran/tutar üretilmez. Mevcut kodun bu mali görünümlerin tamamını sunduğu iddia edilmez.

## Nihai müşteri hizmet bedeli ve hakediş

Hedef Finans akışında Getmaks nihai müşteriye hizmet bedeli faturası keser; tahsilat ayrı izlenir. İşlem kapanışının gerekli kanıtları, fiyat politikası ve sözleşme sürümleri tamamlanmadan hakediş kesinleşmiş gösterilmez.

Danışman hakedişi → danışmanın Getmaks'a hakediş faturası → Getmaks ödemesi ayrı yaşam döngüleridir. Ofis ve danışman hakedişi ayrı kayıtlardır. Beklenen hak, kesinleşen alacak ve ödeme aynı durum değildir.

Pay satırı işlem, hizmet/talep dosyası, ofis, taraf ve bağlı sözleşme/politika snapshot'ına dayanır. Sonraki model veya politika değişikliği geçmiş hesabı değiştirmez. Birden fazla ofis varsa her pay kendi ofis kapsamına bağlıdır; kapsam dışı finans verisi gösterilmez.

## MAXIMUM/ALFA ve Kazanç Havuzu

MAXIMUM/ALFA ofis türüdür; danışman seçtiği ofisin çalışma modelini kullanır. Bu seçim kendi başına alacak veya havuz hakkı doğurmaz; aktif kapsam ve yürürlükteki politika gerekir.

RevenuePolicy marka, ofis, danışman ve varsa Kazanç Havuzu pay parametrelerini saklar. Payların toplamı 10.000 basis-point'tir; mevcut ALFA Kazanç Havuzu payı sıfırdır. MAXIMUM payı kayıt üzerinden belirlenir. Oran, matrah ve uygunluk kod içine gömülmez.

Kazanç Havuzu hedefi: işlem geliri → PoolContribution → PoolPeriod → PoolDistribution → PoolEarning. Katkı, dağıtım ve hakediş ayrıdır; Data Havuzu ile ilişkisel olarak aynı kavram değildir. Gerçek hareketler Faz 6'nın kabul kapsamındadır.

ADR-066 (29 Ekim 2026): MAXIMUM ofiste tamamlanan işlemlerden yapılandırılmış oranlarla havuza katkı ayrılır. Ay sonunda işlem yapan/yapmayan tüm danışmanlara pay dağıtılır; kişisel işlem kapatmış olma şartı konulmaz. Eşit dağıtım kararı verilmemiştir. Katkı oranı/matrahı, dağıtım ağırlığı, dönem içinde katılma/ayrılma/transfer ve askı durumu, Brokerın kendi mesleki faaliyetiyle havuz katılımı, yuvarlama ve iade kuralları DQ-008 kapsamında netleşir. ADR-075 gereği bunun için Danışman unvanına dönüş şartı yoktur. İşlemin tamamlanması, tahsilat ve dağıtımın finanse edilme zamanı ayrı olaylardır; nakit oluşmadan ödeme yapılacağı varsayılmaz.

ALFA'da danışmanın datası ve bireysel kazancı kendisine aittir; danışmanlar arasında ortak havuz paylaşımı yoktur. Bu karar marka/ofis/broker sözleşme haklarının kaldırıldığı veya bütün hizmet bedelinin kesintisiz danışmana ödendiği anlamına gelmez. Bu ticari koşullar ayrıca kesinleştirilecektir; yeni oran üretilmez.

## İşlemde iki taraf danışmanı ve kaynak ofis transfer bedeli — ADR-072

**ADR-075 mesleki unvan güncellemesi:** Bu bölümdeki iki taraf danışmanı, gerçek alıcı/satıcı tarafı profesyonellerini anlatır. Broker gerçek mesleki taraf olarak Broker unvanıyla yer alabilir; danışmana dönmesi veya yönetici olduğu için üçüncü bireysel pay alması gerekmez. Kendi mesleki katkısı, ofis yönetim hakkı ve MAXIMUM katkısı ayrı dayanaklardır; yeni pay oranı tanımlanmaz.

Bireysel işlem kazancı satıcı ve alıcı tarafını temsil eden iki danışman arasında gerçekleşir. MAXIMUM havuz kaydını açmak, portföyü üstlenmek ve alıcıyı getirmek ayrı katkılardır; kayıt açan üçüncü kişi otomatik bireysel pay sahibi değildir. Örnek: Ayşe havuz müşteri kaydını açar, Ahmet portföyü alır, Selim alıcıyı getirir; bireysel paylaşım Ahmet ve Selim arasındadır. Bu, Ayşe'nin aylık MAXIMUM Kazanç Havuzu hakkını kaldırmaz. ALFA ortak havuza katılmaz.

İki danışmanın bireysel paylaşımı; marka/ofis sözleşme payları, MAXIMUM ortak havuz katkısı ve iş ortağının ayrı ek hizmet bedeliyle karıştırılmaz. Marka/ofis payları bu kararla sıfırlanmaz; üçüncü bireysel danışman payı yaratılmaz. İki taraf arasında eşit paylaşım, kesin matrah veya yeni oran belirlenmedi. Kişinin veriyi görmesi/çekmesi veya kayıt açması diğer kişinin kazanılmış maddi/manevi hakkını devretmez.

ADR-073: Transfer bedeli danışmanın yıllık en yüksek işlem cirosuna dayanır; yıllık toplam veya aylık ortalama seçilmez. %10–%30 aralığındaki somut bedel iki brokerın görüşüp kendi aralarında anlaşmasıyla belirlenir. Hedef ofis talep eder; kaynak ofis kabul ederse transfer gerçekleşir. Sistem tek başına oran, ödeyen kişi/hesap veya tahakkuk seçmez; brokerların anlaşması tahsil edildi sonucu değildir. Takvim yılı/son 12 ay sınırı, işlem cirosunun vergi kapsamı, vade, ödeme/iade kanıtı ve ödeme-transfer bağı DQ-018'de kalır. Belgeleme değişikliği mevcut veriye mali hareket yazmaz; bedeller hesaplama koduna gömülmez.

ADR-075 yıllık dönemi geriye dönük yıllık dönem olarak açıklar. Yukarıdaki tarihsel takvim yılı seçeneği artık hedef seçenek değildir; referans anı/kesim ve mali kanıt ayrıntıları DQ-018'de kalır. MAXIMUM Ofis Panelindeki Kazanç ve Hakediş menüsü bu ayrımları gösterir; mevcut ticari koşul görünümü gerçekleşmiş hakediş/dağıtım olarak sunulmaz.

## Stratejik iş ortağı

Stratejik iş ortağı ana işlem hizmet bedelinden varsayılan pay almaz. Marka somut hizmet/görev için müşteriden ayrı peşin uzman hizmet bedeli veya iş ortağının kendi işinden markaya komisyon modelini açıkça yapılandırabilir. Belirsiz koşul veya otomatik formül üretilmez.

Ortak yalnız kendi görevine ve seçilmiş modele ait kayıtları; danışman kendi hakedişini; broker yetkili ofisini; marka yetkili ağ kapsamını görür. Nihai müşteri iç profesyonel paylaşımı görmez.

## Kayıt ve hesap güvenceleri

- Para minor-unit integer + ISO para birimi; oran basis-point integer.
- Fiyat, vergi, dönem, hak, tahakkuk ve tahsilat ayrı alanlardır.
- İptal/iade/düzeltme eski kaydı silmez; ilişkilendirilmiş ters/düzeltme hareketi üretir.
- Kullanım, kapanış, tahsilat, dağıtım ve ödeme idempotent olmalıdır.
- Sağlayıcı doğrulaması olmadan başarılı fatura/ödeme sonucu gösterilmez.
- Yuvarlama, vergi, iade ve finans sağlayıcısı gibi kesinleştirilmemiş ayrıntılar [açık kararlar](07_DECISIONS.md) kapsamında kalır.

## Ana iş akışına bağlı açık mali koşullar — 29 Ekim 2026

30 Ekim ADR-069/070, Birebir Destek'in aylık peşin; Uzman Hizmet'in yalnız başarılı işlem sonunda ücretleneceğini kesinleştirdi. Uzaktan Destek ücretinin zamanı/tarifesi; iş ortağı ek hizmetinin müşteriye sunumu/onayı, alacaklısı ve tahsilat zamanı; artırmanın olası katılım/teminat bedelleri açık kalır. Belirlenmeyen koşuldan otomatik borç üretilmez.

Başlangıç Uzman Hizmet politikaları veritabanındadır: satışta alıcı/satıcı ayrı ayrı %2; kiralamada kiracı bir aylık kira, kiraya veren sıfır; devirde devreden/devralan ayrı ayrı %10. İşlem türü ve ücret tarafı eşleşmelidir. Yeni teklifler politika snapshot'ını korur; tarife değişikliği geçmiş kabulü yeniden hesaplamaz. Bu kayıtlar tamamlanan işlemde fiili alacak/fatura oluşturulduğu anlamına gelmez.

Peşin paket ServicePurchase ve ayrı ServicePaymentReceipt kayıtlarıyla izlenir. Teklifte vergiler dahil ödenecek toplam açıkça yazılır. Müşterinin dekont yüklemesi tahsilat değildir; marka bankadaki hareketi gerçek tutar, para birimi, benzersiz referans ve kontrol notuyla doğrular. Doğrulama bir aylık erişim açar; süre sonu, iptal/duraklama ve yeni dönem ayrı denetlenir. Sanal POS/banka API entegrasyonu, fatura veya Kazanç Havuzu olarak sunulmaz. Aktarım/yenileme eski hareketi silmez.

Brokerın ofis yönetimi ile kendi Broker unvanıyla yürüttüğü mesleki işin mali hak gerekçeleri ayrı izlenmelidir; bunun için ikinci Consultant kimliği/unvanı gerekmez (ADR-077). Bu karar ek pay oranı tanımlamaz; çift sıfat aynı hakkı iki kez üretmez. İşlem sonucunun müşteriye, danışmana, ofise, markaya ve iş ortağına yansıması ilgili geçerli sözleşme/politika koşullarına dayanır. Yatırımcı için işlem gelirinden otomatik pay varsayılmaz.
