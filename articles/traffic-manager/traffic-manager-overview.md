---
title: "aaaWhat è Traffic Manager | Documenti Microsoft"
description: "In questo articolo consentirà di comprendere che cos'è Gestione traffico e se è scelta di routing del traffico destra hello per l'applicazione"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Panoramica di Gestione traffico

Gestione traffico di Microsoft Azure consente di distribuzione hello toocontrol del traffico utente per gli endpoint del servizio in diversi Data Center. Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e macchine virtuali di Azure. È anche possibile usare Gestione traffico con endpoint esterni, non di Azure.

Gestione traffico Usa hello sistema DNS (Domain Name) toodirect client richieste toohello più endpoint appropriato in base a un metodo di routing del traffico e l'integrità di hello degli endpoint hello. Traffic Manager fornisce una gamma di [metodi di routing del traffico](traffic-manager-routing-methods.md) e [opzioni di monitoraggio endpoint](traffic-manager-monitoring.md) toosuit altra applicazione alle esigenze e i modelli di failover automatico. Gestione traffico è toofailure resilienti, ad esempio hello malfunzionamento di un'intera regione di Azure.

## <a name="traffic-manager-benefits"></a>Vantaggi di Gestione traffico

Con Gestione traffico è possibile:

* **Migliorare la disponibilità delle applicazioni critiche**

    Gestione traffico assicura la disponibilità elevata delle applicazioni attraverso il monitoraggio degli endpoint e il failover automatico in caso di inattività di un endpoint.

* **Migliorare la velocità di risposta delle applicazioni a prestazioni elevate**

    Azure consente di siti Web o servizi cloud toorun in dislocati in tutto il mondo hello. Gestione traffico migliora la velocità di risposta dell'applicazione indirizzando endpoint toohello traffico con latenza di rete più bassa di hello per client hello.

* **Eseguire la manutenzione dei servizi senza tempi di inattività**

    È possibile eseguire le operazioni pianificate di manutenzione delle applicazioni senza tempi di inattività. Gestione traffico indirizza gli endpoint tooalternative traffico mentre manutenzione hello è in corso.

* **Combinare applicazioni locali e applicazioni basate sul cloud**

    Gestione traffico supporta esterno, gli endpoint di Azure non abilitarlo toobe utilizzato ibridi di cloud e locali distribuzioni, tra cui hello "burst-to-cloud," "eseguire la migrazione a cloud," e "failover sul cloud" scenari.

* **Distribuire il traffico in distribuzioni complesse e di grandi dimensioni**

    Utilizzando [profili di gestione traffico nidificati](traffic-manager-nested-profiles.md), metodi di routing del traffico possono essere combinato toocreate sofisticate e hello toosupport flessibile regole deve delle distribuzioni più grandi e complesse.

## <a name="how-traffic-manager-works"></a>Modalità di funzionamento di Gestione traffico

Gestione traffico di Azure consente distribuzione hello toocontrol del traffico tra l'endpoint dell'applicazione. Un endpoint è un servizio con connessione Internet ospitato all'interno o all'esterno di Azure.

Gestione traffico offre due vantaggi principali:

1. Distribuzione del traffico in base tooone di diversi [metodi di routing del traffico](traffic-manager-routing-methods.md)
2. [Monitoraggio continuo dell'integrità degli endpoint](traffic-manager-monitoring.md) e failover automatico quando si verificano errori sugli endpoint.

Quando un client tenta tooconnect tooa servizio, innanzitutto necessario risolvere il nome DNS hello dell'indirizzo IP del servizio tooan hello. client Hello si connette quindi il servizio hello tooaccess di toothat IP indirizzo.

**Hello toounderstand di punto più importante è che a livello DNS hello funzionamento di gestione traffico.**  Gli endpoint in base alle regole di hello del metodo di routing del traffico hello del servizio Gestione traffico Usa DNS toodirect client toospecific. I client si connettono endpoint toohello selezionato **direttamente**. Gestione traffico non è un proxy o un gateway. Gestione traffico non vedere il passaggio tra hello client e servizio di hello del traffico hello.

### <a name="traffic-manager-example"></a>Esempio di Gestione traffico

Contoso Corp ha sviluppato un nuovo portale per i partner. URL di Hello per questo portale è https://partners.contoso.com/login.aspx. un'applicazione Hello è ospitata in tre aree di Azure. disponibilità tooimprove e ottimizzare le prestazioni globali, usare Gestione traffico toodistribute client traffico toohello endpoint più vicino disponibile.

tooachieve questa configurazione, vengono completate hello alla procedura seguente:

1. Distribuire tre istanze del servizio. i nomi DNS Hello di queste distribuzioni sono 'contoso-us.cloudapp .net', 'contoso-eu.cloudapp .net' e 'contoso-asia.cloudapp .net'.
2. Creare un profilo di Traffic Manager, denominato 'contoso.trafficmanager.net' e configurarlo in metodo di routing del traffico "Performance" hello toouse tra gli endpoint hello tre.
* Configurare il nome di dominio personale, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net', con un record DNS CNAME.

![Configurazione DNS di Gestione traffico][1]

> [!NOTE]
> Quando si utilizza un dominio personale con gestione traffico di Azure, è necessario utilizzare un toopoint CNAME il nome di dominio personale dominio nome tooyour Traffic Manager. Standard DNS non è un record CNAME in hello 'apice' toocreate (o radice) di un dominio. Non è quindi possibile creare un record CNAME per "contoso.com", detto anche dominio "naked". È possibile creare solo un record CNAME per un dominio in "contoso.com", ad esempio "www.contoso.com". toowork risolvere questa limitazione, è consigliabile utilizzare una semplice richieste toodirect di reindirizzamento HTTP per il nome alternativo di tooan 'contoso.com', ad esempio 'www.contoso.com'.

### <a name="how-clients-connect-using-traffic-manager"></a>Come si connettono i client tramite Gestione traffico

Continuando dall'esempio precedente hello, quando un client richiede hello pagina https://partners.contoso.com/login.aspx, client hello esegue hello dopo il nome DNS di passaggi tooresolve hello e stabilire una connessione:

![Stabilire una connessione tramite Gestione traffico][2]

1. client Hello invia ricorsiva di tooits configurato una query DNS DNS servizio tooresolve hello nome 'partners.contoso.com'. Un servizio DNS ricorsivo, denominato anche servizio "DNS locale", non ospita direttamente i domini DNS, Invece, il client hello off-loads lavoro hello contattato hello DNS autorevole vari servizi su hello necessaria Internet tooresolve un nome DNS.
2. nome DNS di hello tooresolve, il servizio DNS di hello ricorsivo Trova server dei nomi hello per il dominio 'contoso.com' hello. Contatta quindi i record DNS di nome server toorequest hello 'partners.contoso.com'. i server DNS di contoso.com Hello restituiscono i record CNAME hello che punta toocontoso.trafficmanager.net.
3. Successivamente, il servizio DNS di hello ricorsivo Trova server dei nomi hello per il dominio 'trafficmanager.net' hello, che sono fornite da hello del servizio di gestione traffico di Azure. Quindi invia una richiesta di hello 'contoso.trafficmanager.net' DNS record toothose server DNS.
4. Server dei nomi Hello Traffic Manager di ricezione richiesta hello. Scelgono un endpoint in base a:

    - stato Hello configurato di ogni endpoint (non vengono restituiti endpoint disabilitato)
    - controlli di integrità corrente di Hello di ogni endpoint, come determinato dall'integrità di gestione traffico hello. Per altre informazioni, vedere [Informazioni sul monitoraggio di Gestione traffico](traffic-manager-monitoring.md).
    - Hello scelto il metodo di routing del traffico. Per altre informazioni, vedere [Metodi di routing di Gestione traffico](traffic-manager-routing-methods.md).

5. endpoint Hello scelto viene restituito come un altro record DNS CNAME. In questo caso, si supponga che venga restituito contoso-us.cloudapp.net.
6. Successivamente, il servizio DNS di hello ricorsivo Trova server dei nomi hello per il dominio 'cloudapp.net' hello. Contatta tali hello toorequest di nome server 'contoso-us.cloudapp .net' record DNS. Viene restituito un record DNS 'A' contenente l'indirizzo IP hello hello statunitense dell'endpoint del servizio.
7. il servizio DNS di Hello ricorsivo consente di consolidare i risultati di hello e restituisce un singolo client di toohello risposta DNS.
8. client Hello riceve i risultati di DNS hello e si connette toohello indirizzo IP specificato. Hello client si connette toohello endpoint del servizio dell'applicazione non viene direttamente, non tramite Traffic Manager. Poiché si tratta di un endpoint HTTPS, hello client esegue l'handshake SSL/TLS hello necessaria e quindi effettua una richiesta HTTP GET per hello ' / login ' pagina.

il servizio DNS di Hello ricorsivo memorizza nella cache le risposte DNS hello che riceve. resolver DNS Hello nel dispositivo client hello memorizza anche nella cache il risultato di hello. Consente di rispondere più rapidamente utilizzando i dati dalla cache di hello anziché di una query su altri server di nome successive toobe di query DNS. durata Hello della cache di hello è determinata dalla proprietà di (durata TTL) 'time-to-live' hello di ogni record DNS. Valori più brevi determinano la scadenza della cache più veloce e pertanto più round trip toohello Traffic Manager nome server. Valori più lunghi significa che può richiedere traffico toodirect più lontano da un endpoint non riuscito. Gestione traffico consente tooconfigure hello durata (TTL) utilizzato in toobe le risposte DNS di Traffic Manager minimo di 0 secondi e a un massimo di 2.147.483.647 secondi (hello intervallo massimo conforme con [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), consentendo il valore di hello toochoose che bilancia meglio alle esigenze dell'applicazione hello.

## <a name="pricing"></a>Prezzi

Per informazioni sui prezzi, vedere [Prezzi per Gestione traffico](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>domande frequenti

Per le domande frequenti su Gestione traffico, vedere le [domande frequenti su Gestione traffico](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sul [monitoraggio degli endpoint e sul failover automatico](traffic-manager-monitoring.md)di Gestione traffico.

Altre informazioni sui [metodi di routing](traffic-manager-routing-methods.md)di Gestione traffico.

Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

