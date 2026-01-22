# YYGW
## WAS
### HERE

# Network Layer – Sınav Odaklı Özet

## Network Layer’ın Görevi
- Transport layer’dan gelen segmentleri **IP datagram** içine kapsüller
- Göndericide encapsulation, alıcıda decapsulation yapar
- **Tüm router’lar geçen her IP datagramının header’ını inceler**

---

## Forwarding vs Routing (ÇOK SORULUR)
- **Forwarding**:  
  - Yerel karar
  - Paketi **hangi çıkış portuna** göndereceğini belirler
- **Routing**:  
  - Global karar
  - Kaynaktan hedefe **hangi yolun izleneceğini** belirler
⚠️ Tuzak: Routing algoritması ≠ forwarding table

---

## Datagram Network vs Virtual Circuit (VC)
### Datagram Network (Internet)
- Connectionless
- Router’lar **state tutmaz**
- Paketler **destination IP address** ile yönlendirilir
- Esnek, “best effort”

### Virtual Circuit (ATM, Frame Relay)
- Connection-oriented (setup & teardown var)
- Router’lar **connection state tutar**
- Paketler **VC number** taşır
- Kaynaklar önceden ayrılabilir (predictable service)

⚠️ Tuzak: Günümüz Internet’i **VC kullanmaz**

---

## IP Datagram Header – Kritik Alanlar
- **TTL**: Her router’da 1 azalır → 0 olursa paket atılır
- **Header Length**: Opsiyonlar yüzünden değişken olabilir
- **Total Length**: Fragmentation için gereklidir
- **Protocol**: Üst katmanı belirtir (TCP=6, UDP=17)
- **Checksum**:
  - Sadece **IP header** için
  - Her router’da **yeniden hesaplanır**

---

## IP Fragmentation
- MTU küçükse datagram parçalanır
- **Fragmentation router’da**, **reassembly sadece hedefte**
- Alanlar:
  - **Identification**: Aynı datagrama ait parçaları tanır
  - **Fragment Offset**: 8 byte cinsinden
  - **MF (More Fragments)**: Son parça hariç 1

⚠️ Tuzak: Fragmentation **IPv6’da yok**

---

## IP Addressing – Temel Kavramlar
- IP adresi **interface’e** aittir, host’a değil
- Subnet = Aynı subnet kısmını paylaşan interface’ler
- Aynı subnet → **direct communication**
- Farklı subnet → **default gateway (router)** gerekir

---

## Netmask & AND İşlemi (EZBER DEĞİL, MANTIK)
- Host kendi network’ünü bulur:

- Destination aynı sonucu veriyorsa:
- Aynı subnet → direkt gönder
- Farklıysa:
- Router’a gönder

---

## CIDR & Longest Prefix Matching
- CIDR: `/x` → network bit sayısı
- Router:
- Destination IP ile **tüm routing table entry’lerini AND eder**
- **En uzun eşleşen prefix** kazanır

⚠️ Tuzak: Daha spesifik route her zaman önceliklidir

---

## ARP (Address Resolution Protocol)
- Amaç: **IP → MAC** çözümlemesi
- ARP Request:
- **Broadcast** (FF:FF:FF:FF:FF:FF)
- ARP Reply:
- **Unicast**
- ARP mesajları **IP değildir**, link layer payload’udur
- ARP table entry’leri **TTL ile silinir**

---

## DHCP (ÇOK ÇIKAR)
### Amaç
- IP adresi + netmask + default gateway + DNS verir

### Mesaj Akışı
1. DHCP Discover → broadcast (255.255.255.255)
2. DHCP Offer
3. DHCP Request
4. DHCP ACK

⚠️ Tuzak:
- Client IP almadan önce source IP = **0.0.0.0**
- DHCP **UDP kullanır** (67/68)

---

## NAT (Network Address Translation)
- Private IP’ler Internet’te routable değildir
- NAT:
- **Source IP + source port** değiştirir
- Destination IP **değişmez**
- NAT table:  
`(internal IP, port) ↔ (public IP, port)`

Avantaj:
- IP tasarrufu
- Güvenlik artışı

Dezavantaj:
- End-to-end ilkesini bozar

---

## ICMP
- Hata ve kontrol mesajları
- Örnekler:
- Echo request/reply (ping)
- Destination unreachable
- TTL expired (traceroute)

### Traceroute Mantığı
- TTL = 1,2,3,...
- Her router TTL=0 olunca **ICMP Time Exceeded** gönderir
- Hedefte **ICMP Port Unreachable** ile biter

---

## IPv6 – Sınavda Fark Sorulur
- 128-bit address
- Fixed **40 byte header**
- **Checksum yok**
- **Fragmentation yok** (router’da)
- Transition: **Tunneling (IPv6 inside IPv4)**


## SLIDE 2

# DNS (Domain Name System) – Sınav Odaklı Özet

## DNS Nedir?

* İnsanların kullandığı **domain isimlerini** IP adreslerine çevirir
* **Dağıtık (distributed)** ve **hiyerarşik (hierarchical)** bir sistemdir
* **Application Layer** protokolüdür

⚠️ Tuzak: DNS **network layer değildir**

---

## Neden Merkezi DNS Kullanılmaz?

* Single point of failure olur
* Trafik aşırı artar
* Uzak sunucu → yüksek gecikme
* Bakımı zordur

➡️ **Ölçeklenmez (does not scale)**

---

## DNS’in Sağladığı Servisler

* Hostname → IP çevirisi
* **Host aliasing**

  * Alias ↔ canonical name
* **Mail server aliasing**
* **Load balancing**

  * Aynı domain → birden fazla IP

---

## DNS Hiyerarşisi (ÇOK ÇIKAR)

1. **Root DNS Server**
2. **TLD DNS Server** (.com, .org, .edu, .tr, …)
3. **Authoritative DNS Server**
4. **Local DNS Server**

⚠️ Tuzak:

* Local DNS **hiyerarşinin resmi parçası değildir**
* ISP / üniversite tarafından sağlanır

---

## Root DNS Server

* Dünyada **13 mantıksal root server** vardır
* Local DNS çözemediğinde root’a sorar
* Root:

  * “Bilmiyorum ama şuraya sor” cevabı verir

⚠️ Tuzak: Root server **IP adresi vermez**

---

## TLD ve Authoritative DNS

### TLD DNS Server

* .com, .edu, .org, ülke domain’leri
* Hangi authoritative DNS’in sorumlu olduğunu söyler

### Authoritative DNS Server

* Domain için **kesin (authoritative)** cevabı verir
* IP eşlemesi burada bulunur

---

## DNS Name Resolution

### Iterative Query (EN ÇOK SORULAN)

* Local DNS sırayla server’lara sorar
* Her server:

  * “Bilmiyorum ama şuraya sor” der
* **Yük dağıtılır**

### Recursive Query

* Sorgulanan server tüm işi yapar
* Üst seviye server’lara **yük bindirir**

⚠️ Tuzak: Internet’te **çoğunlukla iterative query** kullanılır

---

## DNS Caching

* Öğrenilen eşleşmeler **cache edilir**
* Cache kayıtları **TTL** ile silinir
* TTL bitene kadar:

  * IP değişse bile eski IP dönebilir

⚠️ Tuzak: DNS **best-effort** çalışır

---

## DNS Resource Records (RR) (EZBER SORU)

**Format:**
(name, value, type, TTL)

### Önemli Türler

* **A**

  * name = hostname
  * value = IP address
* **NS**

  * domain → authoritative DNS server
* **CNAME**

  * alias → canonical name
* **MX**

  * domain → mail server

⚠️ Tuzak:

* CNAME **IP vermez**
* Alias → başka bir isim gösterir

---

## DNS Protokolü

* Query ve reply **aynı mesaj formatını** kullanır
* Genelde **UDP** kullanılır
* TCP:

  * Zone transfer için

⚠️ Tuzak: DNS **her zaman TCP kullanmaz**

---

## DNS’e Kayıt Ekleme (Mantık Sorusu)

1. Domain registrar’a kayıt olunur
2. Authoritative DNS bilgileri verilir
3. TLD server’a **NS ve A record** eklenir
4. Authoritative server’da:

   * A record (www)
   * MX record (mail)

---

## DNS Güvenlik Problemleri

### DDoS

* Root server’a saldırı (bugüne kadar başarısız)
* TLD server saldırısı daha tehlikelidir

### Redirect / Poisoning

* Sahte DNS reply gönderilir
* DNS cache zehirlenir

### DNS Amplification

* Sahte kaynak IP ile küçük sorgu
* Büyük reply hedefe gönderilir

---

## Sınavda Çok Gelen Tuzaklar

* DNS **distributed + hierarchical**
* DNS **application layer**
* Iterative ≠ Recursive
* CNAME ≠ A
* Root server **IP vermez**
* Cache + TTL → eski IP dönebilir

## SLIDE 3

# Network Analysis Tools – Sınav Odaklı Özet

## Genel Notlar

* Araçlar hem **UNIX hem Windows** sistemlerde bulunabilir
* Ancak:

  * Opsiyonlar aynı olmayabilir
  * Çıktılar birebir aynı olmayabilir
* Sınavda **sadece temel amaç ve mantık** sorulur, tüm opsiyonlar değil

---

## Ping

* Amaç: Bir hostun **network layer’da aktif olup olmadığını** test etmek
* ICMP kullanır

  * Echo Request
  * Echo Reply

### Ping Mantığı

* Kaynak → ICMP Echo Request
* Hedef → ICMP Echo Reply
* Reply gelirse: **host ulaşılabilir**

⚠️ Tuzak:

* Ping başarısızsa **neden kesin olarak bilinemez**

  * Yol problemi olabilir
  * Geri dönüş yolu farklı olabilir (asimetrik routing)
  * Firewall ICMP’yi engelliyor olabilir

### RTT (Round Trip Time)

* Echo Request gönderilmesi ile Echo Reply alınması arasındaki süredir
* Hostlar arası “mesafe” ölçütü gibi kullanılır

---

## Traceroute / Tracert

* Amaç: Kaynaktan hedefe giden **olası yolu** göstermek
* Geçilen router’ları listeler

### Çalışma Prensibi (ÇOK SORULUR)

1. TTL = 1 olan paket gönderilir
2. İlk router TTL’yi 0 yapar ve **ICMP Time Exceeded** döner
3. TTL = 2, 3, ... şeklinde artırılır
4. Her router kendini ICMP ile belli eder

⚠️ Tuzak:

* Router cevap verirken **farklı bir interface IP’si** kullanabilir

---

## ARP

* Amaç: **ARP cache’i görüntülemek ve değiştirmek**
* IP ↔ MAC eşleşmelerini gösterir

### Temel İşlemler

* Cache görüntüleme
* Cache’ten kayıt silme
* Statik IP–MAC eşlemesi ekleme

⚠️ Tuzak:

* ARP dynamic kayıtları **kalıcı değildir**

---

## Route / Netstat -r

* Amaç: **Routing table’ı görüntülemek ve değiştirmek**
* Windows ve UNIX’te bulunur (syntax farklı)

### Routing Table’da Görülenler

* Network destination
* Netmask
* Gateway
* Interface

⚠️ Tuzak:

* Default route: `0.0.0.0 / 0.0.0.0`

---

## Ipconfig (Windows)

* IP stack bilgilerini gösterir

### Önemli Kullanımlar

* IP adresi, netmask, gateway
* DNS server’lar
* DHCP durumu
* Local DNS cache görüntüleme / temizleme

⚠️ Tuzak:

* `ipconfig` **sadece Windows** içindir

---

## Ip (UNIX)

* UNIX sistemlerde IP yapılandırmasını gösterir/değiştirir

### Temel Kullanımlar

* Interface bilgileri
* Routing table

⚠️ Tuzak:

* `ip` komutu, `ifconfig` ve `route`’un modern halidir

---

## Nslookup

* Amaç: **DNS server’lara sorgu atmak**

### Çalışma Modları

* Interactive
* Non-interactive

### Sık Sorulan Record Türleri

* A
* PTR
* CNAME
* MX

⚠️ Tuzak:

* Nslookup **DNS debugging** için kullanılır

---

## Tcpdump / Windump

* Metin tabanlı **packet analyzer**
* Paketlerin özet bilgisini gösterir

### Temel Özellikler

* Interface seçilebilir
* Filtre uygulanabilir
* Capture dosyaya yazılabilir

⚠️ Tuzak:

* `-n` kullanmazsan **DNS lookup** yapar

---

## Tcpdump Filtre Mantığı (ÇOK ÇIKAR)

* Protokol bazlı: arp, ip, tcp, udp, icmp
* Host bazlı: src, dst, host
* Port bazlı filtreleme
* Boolean operatörler: and, or, not

---

## Wireshark

* Grafik arayüzlü **packet sniffer & analyzer**
* libpcap / WinPcap tabanlı

### Filtre Türleri

* Capture filter → tcpdump syntax
* Display filter → farklı syntax

⚠️ Tuzak:

* Capture filter ≠ Display filter

---

## Sınavda Çok Gelen Noktalar

* Ping → ICMP
* Traceroute → TTL + ICMP Time Exceeded
* ARP → IP–MAC eşlemesi
* Default route mantığı
* DNS cache görüntüleme
* Tcpdump filtreleri
* Wireshark capture vs display filter farkı


## SLIDE 4

# Transport Layer (TCP / UDP) – Sınav Odaklı Özet

## Transport Layer’ın Görevi

* Farklı hostlarda çalışan **uygulama süreçleri (process)** arasında **mantıksal iletişim** sağlar
* Transport protokolleri **end system**’lerde çalışır (router’larda değil)
* Gönderici:

  * Uygulama mesajlarını **segment**’lere böler
* Alıcı:

  * Segmentleri tekrar birleştirip uygulamaya teslim eder

⚠️ Tuzak:

* Network layer → **host–host** iletişim
* Transport layer → **process–process** iletişim

---

## Multiplexing / Demultiplexing (ÇOK ÇIKAR)

* **Multiplexing (sender)**:

  * Birden fazla uygulamadan gelen veriye **transport header** eklenir
* **Demultiplexing (receiver)**:

  * Gelen segment doğru uygulamaya yönlendirilir

### UDP Demultiplexing

* Sadece **destination port** kullanılır
* Aynı port → aynı socket

### TCP Demultiplexing

* **4-tuple** ile yapılır:

  * Source IP
  * Source Port
  * Destination IP
  * Destination Port
* Aynı server portu (80) → farklı client’lar için **farklı socket’ler**

⚠️ Tuzak:

* TCP ≠ UDP demultiplexing

---

## Well-Known Ports

* Port aralığı: **0 – 1024**
* ICANN tarafından rezerve edilir
* Örnek:

  * TCP 80 → HTTP
* Client portları:

  * **Rastgele seçilir**

---

## UDP (User Datagram Protocol)

* **Connectionless**
* **Best-effort** servis
* Paketler:

  * Kaybolabilir
  * Sırası bozulabilir

### UDP Özellikleri

* Handshake yok → düşük gecikme
* Connection state yok
* Küçük header
* **Congestion control yok**

### UDP Nerede Kullanılır?

* Streaming (loss tolerant)
* DNS
* SNMP

⚠️ Tuzak:

* UDP güvenilir değildir
* Güvenilirlik gerekiyorsa **uygulama katmanında** eklenir

---

## UDP Segment Yapısı

* Source port
* Destination port
* Length
* Checksum

### UDP Checksum

* Bit hatalarını tespit eder
* One’s complement toplamı

⚠️ Tuzak:

* Checksum hata **tespit eder**, düzeltmez

---

## Reliable Data Transfer (RDT)

* Amaç: **Unreliable channel** üzerinde güvenilir iletişim
* Kullanılan mekanizmalar:

  * ACK
  * Sequence number
  * Timeout
  * Retransmission

### Pipelined Protokoller

#### Go-Back-N (GBN)

* Receiver sadece **cumulative ACK** gönderir
* Timeout → **tüm onaylanmamış paketler** tekrar gönderilir

#### Selective Repeat (SR)

* Receiver her paket için **ayrı ACK** gönderir
* Timeout → sadece ilgili paket yeniden gönderilir

⚠️ Tuzak:

* GBN ≠ SR farkı çok sorulur

---

## TCP (Transmission Control Protocol)

* **Connection-oriented**
* **Reliable, in-order byte stream**
* Full duplex
* Point-to-point

### TCP Sağladıkları

* Reliable data transfer
* Flow control
* Congestion control

⚠️ TCP Sağlamaz:

* Delay guarantee
* Bandwidth guarantee

---

## TCP Segment Yapısı (EZBER SORU)

* Sequence number
* Acknowledgement number
* Receive window (rwnd)
* Flags: SYN, ACK, FIN, RST
* Checksum

⚠️ Tuzak:

* Sequence number **byte** üzerinden sayılır

---

## TCP Reliable Data Transfer

* Cumulative ACK
* Tek retransmission timer (en eski ACK’siz segment)

### Retransmission Tetikleyicileri

* Timeout
* **3 duplicate ACK → Fast Retransmit**

---

## RTT ve Timeout Hesabı

* SampleRTT: ölçülen RTT
* EstimatedRTT:

  * Exponential weighted moving average

EstimatedRTT = (1 − α)·EstimatedRTT + α·SampleRTT

* TimeoutInterval = EstimatedRTT + 4·DevRTT

⚠️ Tuzak:

* Timeout çok kısa → gereksiz retransmission
* Timeout çok uzun → yavaş tepki

---

## TCP Flow Control

* Amaç: Receiver buffer taşmasını önlemek
* Receiver:

  * **rwnd (receive window)** ilan eder
* Sender:

  * In-flight data ≤ rwnd

⚠️ Tuzak:

* Flow control ≠ congestion control

---

## TCP Connection Management

### 3-Way Handshake (ÇOK ÇIKAR)

1. Client → SYN
2. Server → SYN + ACK
3. Client → ACK

### Connection Close

* FIN kullanılır
* Her iki taraf ayrı ayrı bağlantıyı kapatır

---

## Congestion Control

* Tanım:

  * Network’ün taşıyabileceğinden fazla veri gönderilmesi

### Belirtiler

* Paket kaybı
* Uzun gecikme

⚠️ Tuzak:

* Congestion control ≠ flow control

---

## TCP Congestion Control (AIMD)

* **Additive Increase**:

  * cwnd her RTT’de lineer artar
* **Multiplicative Decrease**:

  * Kayıp olunca cwnd yarıya düşer

### Slow Start

* Başlangıçta cwnd = 1 MSS
* Her RTT’de **iki katına çıkar**

### TCP Reno vs Tahoe

* Reno:

  * 3 duplicate ACK → cwnd / 2
* Tahoe:

  * Her durumda cwnd = 1

---

## TCP Fairness

* Aynı bottleneck’i paylaşan K TCP bağlantısı:

  * Ortalama hız ≈ R / K

⚠️ Tuzak:

* UDP congestion control yapmaz → fairness’i bozar
* Parallel TCP connections fairness’i bozar

---

## Sınavda Çok Gelen Tuzaklar

* TCP = reliable, UDP = best-effort
* TCP byte-stream, message boundary yok
* 4-tuple TCP demux
* GBN vs SR farkı
* Flow control ≠ congestion control
* Fast retransmit = 3 duplicate ACK


## SLIDE 5

# Application Layer – Sınav Odaklı Özet

## Application Layer’ın Amacı

* **Farklı host’larda çalışan uygulamalar (process)** arasında iletişim sağlar
* Sadece **end system**’lerde çalışır
* **Router’lar application layer çalıştırmaz**

⚠️ Tuzak:
Application layer ≠ Network core
Uygulamalar **host’larda**, yönlendirme **router’larda**

---

## Network Application Architectures (ÇOK ÇIKAR)

### Client–Server Architecture

**Server:**

* Always-on (sürekli açık)
* **Permanent IP address**
* Ölçekleme için data center

**Client:**

* Server ile iletişim kurar
* Intermittent (ara ara bağlı olabilir)
* Dynamic IP kullanabilir
* **Client’lar birbirleriyle doğrudan konuşmaz**

⚠️ Tuzak:

* Client–client iletişimi **yok**

---

### P2P (Peer-to-Peer) Architecture

* Always-on server **yok**
* End system’ler **doğrudan** haberleşir
* **Self-scalability**:

  * Yeni peer = yeni kapasite
* Peer’lar:

  * Sık sık disconnect olur
  * IP adresleri değişir

⚠️ Dezavantaj:

* Yönetimi zor
* Güvenlik karmaşık

⚠️ Tuzak:

* P2P uygulamalarda da **client + server process** vardır

---

## Process Kavramı

* **Process**: Host içinde çalışan program
* Aynı host:

  * Inter-process communication (OS üzerinden)
* Farklı host:

  * **Message exchange** ile iletişim

**Client process:**

* İletişimi başlatır

**Server process:**

* Bağlantı bekler

---

## Application Layer Protocol Neyi Tanımlar?

* Mesaj tipleri (request / response)
* Mesaj formatı (syntax)
* Mesajların anlamı (semantics)
* Mesajların **ne zaman ve nasıl** gönderileceği

### Open vs Proprietary Protocol

**Open protocol:**

* RFC ile tanımlı
* Interoperable
* Örn: HTTP, SMTP

**Proprietary protocol:**

* Kapalı
* Örn: Skype

---

## Uygulamaların Transport Layer’dan Beklentileri (EZBER SORU)

### Data Integrity

* File transfer, web → **loss kabul etmez**
* Audio/video → **loss tolerant**

### Timing (Delay)

* VoIP, online oyun → **düşük gecikme şart**

### Throughput

* Video → minimum throughput gerekir
* Elastic apps → ne gelirse kullanır

### Security

* Encryption
* Authentication
* Integrity

---

## TCP vs UDP – Application Katmanı Açısından

| Özellik            | TCP            | UDP            |
| ------------------ | -------------- | -------------- |
| Reliability        | Var            | Yok            |
| Congestion Control | Var            | Yok            |
| Delay              | Yüksek         | Düşük          |
| Kullanım           | Web, FTP, Mail | DNS, Streaming |

⚠️ Tuzak:

* TCP güvenli değildir → SSL/TLS ile güvenli olur

---

## HTTP (HyperText Transfer Protocol)

* **Application layer protokolü**
* **Client–Server**
* TCP kullanır (port 80)
* **Stateless**

⚠️ Tuzak:

* HTTP server **client geçmişini tutmaz**

---

## Non-Persistent vs Persistent HTTP (ÇOK ÇIKAR)

### Non-Persistent HTTP

* 1 TCP connection → 1 object
* Her object için **2 RTT**
* Performans kötü

### Persistent HTTP

* Tek TCP connection
* Birden fazla object
* Daha az RTT

⚠️ Tuzak:

* HTTP/1.1 → persistent default

---

## HTTP Request Message

* ASCII format
* Bölümler:

  * Request line
  * Header lines
  * (Opsiyonel) body

**Method’lar:**

* GET
* POST
* HEAD
* PUT
* DELETE

---

## HTTP Response Message

* Status line
* Header lines
* Data (HTML, image, vb.)

### Önemli Status Code’lar (EZBER)

* 200 OK
* 301 Moved Permanently
* 400 Bad Request
* 404 Not Found
* 505 HTTP Version Not Supported

---

## Cookies (State Tutma Mekanizması)

HTTP stateless olduğu için kullanılır

**4 bileşen:**

1. HTTP response header
2. HTTP request header
3. Browser’daki cookie dosyası
4. Server backend database

**Amaç:**

* Authorization
* Shopping cart
* User tracking

⚠️ Tuzak:

* Cookies → privacy problemi

---

## Web Cache (Proxy Server)

* Client → cache
* Cache’te varsa:

  * Origin server’a gitmez
* Amaç:

  * Delay azaltmak
  * Access link yükünü düşürmek

⚠️ Tuzak:

* Cache hem **client hem server** gibi davranır

---

## Conditional GET

* Cache güncel mi kontrol eder
* Header:

  * `If-Modified-Since`
* Cevap:

  * 304 Not Modified

⚠️ Avantaj:

* Object transfer edilmez

---

## FTP (File Transfer Protocol)

* Client–Server
* TCP kullanır
* Server port: **21**

### FTP Bağlantıları (ÇOK ÇIKAR)

* **Control connection**:

  * Port 21
  * Komutlar
* **Data connection**:

  * Her transfer için ayrı TCP
  * Port 20

⚠️ Tuzak:

* FTP **stateful**’dır

---

## Electronic Mail – Bileşenler

1. User Agent
2. Mail Server
3. SMTP

### SMTP

* TCP port 25
* Push protocol
* ASCII text
* Persistent connection

⚠️ Tuzak:

* SMTP sadece **mail gönderir**
* Mail okuma için kullanılmaz

---

## Mail Access Protocols

### POP3

* Download & delete
* Stateless
* Server’da mail tutulmaz

### IMAP

* Mail server’da kalır
* Folder desteği
* Stateful

### HTTP Mail

* Gmail, Yahoo
* Browser üzerinden

⚠️ Tuzak:

* POP3 ≠ IMAP farkı çok sorulur

---

## P2P File Distribution – BitTorrent

* File → **chunks**
* Tracker → peer listesi
* Rarest-first chunk selection
* **Tit-for-tat** upload mantığı

⚠️ Tuzak:

* Peer’lar hem download hem upload yapar

---

## Distributed Hash Table (DHT)

* (Key, value) çiftleri
* Key → hash ile integer
* Key, **closest successor peer**’a atanır

⚠️ Tuzak:

* Circular DHT
* Lookup:

  * O(N) → shortcuts ile O(log N)

---

## Sınavda Çok Gelen Kavramlar

* Client–Server vs P2P
* Stateless vs Stateful
* HTTP non-persistent vs persistent
* Web cache avantajı
* FTP control vs data connection
* SMTP vs POP3 vs IMAP
* BitTorrent tit-for-tat
* DHT successor mantığı


## SLIDE 6

# Multimedia Networking – Sınav Odaklı Özet

## Multimedia Networking Nedir?

* **Ses (audio)**, **video** ve **gerçek zamanlı iletişim** uygulamalarının ağ üzerinden iletilmesini inceler
* Klasik data uygulamalarından farkı:

  * **Delay (gecikme)**
  * **Jitter (gecikme değişimi)**
  * **Packet loss** çok daha kritiktir

⚠️ Tuzak:
Multimedia uygulamaları **yüksek throughput değil**, **zamanında teslim** ister

---

## Multimedia Türleri (ÇOK ÇIKAR)

### Streaming Stored Audio / Video

* İçerik önceden kaydedilmiştir
* Client, dosya tamamen inmeden oynatmaya başlar
* Örnek: YouTube, Netflix

### Live Streaming

* İçerik canlı üretilir
* Delay toleransı düşüktür
* Örnek: Canlı spor yayınları

### Conversational Voice / Video

* İnteraktif iletişim
* Delay toleransı **çok düşüktür**
* Örnek: VoIP, video call

---

## Audio – Temel Kavramlar

* Analog ses **sampling** ile dijitale çevrilir
* Telefon: 8000 sample/sn
* CD: 44100 sample/sn
* Quantization → **quantization error**

⚠️ Tuzak:
Sampling rate ↑ → kalite ↑ → bitrate ↑

---

## Video – Temel Kavramlar

* Video = sabit hızda gösterilen **frame dizisi**
* Örnek: 24 frame/sn
* Dijital görüntü: pixel dizisi

### Video Coding

* Amaç: **bitrate düşürmek**
* Redundancy türleri:

  * **Spatial coding** (aynı frame içi)
  * **Temporal coding** (frame’ler arası)

---

## CBR vs VBR (ÇOK SORULUR)

### CBR (Constant Bit Rate)

* Sabit encoding hızı
* Network için öngörülebilir

### VBR (Variable Bit Rate)

* Sahneye göre değişken bitrate
* Daha iyi kalite, daha zor network yönetimi

---

## Streaming Stored Video – Zorluklar

* Continuous playout gereksinimi
* Network delay değişkendir (jitter)
* Çözüm:

  * Client-side buffer
  * Playout delay

⚠️ Tuzak:
Buffer arttıkça delay artar

---

## UDP ile Streaming

* Encoding rate hızında gönderim
* Avantaj: düşük delay
* Dezavantaj:

  * Packet loss
  * Congestion control yok

---

## HTTP/TCP ile Streaming

* HTTP GET ile video transferi
* TCP: congestion control + retransmission
* Sonuç:

  * Daha stabil
  * Daha yüksek delay

---

## DASH (Dynamic Adaptive Streaming over HTTP) (ÇOK ÇIKAR)

### Server

* Video chunk’lara bölünür
* Farklı bitratelerde saklanır
* Manifest file içerir

### Client

* Bandwidth ölçer
* Uygun bitrate’li chunk ister
* Bitrate zamanla değişebilir

⚠️ Avantaj:
Adaptif kalite + TCP uyumu

---

## Content Distribution Network (CDN)

* İçerik coğrafi olarak dağıtılmış server’larda tutulur
* Amaç:

  * Delay azaltmak
  * Trafiği yaymak

⚠️ Tuzak:
Tek server ölçeklenmez

---

## Voice over IP (VoIP)

* End-to-end delay:

  * <150 ms iyi
  * > 400 ms kötü
* Packet loss %1–10 tolere edilebilir

### Kayıp Türleri

* Network loss (congestion)
* Delay loss (geç gelen paket)

---

## RTP (Real-Time Protocol)

* Gerçek zamanlı ses/video taşır
* UDP üzerinde çalışır
* Sağladıkları:

  * Payload type
  * Sequence number
  * Timestamp

⚠️ Tuzak:
RTP QoS sağlamaz

---

## RTP Header – Kritik Alanlar

* Payload Type → codec
* Sequence Number → packet loss
* Timestamp → senkronizasyon
* SSRC → stream kaynağı

---

## SIP (Session Initiation Protocol)

* Call setup ve management
* User location
* HTTP benzeri syntax
* Default port: 5060

⚠️ Tuzak:
SIP = signaling
RTP = media

---

## Network Support for Multimedia

### Best Effort

* QoS yok
* Basit

### Differentiated Services

* Trafik sınıfları
* Packet marking

### Per-Connection QoS

* Flow bazlı garanti
* Karmaşık, az kullanılır

---

## Sınavda Çok Gelen Tuzaklar

* Streaming ≠ download
* UDP düşük delay, yüksek loss
* TCP güvenilir ama gecikmeli
* DASH adaptif bitrate
* SIP ≠ RTP
* RTP ≠ QoS
* CDN neden gerekir
* Delay ≠ jitter

# YYGWASHERE
## YYGWASHERE
### YYGWASHERE