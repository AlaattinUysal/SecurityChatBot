# 🛡️ SteganoChat: Güvenli Mesajlaşma Sistemi

[cite_start]**SteganoChat**, Java tabanlı, steganografi ve simetrik şifreleme tekniklerini harmanlayan çok katmanlı bir güvenlik sistemidir[cite: 144]. [cite_start]Bu proje, klasik kullanıcı adı ve parola doğrulamasının ötesine geçerek, gizli anahtarları (secret key) bir görsel içerisine **LSB (Least Significant Bit)** yöntemiyle gizleyen yenilikçi bir kimlik doğrulama mekanizması sunar[cite: 145].

## 🚀 Öne Çıkan Özellikler

* [cite_start]**Steganografik Kimlik Doğrulama:** Kullanıcı parolaları ağ üzerinde açık metin olarak dolaşmaz; bunun yerine PNG formatındaki taşıyıcı resimlerin piksellerine gizlenir[cite: 165, 167].
* [cite_start]**Çift Katmanlı Kriptografi:** Mesaj trafiği, Java Kriptografi Mimarisi kullanılarak **DES** algoritması (ECB Modu ve PKCS5Padding) ile şifrelenir[cite: 146, 193, 195].
* [cite_start]**Sunucu Tarafında Güvenli Yönlendirme:** Sunucu, her mesajı göndericinin anahtarıyla çözer ve alıcının benzersiz anahtarıyla tekrar şifreleyerek iletir[cite: 206, 209].
* [cite_start]**Çevrimdışı (Offline) Mesajlaşma:** Alıcı çevrimdışı olsa bile mesajlar sunucu kuyruğunda (RAM üzerinde) saklanır ve kullanıcı giriş yaptığı anda kendisine iletilir[cite: 183, 185, 187].
* [cite_start]**Çoklu İstemci Desteği:** Multi-threading yapısı sayesinde birden fazla kullanıcı aynı anda sunucuya bağlanarak birbirini bloke etmeden iletişim kurabilir[cite: 152, 154].

## 🛠️ Teknik Mimari ve Protokol

### Kullanılan Teknolojiler
* [cite_start]**Dil:** Java [cite: 144]
* [cite_start]**Ağ:** TCP Socket Programming (5555 Portu üzerinden) [cite: 153]
* [cite_start]**Şifreleme:** DES (Data Encryption Standard) [cite: 146]
* [cite_start]**Steganografi:** LSB (Least Significant Bit) [cite: 165, 168]
* [cite_start]**Arayüz:** Java Swing & AWT [cite: 161]

### Algoritma İşleyişi (LSB)
[cite_start]Görsel üzerindeki desen bozulmalarını önlemek amacıyla pikseller sırayla değil, `Collections.shuffle` kullanılarak karıştırılmış bir sırayla seçilir[cite: 170, 171]. [cite_start]Her bir pikselin RGB değerinin son biti (LSB), gizlenecek parolanın bitleri ile değiştirilir[cite: 168, 169].

## 📂 Dosya Yapısı

* [cite_start]`MainServer.java`: Bağlantıları yöneten ve kullanıcı listesini tutan ana sunucu dosyası[cite: 179].
* [cite_start]`ClientHandler.java`: Sunucu tarafında her istemci için bağımsız çalışan iş parçacığı[cite: 154].
* [cite_start]`SteganoManager.java`: Resim içine veri gizleme (Encoding) ve veri çözme (Decoding) işlemlerini yöneten sınıf[cite: 232].
* `CryptoHelper.java`: DES algoritması ile şifreleme ve deşifreleme fonksiyonlarını barındıran yardımcı sınıf.
* [cite_start]`RegisterForm.java`: Kullanıcının görsel seçimi ve kayıt işlemlerini yaptığı arayüz[cite: 161].
* [cite_start]`ChatScreen.java`: Mesajlaşma ekranı ve çevrimiçi kullanıcı listesinin gösterildiği arayüz[cite: 181].

## 📸 Sistem Kanıtları ve Loglar

Sistem, çalışma sırasında işlemlerin doğruluğunu kanıtlamak için log üretir:
1.  [cite_start]**Stegano Log:** `stego_debug.txt` dosyasında hangi pikselin (X,Y koordinatı) hangi bitinin değiştiği detaylıca tutulur[cite: 232, 233].
2.  [cite_start]**Kripto Log:** Sunucu konsolunda gelen şifreli veri, çözülen açık metin ve alıcı için yeniden şifrelenen veri anlık olarak izlenebilir[cite: 237].
   
