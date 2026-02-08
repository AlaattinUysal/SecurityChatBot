# 🛡️ SteganoChat: Güvenli Mesajlaşma Sistemi

**SteganoChat**, Java tabanlı, steganografi ve simetrik şifreleme tekniklerini harmanlayan çok katmanlı bir güvenlik sistemidir. Bu proje, klasik kullanıcı adı ve parola doğrulamasının ötesine geçerek, gizli anahtarları (secret key) bir görsel içerisine **LSB (Least Significant Bit)** yöntemiyle gizleyen yenilikçi bir kimlik doğrulama mekanizması sunar.

## 🚀 Öne Çıkan Özellikler

* **Steganografik Kimlik Doğrulama:** Kullanıcı parolaları ağ üzerinde açık metin olarak dolaşmaz; bunun yerine PNG formatındaki taşıyıcı resimlerin piksellerine gizlenir  [cite: 165, 167].
* **Çift Katmanlı Kriptografi:** Mesaj trafiği, Java Kriptografi Mimarisi kullanılarak **DES** algoritması (ECB Modu ve PKCS5Padding) ile şifrelenir  [cite: 146, 193, 195].
* **Sunucu Tarafında Güvenli Yönlendirme:** Sunucu, her mesajı göndericinin anahtarıyla çözer ve alıcının benzersiz anahtarıyla tekrar şifreleyerek iletir  [cite: 206, 209].
* **Çevrimdışı (Offline) Mesajlaşma:** Alıcı çevrimdışı olsa bile mesajlar sunucu kuyruğunda (RAM üzerinde) saklanır ve kullanıcı giriş yaptığı anda kendisine iletilir  [cite: 183, 185, 187].
* **Çoklu İstemci Desteği:** Multi-threading yapısı sayesinde birden fazla kullanıcı aynı anda sunucuya bağlanarak birbirini bloke etmeden iletişim kurabilir  [cite: 152, 154].


## 🛠️ Teknik Mimari ve Protokol

### Kullanılan Teknolojiler
* **Dil:** Java [cite: 144]
* **Ağ:** TCP Socket Programming (5555 Portu üzerinden) [cite: 153]
* **Şifreleme:** DES (Data Encryption Standard) [cite: 146]
* **Steganografi:** LSB (Least Significant Bit) [cite: 165, 168]
* **Arayüz:** Java Swing & AWT [cite: 161]

### Algoritma İşleyişi (LSB)
Görsel üzerindeki desen bozulmalarını önlemek amacıyla pikseller sırayla değil, `Collections.shuffle` kullanılarak karıştırılmış bir sırayla seçilir[cite: 170, 171]. Her bir pikselin RGB değerinin son biti, gizlenecek parolanın bitleri ile bit düzeyinde (bitwise) değiştirilir  [cite: 168, 169].

## 📂 Dosya Yapısı

* `MainServer.java`: Bağlantıları yöneten ve kullanıcı listesini tutan ana sunucu dosyası.
* `ClientHandler.java`: Sunucu tarafında her istemci için bağımsız çalışan iş parçacığı.
* `SteganoManager.java`: Resim içine veri gizleme (Encoding) ve veri çözme (Decoding) işlemlerini yöneten sınıf.
* `CryptoHelper.java`: DES algoritması ile şifreleme ve deşifreleme fonksiyonlarını barındıran yardımcı sınıf.
* `RegisterForm.java`: Kullanıcının görsel seçimi ve kayıt işlemlerini yaptığı arayüz.
* `ChatScreen.java`: Mesajlaşma ekranı ve çevrimiçi kullanıcı listesinin gösterildiği arayüz.
