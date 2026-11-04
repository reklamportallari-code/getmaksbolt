# GETMAKS360 V2 — PILOT READINESS AUDIT

Tarih: 4 Kasım 2026  
Proje: `C:/laragon/www/GETMAKS360_V2`  
Yöntem: kaynak kod ve belge üzerinden salt okunur denetim.  
Sonuç: **bir gerçek ofis + Broker + danışmanlar + müşteri Marketplace yolculuğu için henüz pilot kabulüne hazır değil.**

## 1. Sonuç ve kanıtın sınırı

Kurumsal kayıt, CRM, üyelik, ofis kapsamı, hizmet teklifi, peşin paket ve işlem dosyası başlangıcı için kullanılabilir bir omurga var. Ancak yeni ofisin işletmeye açılması, müşterinin Marketplace'ten portföye ulaşması ve gerçekleşen işlemin mali sonuca bağlanması arasında kopukluklar bulunuyor. Bu nedenle yalnız mevcut ekranları doldurmak veya migration uygulamak gerçek pilotu açmaya yetmez.

Başlıca engeller:

1. Yeni ofis aktivasyonu ve ACTIVE/SUSPENDED ofise yeni Broker ataması, ayrı şahsi kabul kanıtı henüz doğrulanamadığı için bilinçli olarak engelleniyor. Bu engel kaldırılarak pilot açılamaz; kanıt ve kabul akışı tamamlanmalı. [E03, E07]
2. Aynı ofisteki başka danışmana ait hizmet dosyası/portföy üzerinde portföy veya ilan oluşturmayı engelleyen kayıt sahipliği kontrolü iki yazım ucunda bulunmuyor. Ofis middleware'i, aynı ofis içindeki kişi/dosya hakkını tek başına korumuyor. [E02, E18]
3. Üye başvurusu bölgesel ofis yönlendirmesine bağlanmıyor. Ofissiz alıcı talepleri marka genelindeki uygun Broker/danışmanlara görünür olabiliyor; mülk sahibi başvurusu mevcut atama Action'ının kabul ettiği türler arasında değil. [E15]
4. Hizmet sözleşmesi ve taşınmaz yetkilendirme modelleri var; bunları gerçek kullanıcı işlemleriyle tamamlayacak yaşam döngüsü bulunamadı. İlan ön koşulları normal kullanımda uçtan uca karşılanmış sayılmaz. [E17]
5. Dahili ilan oluşturma ve ACTIVE yapma var; müşteriye açık Marketplace liste/arama/detay, yayından kaldırma ve müşteri iletişim/lead kanalı bulunamadı. [E01, E18]
6. MAXIMUM çalışma koruması, randevu teyit olayları ve 15 günlük iletişim/aranmama tercihi hedefleri mevcut claim/gösterim akışından daha kapsamlı. Broker'ın kendi havuzunda çalışma hakkı da mevcut izin listesinde karşılanmıyor. [E02, E14, E19]
7. İşlem dosyası STARTED olarak açılıyor; tamamlanmış satış/kira/devir, iki taraf profesyoneli, gerçek ücret doğumu, hakediş ve Kazanç Havuzu dağıtımı zinciri bulunamadı. [E20, E21]
8. Ayrılma/devirde açık iş yönetiminin otomatik aktarılması ve gerçek bildirim teslimi tamamlanmış değil. Scheduler, yedek/geri dönüş ve gerçek ortam kabulü ayrıca kanıtlanmalı. [E10, E25, E26, E30]

Bunlar kaynak kod bulgularıdır; bu denetimde saldırı, tarayıcı denemesi veya testle yeniden üretilmiş sonuçlar değildir. Hangi eksiklerin zorunlu olduğu seçilen pilot modeline bağlıdır: MAXIMUM seçilirse ortak çalışma/iletişim koruması pilot ön koşuludur; ALFA seçimi MAXIMUM'un tamamlandığı anlamına gelmez. Tek ofis pilotu, güvenlik ve veri sahipliği kontrollerini gereksiz kılmaz.

### 1.1 Bu çalışmada yapılan ve yapılmayan

- Kaynaklar, route tanımları, Blade ekranları, migration deklarasyonları, test kaynakları ve belgeler incelendi.
- Test, build, Artisan, seed veya migration komutu çalıştırılmadı. Uygulama boot edilmedi, veritabanına bağlanılmadı; mevcut şema/veriler doğrulanmadı.
- Gerçek `.env`, gizli anahtar, parola veya token değerleri rapora alınmadı. Ortam gereksinimleri yalnız config kaynaklarındaki değişken **adlarından** çıkarıldı.
- Tek yeni çıktı bu tarihli rapordur. Mevcut kod, handoff, ADR, CHANGELOG ve arşiv değiştirilmedi. Legacy dizini kullanılmadı.
- Kaynakta bulunması, kurulu dosya DB'sinde uygulanmış olması veya üretimde çalışması demek değildir.
- Paket 3 **KAPALI**, 03C.4 **KISMİ**. Bu rapor geliştirme veya canlı migration izni değildir.

### 1.2 Belge önceliği

Zorunlu 00 → 01 → 02 → 03 → 05 → 07 → 09 kaynakları ve belge rehberi esas alındı. İstenen `10_SYSTEM_BEHAVIOR_CONTRACT.md`, `11_CROSS_MODULE_INTERACTION_MATRIX.md`, `12_BUSINESS_MODEL_VALIDATION.md` güncel docs kökünde yoktur; üçü de mevcut `docs/archive/docs-2026-10-28-oncesi.zip` içinde bulundu ve dosya çıkarmadan salt okunur okundu.

Arşivdeki eski “başvuru yok”, “ilan ACTIVE yok” gibi ifadeler güncel kaynak karşısında uygulanmış gerçek kabul edilmedi. ADR-075–078 ve güncel PHP önceliklidir. Arşiv, kodun şimdiki durumunun veya faz kabulünün kanıtı değildir.

## 2. Modül bazında kanıtlı durum

**Durum anahtarı:** Çalışır = belirtilen dar davranışın kaynakta route–backend–sonuç zinciri var; gerçek ortam kabulü değildir. Kısmi = zincirin en az bir parçası var, gerekli devamı eksik. Eksik = incelenen kaynaklarda gerekli davranış bulunamadı. Belirsiz = yalnız kaynakla işletim/veri durumu belirlenemez. Tablolardaki veri kaynakları model/migration tanımlarıdır; DB bağlantısıyla doğrulanmadı.

`operations.*` route'ları `/panels/{panel}/operations` altındadır. Marka GET denetimi ile Broker/danışman günlük yazımı ayrı değerlendirilir.

### A. Kurumsal yapı ve kullanıcı yaşam döngüsü

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Marka yönetimi | Kısmi | /admin; ofis, kullanıcı, rol, audit ekranları | AdminDashboardController, OfficeController, RolePermissionRegistry | brands, offices, users, role_permission_overrides | BRAND_ADMIN; izinler Gate üzerinden | Kurumsal kayıt/yönetim ve ağ denetimi | Marka görevlisi bazında ayrıntılı iş ayrımı/ikinci onay hedefi tam değil | E01, E02, E24 | Yüksek |
| Ofis oluşturma | Çalışır — kayıt/SETUP sınırında | /admin/offices/create; admin.offices.store | CreateOfficeOnboarding, CreateOffice | offices, commercial_agreements, status_histories | office.manage | Kuruluş kaydı, kod, SETUP ve seçilen kuruluş yolunun bağları | Kayıt oluşturmak işletme aktivasyonu değil; üç yolun gerçek ortam kabulü yok | E04, E06, E07 | Kritik |
| Broker atama ve davet | Kısmi | Ofis broker atama ekranı; /invitation/accept/{token} | AssignBrokerToOffice, CreateBrokerAndAssignToOffice, BrokerInvitationController | professionals, office_memberships, broker_invitations | Marka broker.assign; davetli tek kullanımlık bağlantı | SETUP ataması ve parola belirleme; aktif işletmeye yeni atama kontrollü engel | Şahsi kabul/atama eki ve gerçek e-posta kabulü eksik | E03, E05, E11 | Kritik |
| Ofis sözleşmesi ve şahsi kabul | Kısmi | admin.offices.show documents sekmesi | OfficeDocumentController; sözleşme sürüm/imza Actions; OfficeSetupReadiness | office_contract_versions/signatures/documents, commercial_agreements | office.contracts.manage / office.documents.manage | Marka–Ofis imza kanıtı yükleme, inceleme ve yürürlük | PartyType yalnız BRAND/OFFICE; Broker şahsi kabulünü ayrıca doğrulayan zincir yok | E03, E06, E07, E29 | Kritik |
| Danışman katılımı / aktivasyon | Kısmi | /member/applications; /broker/consultants; /consultant/onboarding, commercial-terms | InviteConsultant, ReviewProfessionalApplication, ProvisionConsultantApplication, ActivateConsultant | applications/documents, professionals, brand/office_memberships, professional_work_models | Üye kendi başvurusu; ofis Broker'ı ve Marka kapsamlı inceleme | Başvuru/davet → ofis üyeliği/model → ofis şartı → aktivasyon | Hiç danışman anlaşması olmayan kişide operasyon kontrolü koşullu istisna bırakıyor; bildirim teslimi eksik | E08, E09, E12, E25 | Kritik |
| Hesap ve paneller | Kısmi | /login, /register, /member, /admin, /broker, /consultant | Register/Login/Dashboard, User, WorkspaceContext | users, professionals, memberships | Temel MEMBER korunur; ek erişim ilişki/panel bazlı | Üye kaydı/giriş; göreve göre bağımsız panel | MAXIMUM/ALFA ayrı ürün deneyimi tam değil; İş Ortağı/Yatırımcı panel zinciri yok | E01, E02, E28 | Yüksek; son iki panel sonraki faz |
| Askı / sonlandırma | Kısmi | admin/broker danışman durumları; ofis durum ekranı | Suspend/TerminateProfessional, TerminateOffice, RemoveBrokerFromOffice | üyelik/model/abonelik, status_histories, audit_logs | Marka kurumsal; Broker kendi danışmanı ve ticari yetki koşulu | Erişim/statü kapanışı ve tarihçe | Açık dosya yönetim devri, kapanış görevleri ve tasfiye tamamlanmıyor | E03, E10, E11 | Kritik |

### B. Ofis ve Broker operasyonları

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Ofis işletmesi ve açık bağlam | Kısmi | /broker; operations.*; Marka aynı alanlarda denetim | BrokerOfficeAccess, OperationalAssignment, EnsureOperationalAccess | offices, office_memberships, sözleşme/engagement | Broker geçerli kendi ofisi; Marka günlük POST yapamaz | Ofis seçimi/kayıt ofisi doğrulanır; belirsiz çoklu ofis reddedilir | Yeni ofis aktivasyon engeli; her ekranın çoklu ofis ergonomisi kanıtlanmış değil | E02, E03, E11 | Kritik |
| Çoklu ofis ve ticari yetki | Kısmi — kod altyapısı mevcut | admin.brokers.show; admin commercial authority; /broker/commercial | üyelik/model ilişkileri; SetBrokerCommercialAuthority, evaluator | office_memberships, professional_work_models, broker_commercial_authorities | Broker + ofis + yürürlük bazlı | Bir ofisi kapatma diğerinin yetkisini kapatmaz; model ofisten gelir | Paket 2 migration'ının gerçek DB'de uygulanmışlığı bu denetimde bilinmiyor; kişisel kabul engeli sürüyor | E11, E30 | Yüksek |
| MAXIMUM / ALFA | Kısmi | Ortak /broker; danışman operasyonları | WorkModelPolicy, EnsureDataPoolAccess, PoolClaimPolicyEvaluator | offices.office_type, üyelik/model snapshot'ları | MAXIMUM ortak havuz; ALFA ortak havuza kapalı | Ofis modeli CRM/havuz yeteneğini belirler | MAXIMUM Broker claim izni yok; tam ortak görünürlük/hak/gelir modeli tamamlanmıyor | E02, E14 | Kritik — seçilen modele göre |
| Danışman ekip yönetimi | Kısmi | /broker/consultants, create/edit/show | Broker ConsultantController, ConsultantDirectory, ActivateConsultant | consultant memberships, model, authority | Ofis Broker'ı; lifecycle ticari flag'lerle sınırlı | Katılım, profil, aktivasyon, askı/sonlandırma | Ayrılınca açık işlerin kaynak ofis yönetimine otomatik geçişi eksik | E08, E10, E12 | Kritik |
| Ofis transferi / Broker değişikliği | Kısmi | /admin/consultants/{id}/transfer; ofis Broker atama/kaldırma | TransferConsultantToOffice, ApplyScheduledConsultantTransfers, Assign/RemoveBroker | üyelik/model/abonelik tarihçesi | Mevcut transfer Marka üzerinden; değişim kurumsal yetki | Planlı üyelik/model geçişi ve hedef ofis kontrolleri; Broker değişimi mevcut görevle sınırlı | Hedef ofis talebi + kaynak Broker kabulü/bedel anlaşması ve açık iş devri tam değil; yeni aktif Broker ataması engelli | E10, E11, E26 | Yüksek; hareket yapılacaksa kritik |

### C. Danışman operasyonları

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Müşteri CRM | Çalışır — temel oluşturma/görüş sınırında | operations.customers.index/create/show | CustomerController, CreateCustomer, CustomerVisibility | customers, customer_activities, request_files | Danışman kapsamı; Broker ofisi; Marka okuma | Mükerrer kontrolü → normalize CRM kaydı → audit | Tam iletişim tercihi/aranmama kapısı ve MAXIMUM bütün ekip görünürlüğü yok | E13, E14 | Kritik |
| Data Havuzu ve müşteri paylaşımı | Kısmi | operations.data-pool; claim/contact/release/policy | Claim/Create/Release/ExpirePoolClaims, policy evaluator | pool_records, pool_claims, pool_claim_policies | MAXIMUM; Broker'da claim izni bulunmuyor | Süreli claim, temas, iade veya RequestFile dönüşümü | Aynı talebin geri bırakılması, teyitli randevu koruması, 15 gün ve müşteri tercihi hedefi tam değil | E02, E14 | Kritik — MAXIMUM |
| Talep ve hizmet dosyaları | Kısmi | operations.request-files, service-offers, service-files | CreateRequestFile, Create/AcceptServiceOffer, Create/TransitionServiceFile | request_files, service_offers, service_files, parties | Danışman kendi kayıtları; Broker ofisi; müşteri kendi teklif kararı | Dosya → teklif/snapshot → kabul → hizmet ve owner property | Üye intake ataması snapshot/müşteri ofisini tamamlamıyor; owner intake atama yolu kopuk | E15, E16, E23 | Kritik |
| Gayrimenkul / portföy / ilan | Kısmi | operations.properties/portfolios/listings.show; oluşturma POST'ları | CreateServiceFile, CreatePortfolio, Create/ActivateListing | properties, portfolios, listings, service_contracts/authorizations | Profesyonel operasyon; hedef sahiplik yazım kontrolünde açık var | Owner hizmetinden Property → Portfolio → şartlı DRAFT → ACTIVE | Sözleşme/yetkilendirme UI; aynı-ofis sahiplik; ilan düzenleme/kapatma; public yayın yok | E16, E17, E18 | Kritik |
| Randevu ve takip | Kısmi | Talep eşleşme/gösterim eylemleri; /member/showings | Schedule/CompletePropertyShowing, RecordMatchMutual, CustomerActivity | request_listing_matches, property_showings, activities | İlgili dosya profesyoneli; müşteri görünümü | Eşleşme → zamanlı gösterim/form → tamamlandı | Oluşturma/teyit/iptal/gelmedi/yeniden planlama olay zinciri ve havuz koruması bütünleşmiyor | E14, E19, E23 | Kritik — müşteri teması |
| İşlem ve kazanç | Kısmi işlem / Eksik hakediş | Talepte işlem başlat; /member/transactions | StartTransactionFile; TransactionFileStatus | transaction_files, ilişkili talep/ilan/hizmet/mülk | request_file.update ve kapsam; müşteri kendi taraf kayıtları | MUTUAL eşleşmeden tek STARTED kayıt | Tamamlama, iki taraf danışmanı, ücret, hakediş ve ödeme zinciri yok | E20, E21 | Kritik |

### D. Nihai müşteri ve Marketplace

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Üyelik ve müşteri paneli | Kısmi | /register, /member/files/services/documents/showings/transactions | RegisterController, CustomerPortalController, MemberFileVisibility | users, customer_account_links, file_parties ve dosyalar | MEMBER kendi doğrulanmış CRM/dosya bağları | Üyelik → kendi talep/dosya/teklif/belge görünümü | Gerçek müşteri erişim kabulü; hesap kurtarma/kimlik doğrulama operasyonu ayrıca ele alınmalı | E23, E28 | Kritik |
| İlan bulma ve iletişim | Eksik | Public/member Marketplace liste/arama/detay route'u yok; kök login'e yönleniyor | Yalnız dahili ListingController/Visibility bulundu | listings mevcut; publication/lead zinciri bulunamadı | İlan okuma mevcutta profesyonel operasyon iznine bağlı | Dahili detay, Marketplace değildir | Müşteriye açık katalog, alan filtresi, iletişim/lead, yayın/kaldırma bağlantıları | E01, E18 | Kritik — istenen pilotta |
| Müşteri talebi ve hizmet başvurusu | Kısmi | /member/requests; /member/service-intakes/create | Member RequestController, CreateMemberDemandRequest, AssignMemberDemandRequest | office_id/consultant_id başlangıçta NULL request_files ve CRM | Üye kendi gönderimi; atama mevcutta operasyon iznine bağlı | Talep kaydı oluşur; uygun alıcı talebi elle atanabilir | Bölgesel otomatik yönlendirme yok; owner atama reddi; alanlar/snapshot eksik; ofissiz talepler geniş görünür | E15 | Kritik |
| Hizmet teklifi ve geçici mülk yönetimi | Kısmi | Member teklif accept/reject, satın alma dekont/yenileme, my-properties | AcceptServiceOffer, ConfirmServicePayment, ServicePurchase, Member PropertyController | service_purchases/payment_receipts, properties | Müşteri kendi bağını doğrular; tahsilatı Marka doğrular | Kabul → peşin paket bekler → banka kontrolü → süreli mülk düzenleme | Mülk düzenleme ilan düzenleme/yayınlama değildir; otomatik banka/POS ve fatura yok | E16, E22, E23 | Yüksek; paket kullanılacaksa kritik |

### E. Ticari ve finansal yapı

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Ofis/Broker ticari koşulları | Kısmi | /admin/commercial/*; ofis sözleşmeleri; /broker/commercial | AssignCommercialPlan, DefineChargePolicy, SetBrokerCommercialAuthority | plans, agreements, charge_policies, authorities | Marka; ofis kapsamlı sınırlı Broker yetkisi | Parametrik plan/ücret/yetki ve sözleşme tarihçesi | DQ-022 doğum/vade/yenileme/askı/tasfiye takvimi ve otomatik dönemsel zincir açık | E06, E11, E21 | Kritik |
| Abonelik ve ön tahakkuk | Kısmi | Admin plan/ticari sayfaları; danışman commercial-terms | Subscription Actions, RecordUsageEvent; OfficeController.approveAndActivate | subscriptions, usage_events, charge_accruals | Kurumsal ticari izinler; kendi şartlarını okuma | Plan/abonelik; bazı kullanım ve ilk bedel tahakkukları | Genel dönem tahakkuk işi, alacak-fatura-tahsilat-mutabakat zinciri yok; tahakkuk fatura değil | E21 | Kritik — alınacak bedeller kadar |
| Peşin hizmet tahsilatı | Kısmi | /admin/service-payments; Member receipts/renew | ConfirmServicePayment, ServicePurchase | service_purchases, service_payment_receipts | Üye dekont; Marka gerçek banka hareketi doğrulaması | Tutar/para birimi/referans/bütünlük kontrolüyle süre açma | Gerçek banka/POS, mali belge ve iade/mutabakat otomasyonu yok | E22 | Yüksek; peşin paket pilotta ise kritik |
| İşlem gelir paylaşımı ve hakediş | Eksik — politika tanımı var | RevenuePolicy admin ekranı; danışman şart görünümü | AssignRevenuePolicy; StartTransactionFile | revenue_policies; transaction_files; gerçekleşmiş hakediş kayıt zinciri bulunamadı | Kurallar Marka; gelecekte hak sahibine sınırlı görünüm | Pay parametreleri saklanır; işlem yalnız STARTED | Gerçekleşme → taraf ücretleri → iki profesyonel hakkı → dağıtım/ödeme yok | E20, E21 | Kritik — gerçek işlem sonuçları |
| MAXIMUM Kazanç Havuzu / ALFA mali sonucu | Eksik — capability/parametre var | Mevcut ayrı dağıtım/ödeme ekranı bulunamadı | WorkModelPolicy, RevenuePolicy | pool_share_basis_points politika alanı; dönemsel finans havuzu bulunamadı | Model ve ofis kapsamında olmalı | Havuz payı parametresi var, mali sonuç üretmiyor | Katkı, dönem, hak sahibi, dağıtım, itiraz/ödeme yok; ALFA ortak havuz değildir | E14, E21 | Kritik — MAXIMUM'da vaat edilen paylaşım |
| Tam muhasebe / fatura | Eksik | Invoice/ledger/payout ekranı/route'u bulunamadı | Finance/ERP/fatura adapter zinciri bulunamadı | Dahili tahakkuk ve dekont final muhasebe değildir | Mali görev/ikinci onay DQ-014/022 ile netleşmeli | Tam uçtan uca akış yok | Gerçek pilotta onaylı muhasebe süreci ve izlenebilir bağlantı zorunlu; ERP otomasyonu ertelenebilir | E20, E21, E22 | Yüksek; otomasyon sonraki faz |

**Üç gelir kaynağı ayrı tutulmalıdır:** ofis–Marka franchise/sözleşme yükümlülüğü; gerçekleşmiş emlak işleminden hizmet bedeli; peşin müşteri hizmet paketi. Data Havuzu müşteri çalışma alanıdır; Kazanç Havuzu finansal yapıdır. İlan ücreti/pazaryeri komisyonu bugün var sayılmadı. Tarife veya paylaşım oranı bu denetimde belirlenmedi.

### F. Güvenlik ve işletim

| Modül | Mevcut durum | Panel / ekran | Backend | Veri kaynağı | Kullanıcı yetkisi | İş akışı | Eksik | Kanıt | Pilot önemi |
|---|---|---|---|---|---|---|---|---|---|
| Rol/ofis/kayıt izolasyonu | Kısmi | Tüm panel ve operasyon route'ları | User, Registry, panel/role/operational middleware, visibility servisleri | rol override, memberships, office_id, consultant_id | Panel sıfatı + izin + geçerli ofis | Çapraz ofis bound record engeli ve çoklu ofiste açık hedef | Aynı-ofis portföy/ilan yazım sahipliği; ofissiz taleplerin geniş paylaşımı; agreementsiz operasyon istisnası | E02, E08, E15, E18 | Kritik |
| Audit ve geçmiş | Kısmi | /admin/audit; operations.audit | AuditLogger, StatusTransitionRecorder | audit_logs, status_histories | audit.view; ofis bağlamına göre sorgu | Birçok Action olay/eski-yeni/gerekçe kaydeder | Her yazımın audit'i, panel/sıfat ve bütünlüğün kapsamlı kanıtı yok; audit tam değişmez defter değil | E24 | Yüksek |
| Özel belge ve dekont erişimi | Kısmi | Ofis belge indirme, Member upload, ödeme belgesi indirme | OfficeDocumentController, CustomerPortalController, ServicePaymentController | belge metadata + private local storage | Kurumsal Gate; müşteri kendi dosyası | MIME/boyut/sahiplik doğrulaması; özel depoya yükleme | Gerçek depolama izinleri, yedekleme, saklama ve erişim testleri bu denetimde doğrulanmadı | E22, E23, E29 | Kritik |
| Scheduler ve bildirim | Kısmi altyapı / Eksik başvuru teslimi | console komutları; davet e-postası | ExpireClaims, ApplyScheduledTransfers, DispatchOutbox, Job, DeliverApplicationNotification | pool_claims, memberships, outboxes, jobs/failed_jobs | Scheduler/worker servis hesabı; insan işlemi değil | Periyodik işler tanımlı; outbox retry var; davet Mail çağırıyor | Başvuru teslim sınıfı doğrudan kalıcı hata atıyor; host scheduler/worker ve gerçek Mail kanıtı yok | E05, E25, E26 | Kritik |
| Log / backup / üretim yapılandırması | Belirsiz işletim; Kısmi kaynak | /up; config kaynakları | bootstrap exceptions, config app/db/files/session/mail/queue/cache/logging | DB + private files + logs + cache/session | Host/servis erişimi; kullanıcı paneliyle karışmamalı | Health route ve config tanımları mevcut | İzleme/uyarı, tutarlı yedek ve geri yükleme tatbikatı, HTTPS/gizli ayarlar, production dağıtım kanıtı yok | E27, E28, E29, E30 | Kritik |

## 3. Kritik teknik bulguların sınırları

### F1 — Yeni ofis normal akıştan işletmeye açılamıyor

`BrokerOfficeAccess::evidenceGaps` şahsi kabulü eksik sayıp verified=false döndürüyor; `ActivateOffice` bu ortak kapıyı çağırıyor. Bu bir güvenlik korumasıdır; hata düzeltmesi adı altında atlanmamalıdır. Marka/Ofis imza dosyaları Broker şahsi kabulü sayılmaz. Pilot öncesinde kabulün sıfat, metin/sürüm, gerçek kişi ve yürürlük bağlarıyla uygulanması gerekir. [E03, E06, E07]

### F2 — Aynı ofisteki başka danışmanın portföyüne yazım riski

`PortfolioController::store` ve `ListingController::store` show/activate uçlarındaki Gate ve canView kontrolünü taşımıyor. Çağrılan CreatePortfolio/CreateListing Action'ları da aktörün hedef dosyayı yönetme hakkını doğrulamıyor. Operational middleware hedefin **ofisini** doğruluyor; consultant_id sahipliğini doğrulamıyor. Bu nedenle aynı aktif ofiste hedef ID'sini bilen başka danışmanın yazımının kaynakta engellendiği söylenemez. Çapraz-ofis testlerinin geçmesi bu aynı-ofis sınırını kanıtlamaz. Çalıştırılmış exploit iddiası değildir. [E02, E18]

### F3 — Başvurudan ofis operasyonuna geçiş tutarsız

CreateMemberDemandRequest, request için office_id/consultant_id/work_model_snapshot alanlarını NULL bırakıyor. Bu intake kaydı oluşturmak için kasıtlı bir başlangıç olabilir; fakat:

- Bölge bilgisi alınmasına rağmen ofis eşleştirme motoru yok.
- RequestFileVisibility, aynı markadaki ofissiz Demand kayıtlarını Broker ve danışmana açabiliyor; bu MAXIMUM'a özel ofis Data Havuzu değildir.
- AssignMemberDemandRequest, OwnerService türünü reddediyor. Mülk sahibi başvurusunun mevcut ekrandan devamı tamamlanmıyor.
- Demand atamasında yalnız request.office_id ve consultant_id güncelleniyor; müşteri ofisi ve model snapshot'ı tamamlanmıyor. CreateServiceFile snapshot'ı aynen kopyalayıp audit'te `->value` okuyor. NULL snapshot'la bu devam yolunun sağlam çalıştığı kanıtlanamaz; kaynakta hata riski var.
- Marka'nın günlük operasyon POST yasağı korunmalı; bölgesiz talebin kurumsal yönlendirilmesi ile müşteri üzerinde günlük çalışma aynı yetki sayılmamalı.

Bu bir veri sahipliği/akış eksikliğidir; kayıtları elle DB'den düzeltmek kabul ölçütü değildir. [E15, E16]

### F4 — Danışman anlaşması zorunluluğunda koşullu boşluk

EnsureOperationalAccess, danışman anlaşması varlığını kontrol edip **yalnız herhangi bir anlaşma varsa** güncel ACCEPTED anlaşmayı zorunlu tutuyor. Hiç anlaşması olmayan aktif danışmanda bu kontrol işletilmiyor. Mevcut eski kayıtlar için bilerek korunmuş geçiş istisnası olabilir; fakat yeni pilot danışmanlarının kabul kanıtı olmadan operasyon açmaması ayrıca ayrıştırılmalıdır. ActivationReadiness'deki `consultant_agreement` anahtarı ise fiilen ofis şartı kabulünü denetliyor. İki kabulün adı ve sonucu karıştırılmamalı. [E08, E09]

### F5 — İlan ön koşulları var, bunları üretme/yayın yaşam döngüsü eksik

CreateListing SIGNED ServiceContract ve numarası alınmış aktif ServiceAuthorization istiyor. Modeller/ilişkiler bulunuyor; imza/iptal/süre sonu/yetki doğrulamasını gerçek ekranlardan ilerleten lifecycle bulunamadı. Guard ayrıca sözleşmenin tarih aralığını açıkça sorgulamıyor; statüsü SIGNED kalan süresi bitmiş kaydın davranışı doğrulanmalı. EİDS adapter'ı veya gerçek dış yeterlilik kontrolü bulunamadı. ACTIVE Listing sadece dahili durumdur; Marketplace yayınını kanıtlamaz. [E17, E18]

### F6 — MAXIMUM politika alanları kesin müşteri korumasını tamamlamıyor

Claim/contact/expiry süreleri ve policy kaydı var. Ancak tek temas düğmesi teyitli randevu, müşteri gelmedi, yeniden planlama ve son gerçek görüşmeden 15 gün aramama anlamına gelmez. Müşterinin aranmama tercihini tüm arama yollarında hemen uygulayan ortak kapı bulunamadı. Broker claim izni Registry'de yok; ADR-075/076'nın kendi unvanıyla çalışma hedefi hâlâ eksik. WorkModelPolicy'deki gelir capability bayrakları gerçek kazanç hesaplandığını göstermez. [E02, E14, E19]

### F7 — İşlem açılışı, sonuç ve finans birbirinden ayrı kalıyor

StartTransactionFile, MUTUAL eşleşmeden idempotent bir başlangıç kaydı oluşturur. TransactionFileStatus yalnız STARTED/CANCELLED içerir; tamamlanma Action'ı ve iki taraf danışmanına ait mali kayıt zinciri bulunamadı. ServiceFile.COMPLETED da satışın hukuki/ticari kapanışı ve tahsilat değildir. RevenuePolicy pay tanımı, ChargeAccrual ön tahakkuk ve ServicePaymentReceipt peşin paket tahsilat kanıtıdır; bunların hiçbiri kendiliğinden gerçekleşmiş aracılık hakedişi veya fatura değildir. [E16, E20, E21, E22]

## 4. Pilotun 15 kritik senaryosu

“Tamamlandı” burada yalnız belirtilen dar senaryonun kaynakta uçtan uca bulunduğunu belirtir. Hiçbir satır gerçek ortam veya bu oturumda başarılı test anlamına gelmez.

| No | Senaryo | Kaynak sonucu | Kaynak kanıtı / sınır | Test kanıtı — bu oturumda çalıştırılmadı |
|---|---|---|---|---|
| 1 | Marka yeni ofis oluşturur | Tamamlandı — SETUP kaydı | E04; aktivasyon ayrı senaryo | OfficeCommercialLifecycleTest, BrokerBrandOfficeLifecycleTest kaynakları; önceki 111'lik grup ilgili testleri içerir |
| 2 | Mevcut/yeni Broker atar | Kısmi | E05/E11; SETUP/davet var, aktif işletmeye yeni atama bloke | BrokerIdentityLifecycleTest, BrokerOfficeAccessTest, MultiOfficeBrokerTest; geçmiş regresyon |
| 3 | Davet ve şahsi kabul | Kısmi | E03/E05; parola/davet var, ayrı şahsi kabul yok | BrokerOfficeAccessTest kabulün yokluğunu/engeli sınar; kabul tamamlandı testi değil |
| 4 | Ofis aktivasyonu | Kısmi — bloke | E06/E07; readiness + ayrı kabul engeli | OfficeVerificationActivationTest; engelin varlığı başarıyla aktivasyon kanıtı değildir |
| 5 | Broker operasyon yürütür | Kısmi | E02/E03/E11; geçerli eski ACTIVE ilişkide kapsam var, yeni pilot ofis henüz açılamıyor | WorkspaceAccessTest, BrokerOfficeAccessTest; geçmiş kapsam |
| 6 | Danışman daveti / başvuru inceleme | Kısmi | E12/E25; kayıt/provision var, outbox teslimi yok | ProfessionalApplicationLifecycleTest/OutboxTest kaynakları; bu denetimde güncel sonuç yok |
| 7 | Danışman panel erişimi | Kısmi | E08/E09/E12; şart/aktivasyon var, anlaşmasız operasyon istisnası ayrıştırılmalı | ConsultantIdentityLifecycleTest, ConsultantAgreementHierarchyTest kaynakları; bu denetimde çalışmadı |
| 8 | Danışman müşteri oluşturur | Tamamlandı — temel CRM | E13; normalizasyon/mükerrer kontrol/transaction/audit | PhaseTwoCustomerTest ve ilgili CRM test kaynakları; güncel koşu yok |
| 9 | Portföy ve ilan süreci | Kısmi | E16–E18; property/portfolio/draft/active var, kanıt lifecycle/yayın eksik | PortfolioListingFlowTest sözleşme/yetkiyi fixture ile kurar; gerçek UI kabulü değildir |
| 10 | Müşteri Marketplace ilanlarını görür | Eksik | E01/E18; dahili route dışında müşteri katalog zinciri bulunamadı | Uçtan uca Marketplace test kanıtı bulunamadı |
| 11 | Müşteri talep oluşturur | Tamamlandı — intake kaydı | E15; ofissiz talep oluşur, yönlendirme ayrı senaryo | MemberRequestIntakeTest kaynakları; kayıt ve hesap sahipliği hedefleri |
| 12 | Talep ofis/danışmana bağlanır | Kısmi | E15/E16; Demand elle atanır; owner ve snapshot/müşteri ofisi boşluğu var | Eski atama test dosyalarının bulunması bütün intake devamını kanıtlamaz |
| 13 | Havuz ve modeller uygulanır | Kısmi | E02/E14/E19; ALFA engeli var; MAXIMUM randevu/15 gün/Broker çalışma eksik | MultiOfficeBrokerTest geçmiş regresyon; tüm ADR-073 kabulü değil |
| 14 | İşlem dosyası ilişkileri korunur | Kısmi | E19/E20; kaynak ilişkili STARTED var; kapanış/iki taraf hakkı yok | ShowingAndTransactionFlowTest kaynakları; yalnız başlangıç yolculuğu |
| 15 | Gerçek işlem finansa yansır | Eksik | E20/E21; gerçekleşme → ücret → hakediş/ödeme zinciri yok | Tam zincir test kanıtı bulunamadı; peşin paket testi bunun yerine geçmez |

**Geçmiş sayılar:** Paket 2 için 102/547; Paket 2.1/2.2 birleşik koşusunda 111/595, exit 0 kaydı mevcut handoff'tadır. Bu yalnız ilgili 13 dosyalık önceki kapsamdır. Pilotun tamamı, bütün suite veya bu denetimde yeniden çalıştırılmış test sonucu değildir. [E30, E31]

## 5. Gerçek ortam hazırlığı — yalnız kaynak üzerinden

Aşağıdaki değişkenler gereksinim **adlarıdır**; gerçek değerleri okunmadı veya doğrulanmadı.

| Alan | Gerekli yapılandırma / kaynak | Pilot öncesi kanıt | Şimdiki sonuç |
|---|---|---|---|
| Uygulama / web | APP_ENV, APP_DEBUG, APP_KEY, APP_URL; app config, bootstrap; public document root | Gerçek production profili, HTTPS, debug/veri ifşası kontrolü, kararlı anahtar, doğru kök ve yazma izinleri; /up tek başına iş akışı sağlığı sayılmamalı | Belirsiz |
| DB | DB_CONNECTION, DB_DATABASE, DB_URL; SQLite DB_FOREIGN_KEYS; alternatif sürücü seçilirse kendi bağlantı adları | Seçilen gerçek driver/sürüm, FK ve SQLite kilit/journal davranışı; migration geçmişi; tutarlı yedek kopyasında hedef up/down/hata/yeniden deneme | Belirsiz; bellek SQLite geçmiş testi dosya kabulü değil |
| Dosya | FILESYSTEM_DISK; private/public ayrımı; uzakta kullanılacaksa storage config değişken adları | Private belge/dekont webden açık değil; servis hesabı izinleri; DB+dosya eşleşmeli yedek; indirme sahipliği ve MIME/boyut kabulü | Kaynak private alan tanımlı, işletim belirsiz |
| Oturum / cache | SESSION_DRIVER, SESSION_SECURE_COOKIE, SESSION_HTTP_ONLY, SESSION_SAME_SITE, SESSION_DOMAIN; CACHE_STORE | HTTPS cookie ve oturum davranışı; cache/session tabloları veya seçilen servis; scheduler mutex için tutarlı lock deposu | Belirsiz |
| E-posta | MAIL_MAILER, MAIL_HOST, MAIL_PORT, MAIL_USERNAME, MAIL_PASSWORD, MAIL_FROM_ADDRESS, MAIL_FROM_NAME ve seçilen mailer'ın diğer adları | Davet teslimi/geri dönme, token süre/tekrar kullanımı, başarısız teslimin görünürlüğü; başvuru outbox'ına gerçek kanal | Davet Mail çağrısı var; başvuru delivery sınıfı eksik |
| Worker / scheduler | QUEUE_CONNECTION ve bağlantı ayarları; routes/console.php | pool-claims:expire her 5 dakika; consultant-transfers:apply-scheduled ve application-outbox:dispatch her dakika; host tetikleyici + worker yeniden başlatma/başarısız iş takibi | Kayıtlı komut var, host sürekliliği bilinmiyor |
| Log / izleme | LOG_CHANNEL, LOG_STACK, LOG_LEVEL, LOG_DAILY_DAYS; logging config | Hata, başarısız job/outbox ve scheduler gecikme uyarısı; PII/sır maskeleme; saklama ve erişim sınırı | Config var, işletim kanıtı yok |
| Frontend paketleme | composer.lock/package-lock; Vite ve public/build kaynakları | Seçilen sürümde bağımlılık/asset kurulumu, manifest, tarayıcı hata kontrolü, mobil/ofis ekran kabulü | Bu denetimde build veya tarayıcı çalışmadı |
| Yedek / geri dönüş | DB dosyası veya DB servis yedeği, private dosyalar, sürüm/config/anahtar sürekliliği | Yazımlar ile tutarlı nokta, ayrı güvenli kopya, geri yükleme tatbikatı, sorumlu ve kabul edilen veri kaybı/kesinti hedefi | Kod envanterinde sürekli backup/restore işi bulunamadı; eski tek yedek kaydı yeterli değil |

### 5.1 Migration ön kontrolü — uygulanacak iş listesi, bu denetimde yapılmadı

1. Gerçek driver/sürüm, migration geçmişi ve yedek geri yükleme prosedürü ayrıca yetkili kontrollü çalışmada belirlenmeli.
2. Model–üyelik sahibi eşleşmeleri, marka/ofis bağları, Broker döneminde doğan yetkiler, negatif/çakışan dönemler, active_key ve yeni UNIQUE uyumu envanteri çıkarılmalı. Şüpheli satırlar tahminle bağlanmamalı.
3. İzinli ve tutarlı bir **kopyada** önce hedef migration; veri/FK/indeks eşitliği; kontrollü DDL hataları; tekrar deneme ve rollback koşulları doğrulanmalı. Bu çalışma kopya oluşturmadı.
4. Çoklu aktif ilişkiler eski global tekilliklere sığmıyorsa down'ın güvenli reddi beklenmeli. Veri silerek rollback yapılmamalı; kontrollü ileri düzeltme veya tutarlı yedekten dönme planlanmalı.
5. Yeni kodla eski şemanın geçiş aralığı, bakım penceresi/yazım kontrolü, geri dönüşte kod+DB+belge sürüm uyumu belirlenmeli.
6. Eski bütün migration'ların toplu rollback'i hedef migration rollback'iyle aynı kabul edilmemeli. Handoff'ta eski subscription_plans pricing_model down sırası sorunu kayıtlıdır.
7. Uygulama DB'sine işlem ancak ayrı açık izinle yapılmalı; bu rapor ve Paket 2 kabulü böyle bir izin değildir.

### 5.2 Kanıtlanamayan işletim bilgileri

Gerçek APP_ENV/debug/anahtar, kurulu migration durumu, canlı kullanıcı sayısı, SMTP teslimi, worker/host scheduler durumu, yedeklerin varlığı ve geri yüklenebilirliği, TLS/host izinleri incelenmedi. Bilinmeyen işletim koşulları “eksik kod” ile aynı şey değildir; bunlar **Belirsiz** olarak kalır.

## 6. Pilot için geliştirme ve kabul sırası

Bu sıralama öneridir; yeni paket/faz yetkisi oluşturmaz. Mevcut mimariyle sınırlı değişiklikler tercih edilir. “Korunabilir” mevcut çekirdeğin kullanılabileceğini belirtir; her dosyanın aynen kalacağı anlamına gelmez.

### Liste 1 — Pilot öncesi zorunlu

| İş / öncelik | Bağımlılıklar | Modüller | Teknik kapsam | Kabul kriteri | Mevcut kod korunabilir mi? |
|---|---|---|---|---|---|
| P00 — Pilot sınırı ve ticari/usul kararları / Kritik | Ürün sahibi; DQ-002/010/011/014/017/019/021/022 kalan ayrıntıları | Kurumsal, hizmet, finans | Orta — karar ve kabul hazırlığı | Tek ofisin modeli, kullanılacak paket/türler, fiyatların sahibi, müşteri temas ve finansın sorumlusu açık; kararsız tarifeden otomatik borç yok | Evet; kararlar mevcut kurallara bağlanır |
| P01 — Broker şahsi kabulü ve dokuz aktivasyon koşulu / Kritik | P00; sözleşme ve temsil kanıtı | Office, Professional, Authorization | Büyük | Yeni gerçek ofis, gerçek Broker kabul/kanıtlarıyla normal UI üzerinden READY→ACTIVE olur; eksik kabul/davet tek başına operasyon açmaz | Evet; OfficeContractVersion, üyelik ve ortak kapı temel alınır |
| P02 — Yazım sahipliği ve danışman kabul kapısı / Kritik | P00; mevcut izin matrisi | Portfolio, Listing, Service, Authorization | Orta | Aynı ofiste iki danışmanla birbirinin dosyasına portföy/ilan POST'u reddedilir; izin override'ı sunucuda uygulanır; yeni danışman iki kabulün doğru koşullarını sağlamadan çalışamaz; eski istisna ayrı kalır | Evet; mevcut Gate/visibility/Action katmanları |
| P03 — Üye talebi ve owner intake yönlendirmesi / Kritik | Bölge/ofis sahipliği kararı; P01/P02 | Member, RequestFile, Customer, DataPool | Büyük | Bölgede ofis varsa doğru modele uygun ofis akışına, yoksa yetkili Marka yönlendirme kuyruğuna gider; owner intake ilerler; müşteri/ofis/model snapshot tutarlı; ofissiz PII genişçe açılmaz | Evet; RequestFile ve CRM tekrar kullanılabilir |
| P04 — Hizmet sözleşmesi/yetkilendirme ve ilan ön koşulu / Kritik | P00/P01; imza/EİDS kanıt yöntemi | Service, Property, Portfolio, Listing | Büyük | Gerçek müşteriyle gerekli sözleşme/kanıt UI'dan tamamlanır; yetki sahibi ve tarih/iptal koşulları doğrulanır; geçersiz kanıtta ilan oluşmaz/yayında kalmaz | Evet; mevcut modeller/guard'lar kullanılır; sahte fixture kanıtı gerekmez |
| P05 — Müşteriye çalışan Marketplace ve ilan yönetimi / Kritik | P02/P04 | Listing, Member/Marketplace, RequestFile | Büyük | Müşteri aktif ilanı liste/arama/detaydan bulur, kişisel alanlar korunur; ilan düzeltme/kaldırma müşteri kanalına yansır; iletişim/talep doğru ofise bağlı kayda dönüşür | Evet; mevcut Listing/Property/RequestFile kaynakları |
| P06 — Seçilen ofis modelinde müşteri çalışma/iletişim koruması / Kritik | P00/P02/P03; MAXIMUM ise ADR-073/076 | DataPool, Customer, Showing | Büyük — MAXIMUM | 24 saat, teyitli randevu, görüşme sonrası 3 gün, iptal/gelmeme ve 15 gün/derhal aranmama tercihleri sunucuda çalışır; Broker kendi görevinde çalışabilir; sahte randevu hakkı uzatamaz. ALFA'da ortak havuz yok | Evet; claim/policy/activity altyapısı genişletilebilir |
| P07 — Gerçek işlem kapanışı ve mali sonuç / Kritik | P00/P04/P05; tamamlanma ve hesap kanıtları | Transaction, Commercial, Service, finans bağlantısı | Büyük | Onaylı olayla satış/kira/devir kapanır; iki taraf profesyoneli ve tarife snapshot'ıyla ücret/hak kaydı izlenir; tekrar işleme çift bedel doğurmaz; tahakkuk/fatura/tahsilat ayrıdır. MAXIMUM katkı/dağıtım hakkı kaybolmaz | Evet; TransactionFile/RevenuePolicy ve mevcut mali kaynaklar korunabilir |
| P08 — Ayrılma/devirde açık iş güvenliği / Kritik | P00/P01; geçici yönetim/istisna usulü | Office, Professional, Customer/Service | Orta–Büyük | Danışman ayrıldığında açık iş yönetimi ofise, Broker değiştiğinde yeni yetkiliye geçer; dosya/geçmiş/kazanılmış hak korunur; eski erişim kapanır; sahipsiz aktif müşteri kalmaz | Evet; üyelik/erişim/audit temel alınır |
| P09 — Asgari mali işletim ve bildirim / Kritik | P00/P01/P07; banka/muhasebe sorumluları | Commercial, ServicePayment, Notifications | Orta–Büyük | Pilotun doğan franchise/paket/işlem bedelleri ayrı kaynaklarla izlenir; dönem/vade/mutabakat açık; peşin hak yalnız doğrulanmış tahsilattan açılır; gerçek fatura/muhasebe dışarıda tutulacaksa onaylı kayıt bağlantısı ve sorumlusu vardır; davet ve başvuru bildirimleri gerçekten teslim edilir | Evet; tam ERP zorunlu tutulmaz, eksik mali sonuç başarı diye sunulmaz |
| P10 — Ortam, migration ve gerçek uçtan uca kabul / Kritik | Önceki zorunlu işler; ayrı uygulama izni | Tüm pilot + işletim | Orta–Büyük | Gerçek driver/kopyada migration/restore; scheduler/worker/mail/private dosya; iki danışman+bir müşteriyle güvenlik ve bir tam ilan→talep→işlem→mali sonuç yolculuğu; 03C.4 için ayrı ürün sahibi kabulü | Evet; otomatik testler ve mevcut çekirdek kabul temeli olur |

P07, tam bir ERP geliştirmekle eş anlamlı değildir. Gerçek işlem yapacak pilotta borç/alacak ve hak sahipliği sonucunun güvenilir biçimde izlenmesi zorunludur; onaylı dış muhasebe süreci kullanılabilir. Sistemde olmayan fatura veya ödeme otomasyonu varmış gibi gösterilemez. P06/P07'nin MAXIMUM mali ve çalışma şartları, ALFA'ya aktarılmaz.

### Liste 2 — Pilot sırasında tamamlanabilir

Bu işler yalnız güvenli temel akış ve sorumluluklar tamamlandıktan sonra ertelenebilir; yukarıdaki engellerin yerine geçmez.

| İş / öncelik | Bağımlılıklar | Modüller | Teknik kapsam | Kabul kriteri | Mevcut kod korunabilir mi? |
|---|---|---|---|---|---|
| U01 — Marka/ofis istatistik ve tutarlı filtreler / Yüksek | Doğru işlem verisi ve audit | Dashboard, Office, CRM | Orta | Dashboard sayacı ile filtreli liste aynı kapsamı ve sonucu gösterir; Marka istatistiği günlük çalışma hakkı açmaz | Evet |
| U02 — Arama, listeleme ve mobil/ofis kullanım kolaylığı / Orta | P02/P05; gerçek kullanıcı geri bildirimi | Mevcut paneller, Marketplace | Orta | Pilot hacminde müşteri/portföy bulunabilir; ofis bağlamı kaybolmaz; dar ekranlarda kritik eylemler erişilebilir | Evet |
| U03 — Mali kontrol/uyarı ve operasyon raporları / Yüksek | P07/P09; ilk günden onaylı manuel kontrol | Commercial, ServicePayment, Audit | Orta | Süre bitişi, ödenmemiş kalem ve mutabakat farkı görünür; otomasyon önceki kayıtları tekrar ücretlendirmez | Evet |
| U04 — Bildirim takip ve audit inceleme ergonomisi / Orta | P09 gerçek teslim kanalı | Outbox, Audit | Küçük–Orta | Yetkili başarısız teslimi/gerekçeyi görür; tekrar deneme çift müşteri işi veya veri ifşası oluşturmaz | Evet |

### Liste 3 — Pilot sonrası

| İş / öncelik | Bağımlılıklar | Modüller | Teknik kapsam | Kabul kriteri | Mevcut kod korunabilir mi? |
|---|---|---|---|---|---|
| S01 — Tam muhasebe, banka/POS ve e-belge otomasyonu / Sonraki faz | Güvenilir kaynak mali kayıtlar, sağlayıcı/usul kararları | Finance/integrations, Commercial, Service | Büyük | Sağlayıcı sonucu doğrulanır; idempotent belge/tahsilat/iade/mutabakat; geçmiş silinmez | Evet; kaynak mali kimlikler korunur |
| S02 — İş Ortağı ve Marka Yatırımcısı iş akışları / Sonraki faz | DQ-012/013; görev ve mali hak sınırları | Partner/Investor hedefleri | Büyük | Yalnız atanmış görev/yatırım ilişkisi ve doğru mali hak görünür; ana işlemden varsayılan pay yok | Evet; yeni bağımsız CRM kopyası gerekmez |
| S03 — Açık artırma ve dış portal yayın kanalları / Sonraki faz, pilot dışında açıkça tutulursa | Standart ilan/işlem kabulü; artırma/teminat/teklif kararları | Listing, Marketplace, Transaction | Büyük | Seçilen teklif taraf onayı/sözleşmeye gider; otomatik satış varsayılmaz; yayın kaldırma ve tekrar deneme izlenir | Evet |
| S04 — Ölçek, ileri planlı devir ve çok ofis ergonomisi / Sonraki faz | Tek ofis kabulü; gerçek yük; devir/itiraz usulleri | Organization, Professional, Scheduler | Orta–Büyük | Eşzamanlı değişimler izolasyonu korur; ofis bağlamı açık; planlı değişim mevcut hakkı erken kapatmaz | Evet; Paket 2 altyapısı korunur |

## 7. Kaynak ve test kanıtları

E referansları tabloları aşağıdaki somut kaynaklara bağlar. Satırlar denetim tarihindeki kaynak konumlarıdır. Yokluk tespitleri yalnız incelenen app/routes/config/resources ve migration envanteri içindir; gizli bir dış servis veya kurulu production özelliği var/yok sonucu çıkarılmaz.

- **E01 — Route ve ekran sınırı:** [web.php](C:/laragon/www/GETMAKS360_V2/routes/web.php:53); [show.blade.php](C:/laragon/www/GETMAKS360_V2/resources/views/operations/listings/show.blade.php:1); [dashboard.blade.php](C:/laragon/www/GETMAKS360_V2/resources/views/member/dashboard.blade.php:1).
- **E02 — Panel/izin/ofis kontrolü:** [RolePermissionRegistry.php](C:/laragon/www/GETMAKS360_V2/app/Core/Authorization/RolePermissionRegistry.php:14); [User.php](C:/laragon/www/GETMAKS360_V2/app/Models/User.php:88); [EnsureOperationalAccess.php](C:/laragon/www/GETMAKS360_V2/app/Http/Middleware/EnsureOperationalAccess.php:26).
- **E03 — Broker geçerliliği ve şahsi kabul engeli:** [BrokerOfficeAccess.php](C:/laragon/www/GETMAKS360_V2/app/Core/Authorization/BrokerOfficeAccess.php:72); [AssignBrokerToOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/AssignBrokerToOffice.php:44).
- **E04 — Kuruluş kayıt zinciri:** [CreateOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Actions/CreateOffice.php:30); [CreateOfficeOnboarding.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Actions/CreateOfficeOnboarding.php:1); [OfficeController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Admin/OfficeController.php:114).
- **E05 — Davet ve kabul:** [CreateBrokerAndAssignToOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/CreateBrokerAndAssignToOffice.php:27); [BrokerInvitationController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Auth/BrokerInvitationController.php:34); [BrokerInvitation.php](C:/laragon/www/GETMAKS360_V2/app/Models/BrokerInvitation.php:1).
- **E06 — Ofis sözleşmesi ve readiness:** [OfficeSetupReadiness.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Services/OfficeSetupReadiness.php:21); [OfficeContractPartyType.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/OfficeContractPartyType.php:5); [OfficeDocumentController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Admin/OfficeDocumentController.php:100).
- **E07 — Ofis aktivasyon kapısı:** [ActivateOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Actions/ActivateOffice.php:25); [ActivateEffectiveOfficeContract.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Actions/ActivateEffectiveOfficeContract.php:1).
- **E08 — Danışman aktivasyon/operasyon ayrımı:** [ActivationReadiness.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Services/ActivationReadiness.php:14); [ActivateConsultant.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/ActivateConsultant.php:20); [EnsureOperationalAccess.php](C:/laragon/www/GETMAKS360_V2/app/Http/Middleware/EnsureOperationalAccess.php:62).
- **E09 — Ofis şartı ve danışman kabulü:** [CommercialController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Consultant/CommercialController.php:64); [AcceptConsultantAgreementVersion.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Actions/AcceptConsultantAgreementVersion.php:1).
- **E10 — Transfer ve kapanış:** [TransferConsultantToOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/TransferConsultantToOffice.php:34); [TerminateProfessional.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/TerminateProfessional.php:24); [TerminateOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Office/Actions/TerminateOffice.php:21).
- **E11 — Çoklu ofis ve bağımsız yetki:** [OperationalAssignment.php](C:/laragon/www/GETMAKS360_V2/app/Core/Organization/OperationalAssignment.php:75); [2026_11_04_115000_scope_broker_office_memberships_and_authorities.php](C:/laragon/www/GETMAKS360_V2/database/migrations/2026_11_04_115000_scope_broker_office_memberships_and_authorities.php:13); [RemoveBrokerFromOffice.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/RemoveBrokerFromOffice.php:24); [SetBrokerCommercialAuthority.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Actions/SetBrokerCommercialAuthority.php:20); [BrokerCommercialAuthorityEvaluator.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Services/BrokerCommercialAuthorityEvaluator.php:95).
- **E12 — Başvuru ve ekip:** [InviteConsultant.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/InviteConsultant.php:30); [ReviewProfessionalApplication.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/ReviewProfessionalApplication.php:23); [ProvisionConsultantApplication.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/ProvisionConsultantApplication.php:32); [ConsultantController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Broker/ConsultantController.php:1).
- **E13 — CRM:** [CustomerController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Operations/CustomerController.php:48); [CreateCustomer.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Customer/Actions/CreateCustomer.php:23); [CustomerVisibility.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Customer/Services/CustomerVisibility.php:15).
- **E14 — Havuz/model:** [PoolClaimPolicyEvaluator.php](C:/laragon/www/GETMAKS360_V2/app/Domains/DataPool/Services/PoolClaimPolicyEvaluator.php:32); [ClaimPoolRecord.php](C:/laragon/www/GETMAKS360_V2/app/Domains/DataPool/Actions/ClaimPoolRecord.php:1); [MarkPoolClaimContacted.php](C:/laragon/www/GETMAKS360_V2/app/Domains/DataPool/Actions/MarkPoolClaimContacted.php:16); [ExpirePoolClaims.php](C:/laragon/www/GETMAKS360_V2/app/Domains/DataPool/Actions/ExpirePoolClaims.php:19); [WorkModelPolicy.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Policies/WorkModelPolicy.php:11).
- **E15 — Intake, atama ve görünürlük:** [CreateMemberDemandRequest.php](C:/laragon/www/GETMAKS360_V2/app/Domains/RequestFile/Actions/CreateMemberDemandRequest.php:30); [AssignMemberDemandRequest.php](C:/laragon/www/GETMAKS360_V2/app/Domains/RequestFile/Actions/AssignMemberDemandRequest.php:18); [RequestFileVisibility.php](C:/laragon/www/GETMAKS360_V2/app/Domains/RequestFile/Services/RequestFileVisibility.php:25); [RequestController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Member/RequestController.php:37); [RequestFileController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Operations/RequestFileController.php:162).
- **E16 — Talep/hizmet köprüsü:** [CreateServiceOffer.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Service/Actions/CreateServiceOffer.php:28); [AcceptServiceOffer.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Service/Actions/AcceptServiceOffer.php:20); [CreateServiceFile.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Service/Actions/CreateServiceFile.php:26); [TransitionServiceFile.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Service/Actions/TransitionServiceFile.php:21).
- **E17 — Hizmet kanıtı ve ilan guard:** [ServiceContract.php](C:/laragon/www/GETMAKS360_V2/app/Models/ServiceContract.php:14); [ServiceAuthorization.php](C:/laragon/www/GETMAKS360_V2/app/Models/ServiceAuthorization.php:14); [ServiceFile.php](C:/laragon/www/GETMAKS360_V2/app/Models/ServiceFile.php:88); [CreateListing.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Listing/Actions/CreateListing.php:50).
- **E18 — Portföy/ilan yazımı ve görünürlüğü:** [PortfolioController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Operations/PortfolioController.php:34); [ListingController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Operations/ListingController.php:36); [CreatePortfolio.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Portfolio/Actions/CreatePortfolio.php:20); [ActivateListing.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Listing/Actions/ActivateListing.php:19); [ListingVisibility.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Listing/Services/ListingVisibility.php:17).
- **E19 — Gösterim/randevu:** [SchedulePropertyShowing.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Showing/Actions/SchedulePropertyShowing.php:21); [CompletePropertyShowing.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Showing/Actions/CompletePropertyShowing.php:18); [PropertyShowingStatus.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Showing/PropertyShowingStatus.php:5).
- **E20 — İşlem başlangıcı ve mutabakat:** [StartTransactionFile.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Transaction/Actions/StartTransactionFile.php:18); [TransactionFileStatus.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Transaction/TransactionFileStatus.php:5); [CreateRequestListingMatch.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Matching/Actions/CreateRequestListingMatch.php:21); [RecordMatchMutual.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Matching/Actions/RecordMatchMutual.php:16); [2026_10_24_165245_create_transaction_files_table.php](C:/laragon/www/GETMAKS360_V2/database/migrations/2026_10_24_165245_create_transaction_files_table.php:14).
- **E21 — Mali politikalar ve ön tahakkuk:** [RecordUsageEvent.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Actions/RecordUsageEvent.php:24); [AssignRevenuePolicy.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Actions/AssignRevenuePolicy.php:20); [AssignCommercialPlan.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Commercial/Actions/AssignCommercialPlan.php:29); [OfficeController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Admin/OfficeController.php:192).
- **E22 — Peşin paket ve süreli hak:** [ConfirmServicePayment.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Service/Actions/ConfirmServicePayment.php:21); [ServicePurchase.php](C:/laragon/www/GETMAKS360_V2/app/Models/ServicePurchase.php:39); [PropertyController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Member/PropertyController.php:18); [ServicePaymentController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Admin/ServicePaymentController.php:1).
- **E23 — Müşteri dosyası ve belge:** [MemberFileVisibility.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Customer/Services/MemberFileVisibility.php:13); [MemberActivityController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Member/MemberActivityController.php:17); [CustomerPortalController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Member/CustomerPortalController.php:50).
- **E24 — Audit:** [AuditLogger.php](C:/laragon/www/GETMAKS360_V2/app/Core/Audit/AuditLogger.php:20); [AuditLog.php](C:/laragon/www/GETMAKS360_V2/app/Models/AuditLog.php:13); [StatusTransitionRecorder.php](C:/laragon/www/GETMAKS360_V2/app/Core/Audit/StatusTransitionRecorder.php:1).
- **E25 — Bildirim teslim boşluğu:** [DeliverApplicationNotification.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Notifications/DeliverApplicationNotification.php:9); [ProcessApplicationNotificationOutbox.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/ProcessApplicationNotificationOutbox.php:19).
- **E26 — Periyodik işler ve worker:** [console.php](C:/laragon/www/GETMAKS360_V2/routes/console.php:11); [DispatchApplicationNotificationOutbox.php](C:/laragon/www/GETMAKS360_V2/app/Console/Commands/DispatchApplicationNotificationOutbox.php:15); [ProcessApplicationNotificationOutbox.php](C:/laragon/www/GETMAKS360_V2/app/Jobs/ProcessApplicationNotificationOutbox.php:23); [ApplyScheduledConsultantTransfers.php](C:/laragon/www/GETMAKS360_V2/app/Domains/Professional/Actions/ApplyScheduledConsultantTransfers.php:1).
- **E27 — İşletim config kaynakları:** [app.php](C:/laragon/www/GETMAKS360_V2/bootstrap/app.php:1); [app.php](C:/laragon/www/GETMAKS360_V2/config/app.php:1); [database.php](C:/laragon/www/GETMAKS360_V2/config/database.php:19); [queue.php](C:/laragon/www/GETMAKS360_V2/config/queue.php:16); [cache.php](C:/laragon/www/GETMAKS360_V2/config/cache.php:1); [session.php](C:/laragon/www/GETMAKS360_V2/config/session.php:1); [logging.php](C:/laragon/www/GETMAKS360_V2/config/logging.php:1); [mail.php](C:/laragon/www/GETMAKS360_V2/config/mail.php:16).
- **E28 — Üyelik/giriş ve bağımlılıklar:** [RegisterController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Auth/RegisterController.php:22); [LoginController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Auth/LoginController.php:16); [composer.json](C:/laragon/www/GETMAKS360_V2/composer.json:1); [package.json](C:/laragon/www/GETMAKS360_V2/package.json:1).
- **E29 — Özel dosya depolama:** [filesystems.php](C:/laragon/www/GETMAKS360_V2/config/filesystems.php:31); [OfficeDocumentController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Admin/OfficeDocumentController.php:91); [ServicePaymentController.php](C:/laragon/www/GETMAKS360_V2/app/Http/Controllers/Member/ServicePaymentController.php:1).
- **E30 — Geçmiş teslim ve migration hata testleri:** [09_CODEX_HANDOFF.md](C:/laragon/www/GETMAKS360_V2/docs/09_CODEX_HANDOFF.md:13); [BrokerOfficeMigrationFailureTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/BrokerOfficeMigrationFailureTest.php:25); [BrokerOfficeSchemaMigrationTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/BrokerOfficeSchemaMigrationTest.php:26); [MultiOfficeBrokerTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/MultiOfficeBrokerTest.php:34).
- **E31 — Diğer test kaynakları — çalıştırılmadı:** [MemberRequestIntakeTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/MemberRequestIntakeTest.php:12); [PortfolioListingFlowTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/PortfolioListingFlowTest.php:13); [ShowingAndTransactionFlowTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/ShowingAndTransactionFlowTest.php:18); [PrepaidServiceAccessTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/PrepaidServiceAccessTest.php:25); [ConsultantOfficeTransferTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/ConsultantOfficeTransferTest.php:25); [ProfessionalApplicationOutboxTest.php](C:/laragon/www/GETMAKS360_V2/tests/Feature/ProfessionalApplicationOutboxTest.php:20).

### 7.1 Kaynak kanıtı ile test kanıtı ayrımı

- Test dosyasının bulunması veya bir fixture'ın SIGNED sözleşme/ACTIVE ofis üretmesi, bu kaydı gerçek kullanıcı ekranından oluşturma akışının tamamlandığını göstermez.
- MemberRequestIntakeTest talep kaydını; PortfolioListingFlowTest guard ve fixture temelli ilanı; ShowingAndTransactionFlowTest başlangıç zincirini; PrepaidServiceAccessTest ödeme dönemini sınamayı amaçlar. Bunların hiçbiri tek başına tüm pilotu kapsamaz.
- 111/595 sonucu önceki handoff kaydıdır. Bu görevde yeniden test çalıştırılmadı. Diğer test dosyaları için güncel başarılı sonuç iddia edilmez.
- Kod/ayar/veri/scheduler/mail/backup gerçek ortam durumuna bu görevde bakılmadı; geçmiş başarılı otomatik test bunun yerine geçmez.

## 8. Denetim bütünlüğü ve son cevap

Başlangıç/son SHA-256 karşılaştırmasında app, bootstrap, config, database kaynakları (SQLite dosyaları hariç), resources, routes, tests, public, .ai/rules, AGENTS.md ve bağımlılık dosyaları **eşit** bulundu. Mevcut 13 docs dosyası, arşiv, handoff/ADR ve CHANGELOG ayrıca dosya bazında kontrol edildi ve **değişmedi**. Tek yeni dosya bu rapordur; doküman sayısının 13'ten 14'e çıkması kullanıcının bu denetime özel tarihli rapor talebinin sonucudur. Raporun 115 yerel kaynak bağlantısının dosya/satır varlığı ve kanıt referansları kontrol edildi. Bu kontrol DB içeriğinin değişmezliğini iddia etmez; bu görev DB'ye bağlanmadı.

**Getmaks360 V2'nin gerçek pilot öncesinde tamamlaması gereken zorunlu işler:** Broker şahsi kabulünden güvenli ofis aktivasyonuna ulaşan yol; aynı-ofis kayıt sahipliği ve yeni danışman anlaşma kontrolü; bölgesel ve modeline uygun müşteri yönlendirmesi; owner hizmet başvurusunun kesintisiz ilerlemesi; gerçek sözleşme/yetkilendirmeden müşteri Marketplace yayınına giden ilan süreci; seçilen modele uygun çalışma/iletişim korumaları; açık işlerin sahipsiz kalmaması; gerçekleşmiş işlemden izlenebilir ücret ve hak sonucuna geçiş; gerçek bildirim ve işletim/yedek/geri dönüş kanıtlarıdır.

Bu işler mevcut Laravel çekirdeği korunarak aşamalı tamamlanabilir. Ancak bugünkü durumla yeni gerçek ofis + Broker + danışmanlar + Marketplace + mali sonuç için koşulsuz “pilot hazır” denemez. Sonraki geliştirme ancak ayrıca seçilecek kapsam ve yetkiyle yapılmalıdır. **Denetim burada biter; Paket 3 başlamaz, 03C.4 KISMİ kalır.**

