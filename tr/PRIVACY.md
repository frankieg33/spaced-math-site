---
title: "Günlük Mate"
description: "iPhone ve iPad için aralıklı tekrarlı matematik alıştırmaları"
---

# Gizlilik Politikası — Günlük Mate

**Yürürlük tarihi:** 2026-05-21
**Son güncelleme:** 2026-06-10

Bu politika, iOS uygulaması Günlük Mate'nin ("Uygulama") bilgilerinizi nasıl ele aldığını açıklar. v1.0'dan itibaren geçerlidir; buna v2.0'ın profil bazlı paylaşımının yerini alan v3'ün tek aileli CloudKit paylaşım modeli de dahildir.

## Sade bir özet

- Hiçbir sunucu işletmiyoruz. Hiçbir kişisel bilgi toplamıyoruz.
- **iCloud eşitleme**'yi açmadığınız sürece her şey cihazınızda kalır; açtığınızda ise biz değil, Apple bunu özel iCloud hesabınızda saklar.
- Uygulama mikrofonunuzu yalnızca ses modunda bir soruyu yanıtlarken kullanır. Ses, Apple'ın cihaz üzerindeki (Siri sınıfı) konuşma tanımasıyla işlenir ve hemen atılır; onu asla saklamaz, yüklemez veya analiz etmeyiz.
- Hiçbir üçüncü taraf izleyici, reklam veya analiz SDK'sı yoktur.

## Uygulamanın cihazınızda sakladıkları

- **Profiller.** Ad, emoji, renk ve profil bazlı ayarlar.
- **Aralıklı tekrar durumu.** Her kart için (ör. `7 + 8`): planlanan bir sonraki tekrar tarihi, zorluk, kararlılık ve tekrar sayısı.
- **Etkinlik.** Profil başına tamamlanan tekrarların günlük sayımı (seri rozeti ve İstatistik ekranı için kullanılır).
- **Hatalar.** Yakın zamanda yanlış yanıtladığınız soruların bir kuyruğu; böylece Uygulama bunları yeniden gösterebilir.
- **Tercihler.** iCloud eşitlemenin açık olup olmadığı gibi Uygulama genelindeki anahtarlar.

Bunların tümü Uygulamanın kendi yalıtılmış Belgeler klasörüne ve `UserDefaults`'a yazılır. Uygulama diğer uygulamaların verilerini okuyamaz, diğer uygulamalar da Uygulamanın verilerini okuyamaz.

## Uygulamanın iCloud'da isteğe bağlı sakladıkları

iCloud eşitleme **varsayılan olarak kapalıdır**. Açtığınızda (dişli simgesi → **Ayarlar → Eşitleme → iCloud kullan**), Uygulama yukarıda açıklanan aynı verileri Apple'ın **CloudKit** API'si aracılığıyla özel iCloud'unuza yazar. Bu sizin iCloud'unuzdur ve yalnızca aynı Apple Kimliği ile oturum açmış cihazlarda yalnızca size erişilebilir. Bizim ona erişimimiz yoktur.

- Tam olarak eşitlenen veriler: profiller, kart durumları, etkinlik, hatalar ve (isteğe bağlı) aile paylaşımı meta verileri (aileniz için seçtiğiniz bir görünen ad).
- iCloud eşitleme, herhangi bir ses kaydının içeriğini veya herhangi bir analizi **içermez**.
- Farklı bir Apple Kimliği ile oturum açtığınızda, Uygulama değişikliği algılar ve siz açıkça yeniden açana dek eşitlemeyi kapatır; böylece veriler sessizce başka bir hesaba yüklenmez.
- **Profilleri Yönet**'ten bir profili silmek, profili cihazdan ve (iCloud orijinal Apple Kimliğinde erişilebilirken) iCloud kopyanızdan kaldırır.

## Aile paylaşımı

v3'te paylaşım, profil başına değil **aile** düzeyinde gerçekleşir. Dişli simgesi → **Ayarlar → Aile → Aileyi kur**'u açın, ailenize bir ad verin ve standart iOS paylaşım sayfası aracılığıyla aile üyelerini davet edin (Mesajlar, Mail veya AirDrop).

- Sahibinin cihazındaki tüm profiller aileye aittir. Bir aile üyesini davet etmek bunların hepsini bir kerede paylaşır.
- Veriler **aile sahibinin iCloud'unda** bulunur. Katılımcılar kendi iCloud'larında ayrı bir kopya saklamaz; çalışma etkinlikleri, Apple'ın bölge kapsamlı CKShare izin modeli aracılığıyla doğrudan sahibinin CloudKit'ine yazılır.
- Bir aileye katılmak **katılan cihazda geri alınamaz**: katılımcının mevcut yerel profilleri ailenin profilleriyle değiştirilir. Katılmadan önce Uygulama bir **Profilleri dosyaya aktar** seçeneği sunar; böylece mevcut verilerinizin bir JSON kopyasını kaydeder ve fikrinizi değiştirirseniz sonra yeniden içe aktarabilirsiniz.
- Sahip aileyi dağıtırsa (Ayarlar → Aile → Dağıt) veya iCloud'dan çıkış yaparsa, katılımcılar bir sonraki eşitlemede canlı erişimi kaybeder. Aile profillerinin yerel önbelleği kendilerinin olur (çıkışta geri alınamaz bir silme olmaz).
- Bir katılımcı aileyi istediği zaman terk edebilir (Ayarlar → Aile → Ayrıl). Ayrılırken, ailenin profillerini kendi profilleri olarak cihazında tutar.
- Apple'ın `CKShare` sınırı, paylaşılan öğe başına 100 katılımcıdır. Doğal aile ölçeği ~6'dır.

## Dışa aktar / İçe aktar (JSON yedek)

**Ayarlar → Yedek** bölümünde şunları yapabilirsiniz:

- **Profilleri dosyaya aktar**: mevcut cihazdaki tüm profilleri (aile durumu ne olursa olsun) içeren bir JSON dosyası kaydeder. Manuel bir yedek olarak veya geri alınamaz işlemlerden önce kullanışlıdır.
- **Profilleri dosyadan içe aktar**: önceki bir dışa aktarmayı geri yükler. **Birleştir** modu eksik profilleri ekler ve içe aktarılan kopya daha yeniyse mevcut olanları günceller. **Değiştir** modu yerel profilleri siler ve içe aktarılan kümeyi kurar; yalnızca bir ailede değilken kullanılabilir.

## Mikrofon ve konuşma tanıma

Ses modu açıkken, bir soruyu yanıtlarken Uygulama:

1. `AVAudioEngine` ile canlı mikrofon sesini yakalar.
2. Bunu `SFSpeechRecognizer`'a (Apple'ın çerçevesi) aktarır. Modern iOS cihazlarda tanıma varsayılan olarak cihazda çalışır; bazı yapılandırmalar Apple'ın konuşma tanıma sunucularını kullanabilir.
3. Yazıya dökülen rakamları okur ve yanıtı değerlendirir.
4. Nihai bir yanıt elde edilir edilmez yakalamayı durdurur.

Hiçbir ses, döküm veya türetilmiş sinyal saklamayız. Apple'ın `SFSpeechRecognizer`'ı dışında hiçbir tarafa ses aktarmayız. Uygulama ilk kullanımda `NSMicrophoneUsageDescription` ve `NSSpeechRecognitionUsageDescription` ister; izinlerden herhangi biri reddedilirse ses modu otomatik olarak devre dışı kalır ve ekrandaki sayı tuş takımı kullanılır.

## Tanılama günlükleri

Uygulama, Apple'ın standart `OSLog` çerçevesi aracılığıyla yapılandırılmamış tanılama olayları yayar (ör. "çalışma oturumu bitti, doğru=12 yanlış=3"). Bu günlükler:

- Cihazda kalır.
- Yalnızca size görünür; cihaz bir Mac'e bağlıyken Console.app'te.
- Olası kimlik belirleyici değerler (profil id'si, profil adı) için Apple'ın `.private` gizlilik sınıflandırmasını kullanır; böylece yayınlanan derlemelerde bu değerler gizlenir.

`OSLog` içeriğini toplamaz, almaz veya iletmeyiz.

## Toplamadığımız veriler

- Adınız, e-postanız veya iletişim bilgileriniz.
- Konumunuz.
- Herhangi bir cihaz tanımlayıcısı (IDFA, IDFV, reklam id'si).
- Apple'ın iOS ayarlarınız aracılığıyla toplayabileceğinin ötesinde çökme raporları.
- Herhangi bir analiz veya davranışsal telemetri.
- Ödeme veya faturalandırma bilgileri (satın alımlar tamamen Apple tarafından yürütülür).

## Çocukların gizliliği

Günlük Mate, çocuklar için güvenli olacak şekilde tasarlanmıştır. Uygulama kişisel bilgi toplamadığı ve üçüncü taraflarla iletişim kurmadığı için COPPA'nın "kişisel bilgi yok" tanımını karşılar. Reklam göstermeyiz; hesap veya sosyal özellik yoktur. Günlük Mate, tek seferlik bir uygulama içi satın alma (tam uygulamanın kilidini açma) içerir; uygulama çocuklar için tasarlandığından, Apple'ın Çocuklar kategorisi kurallarının gerektirdiği gibi her satın almadan önce bir yetişkin doğrulaması gösterilir. Tüm ödemeler ve her türlü kod kullanımı Apple tarafından App Store aracılığıyla yürütülür. Uygulama ödeme bilgilerinizi asla görmez veya saklamaz.

## Seçenekleriniz

- **Ses modunu kapatın**: profil başına istediğiniz zaman (Ayarlar → Ses modu) veya iOS ayarlarında mikrofon iznini reddederek genel olarak.
- **iCloud eşitlemeyi kapatın**: istediğiniz zaman (dişli simgesi → Ayarlar → Eşitleme → iCloud kullan → kapalı). Kapatmak iCloud kopyalarını silmez; kaldırmak isterseniz her profili tek tek silin.
- **Bir aileyi dağıtın veya terk edin** (Ayarlar → Aile → Dağıt / Ayrıl) paylaşımı durdurmak için. Dağıtmak katılımcıların ailenize erişimini iptal eder; ayrılmak ailenin profillerini cihazınızda kendi profilleriniz olarak tutar.
- **Profilleri bir dosyaya aktarın** (Ayarlar → Yedek → Dışa aktar) ve yerel olarak saklayın — iCloud'a asla dokunmayan manuel bir yedek.
- **Bir profilin ilerlemesini sıfırlayın** profili silmeden (profil ayarları → Sıfırla).
- **Bir profili silin** (Profilleri Yönet → silmek için kaydırın veya dokunun) — eşitleme açıkken iCloud kopyasını da kaldırır. Her şeyi kaldırmak için profil başına tekrarlayın.

## Bu politikadaki değişiklikler

Bu politikayı değiştirirsek, yeni sürüm aynı URL'de güncellenmiş bir **Son güncelleme** tarihiyle yer alır. Önemli değişiklikler Uygulamanın sürüm notlarında da belirtilir.

## İletişim

Bu politika veya verileriniz hakkında sorularınız mı var? E-posta **spacedmath@gmail.com**.
