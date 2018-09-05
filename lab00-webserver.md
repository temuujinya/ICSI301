# ЛАБ 00. Вэб хөгжүүлэлтийн орчин бэлдэх
Энэ лабораторын ажлаар хөгжүүлэлтийн вэб сервер програм суулгах, тохируулах, хөгжүүлэлтийн орчныг бэлдэх, FTP (File Transfer Protocol) ашиглан вэб сайтын файлыг алсаас хөгжүүлэх зэрэг чадварыг эзэмших зорилготой.

Вэб програмыг хөгжүүлж ажиллуулахад бүтээгдэхүүн ажиллуулах вэб сервер (producton web server) болон хөгжүүлэлтийн вэб сервер хэрэгтэй болдог. Учир нь хөгжүүлэлтийн вэб серверийг хөгжүүлэгч өөрийн компьютертээ суулгаж түүн дээр бичиж буй кодыг турших нь хялбар, бас хугацаа хэмнэдэг. Бас нэг давуу тал бол вэб програмын кодыг бичих, турших (test) явцад вэб серверийн аюулгүй байдал, бусад алдааны тухай санаа тавих шаардлагагүй байдаг. 

## Дасгал 1. Apache HTTP server, PHP суулгаж ажиллуулах
Динамик вэб сайт, вэб програмыг ажиллуулахад HTTP сервер (жишээ нь, Apache HTTP Server), сервер талын вэб програмчлалын хэл (жишээ нь, PHP), өгөгдлийн сангийн менежмент систем (жишээ нь, MySQL) зэрэг програм хангамжийг ашиглана. Жишээгээр дурдсан програмуудыг багцалсан WAMP (Windows Apache MySQL and PHP), XAMPP, MAMP зэрэг суулгац програмаар нэг дор суулгаж тохируулах боломж бий. Эсвэл [https://httpd.apache.org/](https://httpd.apache.org/), [http://php.net/](http://php.net/), [https://www.mysql.com/](https://www.mysql.com/) зэрэг вэб сайтуудаас тус тусад нь татаж аваад суулгаж болно. [1] номын Бүлэг 2-оос вэб сервер суулгах талаар уншаарай.

Apache HTTP Server болон MySQL програм хангамжууд нь үйлдлийн системд тогтмол ажиллах сервис төрлийн програм учир дээрх програмыг суулгасны дараа сервисүүдийг асаах (start) шаардлагатай байдаг. Хэрэв вэб сервер ассан бол вэб хөтчөөсөө [http://localhost/](http://localhost/) хаягаар хандан вэб сервер зөв ажиллаж байгаа эсэхийг шалгаж болно. 

> localhost нь тухайн серверийг өөрийг нь зааж байгаа хост нэр юм. Эсвэл энэ нэрэнд харгалзах 127.0.0.1 IP хаягийг оронд нь ашиглаж болно.

Дээрх багц програмуудаар вэб сервер суулгах явцад хэд хэдэн тохиргоог үүсгэж өгдөг. Тухайлбал, аюулгүй байдлын холбогдолтой тохиргоо нь бүтээгдэхүүний вэб сервертэй адилгүй байдаг ба интернэт орчинд вэб програмаа жинхэнээсээ ажиллуулах бол бүтээгдэхүүний вэб сервер бэлдэх зааврын дагуу суулгах нь зүйтэй. Apache вэб серверийн тохиргоог httpd.conf нэртэй текст файлд хадгалдаг. Жишээ нь, WAMP програмын хувьд `c:/wamp/bin/apache[version]/config/httpd.conf` файл бий. Linux үйлдлийн систем, Ubuntu системийн хувьд `/etc/apache2/apache2.conf` нэртэй байдаг.

**Порт** Хэрэв сервер компьютер дээр өөр вэб сервер програм суусан, 80 дугаар портыг ашиглаж байгаа бол эсвэл гарааны 80 портыг өөрчлөх бол Apache HTTP Server програмын ажиллах портыг зөрүүлж тохируулах/эсвэл тэр сервер програмын портыг өөрчлөх шаардлагатай. Учир нь TCP/IP холболтын үед нэг програм нэг портыг ашиглан холболт үүсгэх боломжтой байдаг. Apache HTTP серверийн ашиглах портыг тохиргооны файлд өөрчилж болно. Тохиргооны файлд `Listen 80` мөрийг `Listen 8080` болгон өөрчлөөд сервисээ дахин асаана. Энэ тохиолдолд вэб хөтчөөс http://localhost:8080/ хаягаар Apache HTTP серверт хандана.

**Вэб нөөцийг заах үндсэн директор** WAMP суулгацаар суусан вэб програмын гарааны тохиргоогоор `DocumentRoot "c:/wamp/www/"` эсвэл `DocumentRoot "c:/wamp64/www/"` гэж вэб серверийн нөөцийг (resource) хадгалах үндсэн директорыг/замыг (webroot directory) заасан байдаг. Ubuntu системийн хувьд `/var/www/` эсвэл `/var/www/html/` гэх зам бий. Энэ замыг, мөн дараах кодод үзүүлсэн замыг өөрчилж вэб нөөцийг заах үндсэн директорыг өөрчилж болно. 

***Код 1. Вэб нөөцийг заах үндсэн директорын тохиргоо***
```
<Directory "c:/wamp/www/">
       Options Indexes FollowSymLinks
       AllowOverride None
       Require all granted
</Directory>
```

### Гүйцэтгэх ажил:
1. Apache HTTP сервер суулгаж ажиллуулах
2. Портыг 8080 болгон өөрчилж тохируулах
3. Вэб үндсэн директорыг өөрчлөх

## Дасгал 2. Динамик вэб агуулга ба HTTP
Код 1-д харуулсан PHP кодыг index.php нэртэй текст файлаар хадгалж вэб нөөцийг заах үндсэн директорт хуулна. Вэб хөтчөөс `http://localhost` эсвэл `http://localhost/index.php` хаягаар дуудаж ажиллуулна. 

***Код 2. Энгийн PHP вэб хуудас***
```html
<!DOCTYPE html>
<!-- index.php -->
<html>
  <head>
   <meta charset="UTF-8">
  </head>
  <body>
    <!-- Статик болон динамик агуулгын ялгаа -->
    <p>Энэ бол статик агуулга.</p>
    
    <?php echo "PHP скриптээр, програмын кодоор үүсгэсэн динамик агуулга."; ?>
    <p>Вэб серверийн цаг: 
       <span><?php 
              // Системийн цагийг HTTP гаралтад бичих
              echo "Өнөөдөр бол " . date("Y/m/d");
             ?></span>
    <p>
  </body>
</html>
```

Хэрэв порт өөрчлөгдсөн бол `http://localhost:8080/index.php` гэж HTTP серверт хүсэлт илгээнэ. Вэб сервер index.html, index.php гэх мэт нэртэй файлыг нүүр хуудас (эсвэл нөөцийг заагаагүй үед харуулах нөөц) гэж үздэг бөгөөд вэб клиентээс `http://localhost:8080/` гэж хүсэхэд автоматаар эдгээр хуудсуудын аль нэгийг заасан эрэмбийн дагуу буцааж хариулдаг. 

### Гүйцэтгэх ажил:
1. Вэб хөтчийн Developer Tools->Network хэрэгслээр дээрх хуудсыг үзэхээр вэб хөтчөөс тавьсан хүсэлт (request), вэб серверээс хариулсан хариултын (response) ажиглаж HTTP протоколын толгой утгуудтай (header) танилцаж тус бүрийн хувьд тайлбар бичнэ.
> *Хүсэлт тавихаасаа өмнө Developer Tools->Network хэрэгслийг нээсэн байх шаардлагатай.*
2. Вэб хариултын HTTP body хэсгийг ажиглан статик болон динамик агуулгын ялгааг тайлбарлаж бичнэ үү. Шаардлагатай бол програм кодыг өөрчилж үзээрэй.

## Дасгал 3. URL-ийг файл системийн тодорхой байршилд харгацуулах
Вэб серверт ирсэн хүсэлтийн URL-ээр файл системийн тодорхой байршилд байгаа нөөцөд хандах боломжтой. Энэ боломжийг виртуал директор (virtual directory) хангаж өгдөг. Үүнийг ашиглан нэг вэб серверийн нэг домэйн болон порт дээр олон вэб сайтыг өөр өөр зам дээр (домэйн нэрийн араас /path г.м) ажиллуулж болно. Эсвэл вэб сайтын зарим нөөцийг файл системийн өөр өөр зам дээр хадгалах боломжтой болно.

**Виртуал директор** нь URL дээрх хуурмаг зам бөгөөд тухайн зам вэб сервер дээрх өөр замыг (үндсэн хавтсаас өөр) заадаг. Жишээ нь, Линукс файл системийн `/var/myweb` директорыг виртуал директороор `docs` гэж зааж өгсөн бол http://localhost/docs гэж хандахад `/var/myweb` директорт байгаа вэб нөөцийг заана гэсэн үг. Үүний тулд Код 3-т үзүүлсэн шиг `Alias` [директивийг](https://httpd.apache.org/docs/2.4/urlmapping.html) httpd.conf файлд ашиглана. `http://www.example.com/docs/dir/file.html` гэж хандвал `/var/myweb/dir/file.html` файлыг вэб сервер буцаах юм.

***Код 3. Виртуал директорын Alias директив***
```
Alias "/docs" "/var/myweb"
```
**URL дахин чиглүүлэлт** Клиентийн хүссэн нөөц өөр URL хаяг дээр байгааг клиентэд мэдэгдэж клиент тэр URL хаягаар дахин шинэ хүсэлт тавьж нөөцөд хандах техникийг URL дахин чиглүүлэлт (redirection) гэдэг. Жишээ нь, вэб нөөцийг зааж байсан директор өөрчлөгдсөн тохиолдолд энэ техникийг ашиглаж болно. Тухайлбал, вэб нөөцийг заах үндсэн директор доторх /images директорын нөөцүүд /photos хавтасруу зөөгдсөн бол `Redirect` директивийг ашиглан Код 4-т үзүүлсэн шиг тохиргоо хийж болно.

***Код 4. URL дахин чиглүүлэлтийн тохиргоо***
```
Redirect permanent "/foo/"   "http://www.example.com/bar/"
```

**Виртуал хост** нь нэг вэб сервер дээр (эсвэл олон хамтдаа хоршиж ажиллах вэб серверүүдийн дунд) олон домэйн нэрээр хост хийх (олон вэб ажиллуулах) боломжийг олгоно. Энэ нь нэг сервер олон вэб сайт хооронд серверийн нөөцийг (санах ой, процессор г.м) хувааж ашиглуулах боломж олгодог. Жишээ нь, үүнийг ашиглан дундын веб хостинг (shared web hosting) үйлчилгээг эрхэлж болно. Хөгжүүлэлтийн орчинд өөрийн компьютерийн вэб хөтчөөс хуурмаг домэйн нэрээр хандахад хөгжүүлэлтийн сервер дээр ажиллаж байгаа өөр өөр вэб сайт/програмуудыг заах боломжийг олгодог. Энэ нь олон вэб сайт/програм хөгжүүлж байгаа тохиолдолд өөр өөр нэрээр хооронд ялгахад хэрэг болно. Apache вэб серверийн хувьд энэ [зааврын](https://httpd.apache.org/docs/2.4/vhosts/examples.html) дагуу виртуал хост үүсгэж болно. Жишээ нь, Код 5-д `sisi.milab.edu` домэйн нэрээр `/www/sisi` вэб нөөцөд/сайтад, `pds.milab.edu` домэйн нэрээр `www/pds` вэб нөөцөд хандах тохиргоог хийж болно.

***Код 5. Нэрэнд түшиглэсэн виртуал хостын тохиргоо***
```
Listen 80
<VirtualHost *:80>
    DocumentRoot "/www/sisi"
    ServerName sisi.milab.edu
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/www/pds"
    ServerName pds.milab.edu
</VirtualHost>
```
> Санамж: Дээрх тохиргоо нь зөвхөн Apache вэб серверийн тохиргоо учир үйлдлийн системийн hosts файлд дээрх домэйн нэр түүнд харгалзах IP хаягийг зааж өгөх шаардлагатай. Линукс системийн хувьд `/etc/hosts`, Виндоус системийн хувьд `C:\Windows\System32\drivers\etc` доторх hosts файлыг текст засварлагч програмаар хуурмаг домэйн нэрийг харгалзах IP хаягт (хөгжүүлэлтийн орчинд 127.0.0.1) гэж заах өгнө. Энэ файлыг administrative эрхтэй хэрэглэгчээр өөрчлөх боломжтой.

### Гүйцэтгэх ажил:
1. Өмнө хадгалсан index.php хуудсыг файл системийн өөр газар байршуулж виртуал директор үүсгэн ажиллуулна.
2. URL дахин чиглүүлэх тохиргоог өөрийн вэб сайтад хийнэ.
3. Хоёр вэб сайт үүсгэж виртуал хостоор хандах тохиргоо хийнэ.

## Дасгал 4. Алсаас ажиллах

Бүтээгдэхүүний вэб сервер дээр Apache, MySQL зэрэг програм хангамжийг суулгах, тохиргоог өөрчлөх зэрэг системийн түвшинд алсаас ажиллах бол Telnet болон SSH протоколоор терминалаас хандаж ажиллана. SSH нь Telnet-ийг бодвол илүү аюулгүй, хамгаалалт сайтай бөгөөд Linux, Mac системд суусан байдаг бол Виндоус системд [PuTTY](https://www.putty.org/) програмыг өргөн хэрэглэдэг. Ихэнх вэб хостинг үйлчилгээ алсаас хандах хялбар шийдлүүдийг санал болгодог тул тэдний өгсөн зааврын дагуу ажиллахад хангалттай.

Вэб сайтыг бүхлээр хуулах, алс зайнаас вэб сайтын үндсэн директорын нөөцийг удирдахад FTP протоколыг өргөн ашигладаг. Эхлээд FTP сервер програм суулгаж хэрэглэгчийн эрх, алсаас хандах директор, түүний тохиргоог зааж өгнө. Дараа нь FTP клиент програмаас хост (домэйн эсвэл IP хаяг), порт (гарааны порт нь 22), хэрэглэгчийн нэр, нууц үг зэргээр FTP серверт хандан файл хуулах, устгах, файлд хандах эрхийг (зөвхөн унших, бичих г.м) удирдаж болно. 

### Гүйцэтгэх ажил:
1. FTP сервер ([FileZilla Server](https://filezilla-project.org/)) програмыг вэб сервер компьютертээ суулгаж вэб нөөцийг заах үндсэн директорыг FTP протоколоор хандах боломжтой болгоно.
2. FTP клиент програм ([FileZilla Client](https://filezilla-project.org/), [FireFTP](http://fireftp.net/))

## Дасгал 5. Кодыг хувилбаржуулах нь
Вэб төслийг ихэнх тохиолдолд багаар гүйцэтгэдэг. Багаар хамтарч нэг вэб програм хөгжүүлэхийн тулд дундаа хөгжүүлэлтийн сервер (development server) ашигладаг. Хөгжүүлэлтийн сервер нь төслийн багийн хөгжүүлж буй кодуудыг нэг дор хадгалах, сервер орчинд нь ажиллуулж туршихад хэрэглэнэ. Иймд хөгжүүлэлтийн сервер дээрх бичсэн кодоо хуулахад кодыг хувилбаржуулах систем (code versioning system) ашигладаг бөгөөд өргөн ашигладаг програмууд бол SVN, Git зэрэг юм. Ер нь вэб програм хөгжүүлэхэд ганцаар ажиллаж байсан ч ийм програмыг хэрэглэж дадах хэрэгтэй. Хэрэв та Виндоус үйлдлийн системтэй бол TortoiseSVN програмыг, Линакс үйлдлийн системтэй бол GitLab програмыг суулгаж энэ хичээлийн лабораторын хичээлээр хөгжүүлэх вэб програмын кодыг хувилбаржуулаарай.

## Ном зүй
[1] Robin Nixon, Learning PHP, MySQL, JavaScript, CSS & HTML5, 3rd Edition, 2014, 729 pages, ISBN: 978-1-491-94946-7 [2] Kevin Tatroe, Peter MacIntyre, Rasmus Lerdorf, Programming PHP, 3rd Edition, 2013, 540 pages, ISBN: 978-1-4493-9277-2