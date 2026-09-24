# Практична робота № 1

**Дисципліна:** Основи побудови інформаційних систем та мереж

**Тема:** Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| | |
|---|---|
| **Прізвище, ім'я** | Андреєв Іван |
| **Група** | ІПЗ-1.01 |
| **Номер варіанта** | 1 |
| **Домен варіанта** | perl.org |
| **Середовище виконання** | Windows |
| **Версія curl** | curl 8.13.0 (Windows) libcurl/8.13.0 Schannel zlib/1.3.1 WinIDN |
| **Дата виконання** | 22.09 (фінальна здача 24.09) |

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

**Команда:**

```
curl.exe -v https://perl.org
```

**Вивід:**

```
* Host perl.org:443 was resolved.
* IPv6: (none)
* IPv4: 151.101.65.55, 151.101.1.55, 151.101.193.55, 151.101.129.55
*   Trying 151.101.65.55:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Connected to perl.org (151.101.65.55) port 443
* using HTTP/1.x
> GET / HTTP/1.1
> Host: perl.org
> User-Agent: curl/8.13.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 301 Moved Permanently
< Connection: keep-alive
< Content-Length: 162
< Content-Type: text/html
< Location: https://www.perl.org/
< Server: nginx
< X-Cluster-Zone: dala
< Via: 1.1 varnish, 1.1 varnish
< Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
< Accept-Ranges: bytes
< Age: 2642
< Date: Mon, 21 Sep 2026 21:22:31 GMT
< X-Served-By: cache-dfw-kdfw8210144-DFW, cache-muc13969-MUC
< X-Cache: HIT, HIT
< X-Cache-Hits: 13, 0
< X-Timer: S1790025751.306929,VS0,VE183
< X-Backend: dala
< X-Backend-Front: ssl_shield_dallas_tx_us
< alt-svc: h3=":443";ma=86400,h3-29=":443";ma=86400,h3-27=":443";ma=86400
<
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
* Connection #0 to host perl.org left intact
```

---

### A.2. Запит без захисту з'єднання

**Команда:**

```
curl -v http://neverssl.com
```

**Вивід:**

```
* Host neverssl.com:80 was resolved.
* IPv6: (none)
* IPv4: 34.223.124.45
*   Trying 34.223.124.45:80...
* Connected to neverssl.com (34.223.124.45) port 80
* using HTTP/1.x
> GET / HTTP/1.1
> Host: neverssl.com
> User-Agent: curl/8.13.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Mon, 21 Sep 2026 21:38:36 GMT
< Server: Apache/2.4.68 ()
< Upgrade: h2,h2c
< Connection: Upgrade
< Last-Modified: Wed, 29 Jun 2022 00:23:33 GMT
< ETag: "f79-5e28b29d38e93"
< Accept-Ranges: bytes
< Content-Length: 3961
< Vary: Accept-Encoding
< Content-Type: text/html; charset=UTF-8
<
<html>
        <head>
                <title>NeverSSL - Connecting ... </title>
                <style>
                body {
                        font-family: Montserrat, helvetica, arial, sans-serif;
                        font-size: 16x;
                        color: #444444;
                        margin: 0;
                }
                h2 {
                        font-weight: 700;
                        font-size: 1.6em;
                        margin-top: 30px;
                }
                p {
                        line-height: 1.6em;
                }
                .container {
                        max-width: 650px;
                        margin: 20px auto 20px auto;
                        padding-left: 15px;
                        padding-right: 15px
                }
                .header {
                        background-color: #42C0FD;
                        color: #FFFFFF;
                        padding: 10px 0 10px 0;
                        font-size: 2.2em;
                }
                .notice {
                        background-color: red;
                        color: white;
                        padding: 10px 0 10px 0;
                        font-size: 1.25em;
                        animation: flash 4s infinite;
                }
                @keyframes flash {
                0% {
                        background-color: red;
                }
                50% {
                        background-color: #AA0000;
                }
                0% {
                        background-color: red;
                }
                }
                <!-- CSS from Mark Webster https://gist.github.com/markcwebster/9bdf30655cdd5279bad13993ac87c85d -->
                </style>

                <script>
                        var adjectives = [ 'cool' , 'calm' , 'relaxed', 'soothing', 'serene', 'slow',
                                                        'beautiful', 'wonderful', 'wonderous', 'fun', 'good',
                                                        'glowing', 'inner', 'grand', 'majestic', 'astounding',
                                                        'fine', 'splendid', 'transcendent', 'sublime', 'whole',
                                                        'unique', 'old', 'young', 'fresh', 'clear', 'shiny',
                                                        'shining', 'lush', 'quiet', 'bright', 'silver' ];

                        var nouns =       [ 'day', 'dawn', 'peace', 'smile', 'love', 'zen', 'laugh',
                                                        'yawn', 'poem', 'song', 'joke', 'verse', 'kiss', 'sunrise',
                                                        'sunset', 'eclipse', 'moon', 'rainbow', 'rain', 'plan',
                                                        'play', 'chart', 'birds', 'stars', 'pathway', 'secret',
                                                        'treasure', 'melody', 'magic', 'spell', 'light', 'morning'];

                        var prefix =
                                        // Choose 3 zen adjectives
                                        adjectives.sort(function(){return 0.5-Math.random()}).slice(-3).join('')
                                        +
                                        // Coupled with a zen noun
                                        nouns.sort(function(){return 0.5-Math.random()}).slice(-1).join('');
                        window.location.href = 'http://' + prefix + '.neverssl.com/online';
                </script>
        </head>
        <body>
        <noscript>
                <div class="notice">
                        <div class="container">
                                ⚠️ JavaScript appears to be disabled. NeverSSL's cache-busting works better if you enable JavaScript for <code>neverssl.com</code>.
                        </div>
                </div>
        </noscript>
        <div class="header">
                <div class="container">
                <h1>NeverSSL</h1>
                </div>
        </div>
        <div class="content">
        <div class="container">

        <h1 id="status"></h1>
        <script>document.querySelector("#status").textContent = "Connecting ...";</script>
        <noscript>

                <h2>What?</h2>
                <p>This website is for when you try to open Facebook, Google, Amazon, etc
                on a wifi network, and nothing happens. Type "http://neverssl.com"
                into your browser's url bar, and you'll be able to log on.</p>

                <h2>How?</h2>
                <p>neverssl.com will never use SSL (also known as TLS). No
                encryption, no strong authentication, no <a
                href="https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security">HSTS</a>,
                no HTTP/2.0, just plain old unencrypted HTTP and forever stuck in the dark
                ages of internet security.</p>

                <h2>Why?</h2>
                <p>Normally, that's a bad idea. You should always use SSL and secure
                encryption when possible. In fact, it's such a bad idea that most websites
                are now using https by default.</p>

                <p>And that's great, but it also means that if you're relying on
                poorly-behaved wifi networks, it can be hard to get online.  Secure
                browsers and websites using https make it impossible for those wifi
                networks to send you to a login or payment page. Basically, those networks
                can't tap into your connection just like attackers can't. Modern browsers
                are so good that they can remember when a website supports encryption and
                even if you type in the website name, they'll use https.</p>

                <p>And if the network never redirects you to this page, well as you can
                see, you're not missing much.</p>

        <a href="https://twitter.com/neverssl">Follow @neverssl</a>

        </noscript>

        </div>
        </div>

        </body>
</html>
* Connection #0 to host neverssl.com left intact
```

---

### A.3. Запит до служби доменних імен

*Windows: `Resolve-DnsName ВАШ_ДОМЕН`*

**Команда (перше виконання):**

```
Resolve-DnsName perl.org
```

**Вивід:**

```

Name                                     Type   TTL   Section    Str
                                                                 ing
                                                                 s
----                                     ----   ---   -------    ---
perl.org                                 HINFO  86400 Answer     {AA
                                                                 AA
                                                                 que
                                                                 rie
                                                                 s h
                                                                 ave
                                                                  be
                                                                 en
                                                                 loc
                                                                 all
                                                                 y b
                                                                 loc
                                                                 ked
                                                                  by
                                                                  dn
                                                                 scr
                                                                 ypt
                                                                 -pr
                                                                 oxy
                                                                 , S
                                                                 et
                                                                 blo
                                                                 ck_
                                                                 ipv
                                                                 6 t
                                                                 o f
                                                                 als
                                                                 e t
                                                                 o d
                                                                 isa
                                                                 ble
                                                                  th
                                                                 at
                                                                 fea
                                                                 tur
                                                                 e}

Name       : perl.org
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 151.101.193.55


Name       : perl.org
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 151.101.1.55


Name       : perl.org
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 151.101.129.55


Name       : perl.org
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 151.101.65.55


Name                   : org
QueryType              : SOA
TTL                    : 60
Section                : Authority
NameAdministrator      : h.invalid
SerialNumber           : 1
TimeToZoneRefresh      : 10000
TimeToZoneFailureRetry : 300
TimeToExpiration       : 604800
DefaultTTL             : 2400



```

**Команда (повторне виконання через 5–7 хвилин):**

```
Resolve-DnsName perl.org
```

**Вивід:**

```

Name                                     Type   TTL   Section    Strings
----                                     ----   ---   -------    -------
perl.org                                 HINFO  86400 Answer     {AAAA queries have been locally blocked b
                                                                 y dnscrypt-proxy, Set block_ipv6 to false
                                                                  to disable that feature}

Name       : perl.org
QueryType  : A
TTL        : 3417
Section    : Answer
IP4Address : 151.101.65.55


Name       : perl.org
QueryType  : A
TTL        : 3417
Section    : Answer
IP4Address : 151.101.129.55


Name       : perl.org
QueryType  : A
TTL        : 3417
Section    : Answer
IP4Address : 151.101.193.55


Name       : perl.org
QueryType  : A
TTL        : 3417
Section    : Answer
IP4Address : 151.101.1.55


Name                   : org
QueryType              : SOA
TTL                    : 60
Section                : Authority
NameAdministrator      : h.invalid
SerialNumber           : 1
TimeToZoneRefresh      : 10000
TimeToZoneFailureRetry : 300
TimeToExpiration       : 604800
DefaultTTL             : 2400


```

**Зафіксовані значення:**

| Параметр | Перше виконання | Повторне виконання |
|---|---|---|
| Час виконання (год:хв) | 14:26 | 14:29 |
| IP-адреса | 151.101.65.55 | 151.101.65.55 |
| Значення TTL | 3600 | 3417 |

> Якщо друге значення TTL виявилося більшим за перше — це нормально: кеш резолвера встиг оновитися. Зафіксуйте як є.

---

### A.4. Контрольний ресурс

**Команда:**

```
curl -v https://google.com
```

**Вивід:**

```
* Host google.com:443 was resolved.
* IPv6: (none)
* IPv4: 173.194.193.139, 173.194.193.100, 173.194.193.113, 173.194.193.101, 173.194.193.138, 173.194.193.102
*   Trying 173.194.193.139:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Connected to google.com (173.194.193.139) port 443
* using HTTP/1.x
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.13.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-ut5S1Fu9-gvqui6X9yBpag' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Mon, 21 Sep 2026 21:47:20 GMT
< Expires: Wed, 21 Oct 2026 21:47:20 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

**Випадок 1**

```
curl -v https://expired.badssl.com
```

```
* Host expired.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
* closing connection #0
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
```

**Випадок 2**

```
curl -v https://wrong.host.badssl.com
```

```
* Host wrong.host.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
* closing connection #0
curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

**Випадок 3**

```
curl -v https://self-signed.badssl.com
```

```
* Host self-signed.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
* closing connection #0
curl: (60) schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

> Якщо використано альтернативний спосіб із параметром `--resolve` — зазначити це та навести фактичну команду.

---

## Частина B. Власна модель рівнів

**Кількість виділених груп:** 4

| № | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
|---|---|---|---|
| 1 | Отримання вмісту сторінки | <html> ... </html> | Відображення вмісту для користувача є пріоритетним |
| 2 | Запит HTTP | > GET / HTTP/1.1, < HTTP/1.1 301 Moved | За цим запитом йде запит на HTML дані за допомогою GET. У нашому випадку це була переадресація на іншу адресу. |
| 3 | Перевірка сертифікату та безпека | * schannel: disabled..., * ALPN: curl offers..., * ALPN: server accepted... | Шифрування вже сформованого HTTP-запиту та перевірка сертифікату. |
| 4 | Встановлення з'єднання | * Host perl.org:443 was resolved, * Trying 151.101.65.55:443..., * Connected... | Перетворення домену на IP-адресу через DNS та підключення до порту 443 |


*Групи впорядковано від найближчої до користувача (№ 1) до найближчої до апаратного забезпечення. Зайві рядки вилучити, за потреби — додати.*

**Рядки, які не вдалося віднести до жодної групи:**

| Рядок виводу | Причина утруднення |
|---|---|
| * using HTTP/1.x | Повідомлення версії протоколу |
| * Request completely sent off | Повідомлення про повне відправлення запиту |
| * Connection #0 to host perl.org left intact | Повідомлення про стан з'єднання  |

---

## Контрольні питання

**1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання A.1)?**

> 35 рядків діагностичного виводу

**2. Які рядки наявні у виводі A.1 і відсутні у виводі A.2? Чим це зумовлено?**

> * schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1

Ці рядки відсутні у виводі А.2, оскільки у виводі А.2 використовується протокол HTTP. Через це у виводі немає перевірки сертифікату, шифрування та ALPN. 

**3. Звідки у виводі з'явилося значення `443`, якщо його не було вказано в адресі?**

> У безпечному з'єднанні за замовчуванням використовується порт 443 для HTTPS. Для протоколу HTTP застосовується порт 80.

**4. Як змінилося значення TTL між двома запитами (A.3)? Що означає це число?**

> TTL (Time To Live) - це час існування збереженої адреси в кеші. Змінилось значення бо з першого до другого запиту пройшло 183 секунди.

**5. Чим відрізняються між собою три причини помилок із завдання A.5? Сформулювати кожну однією фразою.**

| Випадок | Причина недовіри |
|---|---|
| `expired` | Прострочений сертифікат |
| `wrong.host` | Адреса не збігається з адресою прописаною в сертифікаті |
| `self-signed` | Сертифікат виданий недовіреним видавцем |

**6. Три рядки з власних виводів, про які не йшлося на лекції 1:**

| № | Рядок виводу | Джерело (номер завдання) |
|---|---|---|
| 1 | * ALPN: curl offers http/1.1 | Завдання A.1 |
| 2 | QueryType : SOA | Завдання A.3 |
| 3 | * schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect. | Завдання A.5 |

*Пояснення до цих рядків не потрібне.*

---

## Висновки

*150–300 слів. Спиратися на власні спостереження, а не на матеріал лекції.*

**D.1. Що виявилося неочевидним або несподіваним**

*Назвати конкретно, з посиланням на рядок виводу.*

> Хронологія рівнів була мені несподіваною. Я завжди думав, що спочатку йде з'єднання, перевірка сертифікату та захисту, запит до HTTP, а потім вже відображення та HTML. Також я не зрозумів, чому я підключився до neverssl.com лише з п'ятого разу, до цього я отримував помилку Timeout. "curl: (28) Failed to connect to neverssl.com port 80 after 21223 ms: Could not connect to server"

**D.2. Чому саме така кількість груп у частині B**

*На якій підставі ухвалено рішення. Що змусило б його змінити.*

> Під час аналізу виводу в завданні A.1 було очевидним, що там було 4 етапи. У виводі було видно, що кожен блок вирішував свою задачу, тому це було встановлення з'єднання, безпека та перевірка сертифікату, запит HTTP та отримання вмісту сторінки. Змусило б змінити лише, якби я аналізував neverssl.com, оскільки це незахищений сайт з протоколом HTTP, тому захист там відсутній. Я додав би 5 груп, якщо я розділив підключення на TCP-порт та DNS.

**D.3. Питання, яке залишилося без відповіді**

> Я не розумію чому не вийшло підключитися  до neverssl.com з першого разу. Хоча може бути, що це був лише захист, бо підключення було через протокол HTTP. Як вже писав в D.1, я не зрозумів логіку такої хронології, яка йде з боку користувача. 

---

## Використання штучного інтелекту

*Розділ обов'язковий. Заповнюється незалежно від того, чи використовувався ШІ. Детальні вимоги — у документі «Політика використання технологій штучного інтелекту».*

**Факт використання:** використано

**Установлений рівень для цієї роботи:** Р3 — ШІ як співвиконавець

**Фактичний рівень використання:** Р3 — ШІ як співвиконавець

### Використані системи

| Система | Версія або модель | Період використання |
|---|---|---|
| Google Studio | Gemini 3.8 Flash, Gemini 3.1 Pro Preview | 22.09 - 24.09 |

### Промпти

*Наводити дослівно, у тому вигляді, у якому запит було надано системі. Переказ не приймається.*

| № | Розділ роботи | Текст промпта |
|---|---|---|
| 1 | Початок роботи, парсинг, визначення варіанту | поясни детально як зробити практичку. що означає бланк і що мені з цим бланком робити. проаналізуй документацію github. поясни всі кроки які мені треба зробити чи треба самостійно форматувати md або просто завантажити той файл який був скинений. чи потрібно все скопіювати з того файлу або що взагалі мені треба писати в md. сам файл md наче сформований скажи в загалом скільки мені ця практична робота займе часу на виконання. роблю я це не вперше, бо в коледжі вже працював з цим треба взяти групу 3 та свій номер зі списку. я перший. у мене вінда |
| 2 | Завдання А.2. Помилка з'єднання з neverssl | curl.exe -v http://neverssl.com не працює. давай спробуємо через killercoda. поясни як там мені протестувати http://neverssl.com |
| 3 | Перевірка виводів з консолі | перевірь, чи правильно було виконано практичну роботу, чи всі виводи правильні. перевіряй лише мої виводи на правильність і чи всі запити дійшли. що мені залишилось доробити якщо я вже попрацював з консоллю |
| 4 | Складання рівнів та перевірка на правильність | груп 4 перше це з'єднання, перевірка сертифікації, третє це запит HTTP, чертверте це отримання вмісту сторінки чи правильно |
| 5 | Парсинг з презентації для виконання частини B | пропарси слайд презентації щоб зробити частину B, бо я не знаю звідки ти взяв це і я не розумію цю логіку |

### Дії з отриманим результатом

| № промпта | Що перевірено | Що змінено | Що відхилено і чому |
|---|---|---|---|
| 1 | Дізнався свій варіант, правильні команди під віндовс та порядок дій.  | Створив репозиторій і завантажив туди md файл | Нічого не відхиляв. |
| 2 | ШІ запропонував надіслати запит повторно. Також отримав пояснення як вводити команди через curl в Ubuntu через Killercoda  | Повторив запит поки він не пройшов. Вставив в практику | Відхилив використання Killercoda через успішне підключення до сайту. |
| 3 | Упевнився, що всі виводи правильні і те що не було такого нюансу, як з сайтом http://neverssl.com | Нічого не змінював, лише перевірив. | Нічого не відхиляв. |
| 4 | Перевірив чи правильно проаналізував завдання А.1. Не помітив що це треба було створити саме за хронологією рівнів від користувача до мережі. | Змінив порядок нумерації. | Не відхиляв змінення порядку через мою неуважність. |
| 5 | Передивився парсинг та пояснення від ШІ. Продивився парсинг слайдів 5, 6, 18 та 19 | Написав обгрунтування своїми словами на базі парсингу та пояснення від ШІ. | Відхилив готовий згенерований текст від ШІ. |

### Підтвердження

Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

> Виводи `curl`, `dig` та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.

---

## Примітки виконавця

*(необов'язковий розділ: що не спрацювало, які команди довелося змінити, які виникли труднощі)*

>
