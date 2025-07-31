# SongMatch Android Uygulaması - Proje Belgesi

## 📱 Proje Özeti
Şarkıları birbiriyle karşılaştırmak için geliştirilmiş Android uygulaması. Kullanıcılar CSV dosyasından şarkı listeleri yükleyip, ikili karşılaştırmalar yaparak hangi şarkıları daha çok sevdiklerini belirleyebilir.

## 🎯 Proje Amaçları
- CSV dosyasından şarkı listesi import etme
- Şarkıları ikili karşılaştırma sistemi ile değerlendirme
- Yatay ekran orientasyonunda kullanım
- Puanlama sistemi ile şarkı tercihlerini kaydetme
- Turnuva usulü karşılaştırma algoritması (1vs2, 1vs3, 1vs4, 2vs3, 2vs4, 3vs4...)

## 📊 CSV Format Gereksinimleri
```csv
Şarkı No,Albüm Adı,Şarkı Adı
1,Abbey Road,Come Together
2,Abbey Road,Something
3,Let It Be,Let It Be
```
- A sütunu: Şarkı numarası (ID)
- B sütunu: Albüm adı
- C sütunu: Şarkı adı

## ✅ Tamamlanan Özellikler

### 1. Proje Yapısı ve Konfigürasyon
- ✅ Yatay ekran orientasyonu (`android:screenOrientation="landscape"`)
- ✅ Room database dependencies eklendi
- ✅ Jetpack Compose UI framework
- ✅ ViewModel ve Repository pattern implementasyonu

### 2. Veritabanı Yapısı
- ✅ **Song Entity**: `id`, `albumName`, `songName`, `score` alanları
- ✅ **SongDao**: CRUD operations ve score güncelleme
- ✅ **SongDatabase**: Room database singleton implementation

### 3. Veri Katmanı
- ✅ **SongRepository**: CSV import ve veritabanı işlemleri
- ✅ **CSV Parser**: CSV dosyasından şarkı listesi okuma
- ✅ **Error Handling**: Import işlemleri için hata yönetimi

### 4. UI Katmanı
- ✅ **MainActivity**: Ana aktivite ve navigation logic
- ✅ **MainScreen**: CSV yükleme ve şarkı listesi görüntüleme
- ✅ **ComparisonScreen**: Split-screen şarkı karşılaştırma
- ✅ **SongViewModel**: UI state management

### 5. Karşılaştırma Sistemi
- ✅ **Algoritma**: Tüm şarkı çiftlerini karşılaştırma
- ✅ **UI Flow**: Ana ekrandan karşılaştırma ekranına geçiş
- ✅ **Puanlama**: Seçilen şarkıya +1 puan verme
- ✅ **Progress Tracking**: Karşılaştırma ilerlemesi takibi

## 🏗️ Teknik Mimari

### Teknolojiler
- **Kotlin** - Programlama dili
- **Jetpack Compose** - Modern UI toolkit
- **Room Database** - Yerel veri saklama
- **ViewModel & LiveData** - MVVM pattern
- **Coroutines & Flow** - Asenkron programlama

### Proje Yapısı
```
app/src/main/java/com/tavla/songmatch/
├── data/
│   ├── Song.kt              # Entity class
│   ├── SongDao.kt           # Database Access Object
│   └── SongDatabase.kt      # Room database
├── repository/
│   └── SongRepository.kt    # Data repository
├── viewmodel/
│   └── SongViewModel.kt     # UI state management
├── ui/theme/               # Compose theme files
└── MainActivity.kt         # Ana aktivite
```

## 🔧 Geliştirme Notları

### Dependencies (build.gradle.kts)
- Room: `2.6.1`
- Compose BOM: `2024.09.00`
- Lifecycle ViewModel: `2.9.2`
- Kotlin KAPT plugin eklendi

### Önemli Dosyalar
- `AndroidManifest.xml`: Landscape orientation ayarı
- `libs.versions.toml`: Version catalog
- Database dosyalar: `/data` klasörü
- UI komponenleri: `MainActivity.kt`

## 🚀 Kullanım Senaryosu
1. Uygulama açılır (landscape mode)
2. "CSV Dosyası Yükle" butonu ile dosya seçimi
3. CSV parse edilir ve veritabanına kaydedilir
4. "Karşılaştırmaya Başla" butonu aktif olur
5. Split-screen karşılaştırma ekranı açılır
6. Kullanıcı tercih ettiği şarkıya tıklar
7. Puan kaydedilir ve sonraki eşleştirmeye geçilir
8. Tüm eşleştirmeler tamamlanana kadar devam eder

## 🐛 Bilinen Sorunlar ve Çözümler
- ✅ **InputStream "stream closed" hatası**: Repository'de CSV okuma yöntemi değiştirildi, önce tüm content okunup sonra işleniyor
- ✅ **Build Hatası**: ViewModel'deki gereksiz kod satırı kaldırıldı
- ✅ **Puanlama Sistemi**: Score update yerine increment metodu kullanılıyor
- ✅ **CSV Parsing Sorunu**: Çoklu delimiter desteği (virgül, noktalı virgül, tab), esnek format handling
- ✅ **Türkçe Karakter Sorunu**: Multi-encoding desteği (UTF-8, Windows-1254), otomatik encoding detection
- CSV dosyası format hatalarında user-friendly mesajlar gösteriliyor

## 🔧 Son Düzeltmeler
- **CSV Import**: `readText()` kullanarak tüm dosya önce okunuyor, stream sorunları çözüldü
- **ViewModel**: `selectWinner` fonksiyonundaki gereksiz kod kaldırıldı
- **Database**: `updateScore` yerine `incrementScore` metoduna geçildi
- **Error Handling**: Comprehensive exception handling eklendi
- **Stream Management**: Manuel stream closing ve proper error handling
- **CSV Parsing İyileştirmesi**: Çoklu delimiter desteği (virgül, noktalı virgül, tab)
- **Flexible Format**: 2-3 sütun desteği, boş değerler için default değerler
- **Encoding Detection**: Otomatik UTF-8/Windows-1254 encoding detection
- **Turkish Character Support**: ı,ş,ğ,ü,ö,ç,İ,Ş,Ğ,Ü,Ö,Ç karakterleri tam desteği

## 🔄 Gelecek Geliştirmeler (İsteğe Bağlı)
- Sonuçları görüntüleme ekranı
- CSV export functionality
- Şarkı önizleme özelliği
- Kategori bazlı karşılaştırma
- Karşılaştırma geçmişi

---
**Not**: Bu dosya her terminal seansında okunmalı ve güncel tutulmalıdır.