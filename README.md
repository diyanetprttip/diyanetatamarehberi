# Diyanet Atama Rehberi — Aday İşlemleri
Bu paket üyelik tabanlı aday paneli başlangıcıdır; ÖSYM AİS'in resmî ürünü değildir.

## Dosyalar
- `index.html`: Üye girişi, aday sonuçları, duyurular, yönetici ekranı.
- `app-config.js`: Supabase URL ve anon/public key ayarları.
- `supabase/schema.sql`: Tablolar ve aday bazlı Row Level Security politikaları.
- `supabase/functions/osym-sync/index.ts`: Yazılı yetki ve resmî API bilgisi geldikten sonra tamamlanacak entegrasyon iskeleti.

## Kurulum
1. Supabase'te proje açın ve SQL Editor'de `supabase/schema.sql` çalıştırın.
2. Supabase Project Settings > API içinden Project URL ve anon/public key değerlerini `app-config.js` içine girin. **Service role key kullanmayın.**
3. Supabase Authentication > URL Configuration'a GitHub Pages adresinizi ekleyin.
4. İlk hesabı portalda oluşturun. Supabase Authentication > Users bölümünden UUID'yi alın.
5. SQL Editor'de `update public.profiles set role='admin' where id='UUID';` komutunu çalıştırın.
6. GitHub Pages'i main / root üzerinden etkinleştirin.

## CSV sonuç aktarımı
Başlıklar: `candidate_user_id,exam_type,exam_name,exam_date,score,correct_count,wrong_count`. `candidate_user_id`, adayın Supabase kullanıcı UUID'sidir. T.C. kimlik numarası veya e-posta yüklemeyin. Basit virgülle ayrılmış CSV kullanın.

## ÖSYM entegrasyonu
Gerçek bağlantı için ÖSYM'nin yazılı izni, resmî API dokümantasyonu ve erişim yetkisi gerekir. Aday AİS şifresi toplama, kapalı sayfaları kazıma veya yetkisiz veri çekme yapılmaz. Gizli API anahtarları Edge Function Secrets içinde tutulmalıdır.
