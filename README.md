# Antigravity Workflows 🚀

Bu repo, **Antigravity AI** için özel olarak tasarlanmış bir dizi "Workflow" (İş Akışı) içerir. Bu iş akışları, AI'nın belirli görevlerde (kod yazma, hata ayıklama, mimari planlama vb.) daha tutarlı, güvenli ve verimli çalışmasını sağlar.

## 📋 Nedir Bu Workflows?

Workflows (İş Akışları), Antigravity AI'ya tekrarlayan görevleri nasıl yapacağını öğreten veya belirli bir çalışma moduna geçmesini sağlayan markdown dosyalarıdır. 

Bu paketin merkezinde `aimodes.md` (AI Mod Yönlendirme) bulunur. Bu ana dosya, görevinizin tipine göre hangi alt modların aktif edilmesi gerektiğini AI'ya söyler.

---

## 🚀 Kurulum

Bu iş akışlarını kullanmak için iki yönteminiz vardır:

### 1. Global Kullanım (Tüm Projeler İçin)
Bu yöntemi kullanarak iş akışlarına her yerden erişebilirsiniz.

1. İş akışlarını bilgisayarınızdaki Antigravity global klasörüne kopyalayın:
   - **Windows:** `C:\Users\KullanıcıAdınız\.gemini\antigravity\global_workflows`
   - **Mac/Linux:** `~/.gemini/antigravity/global_workflows`
2. Dosyaları bu klasöre `.md` uzantısıyla yerleştirin.

### 2. Proje Bazlı (Workspace) Kullanım
Sadece belirli bir projede kullanmak istiyorsanız:

1. Projenizin kök dizinine `.agent/workflows/` klasörü oluşturun.
2. Bu repodaki dosyaları o klasöre kopyalayın.

---

## 🛠 Kullanım

Antigravity panelinde `/` (slash) komutunu yazarak istediğiniz modu çağırabilirsiniz.

**Önerilen Kullanım Senaryosu:**
Yeni bir göreve başlarken şu komutu verin:
> `/aimodes bu görevi analiz et ve uygun modlarla ilerle`

AI, `aimodes.md` içindeki seçim matrisine bakarak göreviniz için en uygun modları (örneğin `AgentGuard`, `ArchitectMode`, `SafeExecutor`) otomatik olarak seçecek ve o kurallara göre çalışacaktır.

---

📄 Workflow yapısı ile ilgili öneri: docs/workflow-yapi-onerisi.md


## 📦 Mevcut Modlar (Workflows)

| Komut | Açıklama |
| :--- | :--- |
| `/aimodes` | **Ana Kontrol Ünitesi.** Görevin tipine göre diğer modları seçer. |
| `/agentguard` | Halüsinasyonu önler, sadece gerçek kütüphaneleri kullanır. |
| `/architectmode` | Kod yazmadan önce mimari planlama ve tasarım yapar. |
| `/contextkeeper` | Büyük dosyalarda bağlam kaybını önlemeye odaklanır. |
| `/debugmaster` | Hata ayıklama süreçleri için gelişmiş analiz yapar. |
| `/fileaware` | Dosya okuma/yazma işlemlerinde dikkatli ve titiz davranır. |
| `/safeexecutor` | Terminal komutlarını çalıştırmadan önce güvenlik kontrolü yapar. |
| `/stepbystep` | Üretim (Production) kodu yazarken adım adım ilerler. |
| `/ultrathink` | Karmaşık problemler için derinlemesine düşünme modu. |
| `/productionsafe` | Kritik sistemlerde güvenli değişiklik protokolü. |
| `/refactorsafe` | Kod temizliği yaparken mevcut yapıyı bozmamayı hedefler. |
| `/testfirst` | TDD (Test Driven Development) yaklaşımını zorunlu tutar. |
| `/dependencycheck`| Bağımlılıkları ve sürüm çatışmalarını kontrol eder. |
| `/multifilesync` | Çoklu dosya değişikliklerinde senkronizasyonu korur. |

---

## 🧪 Deneysel: Dil Bazlı Workflows

Bu repo, mevcut workflow yapısını bozmadan,
örnek olması amacıyla **dil bazlı (C#, Python, Go)** workflow’lar da içermektedir.

Bu dosyalar:
- `workflows/language-based/` altında yer alır
- **Opsiyoneldir**
- Global ve Workspace kullanım senaryolarını ayrı ayrı gösterir

Detaylar için bkz:
- `docs/workflow-yapi-onerisi.md`


---
## 🤝 Katkıda Bulunma

Yeni bir mod eklemek veya mevcutları geliştirmek isterseniz pull request göndermekten çekinmeyin!

1. Bu repoyu fork'layın.
2. Yeni bir branch açın (`feat/yeni-mod`).
3. Değişikliklerinizi yapın ve commit'leyin.
4. Push edin ve bir Pull Request oluşturun.

## 📄 Lisans

Bu proje [MIT](LICENSE) lisansı ile lisanslanmıştır.
