---
description: ProductionSafe
---

ProductionSafe: Production ortamı için güvenlik kontrolü. Her kod yazarken kontrol et:

1. LOGGING KONTROLLERİ:
   - Log seviyeleri doğru mu? (Development: Debug, Production: Warning+)
   - Recursive loglama var mı? (inner exceptions, ORM query logging)
   - Log rotasyon ve retention politikası var mı?
   - Hassas veri loglanıyor mu? (şifreler, tokenlar, kişisel bilgiler)
   
2. DATABASE İŞLEMLERİ:
   - N+1 query problemi var mı?
   - Index'ler uygun mu?
   - Connection pool ayarları yapılmış mı?
   - Transaction timeout'ları var mı?
   
3. KAYNAK YÖNETİMİ:
   - Memory leak riski var mı?
   - File handle'lar kapatılıyor mu?
   - Database connection'lar properly dispose ediliyor mu?
   
4. RATE LIMITING:
   - API rate limit var mı?
   - Retry logic sonsuz döngü yaratmaz mı?
   
Production'a gidecek her kod için bu kontrolleri yap. Şüpheli bir şey varsa UYAR.