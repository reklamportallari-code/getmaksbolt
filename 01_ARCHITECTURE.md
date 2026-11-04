# Mimari ve veri sahipliği

Bu belge mimari ilkeleri ve veri sorumluluklarını tanımlar; canlı veritabanı envanteri veya faz kabulü değildir.

## Katmanlar

**ADR-076 sorumluluk ayrımı:** Ofis yönetim sorumlusu, müşteri ilişki sorumlusu, portföy sorumlusu, fiilî çalışan ve kazanç tarafı aynı kavram değildir. Broker değişiminde açık iş yönetimi yeni Broker/yetkili yöneticiye; danışman ayrılığında ofis yönetimine otomatik aktarılır. Bu, bütün consultant_id alanlarını değiştirme veya tamamlanmış işlem taraflarını devretme talimatı değildir. Eski/yeni sorumlu, zaman, kapsam ve audit; belge/geçmiş/tercih/sözleşme bağları korunur. Broker kendi havuz işini ayrı mesleki kapasiteyle, ek Marka onayı olmadan yapar. Mevcut izin/atama/yaşam döngüsü uygulaması hedefi tam karşılamaz (02 bölüm 9.9); yeni model/tablo/rol bu belgeyle üretilmez.

- app/Core: Audit, Authorization, Organization ve ortak destek.
- app/Domains: Brand, Office, Professional, Subscription, Commercial; Customer, DataPool, RequestFile, Service; ilgili faz açıldığında Property, Portfolio, Listing, Marketplace, Appointment, Showing, Offer, Transaction, Finance, RevenuePool.
- app/Integrations: Identity, Eids, Signature, Notifications, Accounting.
- app/Providers: uygulama bağlama ve servis sağlayıcıları.

Domain ancak ihtiyaç doğduğunda Models, Actions, Policies, Services, DTOs, Events veya Http altına ayrılır. Yeni paralel sahiplik veya yaşam döngüsü motoru kurulmaz.

## Teknik ilkeler

- Controller HTTP doğrulama, yetki, kapsam ve yönlendirme sınırıdır; iş davranışı Action/Service katmanındadır.
- Domainler açık sözleşmeler ve adlandırılmış olaylarla iletişim kurar.
- Yetki varsayılan olarak reddedilir. Menü gizlemek yeterli değildir; route, policy ve aksiyon aynı kapsamı doğrular.
- Kritik değişiklik AuditLog; durum geçişi StatusHistory üretir. İlişkili kayıtlar transaction içinde değişir.
- Tarihçeli aktif kayıtlar bitiş alanı ve nullable unique active_key ile korunur; geçmiş satırlar silinmez.
- Para integer minor-unit ve para birimiyle, oran integer basis-point ile tutulur; float kullanılmaz.
- Eski dosyanın çalışma modeli ve ticari koşul snapshot'ı yeni politika/ofis seçimiyle değiştirilmez.
- Dosya/ofis numarası DocumentSequence transaction ve satır kilidiyle üretilir; count()+1 kullanılmaz.

## Temel kayıtların sorumluluğu

**Kimlik ve organizasyon:** Professional tek mesleki kayıttır; brokerlık ofis kapsamlı görev/unvandır. Atanmış Broker için ayrıca Consultant kimliği/unvanı oluşturulmaz (ADR-075/076/077); temel mesleki yeterlilik ile ekranda kullanılan unvan farklıdır. 30 Ekim uygulamasında broker yetkisi ofis görevinden çözülür; eski BROKER/CONSULTANT tür kolonu ve geçmiş kayıtlar korunur. Tam veri geçişi ayrıca incelenecektir. User temel hesap; Professional profesyonel kimlik; BrandMembership marka ilişkisi; OfficeMembership ofis görevi/üyeliği; BrokerEngagement ayrı broker ilişki geçmişidir. ProfessionalApplication başvuru ve inceleme kaydıdır, aktif yetki değildir.

**Ofis ve çalışma modeli:** Office.office_type MAXIMUM/ALFA türünün kaynağıdır. Danışmanın güncel çalışma modeli seçtiği ofisten gelir. ProfessionalWorkModel tarihçesi, WorkModelPolicy ve dosya snapshot'ları korunur. Eski NULL/uyumsuz kayıtlar tahminle doldurulmaz; veri geçişi ayrı doğrulanır.

**Ticari yapı:** SubscriptionPlan ürün; Subscription atama/dönem; CommercialAgreement taraf ilişkisi; ChargePolicy ücret kuralı; PlanEntitlement hak; CommercialException standart şart snapshot'lı istisna; BrokerCommercialAuthority sınırlı yetki; RevenuePolicy paylaşım parametresidir. UsageEvent → ChargeAccrual final fatura değildir.

**Müşteri ve operasyon:** Customer CRM kimliği; CustomerActivity görüşme/takip; RequestFile talep; ServiceOffer teklif ve revizyon; ServiceFile hizmet; FileParty dosya tarafı; CustomerAccountLink açık hesap–CRM bağlantısıdır. Müşterinin ticari rolü User'a yazılmaz.

**Havuz:** PoolRecord MAXIMUM ofis iş fırsatı; PoolClaim geçici çalışma üstlenmesi; PoolClaimPolicy tarihli süre/limit kuralıdır. Atanmamış üye RequestFile ve marka atama bekleyen başvurular listesiyle aynı kayıt değildir. ADR-074'ün marka izleme/ofis izolasyonu ve danışmana broker yetkilendirmesi sınırı sürer; ADR-075 brokerın kendi Broker unvanıyla mesleki çalışmasını ayrıca tanır. Ofis yönetimi başka kişinin çalışma hakkını otomatik devretmez. Güncel geniş yönetim izinleri veya danışmana dönüş zorunluluğu bu hedefin uygulanmış karşılığı değildir.

**Belge ve kanıt:** Ofis belge gereksinimi/sürümleri ile başvuru belge gereksinimi/sürümleri ayrıdır. OfficeContractVersion metin ve şartların değişmez sürümüdür. Yüklenmiş kanıt, imza doğrulaması ve ticari ilişkinin ACTIVE durumu birbirinin yerine geçmez.

**Sistem — mevcut uygulama:** SystemSettings izinli ayarlar; RolePermissionRegistry izinlerin kaynağı; role_permission_overrides yalnız mevcut rol yetkisini kapatma sınırıdır. Kullanıcıya özel izin ataması mevcut değildir. ADR-071 hedefinde marka kullanıcılarının operasyon, ticari yönetim, profesyonel ilişkiler, hizmet ve denetim yetkileri ayrılır; mevcut rol geneli override yapısı bu hedefi karşılamış sayılmaz. Teknik temsil seçimi DQ-014 kapsamında değerlendirilir; bu ürün kararı kendiliğinden yeni RBAC motoru veya UserRole enum değerleri oluşturmaz.

Bu gruplar eski 04_DATA_MODEL belgesinin sorumluluk özetidir. Tam tarihsel alan listesi arşivdedir; geliştirmeden önce gerçek şema Boost ile kontrol edilir.

## Panel ve süreç sözleşmesi

**ADR-078 — Mevcut katmanlarda ofis/Broker yaşam döngüsü hedefi:** Hesap/davet, ofis ilişkisi, resmî Broker unvanı, SETUP hazırlığı ve aktif işletme izni ayrı kapılardır. Davet kabulü + etkin hesap + gerekli üyelik hazırlık erişimi sağlayabilir; bu erişim unvan, ACTIVE yapma, Marka adına kabul/taahhüt veya açılmamış operasyon/finans yetkisi vermez. Unvan geçerli franchise/ofis ilişkisi veya Marka atamasından çözülmelidir; kalıcı User.role/panel etiketi tek başına kaynak değildir. Başka ofisteki geçerli Broker ilişkisi korunur; güncel veri modelinin çoklu ilişkiyi desteklediği varsayılmaz, toplu kayıt dönüşümü yapılmaz.

Mevcut Office/CommercialAgreement/OfficeContractVersion ve imza/kanıt alanları, **Getmaks Ofis Franchise ve İşletme Sözleşmesi** hedefi açısından değerlendirilmelidir: taraflar Getmaks A.Ş. ve ofis tüzel kişiliği; ofis temsil/imzası, metinde tanımlı Brokerın şahsi kabulü ve Marka ticari onayı farklı sıfat/kanıtlardır. Aynı gerçek kişi sıfatları birleştirmez. Mevcut BRAND/OFFICE imza kaydı Broker şahsi kabulünün uygulanmış karşılığı sayılmaz; ayrı zorunlu Broker sözleşmesi veya yeni tablo/enum önerilmez. Metin/ek/sürüm, gerçek taraf ve temsil yetkisi, kabul tarihi ve kanıt zinciri korunur; hukuki imza düzeni DQ-002'dir. BrokerEngagement ve eski ticari/sözleşme kayıtları tarihsel olarak korunur; zorunlu ikinci sözleşme/aktivasyon kapısı değildir.

OfficeSetupReadiness ve aktivasyon hedefi 02 bölüm 8.4.3'teki dokuz koşulla aynı olmalıdır; danışman kadrosu/ilk ilan veya kararsız ödeme zorunluluğu eklenmez. Route/permission/middleware/policy, Action/Service, görünürlük ve audit aynı ilişki/yürürlük sınırını kullanmalıdır. Broker değişiminde gerekli atama/kabul/yetkilendirme tamamlanınca tek yürürlük anında eski yetki sonlanır, yeni yetki başlar; aynı ofiste çift aktif yetki oluşmaz. Ana sözleşme devamı atama/ek/sürüm geçmişiyle izlenir. Başarısız devir başarı gösterilmez; Marka müdahale/yeniden ataması mümkündür, teknik atomiklik/tekrar usulü DQ-021'de kalır.

Sözleşme iptal/sonunda ilgili Broker ilişkisi/yetkisi ve işletme erişimi derhal kapanır; başka geçerli Broker ilişkisi yoksa danışman statüsüne dönülür. Danışman statüsü otomatik ofis çalışma izni değildir. TERMINATED ofisin normal reaktivasyonu yoktur. Belge/demirbaş teslimi, mali hesaplaşma, dosya/veri devri ve tutanaklar ayrı kapanış görevleridir; eski Broker rolünü veya işletme erişimini açık tutmaz. Geçmiş taraflar/kazançlar/kanıtlar korunur. Bu paragraf ve yukarıdaki bütün hükümler yalnız uygulama hedefidir; mevcut PHP, şema, route veya erişim modeli değiştirilmiş/doğrulanmış değildir.

**ADR-077 — Kurumsal denetim ve ofis işletmesinin uygulanabilir sınırı:** Tek Professional kaydı korunur; Broker göreviyle atanmış kişinin sistemdeki mesleki unvanı Brokerdır, kişisel işlem için ikinci Consultant kimliği/unvanı oluşturulmaz. Kaynakta kalan CONSULTANT türü tarihsel/teknik temsildir; bu belge veri dönüşümü yapmaz. Hesap/temel üyelik/mesleki kimlik/kurumsal ilişki/panel erişimi/kayıt okuma/kayıt yönetme/çalışma sorumluluğu/işlem taraflığı/kazanç hakkı ayrı denetlenir (02 bölüm 8.2). Marka kurumsal yetkilendirme ve denetim, Broker kendi ofis işletmesi, yetkili danışman dosya çalışması, ortak sözleşmeli görev, müşteri kendi karar kapsamındadır. Açık ayrıntılar DQ-014/020/021/022'dir.

Bu sınır mevcut katmanlara aynı iş kararı olarak yansıtılmalıdır: **ekran/component** izinli eylemi sunar; **route/permission/middleware/policy** aktör, panel, ofis ve hedefi doğrular; **Action/Service** kurumsal müdahale ile günlük çalışma/atamayı ayırır; **görünürlük** okuma hakkından yazım üretmez; **audit/olay/görev/bildirim** gerçek sıfat, gerekçe, kapsam ve sonucu izler. Marka rolü veya panel erişimi bu kapıları aşan genel operasyon muafiyeti değildir. Ofis yönetim sorumluluğunun devri bütün consultant_id alanlarını veya mali tarafları değiştirmez. Bunlar uygulama hedefidir; yeni rol, permission adı, tablo veya mimari üretilmez. 2–3 Kasım salt okunur incelemelerindeki geniş Marka izinleri, eksik Broker claim ve otomatik devir bu belgeyle düzeltilmiş sayılmaz.

Finansın kaynak ayrımı mevcut CommercialAgreement/OfficeContractVersion, TransactionFile ve ServicePurchase/ServicePaymentReceipt kayıtlarının iş anlamlarına dayanır (03, ADR-077). Tahakkuk/fatura/tahsilat/hakediş/dağıtım/ödeme ayrı sonuçlardır; pazaryeri ayrı muhasebe veya CRM kopyası değildir. Muhasebe çalışma alanının teknik rol/panel karşılığı DQ-014'tedir; yedi hedef panele sekizinci panel eklenmez.

30 Ekim uygulaması: SetPanelContext adres üzerinden istek kapsamını belirler; oturumdaki panel seçimi kullanılmaz. User.operationalRole, izin kontrolü ve operasyon görünürlükleri aynı kapsamı kullanır. Tek hesap ve tek Professional korunur; brokerlık OfficeMembership görevidir. OfficeApplication.broker_membership_id başvuru ile kurulan görevi bağlar. Eski tür ve tarihçeler topluca yeniden yazılmaz.

ServiceOffer paket/fiyat snapshot'larını, karar veren kullanıcıyı, karar kaynağını ve zamanı taşır. ServicePurchase kabul edilmiş peşin paketin dönem/tutar kaydı; ServicePaymentReceipt özel depodaki ödeme belgesi ve marka banka kontrolü kaydıdır. Dosya WAITING_PAYMENT iken normal durum geçişiyle ACTIVE yapılamaz. Erişim, doğrulanmış tahsilat + güncel dönem + dosya + müşteri hesap bağlantısıyla çözülür; yeni kullanıcı rolü oluşturmaz.

Yedi hedef panelin iş sorumlulukları ve uçtan uca akışı 02'de tanımlıdır (ADR-075); mevcut kod dört rol/ortak ofis bağlamı kullanır. Aynı kaynak dosyanın farklı yetkili görünümleri kullanılır; panel başına dosya kopyası oluşturulmaz. Kaydı değiştiren kullanıcı ile işlem yaptığı sıfat/ofis kapsamı ayrıştırılır. Audit, bekleyen görev, bildirim ve mali sonuç birbirinden ayrı sorumluluklardır. İşlem türü (satış/kiralama/devir) ile ilan yöntemi (standart/açık artırma) ayrı eksenlerdir; artırma bitişi emlak işlemi kapanışı değildir.

## Ortak servisler ve izolasyon

- OperationalAssignment aktörün ofis/danışman kapsamını, ConsultantDirectory ortak danışman sorgusunu çözer.
- WorkModelPolicy model kabiliyetlerini; DataPoolVisibility havuz kapsamını; MemberFileVisibility müşteri dosya görünürlüğünü merkezileştirir.
- OfficeSetupReadiness hazır olma, aktivasyon ve yeniden aktivasyonda aynı koşulları uygular.
- CommercialTermsPresenter teknik anahtarları kullanıcı diline çevirir; tutar ve politikayı değiştirmez.
- Pazaryeri ayrı CRM, müşteri veya portföy kopyası üretmez.
- Scheduler kaydı ile işletim sistemi zamanlayıcısının gerçekten çalışması ayrı kanıtlardır.

## Marka Paneli için hedef sözleşme — 1 Kasım 2026

Ürün kapsamı ve 16 kabul ölçütü tek yerde [02, bölüm 8](02_BUSINESS_RULES.md#8-marka-paneli--ürün-ve-işleyiş-sözleşmesi) içindedir (ADR-071). Aşağıdakiler uygulama gerekliliğidir; mevcut kodun tamamlandığı iddiası değildir:

- Kalıcı hesap rolü seçili paneldeki görev/izin denetimini aşamaz. Yönetim, görünürlük, taraflık ve öz kabul ayrı kapılardır.
- Kritik işlemin kullanıcı/panel/sıfat/kurumsal ilişki/izin/hedef/karşı taraf/kanıt/sonuç bağlamı açık izlenir. Konunun kapsamı aktörün kendi ofisiyle karıştırılmaz. Mevcut AuditLogger bütün alanları henüz saklamaz.
- Dashboard ve hedef liste aynı kapsam/sorgu/filtre tanımını kullanır; ayrı sayaç mantığıyla çelişen sonuç üretilmez.
- ADR-072: Kurulmuş ofisin türü değişmez; yerinde model dönüşümü tasarlanmaz. Broker devir sonrası yönetim yetkilerini bırakır; yönetim yetkileri kapanır. Başka tür ayrı Ofis Başvurusu gerektirir. Eski ofis/dosya/model geçmişi korunur; kaynak ofisin marka yönetimi temsil ayrıntıları DQ-010'dadır. ADR-078 ayrımı geçerlidir: aktif Brokerın mesleki işi için unvan dönüşü gerekmez; ilgili resmî ilişki bitince başka geçerli Broker ilişkisi yoksa kişi danışman statüsüne döner, işletme erişimi sürmez.
- ADR-072: Ofis şartı öz kabulü aktivasyon, güncel danışman anlaşması öz kabulü operasyon kapısıdır. Kanıtlar ayrıdır; anlaşma kaydının hiç olmaması operasyonu muaf tutmaz. DQ-015/016 kararı verilmiştir; uygulama kanıtı değildir.
- Olay, görev, bildirim, teslim ve kabul ayrı izlenir. Başarısız teslim, tamamlanmış görev veya karşı taraf kabulü olarak sunulmaz.
- Ortak kaynak kaydın yetkili görünümleri kullanılır; yeni paralel dosya/hizmet mimarisi bu belge değişikliğinin kapsamı değildir.
- MAXIMUM'da ortak data görünürlüğü, geçici çalışma koruması, ilerleme/randevu ve müşteriyi aramama süresi ayrı sorumluluklardır. ADR-073: çekimden 24 saatte ilerleme yoksa otomatik bırakılır; randevulu süreçte 3 gün gerçekleşen görüşmeden, 15 gün aramama son görüşmeden başlar ve aynı danışmanı da kapsar. Claim/çalışma korumasının bitişi iletişim kısıtını kaldırmaz. Değerler politika üzerinden izlenir; geçici üstlenme mülkiyet veya gelir payı devri değildir.
- ADR-073 randevu ekinde oluşturma, müşteri teyidi, gerçekleşme, iptal, müşteri gelmedi ve yeniden planlama ayrı kanıtlı olaylardır. Tarih/saat + iletişim/teyit kanıtı görüşmeye kadar korur; gerçekleşme sonrası 3 günde ilerleme yoksa bırakılır. İptal/gelmemede 24 saat yeniden planlama; danışman ihmaliyle ek süre yoktur. Müşterinin aranmama tercihi derhal etkili olur; 15 gün dolması diğer izinleri veya bu tercihi geçersiz kılmaz. Tek planlama kaydı gerçekleşme/teyit kanıtı değildir.
- Olağan ofisler arası transfer hedef ofisin talebi ve kaynak ofisin kabulünü ister (ADR-073). Yıllık en yüksek işlem cirosuna dayalı bedel iki brokerın anlaşmasıdır; atama, kaynak kabulü, yürürlük ve gerçek ödeme ayrı kanıtlardır. Mevcut marka tarafından tek adım transfer bu hedefi karşılamış sayılmaz.
- Taşınmaz ticareti yetki numarasının danışmana mı ofise mi ait olduğu, MYK/eğitim/vergi/sözleşme belgesi ve EİDS sağlayıcı doğrulaması ayrı kanıtlardır. Profil alanı veya belge yükleme gerçek sağlayıcı cevabının yerine geçmez.

## Legacy eşleme kaydı

Eski 08_LEGACY_MAPPING içeriği burada birleştirildi. Kayıtlı yeniden kullanım kararı yoktur.

Legacy kaynak: C:\laragon\www\GETMAKS360. Yetkili uygulama: C:\laragon\www\GETMAKS360_V2.

Legacy silinmez, yeniden adlandırılmaz, toplu taşınmaz; açık karar olmadan dosya kopyalanmaz. Yeni yeniden kullanım kararı bu bölümde kaynak yol, hedef yol, REUSED/REWRITTEN/REJECTED kararı ve gerekçesiyle tutulur.
