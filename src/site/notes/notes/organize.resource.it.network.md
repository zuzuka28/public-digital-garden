---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.network/","title":"Network"}
---


<https://habr.com/ru/companies/ruvds/articles/759988/> - годно!


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.osi/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# OSI

</div>




OSI - 7 уровней.
Базовая модель.

TCP/IP - 4 уровня.
Более обобщенный вид.

| OSI                   | TCP/IP               |
| --------------------- | -------------------- |
| L7 Application Layer  | L7 Application Layer |
| L6 Presentation Layer | L7 Application Layer |
| L5 Session Layer      | L7 Application Layer |
| L4 Transport Layer    | L4 Transport Layer   |
| L3 Network Layer      | L3 Internet Layer    |
| L2 Data Link Layer    | L2 Link Layer        |
| L1 Physical Layer     | L2 Link Layer        |

## Примеры протоколов

| OSI                   | Example                |
| --------------------- | ---------------------- |
| L7 Application Layer  | http, ftp, dns, telnet |
| L6 Presentation Layer | ssl, tls               |
| L5 Session Layer      | pptp                   |
| L4 Transport Layer    | tcp, udp               |
| L3 Network Layer      | ip, arp,               |
| L2 Data Link Layer    | Ethernet               |
| L1 Physical Layer     | Ethernet, Bluetooth    |

</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.addressing/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# Addressing

</div>




Для пересылки данных требуется указать отправителя и получателя, что и называется адресацией.

На разных уровнях сетевой модели используются разные способы идентификации

- L2 MAC-адреса
- L3 IP-адреса
- L4 Порты

</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.routing/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# Routing

</div>




Хост - физическое устройство с адресом.

Типы адресов

- индивидуальный адрес (unicast address) - уникальный адрес в подсети
- широковещательный адрес (broadcast address) - общий адрес для всех хостов в подсети
- групповой адрес (multicast address)

Глобальная сеть состоит из множества подсетей

При пересылке между хостами в одной подсети просматривается таблица маршрутизации и трафик направляется на нужное устройство.
Если хост не найден в подсети, то трафик направляется на специальный шлюз, который решит, куда дальше направить трафик.

Шлюз использует [[notes/organize.resource.it.network.nat\|NAT]], поэтому внешний IP для всех устройств в подсети идентичен.

</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.pdu/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# PDU

</div>




Данные пересылаются отдельными частями, где каждая часть содержит информацию о том, от кого и для кого сообщение, а так же некоторая мета-информация.

Часть пересылаемых данных называется **PDU** ( protocol data unit ) и состоит из header и payload. На разных уровнях PDU называются по-разному

- L2 - фрейм;
- L3 - пакет (IP, ICMP);
- L4 сегмент или датаграмма (TCP, UDP);
- L7 сообщение (DNS, DHCP).

При пересылке данные оборачиваются в информацию о пересылке как капуста, то есть на каждом уровне добавляется своя информация для идентификации получателя. Капуста растет от L7 к L1.

Что содержат PDU на разных уровнях и в разных протоколах.

- L2 фрейм

  - Dst MAC
  - Src MAC
  - данные
  - чек-сумма

- L3 пакет

  - версия
  - размер сообщения
  - отступ фрагмента
  - флаги
  - ttl
  - протокол
  - чексумма заголовка
  - Dst IP
  - Src IP
  - Опции ( IP пакеты достаточно гибкие, поэтому там можно задать разные )
  - данные

- L4 UPD датаграмма

  - Dst Port
  - Src Port
  - размер сообщения
  - чек-сумма
  - данные

- [[notes/organize.resource.it.network.tcp#состав-tcp-сегмента-pdu\|L4 TCP сегмент]]

</div></div>


## Протоколы


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.arp/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# ARP

</div>




ARP (Address Resolution Protocol) - протокол для определения MAC адреса по IP адресу.

Используеися для определения получателя в подсети.

Существуют протоколы reverse ARP (RARP), вычисляющие IP по MAC.

</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.dhcp/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# DHCP

</div>




DHCP (Dynamic Host Configuration Protocol) - Протокол динамической конфигурации хоста.
Используется для автоматической конфигурации хоста, чтобы не делать этого вручную.

</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.dns/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# DNS

</div>




DNS (Domain Name System) -Протокол преобразования домена хоста в его IP.

Eсть много видов DNS записей, которые можно получить

- A (Address) — IP-адрес, закреплённый за доменным именем;
- AAAA (IPv6 Address) — IPv6-адрес, закреплённый за доменным именем;
- CNAME (Canonical Name);
- MX (Mail Exchanger);
- NS (Name Server);
- PTR (Pointer);
- SOA (Start of Authority);
- TXT (Text);
- SRV (Service).


</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.tcp/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# TCP

</div>




TCP - Протокол гарантирующий передачу данных и их последовательность на транспортном уровне.
TCP создает надежное полнодуплексное соединение.

## Состав TCP Сегмента (PDU)

- Dst Port
- Src Port
- номер sequence
- номер ack
- отступ фрагмента
- чексумма
- окно
- Опции
- данные

Для каждого сообщения присваивается Sequence number и Acknowledge number благодаря которым можно отслеживать пересылку.

При потере данных данные отслеживаются по sequence и отправляются повторно.

Для управления TCP-соединением используются флаги в отсылаемых TCP-сегментах. Наиболее важными являются:

- `SYN` — используется при установлении TCP-соединения;
- `ACK` — означает, что сегмент был получен принимающей стороной;
- `FIN` — используется при нормальном (graceful) закрытии TCP-соединении;
- `RST` — используется при аварийном закрытии TCP-соединения.

## Пример обмена данными по TCP

1. Client SYN -> Server
2. Client <- SYN, ACK Server
3. Client ACK -> Server
4. Передача данных
5. Client FIN, ACK -> Server
6. Client <- ACK Server
7. Client <- FIN, ACK Server
8. Client ACK -> Server

То есть сначала происходит 3 фазный handshake и открытие коннекта, потом передача, а потом 4 фазный handshake и закрытие коннекта.


</div></div>



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/notes/organize.resource.it.network.udp/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">

<div class="markdown-embed-title">

# UDP

</div>




UDP - Быстрый протокол передачи данных, допускается дублирование или пропуск данных, не важен порядок доставки.

</div></div>



<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">

<div class="markdown-embed-title">

# HTTP

</div>




<https://habr.com/ru/companies/avito/articles/710678/> - годно!

<https://youtu.be/UMwQjFzTQXw?si=GuMSSxCJ8TslTB-r>

HTTP (HyperText Transfer Protocol) - протокол прикладного L7 уровня, разработанный для создания распределенных медиасистем.

HTTP использует [[notes/organize.resource.it.network.tcp\|TCP]] для передачи данных

## HTTP 1.0

- может содержать Header - это сделало протокол более гибким, позволяя пересылать метаинформацию
- версионирование - запрос содержит используемую версию протокола, чтобы корректно обрабатывать запросы.
- статус коды
- Content-type - информация о типе пересылаемых даных, что позволило использовать протокол для передачи разных данных
- методы GET, POST, HEAD
- запросы совершаются по принципу открыл соединение - сделал запрос - закрыл соединение
- использует текстовый формат пересылки

## HTTP 1.1

- обязательный заголовок Host, для идентификации конкретного хоста. Это нужно для размещения на одном адресе нескольких сайтов. 
- долговременные соединения, через которые можно сделать несколько *последовательных* запросов
- Continue Status - для избежания проблем с отклонением запросов теперь есть возможность посылать только мета-данные и потом послать запрос, если сервер готов его обработать.
- методы PUT, PATCH, DELETE, CONNECT, TRACE, OPTIONS
- возможность сжатия данных GZip
- кэширование ресурсов на стороне клиента

## HTTP 2.0

- мультиплексирование запросов - теперь через одно соединение можно посылать несколько запросов *асинхронно*.
- приоритизация запросов - можно задать приоритет для запросов, например - грузить css перед js файлами.
- автоматическое сжатие данных GZip - теперь данные сжимаются всегда по умолчанию (бинарный формат пересылки)
- Connection Reset - возможность пересоздать соединение
- Server push - возможность сервером переслать данные клиенту заранее

## HTTP 3.0

Модернизированная версия протокола.

Новая версия протокола *полагается не на TCP*, а на *протокол **QUIC** основанный на UDP*.

</div></div>

