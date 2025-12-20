> ⚠️ Bu doküman mevcut workflow yapısını değiştirmeyi önermez.
> Amaç, dil bazlı ve kullanım senaryosu odaklı workflow’lar için
> opsiyonel ve genişletilebilir bir örnek sunmaktır.


\# Workflow Yapılandırma Önerisi



Mevcut durumda workflow dokümantasyonlarının tamamı repo ana dizininde

yer almaktadır. Workflow sayısı arttıkça bu durum hem okunabilirlik

hem de sürdürülebilirlik açısından zorluklar oluşturabilir.



Bu nedenle workflow’ların \*\*genel (global)\*\* ve \*\*dil bazlı proje workflow’ları\*\*

olarak ayrılması faydalı olabilir.



\## Önerilen Yapı



```text

workflows/

├─ global/

│   ├─ logging.md

│   ├─ security-baseline.md

│   ├─ ci-common.md

│

├─ language-based/

│   ├─ csharp/

│   │   ├─ build.md

│   │   ├─ test.md

│   │   └─ deploy.md

│   │

│   ├─ python/

│   │   ├─ venv.md

│   │   ├─ lint.md

│   │   └─ ci.md

│   │

│   ├─ go/

│   │   ├─ build.md

│   │   └─ test.md

│   │

│   └─ nodejs/

│       └─ ci.md



