---
title: aaaOverview di DNS inverso in Azure | Documenti Microsoft
description: Informazioni sul funzionamento del DNS inverso e su come usarlo in Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Panoramica del DNS inverso e supporto in Azure

In questo articolo fornisce una panoramica di come inversa il funzionamento DNS e hello inversi scenari DNS supportati in Azure.

## <a name="what-is-reverse-dns"></a>Che cos'è il DNS inverso?

I record DNS convenzionali attiva un mapping da un indirizzo IP di DNS nome (ad esempio, 'www.contoso.com') tooan (ad esempio 64.4.6.100).  DNS inverso consente traduzione hello di un nome di tooa indietro (64.4.6.100) indirizzo IP ('www.contoso.com').

I record DNS inversi vengono usati in varie situazioni. Ad esempio, i record DNS inversi vengono ampiamente utilizzati contro la posta indesiderata di posta elettronica verificando mittente hello del messaggio di posta elettronica.  Recupera server di posta elettronica ricevente Hello hello record DNS inverso di hello l'indirizzo IP del server di invio e verifica se che ospita la posta elettronica toosend autorizzati da hello origina dominio. 

## <a name="how-reverse-dns-works"></a>Come funziona il DNS inverso

I record DNS inversi sono ospitati in speciali zone DNS, chiamate zone "ARPA".  Queste zone formano una gerarchia DNS separata in parallelo con normale gerarchia hello hosting domini, ad esempio 'contoso.com'.

Ad esempio, i record DNS 'www.contoso.com' hello viene implementata tramite un record DNS 'A' con nome hello 'www' nell'area di hello 'contoso.com'.  Questo record A punti toohello corrispondente dell'indirizzo IP, in questo caso 64.4.6.100.  ricerca inversa Hello viene implementata separatamente, con un record 'PTR' denominato '100' nell'area di hello '6.4.64.in-addr.arpa' (si noti che gli indirizzi IP vengono annullati in zone ARPA).  Se è stato configurato correttamente, il record PTR, punta nome toohello 'www.contoso.com'.

Quando un'organizzazione viene assegnata un blocco di indirizzi IP, acquisiscono hello toomanage destra hello ARPA la zona corrispondente. salve le zone ARPA corrispondente indirizzo IP di toohello blocchi utilizzati da Azure sono ospitati e gestiti da Microsoft. Provider di servizi Internet può ospitare zone ARPA hello per i propri indirizzi IP per l'utente o potrebbe consentire tooyou host zone ARPA hello in un servizio DNS di propria scelta, ad esempio DNS di Azure.

> [!NOTE]
> Le ricerche DNS dirette e le ricerche DNS inverse vengono implementate in gerarchie DNS separate parallele. ricerca inversa di Hello per 'www.contoso.com' **non** ospitato nell'area di hello 'contoso.com', ma è ospitato in zone ARPA hello per blocco di indirizzi IP corrispondente hello. Per i blocchi di indirizzi IPv4 e IPv6 vengono usate zone separate.

### <a name="ipv4"></a>IPv4

nome Hello di una zona di ricerca inversa IPv4 deve essere nel seguente formato hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Ad esempio, quando si crea una zona inversa toohost record per l'host con indirizzi IP che si trovano nel prefisso 192.0.2.0/24 hello, nome della zona hello verrebbe creato isolando il prefisso di rete hello di indirizzo hello (192.0.2) e quindi inversione dell'ordine di hello (2.0.192) e l'aggiunta di hello suffisso `.in-addr.arpa`.

|Classe di subnet|Prefisso di rete  |Prefisso di rete inverso  |Suffisso standard  |Nome della zona inversa |
|-------|----------------|------------|-----------------|---------------------------|
|Classe A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|Classe B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|Classe C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Delega IPv4 senza classi

In alcuni casi, è inferiore a una classe C intervallo IP hello allocata tooan organizzazione (/ 24) intervallo. In questo caso, intervallo IP hello non rientra in un limite di zona all'interno di hello `.in-addr.arpa` gerarchia della zona e pertanto non può essere delegato come una zona figlio.

Viene invece utilizzato un meccanismo diverso tootransfer controllo di ricerca inversa singoli (PTR) registra zona DNS tooa dedicato. Questo meccanismo di delega a una zona figlio per ogni intervallo IP, quindi esegue il mapping di ogni indirizzo IP in hello intervallo singolarmente zona figlio toothat utilizza i record CNAME.

Si supponga, ad esempio, che un'organizzazione viene concessa hello IP intervallo 192.0.2.128/26 dal proprio provider Internet. Questo rappresenta 64 indirizzi IP, da 192.0.2.128 too192.0.2.191. Il DNS inverso per questo intervallo viene implementato come segue:
- organizzazione di Hello crea una zona di ricerca inversa denominata 128-26.2.0.192.in-addr. arpa. prefisso Hello rappresenta ' 128-26' hello rete segmento assegnato toohello organizzazione all'interno di hello classe C (/ 24) intervallo.
- Hello ISP crea tooset record NS backup hello delega DNS per hello sopra l'area da zona padre di classe C hello. Viene inoltre creato il record CNAME in zona di ricerca inversa hello padre (classe C), il mapping di ogni indirizzo IP hello IP intervallo toohello nuova zona creata dall'organizzazione hello:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- organizzazione di Hello quindi gestisce singoli record PTR hello all'interno della zona figlio.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Una ricerca inversa per le query per un record PTR '192.0.2.129' indirizzo IP hello denominato '129.2.0.192.in-addr.arpa'. Questa query viene risolta tramite hello CNAME record PTR toohello hello padre della zona in zona figlio hello.

### <a name="ipv6"></a>IPv6

nome Hello di una zona di ricerca inversa IPv6 deve essere hello seguente formato:`<IPv6 network prefix in reverse order>.ip6.arpa`

Ad esempio: Quando si crea una zona inversa toohost record per gli host con indirizzi IP in hello 2001:db8:1000:abdc:: / 64 prefisso, nome della zona hello verrebbe creato isolando il prefisso di rete hello dell'indirizzo hello (2001:db8:abdc::). Espandere quindi tooremove prefisso di rete IPv6 hello [zero compressione](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), se è stato utilizzato tooshorten prefisso dell'indirizzo IPv6 hello (2001:0db8:abdc:0000::). Invertire l'ordine di hello, utilizzando un punto come delimitatore tra ogni numero esadecimale nel prefisso hello hello, hello toobuild invertita prefisso di rete (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) e aggiungere il suffisso hello `.ip6.arpa`.


|Prefisso di rete  |Prefisso di rete espanso e inverso |Suffisso standard |Nome della zona inversa  |
|---------|---------|---------|---------|
|2001:db8:abdc::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Supporto di Azure per DNS inverso

Azure supporta due scenari di separato relative tooreverse DNS:

**Hosting hello ricerca inversa zona corrispondente tooyour blocco di indirizzi IP.**
DNS di Azure è possibile utilizzare anche[le zone di ricerca inversa di ospitare e gestire i record PTR hello per ogni ricerca DNS inversa](dns-reverse-dns-hosting.md), per IPv4 e IPv6.  processo di creazione di zona di ricerca inversa (ARPA) di hello, configurare la delega di hello, Hello e configurazione PTR record è hello stesso come per le zone DNS regolare.  Hello solo differenze sono che è necessario configurare la delega hello ISP anziché registrar DNS e deve essere utilizzato solo hello il tipo di record PTR.

**Configurare record DNS inverso hello per hello l'indirizzo IP assegnato tooyour servizio di Azure.** Azure consente troppo[configurare ricerca inversa hello per gli indirizzi IP di hello allocati tooyour servizio Azure](dns-reverse-dns-for-azure-services.md).  Questa ricerca inversa viene configurata da Azure come un record PTR hello corrispondente ARPA zona.  Queste zone ARPA, corrispondente a intervalli di IP hello tooall utilizzati da Azure, sono ospitate da Microsoft

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Informazioni su come troppo[zona di ricerca inversa hello host per l'intervallo di IP assegnato dal provider di servizi Internet in Azure DNS](dns-reverse-dns-for-azure-services.md).
<br>
Informazioni su come troppo[gestire record di ricerca inversa DNS per i servizi di Azure](dns-reverse-dns-for-azure-services.md).

