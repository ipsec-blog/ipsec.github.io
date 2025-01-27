---
layout: post
title:  "Bountyhunter"
date:   2021-04-07 14:32:04 +0700
categories: [OSCP, HTB]
---

## Enumeration

### Nmap

Nmap ile varsayılan port taraması yapılabilir. Ancak makine çözerken kolayımıza gelse de gerçek sistemlerde tüm portlanrın taranması tavsiye edilir.

### dirsearch

Dizin taraması yaptığımızda aşağıda ki dizinler dikkatimizi çekiyor. Tarama yaparken dosya formatlarının taranması seçeneğini eklemeyi unutmayın!

`/resources`

`/db.php`

### Web Enumeration

Makinede 80 portu açık olduğu için genel manada owasp top 10 açıklarından yada web araçlarından hangisini kullanacağımızı araştırmalısınız!

**XXE** açığının varlığı burp kullanılarak denenebilir.

Dirsearch taraması ile elde edilen dizin bilgilerinin üzerinde durularak `File Transfer` methodlarına bakılabilir.

Yine transfer edilen dosya hash çeşitlerinden biri ile `encryption` edildiğinden cryiptograpy seçeneklerine bakılmalı.

Sistem üzerinde ki kullanıcıların tespiti açısından hassas dosyalar taranarak bulunabilir.

Elde edilen parola ile **ssh** bağlantısı denenebilir.

## Privilege Escalation

### SSH

Ssh bağlantısı ile sisteme bağlandıktan sonra user.txt dosyamızı okuyabiliriz.

Biraz dizin taraması yaptıktan sonra sistemde tek kullanıcı olduğunu göreceksiniz. 

Yetki yükseltmek için `sudo -l` komutunun çıktısını kontrol edebiliriz.

Çıktıyı araştırdığımızda `python` dosyasının **root** parolası istemeden çalıştırılabileceğini görüyoruz.

Ancak çıktıda ki dizini kontrol edip python dosyası çalıştırılmadan önce kodlar okunarak yetki yükseltmeye sebep olacak şekilde `ticket` dosyası oluşturulabilir. 

Dizinde ki `Invalid_Tickets` klasöründen faydalanılabilir.


Verilen ip uçlarını takip ederek doğru yöntemleri uyguladıysanız `root.txt` dosyasını okuyabilirsiniz.







