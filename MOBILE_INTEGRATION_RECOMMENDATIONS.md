# Mobil Cihaz Entegrasyonu Önerileri

Bu not, mevcut PWA tabanlı sayaç projesinin mobil deneyimini güçlendirmek için teknik öneriler içerir.

## 1) Hızlı Kazanımlar (yüksek etki / düşük efor)

1. **Service worker cache listesi düzeltmesi**
   - `sw.js` içinde cache’e eklenen dosya listesinde `timer.html` geçiyor; projede ana dosya `index.html`.
   - Sonuç: ilk yükleme sonrası offline davranış beklenenden farklı olabilir.
   - Öneri: `FILES` listesini `['index.html', 'manifest.json', 'sw.js']` gibi güncelleyin.

2. **iOS için dokunmatik hedefleri büyütme**
   - `⋯`, `Start`, `Apply` gibi düğmelerde minimum 44x44 px hedef alanı garanti edin.
   - Özellikle küçük ekranlarda yanlış dokunmaları azaltır.

3. **Safe-area (notch/dynamic island) desteği**
   - Tam ekran PWA’da alt/üst sabit konumlu öğeler (`#menu-btn`) kenarlara çok yaklaşabilir.
   - Öneri: `padding-bottom: env(safe-area-inset-bottom)` ve ilgili `env(...)` değerleriyle konumları güvenli alanlara taşıyın.

4. **Ekran yönü optimizasyonu**
   - Sayaç görünümünde yatay modda daha büyük font + daha iyi merkezleme uygulanabilir.
   - `@media (orientation: landscape)` ile ayrı tipografi ayarı ekleyin.

## 2) Platform Entegrasyonları

1. **Android için WebAPK/PWA yükleme akışı netleştirme**
   - README’ye “Ana ekrana ekle” adımlarını ekran görüntülü ekleyin.

2. **iOS için web app meta iyileştirmesi**
   - `apple-touch-icon` ekleyin (PNG).
   - Splash screen görselleri (isteğe bağlı) üretin.

3. **Bildirim + alarm fallback’i**
   - Sekme arka planda kaldığında titreşim her zaman tetiklenmeyebilir.
   - İzinli senaryoda local notification fallback’i tasarlayın.

## 3) Zamanlayıcı Güvenilirliği

1. **setInterval drift düzeltmesi**
   - 1 saniyelik interval mobilde arka plan/gecikme durumlarında kayma yapar.
   - Çözüm: başlangıç zamanını tutup `Date.now()` farkına göre kalan süreyi hesaplayın.

2. **Arka plan/geri dönüş toparlama**
   - `visibilitychange` sadece wake lock için değil, sayaç doğrulaması için de kullanılmalı.
   - Uygulama geri gelince kalan süre yeniden hesaplanmalı.

## 4) Mobil UX İyileştirmeleri

1. **Haptics katmanlama**
   - Mevcut titreşimi (kısa-uzun-kısa) farklı olaylar için ayrıştırın: reset, bitiş, apply.

2. **Erişilebilirlik**
   - Butonlara `aria-label` ekleyin (`menu`, `start`, `apply` vb.).
   - Kontrastın düşük olduğu ikincil metinlerde (`#444`, `#555`) WCAG kontrolü yapın.

3. **Girdi ergonomisi**
   - `MMSS` girişi için otomatik format (örn. `1234` -> `12:34`) gösterimi hata oranını düşürür.

## 5) İleri Seviye (opsiyonel)

1. **Capacitor ile native shell**
   - Aynı web kodunu iOS/Android paketi olarak dağıtıp daha tutarlı arka plan ve titreşim API’leri elde edebilirsiniz.

2. **Arka planda ses alarmı (native katman)**
   - Kritik kullanım senaryolarında (antrenman/interval) uygulama arka plandayken de alarm güvenilirliği artar.

3. **Kilit ekranı / medya kontrol entegrasyonu (native)**
   - Başlat-durdur-reset kontrolü kilit ekranından erişilebilir olabilir.

## Önerilen Yol Haritası

- **Aşama 1 (1 gün):** SW cache düzeltmesi, safe-area, dokunmatik hedefler, landscape CSS.
- **Aşama 2 (1-2 gün):** drift düzeltmesi + visibility toparlama + a11y etiketleri.
- **Aşama 3 (2-4 gün):** bildirim fallback, yükleme yönergeleri, ikon/splash iyileştirme.
- **Aşama 4 (opsiyonel):** Capacitor paketleme ve native alarm yetenekleri.
