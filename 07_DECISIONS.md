# Güncel kararlar ve açık konular

Güncelleme: 3 Kasım 2026. ADR-078, ADR-077 yetki sınırını ofis/Broker yaşam döngüsü, ana sözleşme ve hazırlık/aktivasyon/kapanışla bütünleştirir. ADR-075/076'nın geçerli görev sırasında Broker unvanıyla çalışma ve geçmiş hakları koruma ilkeleri sürer; görevin kazanılması/sona ermesi artık ADR-078'de kesindir. Eski kararlar silinmez, tarihsel öncelikleri belirtilir. Davranış 02/03'te, uygulanma ve kabul kanıtı 09'dadır.

## ADR-061 — Ofis türü danışmanın çalışma modelini belirler

**Durum: ürün sahibi tarafından 28 Ekim 2026 tarihinde açıkça kesinleştirildi.**

“Ofis türüdür. Aynı zamanda Danışman çalışma modelidir. Bir danışman hangi ofisi seçmişse o modeli seçmiş demektir.”

- MAXIMUM ve ALFA hem Office türü hem Consultant çalışma modelidir.
- Seçilen ofisin modeli danışmanın modelini belirler; ayrı ve çelişen danışman modeli seçimi yapılmaz.
- Office.office_type güncel model kaynağıdır; ProfessionalWorkModel tarihçesi ve dosya snapshot'ları korunur.
- Ofis transferinde hedef ofisin modeli esas alınır. Eski dosyalar geriye dönük yeniden hesaplanmaz.
- Bu karar yeni oran, ücret, otomatik veri dönüşümü veya faz onayı değildir.
- ADR-003/037'nin “ofis tipi değildir” ifadesi ve ADR-060'ın iki modeli bağımsız eksen olarak bırakan yorumu bu kararla geçersizdir. Eski kayıtları koruma kuralı sürer.
- NULL/uyumsuz eski veriler, ofis türü sonradan değişirse yürürlük/etki ve transfer sınırları ayrı inceleme konusudur.

## ADR-062 — Tek güncel belge seti

Bu revizyonla yedi çalışma belgesi korunur; ayrıntılı ürün kaynakları tek referansta birleşir. Veri modeli/legacy 01'de, kabul 09'da, açık kararlar bu belgededir. Yeni değişiklikler yalnız kök CHANGELOG'a yazılır. Eski raporlar ve sürümler güncel talimat olarak okunmaz.

## ADR-063 — Temel profesyonel danışmandır; brokerlık ofis görevidir

**2 Kasım güncellemesi:** Temel profesyonel kaydı/kimliği koruma sürer. Brokerın işlem için Danışman unvanına veya ayrı danışman statüsüne geçmesini gerektiren yorum ADR-075 ile geçersizdir; Broker kendi mesleki unvanıyla çalışır.

**Durum: ürün sahibinin açık anlatımıyla kesin.** Her gayrimenkul profesyoneli önce Gayrimenkul Danışmanıdır. Franchise ofisi açması veya marka şubesine atanması Broker unvanını/görevini doğurur. Brokerlık danışmanlığın yerine geçmez. Kodun mevcut karşılıklı dışlayan BROKER/CONSULTANT türleri bu hedefe uyarlanmış sayılmaz; geçmiş ve erişim korunarak ayrı uygulama gerekir. Stratejik iş ortağının uzman profesyonelliği kendiliğinden gayrimenkul danışmanı veya broker yetkisi vermez.

## ADR-064 — Altı panel aynı işin farklı sorumluluklarını taşır

**Tarihsel sayım:** 2 Kasım ADR-075 hedefi yedi panele ayırır: MAXIMUM ve ALFA ayrı Ofis Paneli deneyimleridir. Standard Member temel üyelik olup sekizinci ticari panel değildir. Aşağıdaki altı sayımı yeni hedef olarak uygulanmaz; ortak kaynak/ilişki/kapsam ilkesi sürer.

**Durum: ürün sahibi kararı kesin.** Standart, Danışman, Ofis, İş Ortakları, Yatırımcı ve Getmaks panelleri vardır. Broker görevini Ofis Panelinde yürütür. Her üyede Standart Panel korunur; ek alanlar geçerli görev/ilişkilerinden doğar. Paneller kişi, görev, işlem ve sonuçla birlikte geliştirilir. Bir panel seçimi yeni yetki yaratmaz; aynı kişinin hangi sıfatla hareket ettiği izlenir. Ayrıntılı yetki ve iş ortağı/yatırımcı hakları ayrıca belirlenir.

## ADR-065 — Amaç aracılık ve sonuç; ilan yöntemi ayrı eksendir

**Durum: amaç, iki yöntem ve teklif sonrası yol kesin; ayrıntılı kapılar açık.** Alım–satım, kiralama ve devir için standart ilan veya açık artırma usulü ilanla taraflar buluşturulur. Ofis modeli, hizmet paketi, dosya türü ve ilan yöntemi karıştırılmaz. Talep, Hizmet ve İşlem Dosyalarının ana akışı 02'de tutulur. Ürün sahibinin 29 Ekim yanıtı: seçilen açık artırma teklifi taraf onayına ve sözleşme sürecine gider. Teklif seçimi otomatik satış, işlem tamamlanması veya tahsilat değildir.

## ADR-066 — MAXIMUM ekip ve aylık havuz; ALFA bağımsız çalışma

**Durum: ürün sahibinin 29 Ekim 2026 yanıtıyla kesin.** MAXIMUM ofiste broker ve danışmanlar ekip olarak çalışır. Danışman Data Havuzundan Talep Dosyasını alır; müşteriye uygun portföy bulunamaz ve takip sürdürülecekse havuza geri bırakır. Aynı talebin kimliği, çalışma geçmişi ve takip durumu korunmalıdır. Mevcut PoolRecord → RequestFile dönüşümü bu geri bırakma döngüsünü karşılamış sayılmaz.

MAXIMUM ofiste tamamlanan işlemlerden belirli, yapılandırılmış oranlarla Kazanç Havuzuna katkı ayrılır; ay sonunda işlem yapan/yapmayan tüm danışmanlara dağıtılır. Ofisteki her hareket ekibe katkıdır. Eşit pay, oran, matrah ve dönem içi değişiklik kuralları bu karardan türetilmez. Data Havuzu talep yönetimi; Kazanç Havuzu mali katkı/dağıtımdır.

ALFA danışmanlar birbirinden bağımsız, marka ve ofis/brokera bağlı çalışır; datası ve bireysel kazancı kendisine aittir, ortak havuz paylaşımı yoktur. Marka/broker sözleşme haklarının sıfırlandığı varsayılmaz. Geçmiş snapshot'lar korunur; bu karar veri geçişi, finans uygulaması veya faz kabulü değildir.

## ADR-067 — Giriş doğrudan ilgili panele gider

Panel içinden çalışma alanı değiştirme kutusu ve girişten sonra ek panel seçme ekranı kullanılmaz. Giriş hesaba göre doğrudan Standart/Getmaks/Ofis/Danışman paneline gider. Yerel deneme hesabı kısayolları ilk giriş formunda bilgileri doldurur; normal parola doğrulamasını aşmaz. Değiştirilmiş parolalar tahmin edilmez veya sıfırlanmaz. Panel kapsamı oturumdaki seçime değil isteğin adresine bağlıdır; iki sekme birbirinin kapsamını değiştirmez. Bir kişinin diğer sıfatındaki yetkileri danışman/müşteri ekranındaki veri kapsamına taşınmaz.

## ADR-068 — Başvuru ofis içindir; broker görevi ofisten doğar

Bağımsız Broker Başvurusu oluşturulmaz. Standart üye Ofis Başvurusu yapar; marka kabulünde aynı kullanıcıya bağlı temel danışman kimliği, marka üyeliği ve oluşturulan ofiste broker görevi kurulur. Başvuru broker üyeliğine açık yabancı anahtarla bağlanır. Mevcut danışman da kendi ofisinin yöneticisi atanabilir; eski üyelik/model tarihçesi korunur. Ofis, kuruluş/belge/sözleşme koşulları tamamlanmadan operasyon açmaz. Eski BROKER türü ve başvuru kayıtları silinmez veya topluca dönüştürülmez; yeni broker kuruluşları temel CONSULTANT kimliğini kullanır.

## ADR-069 — Üç hizmet paketi ve değiştirilebilir ücret koşulları

30 Ekim ürün sahibi açıklaması önceki paket yorumlarının önündedir:

- Uzaktan Destek online danışmanlıktır. Ücretin zamanı ve tarifesi ayrıca yapılandırılır; Uzman Hizmet'in başarı koşulu buna kendiliğinden uygulanmaz.
- Birebir Destek'te mülk sahibi süreli erişimle satış/kiralama/devri kendisi yürütür, Getmaks refakat eder. Aylık bedel önceden alınır. 15.000/30.000 TL örnektir; sabit tarife değildir.
- Uzman Hizmet'te tüm satış/aracılık/işlem süreci Getmaks tarafından yürütülür. Peşin ücret yoktur; işlem gerçekleşirse ücret doğar. Geçerli sözleşme ve yetkilendirme kanıtları ayrıca gerekir.
- Başlangıç Uzman Hizmet tarifeleri: satışta alıcı ve satıcıdan ayrı ayrı %2; kiralamada yalnız kiracıdan bir aylık kira bedeli, kiraya verenden sıfır; devirde devreden ve devralandan ayrı ayrı %10. Bunlar değiştirilebilir ServicePricingPolicy kayıtlarıdır, hesaplama koduna gömülmez. Vergi ve gerçekleşen bedelin kesinleştirilmesi ayrıca sözleşmede belirlenir.
- Paket kapsamı ve seçilen fiyat politikası yeni teklif oluşturulurken snapshot olarak korunur. Başka tarafın tarifesi müşteriye uygulanamaz. Sonraki paket/politika değişikliği eski teklifi değiştirmez.

## ADR-070 — Peşin paket için havale kontrolü ve süreli erişim

Uygulanan ilk tahsilat yolu havaledir: müşteri ödeme belgesini özel depoya yükler; marka yetkilisi bankadaki hareketi kontrol edip gerçek tutar, para birimi, benzersiz banka referansı ve kontrol notuyla doğrular. Yükleme tek başına tahsilat veya erişim değildir. Bu yol sanal POS veya otomatik banka doğrulaması olarak sunulmaz.

Teklifte vergiler dahil ödenecek toplam açıkça girilir; belirsiz vergi/yuvarlama kuralından toplam türetilmez. Doğrulama sonrası bir aylık kullanım başlar; sürenin sonunda erişim kontrolü yazımları da kapatır. Aynı banka hareketi ikinci paketi açmaz. Müşteri, süre bitince aynı koşullarla bir aylık yenilemeyi açıkça isteyebilir; yeni dönem ayrı kayıt ve yeni tahsilat ister. İptal/duraklama erişimi engeller. Yeni profesyonel rol veya ayrı bir yedinci panel oluşturulmaz; mülk yönetimi müşterinin Standart Panelindedir. Fatura, otomatik POS, iade ve genel hakediş/Kazanç Havuzu bu teslimin tamamlanmış kapsamı değildir.

## ADR-071 — Marka Paneli ürün ve işleyiş sözleşmesi

**Güncel öncelik — ADR-072/075/076/077:** Aşağıdaki özgün kayıt tarihsel aşamayı korur. Kapı eşlemesi DQ-015 ile kesinleşti; ofis türü değişmez, Brokerın kişisel işi için danışman unvanına dönüş gerekmez, ayrılıkta açık işlerin yönetim devri ADR-076 ile kesindir. Marka operasyon görevi günlük müşteri işini devralma yetkisi değildir (ADR-077). Bu eski açık/geçiş ifadeleri yeni kararın önüne geçmez.

**Durum: 1 Kasım 2026 ürün sahibi metnindeki kesin ilkeler kaydedildi; uygulama ve faz kabulü değildir.** Ayrıntılı tanım ve 16 kabul ölçütü tek yerde 02'nin 8. bölümündedir; mali ayrımlar 03'tedir. Yeni panel şartnamesi dosyası açılmaz.

Marka yönetim merkezidir; bütün kayıtların sahibi/tarafı veya başkası adına kabul eden değildir. Marka kullanıcılarında üst yönetim, operasyon, ticari yönetim, profesyonel ilişkiler, denetim ve hizmet görevlerinin yetkileri ayrılır. Bunlar hedef iş sıfatlarıdır; teknik atama modeli DQ-014'tedir. Kalıcı User.role seçili paneli aşamaz. Dashboard ile liste aynı sorgu/kapsam/filtreyi kullanır. Kritik işlem kullanıcı, panel, sıfat, kurumsal kapsam, izin, hedef, karşı taraf, kabul kanıtı ve sonucu izler. Olay/görev/bildirim/teslim/kabul ayrı sorumluluklardır.

Ofis türü kontrollü geçiştir, profil güncellemesi değildir. Broker görevinin bitişi profesyonelliği kendiliğinden bitirmez; danışman devamı açık işlem ister. Transferde dosya taşıma veya erişim kapanışı otomatik varsayılmaz. Ofis şartı ve danışman anlaşması kabulü ayrı kalır; kapı eşlemesi henüz kesinleşmedi. Bu sınırların ayrıntıları DQ-005/010/015/016'dadır.

İş ortağı/yatırımcı ve kapsamlı mali görünüm hedef sorumluluklardır; uygulanmış özellik sayılmaz. Kaynak metnin sonundaki açık karar sınırı korunur: uygulama talimatına geçmeden ilgili kurallar netleşir. Yeni oran, teknik yetki modeli, veri dönüşümü veya ileri faz onayı türetilmez.

## ADR-072 — Sabit ofis türü, danışman devamı, iki kabul ve MAXIMUM çalışma hakkı

**Güncel öncelik:** Aşağıdaki özgün 1 Kasım kaydı tarihsel olarak korunur. Aktif görevde mesleki unvan ADR-075/076, ilişki sonu statü ve ana sözleşme yaşam döngüsü ADR-078, açık iş yönetim devri ADR-076 ile güncellenmiştir. Ofis türü değişmezliği ve danışmanın iki kabulü geçerlidir. Eski “anlaşma bitince yeni Brokerla devam” ifadesi, yürürlükte ana sözleşmede Broker değişimi ile sözleşmenin sona ermesini eşitlemez.

**Durum: 1 Kasım 2026 ürün sahibinin üç soruya yanıtı ve ek açıklamalarıyla kesinleşen iş kuralları; uygulama/veri geçişi veya faz kabulü değildir.**

- Ofis çalışma şartlarının öz kabulü aktivasyon, danışman anlaşmasının öz kabulü operasyon için zorunludur. İki kanıt ayrıdır; anlaşma kaydı yok diye operasyon muafiyeti yoktur. DQ-015 kapandı.
- Broker görevi bitince aynı ofiste danışman olarak devam edilir; ofisten ayrılma ayrı işlemdir. Ofis yönetim/ticari yetkileri kapanır; temel kimlik korunur. DQ-016 kapandı.
- Kurulmuş ofiste MAXIMUM/ALFA türü değiştirilemez. Broker ofisi markaya/yeni brokera devreder, danışman olur; diğer tür için ayrı Ofis Başvurusu yapar. Mevcut ofis anlaşması bitince marka broker atar veya ofis marka yönetimine geçer. ADR-071'deki yerinde kontrollü tür değişimi hedefinin yerine bu karar geçer; DQ-005'in ana kararı kapandı. Devir/temsil ve açık işlerin devamı DQ-010'da kalır.
- İşlemde satıcı/alıcı tarafını temsil eden iki danışmanın bireysel kazanç paylaşımı vardır. Ayşe havuz kaydını açar, Ahmet portföyü alır, Selim alıcıyı getirirse bireysel paylaşım Ahmet/Selim arasındadır. Ayşe'ye üçüncü bireysel pay doğmaz; MAXIMUM aylık ortak havuz hakkı korunur. Marka/ofis paylarının sıfırlandığı veya iki danışmanın eşit paylaşacağı sonucu çıkarılmaz.
- Transferde kaynak ofise "son yaptığı en yüksek ciro"nun %10–%30 aralığında bedel vardır. Matrah/dönem, oranı belirleyen ve ödeyen henüz net değil (DQ-018); otomatik hesap/borç üretilmez.
- Danışmanın kendi veya ofisinin taşınmaz ticareti yetki numarası, mesleki belge/sözleşme ve EİDS yetki/yeterlilik kontrolü ürün gerekliliğidir. Danışmanda MYK, temel eğitim, şahıs vergi levhası ve danışman sözleşmesi; ofiste Seviye 5 MYK, temel eğitim, LTD vergi levhası, danışman/ofis sözleşmeleri istenir. Bu kayıt hukuki uygunluk veya entegrasyon doğrulaması değildir; uygulama ayrıntıları DQ-019'dadır.
- MAXIMUM havuzu ofisin yetkili danışmanlarının ortak çalışma kaynağıdır; veri saklama ve eşzamanlı müşteri araması engellenir. Çekim sonrası 24 saatte bırakma veya ilerleme; randevu/aksiyon için 3 gün koruma; görüşülen müşteriye 15 gün aramama kuralı belirlenmiştir. Zaman başlangıcı, otomatik bırakma ve aktör kapsamı DQ-017'dedir. Geçici üstlenme başkasının hakkını devretmez. ALFA'da ortak havuz yoktur.

## ADR-073 — Havuz zamanları ve karşılıklı ofis transferi

**Durum: 1 Kasım 2026 ürün sahibinin DQ-017/018 açıklaması; uygulama veya faz kabulü değildir.**

- Çekimden 24 saat sonra ilerleme yoksa otomatik geri bırakılır. Randevu varsa 3 günlük koruma gerçekleşen görüşmeden sonra başlar. Son görüşmeden itibaren 15 gün aramama aynı danışmanı da kapsar. Claim veya 3 günlük koruma bitişi 15 günlük arama yasağını kaldırmaz.
- Yetki/sonuç alındığında Talep Dosyası ve Hizmet Dosyası İşlem Dosyasında ilişkilendirilir; kaynak geçmişi korunur. İşlem açılışı, tamamlanma ve mali sonuç farklıdır; tür bazlı kanıtlar DQ-011'de kalır.
- Transfer bedelinin dayanağı yıllık en yüksek işlem cirosudur. Önceki %10–%30 aralığında somut bedeli iki broker görüşüp kendi aralarında kararlaştırır; sistem otomatik bir oran/borç/ödeyen seçmez.
- Transfer talebini yeni/hedef ofis yapar; mevcut/kaynak ofis kabul ederse gerçekleşir. Olağan transfer tek taraflı marka atamasıyla veya kaynak kabulü olmadan tamamlanmaz. Karşılıklı kabul, yürürlük ve ödeme ayrı izlenir; geçmiş dosyalar otomatik taşınmaz.

Önceki ADR-072'de açık bırakılan süre başlangıcı/aktör ve transfer matrahı/başlatan-kabul eden soruları bu yanıtla çözülmüştür. DQ-017/018 yalnız kalan uygulama ayrıntılarını taşır; aynı sorular yeniden açılmaz.

### ADR-073 uygulama eki — randevu kanıtı ve müşteri iletişim tercihi

**Durum: ürün sahibinin ek açıklamasıyla kesin; uygulama/test kabulü değildir.** İlk çekimden 24 saatte somut aksiyon yoksa otomatik havuza bırakılır. Tarih/saatli randevu; müşteriyle iletişim ve müşteri teyidi kanıtıyla desteklenirse görüşme gerçekleşene kadar danışmanı korur. Kayıt oluşturma düğmesi veya kanıtsız ileri tarih yeterli değildir.

Görüşme tamamlandıktan sonra 3 günlük çalışma koruması başlar; ilerleme yoksa havuza dönüş olur. İptal veya müşterinin gelmemesinde 24 saat yeniden planlama hakkı vardır; yeni randevu/aksiyon yoksa havuza döner. Yeni randevu aynı iletişim/teyit kanıtı koşullarını taşır. Danışmanın kendi ihmali ek süre kazandırmaz.

Randevu oluşturma, müşteri teyidi, gerçekleşme, iptal, müşteri gelmedi ve yeniden planlama ayrı olay/kanıt kayıtlarıdır; gerçek aktör/zaman/gerekçe izlenir. Bunlar mevcut uygulamada hazır enum/işlev sayılmaz.

Son gerçekleşen görüşmeden 15 gün boyunca aynı danışman dahil müşteri aranamaz. Koruma bitişi/yeniden planlama bu sınırı aşamaz. 15 günün dolması tek başına arama izni değildir; diğer izinler ve müşteri tercihleri korunur. Müşteri aranmamak istediğini belirtirse tercih derhal uygulanır; süre bitişi otomatik yeniden izin oluşturmaz. DQ-017'de teyitli randevu, iptal/gelmeme ve tercih önceliği soruları kapanmıştır.

## ADR-074 — MAXIMUM Data Havuzunda izleme, yetkilendirme ve çalışma ayrımı

**2 Kasım güncellemesi:** Marka izleme/ofis izolasyonu ve danışmana broker yetkilendirmesi korunur. Brokerın kendi mesleki faaliyetini yalnız Danışman Panelinde/danışman unvanıyla yapabileceği kısmı ADR-075 günceller. Eski metin tarihsel gerekçe olarak korunur; brokerın yönetim gücüyle başkasının hakkını alması hâlâ yasaktır.

**Durum: ürün sahibinin açık düzeltmesiyle kesin; uygulama veya faz kabulü değildir.** Bu karar Data Havuzu müşteri çalışma kapsamındadır; markanın genel kurumsal yönetimini veya ayrı Kazanç Havuzu mali kurallarını kaldırmaz.

- Data Havuzu yalnız ilgili MAXIMUM ofisinin özelliğidir. ALFA'da ortak havuz yoktur. Markanın atama bekleyen üye talepleri listesi MAXIMUM Data Havuzu değildir.
- Marka bütün ofisleri, broker Ofis Panelinden yalnız kendi ofisini izler. Data Havuzunda izleme ilgili MAXIMUM ofis kaynağında kalır; Marka/Ofis paneli müşteri çekme, geri bırakma, temas/randevu veya ilerleme yazımı yapmaz. Bütün ofisleri izlemek ALFA'da ortak havuz bulunduğu anlamına gelmez.
- Havuz üzerinde çalışma hakkını broker yetkilendirir; müşteri üzerindeki çalışma işlemleri yalnız yetkili danışmanın Danışman Panelindedir. Brokerın Ofis Panelinden yetkilendirme yapması kendisine o panelde müşteri çalışma hakkı vermez.
- Marka yöneticisi/broker ayrıca danışmansa aynı müşteri üzerinde yalnız danışman sıfatı, geçerli ofis ilişkisi ve broker yetkilendirmesiyle çalışabilir. Kalıcı rol veya panel seçimi tek başına çalışma hakkı değildir.
- Havuzun ortak görünürlüğü, kişilerin mevcut hakları, eşzamanlı çalışma/iletişim korumaları ve ADR-073 süreleri korunur. Yetkilendirme bu korumaları aşamaz; başka ofis veya ALFA'dan otomatik erişim açılmaz.
- Eski belgelerin marka/broker havuz yazımı anlamına gelen ifadeleri hedef yetki olarak kullanılmaz. Teknik izin listesi/controller/middleware uyarlaması ve doğrulaması ayrı uygulama işidir. Yetkilendirmenin kişi/görev kapsamı ve geri alınmasının devam eden işe etkisi açık tasarımda ayrıca izlenir; her müşteri çekimi için yeni broker onayı gerektiği varsayılmaz.

## ADR-075 — Yedi hedef panel ve MAXIMUM Ofis Paneli tasarımı

**ADR-078 yaşam döngüsü sınırı:** Aktif Brokerın kendi unvanıyla mesleki çalışması korunur; davet/hazırlık bu unvanı vermez. İlgili resmî ilişki bitince başka geçerli Broker ilişkisi yoksa danışman statüsüne dönüş kesindir; aşağıdaki “danışmana dönüş gerekmez” ifadesi aktif görevde işlem yapmak içindir.

**Son entegrasyon önceliği:** Aşağıda o aşamada DQ-020/021'e bırakılan kişisel havuz üstlenme, dağıtım/sorumlu belirleme ve ayrılıkta otomatik yönetim devri ADR-076 ile kesinleşti. Eski açık karar cümleleri tarihsel aşamayı gösterir; güncel bekleyen karar değildir.

**Durum: 2 Kasım 2026 ürün sahibinin MAXIMUM taslağı ve entegrasyon talimatındaki açık hükümler.** Yalnız belge/tasarım çalışmasıdır; yeni mimari/veri modeli/kod/migration/seed/test veya faz kabulü değildir. Ana ürün ve ekran/etkileşim/kabul sözleşmesi tek yerde 02 bölüm 9'dadır. ALFA panel tasarımına geçilmez.

- Yedi hedef panel: Marka, MAXIMUM Ofis, ALFA Ofis, Danışman, Stratejik İş Ortakları, Marka Yatırımcı, Nihai Müşteri. Standard Member ortak temel üyelik ve müşteri alanıdır; sekizinci ticari panel değildir. Önceki altı sayımı güncellenmiştir; mevcut kod yedi panel hazır sayılmaz.
- Broker atandığı andan itibaren Broker unvanıyla ilan, müşteri ilişkisi, portföy ve işlem yapabilir. Danışmana dönüş veya ikinci danışman statüsü şartı yoktur; MAXIMUM/ALFA ortak mesleki ilkedir. Tek profesyonel kimlik korunur; yönetim yetkisi ve kendi mesleki faaliyeti ayrı sıfat/izin/kanıttır. Salt yönetimden müşteri/portföy/kazanç hakkı doğmaz.
- Marka tüm ofisleri denetler ve kurumsal yetkisini kullanır; MAXIMUM Data Havuzunun günlük çalışma sahibi değildir. Broker kendi ofisini yönetir/yetkilendirir. Danışmanın çalışma kapsamı broker yetkisine bağlıdır. Başka ofis ve ALFA havuz erişimi otomatik değildir. Brokerın kendi havuz üstlenmesi/çıkar çatışması ayrıntıları DQ-020'de açık kalır; kendi mesleki faaliyet hakkı yeniden sorulmaz.
- Kayıt kaynağı, çalışma hakkı, müşteri ilişki sorumlusu, portföy sorumlusu ve işlem kazanç tarafı ayrı tutulur. Bireysel paylaşım iki taraf profesyoneli arasındadır; Broker gerçek işlem tarafıysa kendi unvanıyla yer alabilir. Yönetici veya ilk kayıt sahibi olmak üçüncü bireysel pay yaratmaz. Marka/ofis hakkı ve ortak havuz ayrı kalır; yeni oran/vergi üretilmez.
- ADR-072'nin ofis türü değişmezliği, devir sonrası danışman devamı, iki kabul; ADR-073'ün 24 saat, teyitli randevu, görüşme sonrası 3 gün, iptal/gelmemede 24 saat, ihmal ve 15 gün/iletişim tercihi kuralları değişmez.
- Transfer hedef talebi/kaynak kabulüyle olur. Yeni taslak geriye dönük yıllık dönemin en yüksek işlem cirosunu esas alır; takvim yılı seçimi varsayılmaz. %10–%30 somut bedeli iki broker anlaşır; kesim günü/kanıt ve ödeme ayrıntıları DQ-018'de kalır.
- Müşteri ve portföy devri ayrı süreçtir; gerekli malik yetkisi ve sözleşme koşulları korunur. Gerekçesiz aktif ilişki devri yoktur. Zorunlu devir, itiraz süresi/prosedürü, acil kısıt, portföy müdahalesi ve ayrılıkta nihai sorumlu yalnız öneridir; DQ-021'de açık bırakılır.

## ADR-076 — MAXIMUM Broker inisiyatifi ve otomatik açık iş yönetim devri

**ADR-078 önceliği:** Aşağıdaki aktif görev/iş devri ve geçmiş hak koruması sürer. Görev sonrası unvan artık belirsiz değildir: başka geçerli Broker ilişkisi yoksa danışman statüsü; sözleşme sonu derhal ilgili yetki/işletme erişimi kapanışı. Ana sözleşme değişimde devam eder, kapanış işleri erişimi uzatmaz. Özgün tarihsel açıklamalar bu yeni hükmün önüne geçmez.

**Durum: 2 Kasım 2026 son kullanıcı kararı; yalnız belge entegrasyonu.** Uygulama/veri değişikliği, çalıştırılmış test veya faz kabulü değildir. Güncel sözleşme 02 bölüm 9.3, kaynak farkları 9.9, ek kabul ölçütleri 9.10'dadır.

- Franchise/atanmış şube Brokerı kendi ofisinin günlük operasyonunu yönetir. Müşteri/portföy sorumlularını ve görev dağılımını belirler; sistemin standart çalışma/dağıtım düzenini değiştirebilir. Marka bütün ofislerin istatistik/performansını izler ve Brokerdan açıklama ister; günlük müşteri işini üstlenmez.
- Broker kendi MAXIMUM havuzunda Broker unvanıyla kişisel mesleki iş üstlenir; ayrıca Marka onayı gerekmez. Yönetim yetkisi ve kişisel çalışma ayrı kapasite/kanıttır; tek izne veya role indirgenmez.
- Broker/ofis yöneticisi değişiminde açık müşteri ilişkileri, portföy yönetimi, Talep/Hizmet/İşlem Dosyaları, görev/randevu/takiplerin yönetim sorumluluğu yeni Broker veya yetkilendirilmiş yöneticiye otomatik geçer.
- Danışmanın ofis üyeliği/çalışma ilişkisi sona erince açık işler otomatik ofis yönetimine geçer. Broker kendisi yürütür, başka yetkili danışmana atar veya yeni çalışan belirlenene kadar yönetiminde tutar. Salt askı sonlandırmayla eşitlenmez.
- Eski/yeni sorumlu, tarih ve aktarılan kayıtlar audit'te izlenir. Belgeler, faaliyetler, müşteri tercihleri ve yürürlükteki sözleşme/yükümlülükler korunur. Müşteri ilişkisi, portföy, yönetim sorumluluğu, fiilî çalışma ve kazanç ayrı tutulur. Tamamlanmış işlem tarafları/kazanılmış hakedişler değişmez; bütün `consultant_id` alanları yeni Brokera çevrilmez.
- **Öncelik/tarihçe:** ADR-072'nin ofis türü değişmezliği, ayrı ofisten ayrılma ve iki kabul ilkeleri; ADR-073'ün teyit/randevu/iletişim korumaları korunur. ADR-072'nin danışman unvanına dönüş ifadesi tarihsel kayıttır: Brokerın mesleki çalışması için dönüş şartı yoktur (ADR-075/076). Görev sonu yönetim yetkileri kapanır, profesyonel kimlik sürer; yeni bir görev-sonrası unvan modeli icat edilmez. ADR-074'ün yalnız danışmana çalışma sınırı Brokerın kendi mesleki işi için geçersizdir; Marka izleme/ofis izolasyonu sürer. ADR-075'te açık bırakılmış kişisel havuz üstlenme, dağıtımı değiştirme ve ayrılıkta nihai yönetim sorumlusu artık kesindir.
- DQ-020/021 yalnız kalan inceleme/itiraz/acil kısıt/geçici yönetici ve devir hata/bildirim prosedürlerini taşır. Yeni süre veya mali sonuç belirlenmez. Yedi hedef panel korunur; ALFA panel tasarımına geçilmez.

## ADR-077 — Franchise/ofis ağı, kurumsal müdahale ve günlük işletme sınırı

**Yaşam döngüsü önceliği — ADR-078:** Aşağıdaki kurumsal/operasyon ayrımı ve üç mali kaynak korunur. Brokerın resmî ilişkiyle unvan kazanması/ilişki bitince danışman statüsüne dönüşü, üç kuruluş seçeneği, ana ofis sözleşmesi ve değişimde sözleşmenin devamı ADR-078 ile kesinleşmiştir. Bunlar eski açık ifadelerden yeniden belirsiz sayılamaz.

**Durum: 3 Kasım 2026 ürün sahibinin rapor değerlendirmesi ve kurumsal sınır talimatındaki kararlar; yalnız dokümantasyon.** Yeni mimari, kod/veri değişikliği, uygulama veya faz kabulü değildir. Yetki/aktör/modül matrisi ve on kavram 02 bölüm 8.2; kuruluş eksenleri 8.4; ek kabul hedefleri 8.9; üç mali kaynak 03'tedir.

- Getmaks bugünkü ana modeli franchise/ofis ağı olan gayrimenkul markasıdır. Getmaks360 ticari/operasyonel/finansal süreçleri yönetir; dijital pazaryeri ayrı fakat bütünleşik portföy yayını ve müşteri erişim kanalıdır. Pazaryeri benzetmesinden yeni işletme/ücret modeli çıkarılmaz.
- Marka politika/franchise koşulunu, ofis kuruluşu/uygunluğunu, Broker yetkilendirmesi/kurumsal statüleri ve ticari yükümlülük takibini yönetir; tüm ofisleri denetler/açıklama ister. Güvenlik, sözleşme ihlali ve kurumsal yükümlülük kapsamında müdahale, askı, yetki kısıtı ve sonlandırma sürecini yürütebilir. **Denetim günlük operasyon yetkisi değildir.** Müdahale usulünün ayrıntıları DQ-014/020/021'de kalır; yeni genel yazım/başkasının yerine kabul yetkisi yaratılmaz.
- Broker kendi ofisinin günlük işletme, danışman katılımı/görev, müşteri/portföy/dosya dağıtımı ve çalışma düzenini yönetir; varsayılan iş akışını kurumsal sözleşme/tercih/koruma sınırları içinde değiştirebilir. Kendi mesleki faaliyeti ayrı kapasitedir. Atanmış Broker sistem genelinde Broker unvanı taşır; ikinci Consultant kimliği/unvanı gerekmez. Kendi MAXIMUM havuz çalışması için ayrıca Marka onayı yoktur (ADR-076).
- Danışman verilen görev/dosya/erişim; stratejik ortak tanımlı sözleşme/görev; müşteri kendi hesap/kişisel bilgi/talep/tercih/belge/karar kapsamındadır. Talep açılması otomatik danışman sahipliği değildir. Yatırımcıya sözleşmede tanımsız operasyon/veri/kazanç hakkı verilmez.
- Hesap, standart üyelik, profesyonel kimlik, kurumsal ilişki, panel görüntüleme, kayıt görüntüleme, kayıt yönetme, çalışma sorumluluğu, işlem taraflığı ve kazanç hakkı farklıdır; panel/rol/katılım bunların hepsini otomatik vermez. Yedi hedef panel sırası Marka, MAXIMUM Ofis, ALFA Ofis, Danışman, Stratejik İş Ortakları, Marka Yatırımcı, Nihai Müşteri olarak korunur. Standart Üye temel alandır; sekizinci ticari panel değildir.
- Broker değişiminde açık müşteri/portföy/talep/hizmet/işlem/görev/randevu/takip yönetimi yeni Broker/yetkili yönetime otomatik geçer. Danışman ayrılınca otomatik ofis yönetimine geçer; Broker kendisi yürütür, atar veya yönetim kuyruğunda tutar. Eski/yeni sorumlu, tarih, neden ve kayıt kapsamı; belge/geçmiş/tercih ve tamamlanmış taraf/haklar korunur. Yönetim devri fiilî çalışan veya kazanç devri değildir.
- MAXIMUM ofis içi ortak Data Havuzu müşteri/talep/portföy çalışma alanıdır; tamamlanan işlemlerin mali katkı/dönemsel dağıtımı ayrı Kazanç Havuzudur. ALFA bireysel sorumlulukla çalışır; MAXIMUM ortak havuz/dağıtımı varsayılmaz. Yeni oran veya eşit dağıtım kararı yoktur.
- Üç finansal kaynak: **A** ticari ilişki/sözleşmeden ofis yükümlülükleri; **B** gerçekleşmiş İşlem Dosyası hizmet bedeli/hak paylaşımı; **C** peşin müşteri hizmet satın alma ve ödeme kaydı. Paylaşım ikinci gelir yaratmaz. Tahakkuk/fatura/tahsilat/hakediş/dağıtım/ödeme ayrı; ilan ücreti/pazaryeri komisyonu kararlaştırılmamıştır (ADR-069/070 korunur).
- Üç başlangıç (Marka doğrudan kuruluşu, ilk Ofis Başvurusu, mevcut Broker kuruluşu) tutarlı kurumsal/ticari sonuca bağlanır; kuruluş içi mevcut kişi/yeni davet/erteleme seçenekleriyle karıştırılmaz. Doğrudan kuruluş ek dış onaya zorlanmaz. Sözleşme, aktivasyon ve ödeme birbirinin yerine geçmez; açık ödeme/yenileme/yaptırım koşulları DQ-022'dir.
- **Öncelik ve çelişki:** ADR-061/072 tür ve kabul, ADR-073 iletişim, ADR-075 panel/unvan, ADR-076 yönetim devri kararları sürer. ADR-071'in geniş operasyon/geçiş, ADR-074'ün yalnız danışmana havuz çalışma ve eski altı panel yorumları güncel hedef değildir; tarihsel metinleri korunur. Görev bittikten sonraki unvanın tüm durumları veya ALFA/franchise birleşimleri bu kararla icat edilmez (DQ-003/016). Teknik erişim modeli DQ-014, itiraz/acil kısıt/geçici yönetici/devir hata-bildirimi DQ-020/021'de açıktır.

## ADR-078 — Ofis yaşam döngüsü, ilişkiye bağlı Broker unvanı ve ana sözleşme

**Durum: 3 Kasım 2026 ürün sahibinin “Ofis Yaşam Döngüsü ve Broker Yetki Modeli” talimatındaki kesin kararlar.** Yalnız dokümantasyon; kod, veritabanı, test/build veya mimari değişikliği değildir. ADR-077 yetki sınırı korunur. Ana davranış/aktör/koşullar 02 bölüm 8.4, teknik hedef 01, mali koruma 03 ve uygulama sınırı 09'dadır.

- **Üç kuruluş yolu:** Mevcut Broker ile, yeni Broker davetiyle veya Broker atamasını erteleyerek kuruluş. Ertelemede Marka ofis hazırlığını Broker atanana kadar yürütür; atama sonrası günlük hazırlık/işletme sorumluluğu Brokera geçer, Markanın kurumsal yönetim/denetimi sürer. Markanın brokersız hazırlık yürütmesi sınırsız gündelik müşteri operasyonu değildir. Doğrudan/başvuru kuruluş kaynağı ayrı eksendir; doğrudan kuruluş dış onay kuyruğuna zorlanmaz.
- **Hazırlık:** Davet kabulü, etkin hesap ve gerekli ofis ilişkisi/üyeliği sonrasında SETUP'ta sınırlı hazırlık erişimi verilebilir. Tam işletme yetkisi veya Broker unvanı yalnız bu erişimden doğmaz. Hazırlık erişimi ACTIVE yapma, Marka adına sözleşme kabulü/ticari taahhüt, açılmamış operasyon veya yetkisiz finans işlemi vermez.
- **Unvan:** Broker bağımsız/kalıcı kullanıcı unvanı değildir. Resmî ofis franchise ilişkisi veya geçerli Marka Broker atamasıyla kazanılır. Bu ilişki yoksa kişi Gayrimenkul Danışmanı statüsündedir. Davet/tek başına panel erişimi unvan vermez; başka ofisteki geçerli Broker ilişkisi korunur. Aktif Broker kendi mesleki işini Broker unvanıyla yapar, ikinci Consultant kimliği oluşturulmaz. Görev sonu danışman statüsü yeni hesap/kimlik veya otomatik başka ofiste çalışma izni değildir.
- **Ana sözleşme:** Getmaks A.Ş. ile ilgili ofis tüzel kişiliği arasında **Getmaks Ofis Franchise ve İşletme Sözleşmesi**. Broker metinde açıkça tanımlanır; görev/yetki/yükümlülük/sorumlulukları ve şahsi yükümlülük kabulü aynı sözleşmede düzenlenir. Ayrı Broker sözleşmesi zorunlu değildir. Ofis adına temsil/imza yetkisi ile Brokerın şahsi kabulü farklı sıfat/kanıttır. Aynı kişi iki sıfatı taşısa da biri diğerinin yerine geçmez. Hukuki geçerlilik ve imza düzeni hukukçu incelemesindedir.
- **Kabul sırası:** Marka hazırlar → ofis yetkili temsilcisi tüzel kişilik adına kabul/imza verir → tanımlı Broker şahsi görev/sorumluluklarını kabul eder → Marka yetkilisi gerekli marka/ticari onayı verir → sistem taraf, temsil/yetki, sözleşme sürümü, tarih ve imza kayıtlarını doğrular. Bu beş adım mevcut iki taraf imza kaydının yeterli olduğu iddiası değildir.
- **READY → ACTIVE:** Tüzel kişilik bilgileri, doğrulanmış yetkili temsilci, aktif Broker kimliği, Broker–ofis üyeliği, ofis sözleşmesi kabulleri, aynı sözleşmede Broker şahsi kabulü, Marka ticari onayı, kuruluş belgeleri ve MAXIMUM/ALFA modeli birlikte gerekir. Karar Marka'dadır; eksikler açık gösterilir. Danışman kadrosu veya ilk ilan aktivasyon şartı değildir. DQ-022'deki belirsiz bedel/vade/ödeme/yaptırım yeni ön koşul yapılmaz. Doğrudan kuruluşun ticari onayı ayrıca dış başvuru kuyruğu gerektirmez.
- **Broker değişimi:** Resmî yeni atama, gerekli kabul ve yetkilendirme tamamlanınca yürürlüğe girer; aynı yürürlük anında eski yetki biter, yeni yetki başlar. Aynı ofiste iki aktif Broker yetkisi oluşmaz. Ana ofis sözleşmesi yürürlükte kalır; zorunlu yeniden sözleşme yerine gerekli atama/sözleşme ekleriyle değişim izlenebilir. Başarısız devirde Marka müdahale edip yeniden atama yapabilir; teknik tekrar/istisna prosedürü DQ-021'de kalır. Başka geçerli Broker ilişkisi olmayan eski Broker danışman statüsüne döner. ADR-076 açık iş yönetim devri ve geçmiş kazanç/kanıt koruması sürer.
- **Sözleşme sonu/kapanış:** İptal veya sona ermede ilgili ofisin Broker ilişkisi/unvanı ve Broker yetkileri derhal sonlanır; işletme erişimi kapanır. Başka geçerli Broker ilişkisi yoksa kişi danışman statüsündedir. TERMINATED terminal ofis durumudur. Kapanıştaki mali hesaplaşma, belge/demirbaş teslimi, portföy/müşteri dosyaları, veri devri ve tutanaklar ayrı süreçtir; gerektiğinde ıslak imzalı belgeler alınabilir. Bu yükümlülükler Broker unvanı veya işletme erişimini sürdürmez. Geçmiş ve doğmuş mali haklar korunur.
- **Eski hükümlere öncelik:** Bağımsız Broker sözleşmesini zorunlu/ayrı aktivasyon kapısı sayan eski yorum geçersizdir. Tarihsel BrokerEngagement/ticari kayıtlar silinmez; bu kararla yeni borç/maaş/komisyon veya zorunlu ikinci sözleşme üretilmez. ADR-075/076/077'nin “danışmana dönüş gerekmez” ilkesi aktif görevde mesleki iş içindir; görev bittikten sonraki unvanı kalıcılaştırmaz. ADR-072'nin her durumda aynı ofiste otomatik danışman devamı yorumu yerine başka geçerli Broker ilişkisini koruyan güncel statü kuralı geçer; danışman çalışma erişimi ayrıca kendi koşullarına bağlıdır. Değişimde ana sözleşme devamı ve kapanışta yetki sonu artık açık soru değildir.

## Korunan kararlar

- **ADR-001/002/010:** tek marka, yönetilebilir ofisler, ofis başına tek aktif broker, tek pazaryeri; public landing MVP dışı.
- **ADR-004–009/018/027:** Data ve Kazanç Havuzu ayrı; model kabiliyetleri, snapshot ve finans fazı sınırı korunur.
- **ADR-011–021:** tarihçe/aktif anahtar, merkezi yetki, duplicate uyarısı, RequestFile adı, claim süre sonu, fiyat politikası, kilitli sayaç ve teklif revizyonu.
- **ADR-022–032:** faz kapısı; plan/ücret/hak ayrımı; tarihli ticari ilişkiler; sınırlı broker yetkisi; istisna snapshot'ı; tahakkuk fatura değildir; yönetim bağlamı ve yaşam döngüsü tarihçesi.
- **ADR-033–039:** doğrudan kuruluş, dış başvuru approval'ı ve readiness ayrımı; profesyonel aktivasyon koşulları; kullanılabilir panel düzeni. ADR-039 içindeki “başvuru domaini henüz yok” cümlesi tarihsel durumdur, güncel kural değildir.
- **ADR-040–051:** dosya merkezli CRM, talep/hizmet yönü, ofis scope'u, havuz ataması, otomatik ofis kodu, çalışan menü/izin, Türkçe sunum, sistem erişim kilidi ve ofis merkezli üyelik.
- **ADR-052–059:** ticari/operasyon/hizmet ayrımı; hizmet paketi; sözleşme/harici yetki/gayrimenkul ayrımı; kanıtlı aktivasyon; kalıcı üye hesabı ve dosya tarafı.
- **ADR-060:** bütünleşmiş panel, ayrı üyelik/ilişki/başvuru durumları ve veri geçmişini koruma sürer; model semantiğinde ADR-061 geçerlidir.

ADR-001–060'ın özgün metni [arşivdeki](archive/docs-2026-10-28-oncesi.zip) 07_DECISIONS.md içindedir. İlgili davranışın güncel özeti [iş kuralları](02_BUSINESS_RULES.md) ve [finans kurallarıdır](03_FINANCE_RULES.md).

## Açık karar ve doğrulamalar

### DQ-001 — Belge işletim koşulları

Eski “belge modeli/yükleme yok” tespiti güncel değildir; 19 Ekim kaydı sürümlü belge ve inceleme uygulamasını bildirir. Gerçek zorunlu belge listesi, saklama süresi, işletme incelemesi ve tarayıcı kabulü ayrıca doğrulanmalıdır.

### DQ-002 — Sözleşme kanıtı ve yürürlük

Sürümlü metin/şart, taraf kanıtı ve yetkili inceleme kararı kayıtlıdır. Bu, gerçek e-imza entegrasyonu veya hukuki doğrulama değildir. Kullanılacak gerçek metinler, yetkili kişiler, işletme kabulü ve mevcut ofislerin eksikleri açık kalır.

**ADR-078 ile kesinleşen model:** Ana sözleşmenin adı/tarafları, Brokerın aynı metinde tanımı ve şahsi kabulü, ofis temsil/imzasından ayrımı, kabul sırası ve değişimde sözleşme devamı kesinleşmiştir. **Kalan inceleme:** hukukçunun somut metin/ek, şahsi yükümlülük ve imza düzenini değerlendirmesi; gerçek temsil/imza yetkisinin ve kabul/ıslak veya harici imza kanıtının doğrulama yöntemi. Aynı kişinin iki sıfatı için kanıtın nasıl düzenleneceği veya e-imza entegrasyonu kendiliğinden icat edilmez. Bu açıklar ayrı zorunlu Broker sözleşmesi oluşturma kararı değildir.

### DQ-003 — Franchise ve temsil ayrımı

Franchise yükümlülüğü, ofis yönetim modeli, kuruluş kaynağı ve broker ataması farklıdır. MAXIMUM franchise kuruluşu ile ALFA marka ataması kaynaklarda ayrılmıştır. Eksik sözleşme/temsil koşulları tahmin edilmez; belirsiz mali yükümlülük oluşturulmaz.

### DQ-004 — Faz ve kabul mutabakatı

Eski handoff aynı anda 03C.3 COMPLETED, 03C.4 KISMİ ve 4B.1 başlığı taşıyordu. Güvenli devam sınırı 09'da açıklandı. İleri-faz kodunun bulunması kabul değildir; eksik ürün sahibi kabul kaydı tamamlanmalıdır.

### DQ-005 — Model geçişinin veri etkisi

**Ana karar kapandı — ADR-072:** Mevcut ofisin türü değiştirilemez; yerinde MAXIMUM/ALFA dönüşümü yoktur. Devir, brokerın yönetim yetkilerinin kapanması ve profesyonel devamı (unvan yorumu ADR-075/076) ve diğer tür için yeni Ofis Başvurusu ayrı ilişki adımlarıdır. Eski NULL/uyumsuz model verisinin tespiti ve geçmişi koruyan düzeltme ayrı uygulama incelemesidir; bu kararla toplu veri dönüşümü yapılmaz. Marka yönetimi, yeni ofis üyeliği ve açık işlerin devir ayrıntıları DQ-010'dadır; ofis türü değişebilir mi sorusu yeniden açılmaz.

### DQ-006 — Güncel uygulama kanıtı

Onaylı adayın onboarding tamamlama zinciri, broker ilişki kapsamı/C5, scheduler sürekliliği ve gerçek tarayıcı kabulü eski belgelerden tamamlanmış veya eksik ilan edilemez; ilgili kod/test/ortam kanıtıyla yeniden durumlandırılmalıdır.

### DQ-007 — Kaynak erişimi ve ileri finans

Eski panel şartnamesinin atıf yaptığı GETMAKS360_ANA_TASARIM_VE_UYGULAMA_SARTNAMESI.md ile GETMAKS360_CODEX_TEK_ANA_TALIMAT.txt özgün docs envanterinde yoktur. İçerikleri biliniyormuş gibi karar türetilmez. Finans sağlayıcısı, yuvarlama/vergi/iade ve stratejik ortak/yatırımcı ayrıntıları ilgili fazda açık kapsam ister.

### DQ-008 — Ofis modelleri ve hizmet paketlerinin ayrıntısı

**Kesinleşen:** ADR-061 ve ADR-066 ile ofisten model alma, MAXIMUM ekip/talep geri bırakma/aylık tüm danışmanlara paylaşım ve ALFA bağımsız data/kazanç yapısı belirlendi.

**Paketlerde kesinleşen:** ADR-069/070 kapsamı, Birebir Destek'te aylık peşin koşulu, Uzman Hizmet'te başarıya bağlı ücret ve başlangıç tarifeleri. Uzaktan Destek'in ücret doğum olayı/tarifesi; vergi ve otomatik ödeme sağlayıcısı ayrıntıları açık kalır.

**Diğer açıklar:** MAXIMUM katkı oranı/matrahı, dağıtım ağırlıkları, dönem içinde katılma/ayrılma/transfer/askı, Brokerın kendi mesleki faaliyetiyle havuz katılımı ve tahsilat-dağıtım zamanı; ALFA marka/ofis/broker ticari hakları. ADR-075 Brokerı bu hak için Danışman unvanına dönüşmeye zorlamaz.

### DQ-009 — Açık artırma kuralları

**Kesinleşen:** Seçilen teklif taraf onayına ve sözleşme sürecine gider (ADR-065). Otomatik satış, borç veya imza değildir.

**Açık kalan:** Uygulanacak işlem/paketler, katılımcılar, teklif görünürlüğü, artış/alt sınır, süre/uzatma, geri çekilme, varsa teminat, teklif seçim ölçütü/yetkisi, taraf onayının kanıtı ve ret/onaysızlık/sonuçsuz bitiş davranışı.

### DQ-010 — Bölgesel sorumluluk ve ofisler arası işbirliği

Bölge sınırı, dosyayı atama yetkisi, uygun ofis seçimi, başka ofisin ilanıyla eşleşme, ortak danışmanlık ve görünürlük/mali kapsam belirlenmeli. Mevcut aynı-ofis eşleştirme kontrolü yeni ağ modelinin tamamını karşılamaz; kontrol kendiliğinden kaldırılmaz.

ADR-071 transfer görünümündeki kaynak/hedef model, açık dosya/müşteri/hizmet, yeni şart ve ticari/abonelik etkisi korunur. **ADR-076/077 güncellemesi:** Ayrılan danışmanın açık işlerinin yönetimi otomatik kaynak ofis yönetimine geçer; bu sorumlu yeniden açık konu sayılmaz. Hedef ofise dosya veya kazanç otomatik taşınmaz. Kalan ofisler arası fiilî çalışma/görünürlük, ofis askı/sonlandırmasında hizmet devamı ve gerçek sorumlu kişinin görevlendirilmesi ayrıntıları açık kalır; mali tasfiye DQ-022'yle birlikte ele alınır.

ADR-076 ile Broker değişiminde açık işlerin yönetimi yeni Broker/yetkili yöneticiye; danışman ayrılığında ofis yönetimine otomatik geçer. Kaynak kayıtlar başka ofise taşınmaz, geçmiş haklar korunur. Marka yönetiminde gerçek kişinin görevlendirilmesi, yeni Broker henüz yokken temsil usulü ve ofis askı/sonlandırmasında hizmet devamı ayrıntıları açıktır. ADR-072'nin danışman unvanına dönüş yorumu ADR-075/076 ile güncellenmiştir; yeni tür başvurusu ve tek aktif ofis kuralı sürer. Transfer mali koşulları DQ-018'dedir.

### DQ-011 — İşlem açılışı ve tür bazlı kapanış

Satış, kiralama ve devir için işlem açılışını doğuran karar; zorunlu taraflar/kanıtlar; müşteri ve profesyonel beyanının ayrımı; kapanış/iptal yetkilisi ve kaynak dosyaların devamı kesinleştirilmeli. Devirde taşınmaz ve işletme/devredilen hak kapsamı ayrıca netleşmeli. İlk uçtan uca uygulama adayı standart ilanla satıştır; henüz ürün sahibi öncelik kararı değildir.

### DQ-012 — İş ortağı ek hizmeti

Kim hangi kapsamda görevlendirir, ortak ne teslim eder, müşteri ek hizmet/ücreti nasıl kabul eder, ücret kime ve ne zaman doğar, ret/iptal/iade nasıl olur? Ek ücretli katılım hedefi kesindir; bu ayrıntılar belirlenmeden görevlendirme tahsilat veya kabul sayılmaz.

### DQ-013 — Yatırımcı ilişkisi

Yatırımcı kimliği, yatırım ilişkisi ve sözleşmesi, rapor kapsamı ve varsa mali hakları tanımlanmalı. Yatırımcı paneli işlem yürütme veya müşteri dosyası erişimi vermez; ayrıntısı olmayan getiri/pay kuralı kurulmaz.

### DQ-014 — Marka görevleri, tek başına karar ve hizmet standardı

**Kesin sınır — ADR-071/077:** Marka kurumsal politika/kuruluş/Broker yetkilendirme/statü/denetim ve gerekçeli kurumsal müdahale; Broker kendi ofisinin günlük işletme/ekip/iş dağıtımını yönetir. Danışman, ortak ve müşterinin sınırı 02 bölüm 8.2 matrisindedir. Marka denetimi günlük müşteri işi değildir; yönetim başka tarafın öz kabulünün yerine geçmez. Bu sınırlar yeniden karar beklemez.

**Kalan usul:** Hangi Marka görevlisinin hangi işlemi tek başına yapabileceği, nerede ikinci yetkili/kanıt/karşı taraf imzası gerektiği, hizmet standardı onayı ve hangi bildirim tesliminin işlem ön koşulu olduğu. Kurumsal müdahalenin somut eşik/kanıt/inceleme/kaldırma ayrıntıları DQ-020/021 ile birlikte açık kalır. Marka için sınırsız operasyon veya otomatik günlük sorumlu ataması üretilmez.

Mevcut rol geneli override yapısı aynı BRAND_ADMIN rolündeki iki kullanıcıyı ayrı izinlerle yönetmez. Hedef görevlerin teknik temsil/atama yöntemi ayrıca tasarlanmalı; altı yeni kullanıcı rolü veya yeni RBAC motoru otomatik kabul edilmiş değildir.

### DQ-015 — Danışmanın iki kabulü ve erişim kapıları

**Kapandı — ADR-072:** Ofis şartları aktivasyon; danışman anlaşması operasyon için zorunludur. Ayrı öz kabul/sürüm kanıtları dashboard/liste/readiness/operasyon kapılarında tutarlı uygulanır. Anlaşma kaydının hiç bulunmaması operasyon muafiyeti değildir. Güncel kodun uyarlanması/kabulü ayrıca gereklidir; karar yeniden sorulmaz.

### DQ-016 — Broker görevi bitişinde danışman devamı

**Kapandı — ADR-078 ile güncel statü kesin:** İlgili ofisteki resmî Broker ilişkisi sona erince o ofisin yetkileri kapanır; başka geçerli Broker ilişkisi yoksa kişi Gayrimenkul Danışmanı statüsüne döner. Başka ofisteki geçerli Broker ilişkisi korunur. Bu dönüş ikinci hesap/profesyonel kimlik, kapanmış ofiste işletme veya otomatik danışman çalışma izni oluşturmaz. Aktif görevde Broker unvanıyla mesleki faaliyet ilkesi sürer. Ana sözleşme sonu/kapanış yükümlülükleri yetkiyi uzatmaz; geçmiş ve mali haklar korunur. Eski ADR-072/075/076 yorumları bu ayrımla tarihsel okunur.

### DQ-017 — MAXIMUM çalışma koruması ve müşteriyi aramama süreleri

**Ana zaman kararları kapandı — ADR-073:** Çekimden 24 saatte ilerleme yoksa otomatik bırakılır. Randevulu süreçte 3 gün gerçekleşen görüşmeden başlar. Son görüşmeden itibaren 15 gün aramama aynı danışmanı da kapsar. Yeniden çekim veya çalışma koruması bitişi aramama süresini sıfırlamaz. Ortak çalışma hakkı, geçici koruma ve müşterinin huzuru birlikte korunur.

**Randevu ayrıntıları da kesinleşti:** Tarih/saat + iletişim ve müşteri teyidi kanıtıyla görüşmeye kadar koruma; gerçekleşmeden sonra 3 günde ilerleme yoksa bırakma; iptal/gelmemede 24 saatte yeniden randevu/aksiyon yoksa bırakma; danışman ihmaliyle ek süre yok. Altı randevu olayı ayrı izlenir. Aranmama tercihi derhal uygulanır; 15 gün dolunca diğer izin/tercihler hâlâ kontrol edilir.

**Kalan uygulama ayrıntıları:** Somut aksiyon ve iletişim/teyit için kabul edilen kanıt yöntemleri, ihmalin kim tarafından hangi kanıtla değerlendirileceği, çakışan olayların doğrulanması ve müşterinin başlattığı iletişimin kapsamı. Bunlar otomatik süre yenileme veya arama muafiyeti oluşturmaz. Önceki ana süre/teyit/iptal/gelmeme/tercih soruları yeniden açılmaz.

### DQ-018 — Danışman transfer bedelinin hesap ve ödeme koşulları

**Ana karar kapandı — ADR-073:** Yıllık en yüksek işlem cirosu esas alınır; somut transfer bedelini iki broker görüşüp kendi aralarında kararlaştırır. Önceki %10–%30 aralığı korunur; sistem oran veya ödeyen seçmez. Hedef ofis talep eder, kaynak ofis kabul ederse transfer gerçekleşir. Karşılıklı kabul gerçek ödeme değildir.

**2 Kasım kesinleşen:** Geriye dönük yıllık dönemin en yüksek işlem cirosu (ADR-075); takvim yılı toplamı veya aylık ortalama seçilmez. **Kalan ayrıntılar:** yıllık pencerenin kesin referans anı/kesim hesabı, ciro vergi/para birimi kapsamı, anlaşılmış bedelin ödeme/vade/itiraz/iade kanıtı ve transferle ödeme bağı. Marka kaynak onayı olmadan olağan transferi tek taraflı tamamlayamaz. Yeni yüzde, otomatik borç veya tahsilat engeli üretilmez; belirlenmiş matrah ve iki broker anlaşması yeniden sorulmaz.

### DQ-019 — Mesleki belge ve EİDS kanıt ayrıntıları

ADR-072 ürün gereklilikleri 02 bölüm 8.5'tedir. Yetki numarasının hangi danışman/ofis ilişkisine dayandığı, ofisteki Seviye 5 MYK/eğitim belgesinin ilgili gerçek kişi sahibi, belge geçerlilik/inceleme ve eksik durum davranışı ile danışman aktivasyonu ve ilan yayımındaki kapılar ayrıntılandırılmalıdır. EİDS sağlayıcısının gerçek yanıtı ve entegrasyon yetkileri doğrulanmadan numara/belge kaydı sağlayıcı doğrulaması sayılmaz. Bu liste mevzuat uygunluğunun doğrulandığı anlamına gelmez.

### DQ-020 — Broker havuz çalışması: ana kararlar çözüldü, inceleme usulü açık

**Çözüldü — ADR-076:** Broker kendi MAXIMUM havuzunda kendi unvanıyla çalışır; ayrıca Marka onayı gerekmez. Kendi ofisinde operasyonel inisiyatif, standart dağıtım/çalışma düzenini değiştirme ve danışman yetkilendirmesi Brokera aittir. Yönetim ve kişisel çalışma ayrı kapasitedir; başka ofis/ALFA erişimi veya geçmiş hak silme yetkisi doğmaz.

**Gerçek açıklar:** Brokerın kendisinin taraf olduğu ihtilafta bağımsız incelemeyi kimin yapacağı ve karar kanıtı; yetkilendirmenin kişi/görev/dosya kapsamı ve yalnız erişim geri alındığında devam eden işin prosedürü. İlişki sona ererse devralan zaten ofis yönetimidir; bu soru yeniden açılmaz. Teknik izin/policy uyarlaması uygulama eksiğidir, yeniden Marka onayı kararı değildir.

### DQ-021 — Sorumlu belirleme ve otomatik devir kesin; kalan prosedürler

**Çözüldü — ADR-076:** Müşteri/portföy sorumlularını Broker belirler ve sistemin standart işleyişini değiştirebilir. Broker değişiminde açık işlerin yönetimi yeni Broker/yetkilendirilmiş yöneticiye; danışmanın ofis/çalışma ilişkisi sona erince açık işleri otomatik ofis yönetimine geçer. Broker kendisi yürütür, danışmana atar veya yönetiminde bekletir. Ayrılıkta nihai yönetim sorumlusu ve otomatik devir artık açık değildir.

**Korunan sınırlar:** Müşteri devri, portföy devri, fiilî çalışma ve kazanç hakkı ayrıdır. Eski/yeni sorumlu, tarih, belgeler/faaliyet/audit korunur. Müşteri tercihleri, gerekli malik yetkisi, sözleşmeler ve yükümlülükler aşılmaz; tamamlanmış işlem tarafları ve kazanılmış hakedişler değiştirilmez.

**Gerçek açıklar:** (1) İtiraz süresi, inceleyen ve sonuç/düzeltme prosedürü. (2) Salt askı/acil geçici erişim kısıtının kanıtı, inceleme ve kaldırılması. (3) Yeni Broker/yetkili yönetici henüz belirlenmemişse geçici gerçek kişinin görevlendirilme yöntemi. (4) Bildirim/teslim kanıtı, kısmi başarısızlık, atomiklik ve tekrar denemede devir kayıtlarının doğrulanması. Yeni sabit süre, varsayılan hak kaybı veya otomatik kazanç devri üretilmez; kesinleşmiş yetki her işlem için yeni Marka onayına bağlanmaz.

### DQ-022 — Franchise yükümlülükleri, yenileme ve mali tasfiye

**Kesin çerçeve — ADR-077:** Marka sözleşme/ticari koşulları belirler; Ofis/Broker kendi taraf kabulü ve yükümlülüğündedir. A ofis ticari ilişkisi, B gerçekleşmiş İşlem Dosyası, C peşin paket satın alma/ödeme kaydı ayrı kaynaklardır. Ödeme, imza veya aktivasyon birbirinin kanıtı değildir; paylaşım yeni gelir değildir. İlan ücreti/pazaryeri komisyonu varsayılmaz.

**Çözüldü — ADR-078:** Broker değişiminde ana ofis sözleşmesi yürürlükte kalır; yeniden oluşturulması zorunlu değildir, atama/sözleşme ekleriyle izlenir. Ofis tüzel kişiliği temsil/imzası, Broker şahsi kabulü ve Marka ticari onayı aynı ana sözleşmede ayrı kanıtlardır. Sözleşme bitince ilgili Broker yetkisi ve işletme erişimi derhal kapanır; mali kapanış bunu uzatmaz.

**Kullanıcı kararı gerekenler:** Açılış bedelinin doğum/tahsilat/iade koşulları; aylık/yıllık başlangıç, vade, kısmi dönem ve yenileme hesabı; gecikme süre/yaptırımı; otomatik/onaylı yenileme; askı/sonlandırmada dönem yükümlülüğü ve açık borç/alacak/hakediş tasfiyesinin ayrıntıları. Ana sözleşme/eklerin hukuki geçerlilik ve imza incelemesi DQ-002; MAXIMUM/ALFA ticari farklılıkları DQ-003/008; gerçek hizmet devam sorumlusu DQ-010/021; mali görev/ikinci onay DQ-014 ile ilişkilidir. Yeni oran, süre, borç, otomatik yaptırım veya aktivasyondan önce ödeme zorunluluğu üretilmez.
