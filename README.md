<h1>DiscordWebhookAPI<img src="https://www.freepnglogos.com/uploads/discord-logo-png/discord-logo-logodownload-download-logotipos-1.png" height="64" width="64" align="left"></img>&nbsp;<img src=""></img></h1>
<br />

Discord Webhooks aracılığıyla kolayca mesaj göndermek için bir PocketMine-MP Eklentisi.

# Kullanım:
Kurulum kolaydır, [buradan](eklenicek) derlenmiş bir phar alabilir veya virionun kendisini eklentinize entegre edebilirsiniz.

Bu virion tamamen nesne yönelimlidir. Bu nedenle, onu kullanmak için 'Webhook' nesnesini, 'Message' nesnesini ve isteğe bağlı 'Embed' nesnesini (gerekirse) içe aktarmanız gerekir.

## Basit Kullanım:
### Sınıfları içe aktar
Kodumuzda kolayca kullanabilmek için bu sınıfları içe aktarmanız gerekecek.
```php
<?php

use Eren\DiscordWebhookAPI\Message;
use Eren\DiscordWebhookAPI\Webhook;
use Eren\DiscordWebhookAPI\Embed; // optional
```
### Bir Discord "Webhook" nesnesi oluşturun
Web kancasının URL'sine ihtiyacınız olacak. Discord Metin Kanalında Discord web kancalarının nasıl oluşturulacağı hakkında daha fazla bilgi için lütfen [burayı tıklayın](https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks).
```php
$webHook = new Webhook("WEBHOOK URL'NİZ");
```
### Bir Discord "Mesaj" nesnesi oluşturun
Göndermek istediğiniz her mesaj için yeni bir 'Mesaj' nesnesi oluşturmanız gerekecek... Ayrı web kancaları için farklı mesaj nesneleri kullanabilirsiniz ve bu nesne 'Web kancası' nesnesine bağlı **ÇALIŞMAZ**. Tek başınadır ve kendi kendine çalışır.
```php
$msg = new Message();
$msg->setUsername("KULLANICI ADI"); // optional
$msg->setAvatarURL("https://minotar.net/avatar/user"); // Elleme!
$msg->setContent("BURAYA METİN EKLEYİN"); // isteğe bağlı. Maksimum uzunluk 2000 karakterdir, sınır discord tarafından belirlenir, bu nedenle bu API içinde sabit kodlanmamıştır
```
### Mesajı gönderme
Mesajı şimdi web kancasına kolayca gönderebilirsiniz! :tada: Bu, Ana İş parçacığının engellenmesini önlemek için Sunucunun AsyncPool'unda yeni bir AsyncTask zamanlayacaktır. Ancak unutmayın, **boş mesaj GÖNDEREMEZSİNİZ.** bunu yapmak yalnızca Discord'un kendisinden alınan bir hata üretecektir.
```php
$webHook->send($msg);
```
Bu ne kadar kolaydı? ^-^ Şimdi çok daha gelişmiş ve havalı şeyler, Embedler!
### Embedler
İletiyi göndermeden önce bir yerleştirme eklemek isteyebilirsiniz. Bir mesajın içinde birkaç gömülü olabilir! Yalnızca bir embed oluşturmanız ve onu mesaj nesnesine eklemek için `Message->addEmbed()` yöntemini kullanmanız gerekir.
```php
$embed = new Embed();
```
Şimdi, yerleştirmenin düzgün çalışması için içinde bir şey olması gerekiyor, bu yüzden bir başlık (isteğe bağlı) ve bir açıklama (isteğe bağlı) ekleyeceğiz. **Tüm alanlar isteğe bağlıdır, ancak EN AZ bir alan içermeli, yoksa mesaja eklemeyi reddeder**
```php
$embed->setTitle("Başlığı buraya gömün");
$embed->setDescription("Çok harika bir açıklama");
```
Bir altbilgi metni bile ayarlayabiliriz! Yerleştirmelerin alt kısmındaki metin...
```php
$embed->setFooter("UwU);
```
Hatta altbilgiye bir simge ekleyin...
```php
$embed->setFooter("UwU","https://minotar.net/avatar/hyzama0");
```
Embed oluşturulduğuna ve geçerli bir içeriğe sahip olduğuna göre, onu `Message` nesnesine eklememiz gerekecek... Bunun için `Message->addEmbed()` yöntemini kullanmamız gerekecek.
```php
$msg->addEmbed($embed);
```
**API'nin Temel Kullanımı için bu kadar. Daha fazla bilgi edinmek için API'nin kaynak kodunu kendiniz okuyarak (kod basit ve açıklayıcıdır) veya favori IDE'nizi kullanarak kendiniz indeksleyerek keşfedebilirsiniz. :3**
# Bu API'yi daha önce test etmek için kullanılan Örnek Kod:
```php
// URL'si ile bir discord web kancası oluşturun
$webHook = new Webhook("WEBHOOK URL'NİZ");

// Yeni bir Mesaj nesnesi oluşturun
$msg = new Message();

$msg->setUsername("KULLANICI ADI");
$msg->setAvatarURL("https://minotar.net/avatar/hyzama0");
$msg->setContent("BURAYA METİN EKLEYİN");

// Yerleştirme rengi olarak #FF0000 (KIRMIZI) ve başlık olarak "EMBED 1" olan bir yerleştirme nesnesi oluşturun
$embed = new Embed();
$embed->setTitle("EMBED 1");
$embed->setColor(0xFF0000);
$msg->addEmbed($embed);

$embed = new Embed();
$embed->setTitle("EMBED 2");
$embed->setColor(0x00FF00);
$embed->setAuthor("YAPIMCI", "https://minotar.net/avatar/hyzama0", "https://minotar.net/avatar/hyzama0");
$embed->setDescription("UwU");
$msg->addEmbed($embed);

$embed = new Embed();
$embed->setTitle("BAŞLIK");
$embed->setColor(0x0000FF);
$embed->addField("FIELD ONE", "Burada biraz metin");
$embed->addField("FIELD TWO", "Burada biraz metin", true);
$embed->addField("FIELD THREE", "Burada biraz metin", true);
$embed->setThumbnail("https://minotar.net/avatar/hyzama0");
$embed->setImage("https://minotar.net/avatar/hyzama0");
$embed->setFooter("UwU","https://minotar.net/avatar/hyzama0");
$msg->addEmbed($embed);

$webHook->send($msg);
```
-----
**Bu API, :heart: Eren tarafından yapılmıştır, UwU!~ :3**
