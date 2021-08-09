---
attachments: [Clipboard_2021-08-08-21-39-10.png]
tags: [HTB]
title: Bountyhunter
created: '2021-08-08T18:37:10.527Z'
modified: '2021-08-09T09:32:18.426Z'
---

## Enumeration

### Nmap
```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d4:4c:f5:79:9a:79:a3:b0:f1:66:25:52:c9:53:1f:e1 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDLosZOXFZWvSPhPmfUE7v+PjfXGErY0KCPmAWrTUkyyFWRFO3gwHQMQqQUIcuZHmH20xMb+mNC6xnX2TRmsyaufPXLmib9Wn0BtEYbVDlu2mOdxWfr+LIO8yvB+kg2Uqg+QHJf7SfTvdO606eBjF0uhTQ95wnJddm7WWVJlJMng7+/1NuLAAzfc0ei14XtyS1u6gDvCzXPR5xus8vfJNSp4n4B5m4GUPqI7odyXG2jK89STkoI5MhDOtzbrQydR0ZUg2PRd5TplgpmapDzMBYCIxH6BwYXFgSU3u3dSxPJnIrbizFVNIbc9ezkF39K+xJPbc9CTom8N59eiNubf63iDOck9yMH+YGk8HQof8ovp9FAT7ao5dfeb8gH9q9mRnuMOOQ9SxYwIxdtgg6mIYh4PRqHaSD5FuTZmsFzPfdnvmurDWDqdjPZ6/CsWAkrzENv45b0F04DFiKYNLwk8xaXLum66w61jz4Lwpko58Hh+m0i4bs25wTH1VDMkguJ1js=
|   256 a2:1e:67:61:8d:2f:7a:37:a7:ba:3b:51:08:e8:89:a6 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBKlGEKJHQ/zTuLAvcemSaOeKfnvOC4s1Qou1E0o9Z0gWONGE1cVvgk1VxryZn7A0L1htGGQqmFe50002LfPQfmY=
|   256 a5:75:16:d9:69:58:50:4a:14:11:7a:42:c1:b6:23:44 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJeoMhM6lgQjk6hBf+Lw/sWR4b1h8AEiDv+HAbTNk4J3
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.41 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 556F31ACD686989B1AFCF382C05846AA
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Bounty Hunters
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
### dirsearch

Dizin taraması yaptığımızda aşağıda ki dizinler dikkatimizi çekiyor.

`/resources`

`/db.php`

### Web Enumeration

Makinede 80 portu açık olduğu için genel manada owasp top 10 açıklarından yada web araçlarından hangisini kullanacağımızı araştırmamız gerekiyor.

**XXE** açığının varlığı burp kullanılarak denenebilir.

Dirsearch taraması ile elde edilen dizin bilgilerinin üzerinde durularak `File Transfer` methodlarına bakılabilir.

Yine transfer edilen dosya hash çeşitlerinden biri ile `encryption` edildiğinden cryiptograpy seçeneklerine bakılmalı.

Elde edilen şifre ile **ssh** bağlantısı denenebilir.

## Privilege Escalation

### SSH

Ssh bağlantısı ile sisteme bağlandıktan sonra user.txt dosyamızı okuyabiliriz.

Biraz dizin taraması yaptıktan sonra sistemde tek kullanıcı olduğunu göreceksiniz. 

Yetki yükseltmek için `sudo -l` komutunun çıktısını kontrol edebiliriz.

Çıktıyı araştırdığımızda `python` dosyasının **root** parolası istemeden çalıştırılabileceğini görüyoruz.

Ancak çıktıda ki dizini kontrol edip python dosyası çalıştırılmadan önce kodlar okunarak yetki yükseltmeye sebep olacak şekilde konfigüre edilmeli.


Verilen ip uçlarını takip ederek doğru yöntemleri uyguladıysanız `root.txt` dosyasını okuyabilirsiniz.






