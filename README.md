# Hava Durumu (Vue 3 + Vite) 🌤️

Bu proje, Vue 3 ve Vite kullanılarak geliştirilmiş modern ve hızlı bir hava durumu uygulamasıdır. Kullanıcıların istedikleri şehrin veya ilçenin güncel hava durumu verilerini (sıcaklık, hissedilen sıcaklık, nem oranı ve hava durumu) anlık olarak görüntülemelerini sağlar.

## Kullanılan Teknolojiler ve API
- **[Vue.js (Vue 3)](https://vuejs.org/)**: Kullanıcı arayüzü ve modern bileşen yapısı için.
- **[Vite](https://vitejs.dev/)**: Hızlı geliştirme ortamı ve paketleme için.
- **[wttr.in API](https://github.com/chubin/wttr.in)**: Hava durumu verilerini almak için kullanılmıştır. Herhangi bir API anahtarı (API Key) gerektirmeden hızlı bir şekilde JSON formatında hava durumu verileri sunar.

## Kurulum ve Çalıştırma Adımları

Projeyi kendi bilgisayarınızda çalıştırmak için sisteminizde [Node.js](https://nodejs.org/) kurulu olması gerekmektedir. Ardından aşağıdaki adımları takip edebilirsiniz:

### 1. Projeyi Klonlayın
```bash
git clone https://github.com/samicankaya/HavaDurumuVue.js.git
```

### 2. Proje Dizinine Girin
```bash
cd HavaDurumuVue.js
```
*(Eğer projeyi sıfırdan oluşturduğunuz bir klasörde çalıştırıyorsanız direkt o klasörde terminal açabilirsiniz.)*

### 3. Bağımlılıkları Yükleyin
```bash
npm install
```

### 4. Geliştirici Sunucusunu Başlatın
```bash
npm run dev
```

Bu komutu çalıştırdıktan sonra terminalde size bir yerel sunucu adresi (genellikle `http://localhost:5173`) verilecektir. Bu bağlantıyı tarayıcınızda açarak uygulamayı kullanmaya başlayabilirsiniz.

---

### Üretime (Production) Hazırlama (Opsiyonel)
Eğer projeyi canlıya almak (deploy etmek) isterseniz aşağıdaki komut ile optimize edilmiş dosyaları oluşturabilirsiniz:
```bash
npm run build
```
Bu işlem sonucunda `dist` adında bir klasör oluşur ve bu klasörü herhangi bir sunucuda yayınlayabilirsiniz.
