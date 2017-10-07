---
title: aaaIntroduction tooAzure Gateway applicazione | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica del servizio Gateway applicazione hello per il bilanciamento del carico layer 7, tra cui le dimensioni di gateway, caricare il bilanciamento del carico, basato su cookie di affinità di sessione HTTP e offload SSL."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Panoramica del gateway applicazione

Il gateway applicazione di Microsoft Azure è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller) e varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione. Consente ai clienti la produttività di toooptimize web farm ripartendo gateway toohello di terminazione di CPU con utilizzo intensivo SSL applicazione. Fornisce inoltre altre funzionalità di routing layer 7 tra cui la distribuzione round robin di traffico in ingresso, l'affinità di sessione basato su cookie, il routing basato sul percorso URL e hello possibilità toohost più siti Web protetti da un singolo Gateway applicazione. Firewall applicazione web (WAF) viene inoltre fornito come parte del gateway applicazione hello WAF SKU. Fornisce una protezione di applicazioni tooweb vulnerabilità web e gli attacchi comuni. Il gateway applicazione può essere configurato come gateway con connessione Internet, come gateway solo interno o come una combinazione di queste due opzioni. 

![scenario](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Funzionalità

Gateway applicazione fornisce attualmente hello seguenti funzionalità:


* **[Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)**  -hello web application firewall (WAF) in Gateway applicazione Azure protegge le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione.
* **Bilanciamento del carico HTTP** : il gateway applicazione fornisce il bilanciamento del carico round robin. Il bilanciamento del carico viene eseguito al livello 7 e viene usato solo per il traffico HTTP(S).
* **Affinità di sessione basato su cookie** -funzionalità di affinità di sessione basato su cookie hello è utile quando si desidera tookeep una sessione utente in hello stesso back-end. L'utilizzo di cookie di gestito dal gateway, Gateway applicazione hello è toodirect in grado di traffico successive da un toohello sessione utente stesso back-end per l'elaborazione. Questa funzionalità è importante nei casi in cui lo stato della sessione salvato localmente sul server back-end hello per una sessione utente.
* **[Offload Sockets Layer (SSL) protetta](application-gateway-ssl-arm.md)**  -questa funzionalità accetta attività dispendiose di hello di decrittografare il traffico HTTPS disattivare i server web. Dal carattere di terminazione hello connessione SSL al Gateway applicazione hello e l'inoltro dei server di toohello richiesta hello non crittografato, server web hello è unburdened per la decrittografia.  Gateway applicazione crittografa nuovamente risposta hello prima di inviarlo client toohello indietro. Questa funzionalità è utile negli scenari in cui si trova hello back-end in hello stesso protetti rete virtuale come hello Gateway applicazione in Azure.
* **[Terminare tooEnd SSL](application-gateway-backend-ssl.md)**  -supporta Gateway applicazione termina tooend la crittografia del traffico. Gateway applicazione esegue questa operazione terminerà hello di connessione SSL al gateway applicazione hello. gateway Hello Applica regole di routing hello traffico toohello, crittografare nuovamente i pacchetti hello e inoltra hello pacchetto toohello back-end appropriati in base alle regole di routing hello definite. Le risposte dal server web hello attraversa hello stessa procedura adottata toohello back-end utente.
* **[Il routing del contenuto basato su URL](application-gateway-url-route-overview.md)**  -questa funzionalità fornisce funzionalità di hello toouse diversi server di back-end per il traffico diverso. Traffico per una cartella nel server web hello o per una rete CDN potrebbe essere diverso tooa indirizzato back-end. Questa funzionalità riduce il carico non necessario nei back-end che non gestiscono contenuto specifico.
* **[Routing multisito](application-gateway-multi-site-overview.md)**  -consente di gateway applicazione per tooconsolidate backup too20 siti Web su un gateway singola applicazione.
* **[Supporto WebSocket](application-gateway-websocket.md)**  -un'altra grande funzionalità di Gateway applicazione è il supporto nativo di hello per Websocket.
* **[Il monitoraggio dello stato](application-gateway-probe-overview.md)**  -gateway applicazione fornisce probe di integrità predefinito personalizzato e monitoraggio delle risorse di back-end toomonitor per scenari più specifici.
* **[Criteri SSL e crittografie](application-gateway-ssl-policy-overview.md)**  : questa funzionalità consente hello versioni del protocollo SSL toolimit hello e gruppi che sono supportati e hello ordine in cui vengono elaborati gli algoritmi di crittografia hello.
* **[Richiesta di reindirizzamento](application-gateway-redirect-overview.md)**  -questa funzionalità fornisce il listener HTTPS tooan le richieste di hello funzionalità tooredirect HTTP.
* **[Supporto di back-end multi-tenant](application-gateway-web-app-overview.md)**: il gateway applicazione supporta la configurazione di servizi back-end multi-tenant, come App Web di Azure e il gateway API, come membri del pool back-end. 
* **[Diagnostica avanzata](application-gateway-diagnostics.md)**: il gateway applicazione fornisce i log di diagnostica e accesso completi. I registri firewall sono disponibili per le risorse del gateway applicazione con WAF abilitato.

## <a name="benefits"></a>Vantaggi

Il gateway applicazione è utile per:

* Le applicazioni che richiedono le richieste da hello stesso client o utente della sessione tooreach hello stessa macchina virtuale back-end. ad esempio applicazioni carrello acquisti e server di posta Web.
* Rimozione del sovraccarico della terminazione SSL per le server farm Web.
* Applicazioni, ad esempio una rete di distribuzione del contenuto, che richiede più le richieste HTTP su hello stesso toobe di connessione TCP a esecuzione prolungata indirizzati o server back-end toodifferent con bilanciamento di carico.
* Applicazioni che supportano il traffico WebSocket
* Protezione delle applicazioni Web dai comuni attacchi basati sul Web, come attacchi SQL injection, attacchi di scripting intersito e hijack delle sessioni.
* Distribuzione logica del traffico in base a diversi criteri di routing, ad esempio percorso dell'URL o intestazioni del dominio.

È completamente gestito in Azure e offre scalabilità e disponibilità elevata, oltre a un set completo di funzionalità di registrazione e diagnostica che ne migliorano la gestibilità. Quando si crea un gateway applicazione, un endpoint (indirizzo VIP o IP ILB interno) viene associato e usato per il traffico di rete in ingresso. Questo indirizzo VIP o ILB IP viene fornito dal bilanciamento del carico di Azure a livello di trasporto hello (TCP/UDP) e tutti traffico di rete da gateway di applicazione toohello con bilanciamento carico di istanze di lavoro. Hello gateway applicazione quindi route hello traffico HTTP/HTTPS in base alla relativa configurazione, se si tratta di una macchina virtuale, servizio cloud, interno o un indirizzo IP esterno.

Gateway applicazione bilanciamento del carico come un servizio gestito di Azure consente di hello provisioning di un bilanciamento del carico layer 7 dietro il bilanciamento del carico di hello Azure software. Gestione traffico può essere scenario hello toocomplete utilizzato, come illustrato nella seguente immagine, in cui gestione traffico fornisce il reindirizzamento e la disponibilità del traffico di risorse di gateway di toomultiple dell'applicazione in diverse aree geografiche, mentre gateway applicazione fornisce hello tra l'area livello 7 il bilanciamento del carico. Un esempio di questo scenario è reperibile in: [tramite bilanciamento del carico servizi in cloud di Azure hello](../traffic-manager/traffic-manager-load-balancing-azure.md)

![Scenario di Gestione traffico e gateway applicazione](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Istanze e dimensioni del gateway

Il servizio Gateway applicazione è attualmente disponibile in tre dimensioni: **Small**, **Medium** e **Large**. Le dimensioni delle istanze piccole sono destinate a scenari di sviluppo e test.

È possibile creare i gateway applicazione too50 per sottoscrizione e il gateway di ogni applicazione può contenere istanze too10. Ogni gateway applicazione può essere costituito da 20 listener HTTP. Per un elenco completo dei limiti del gateway applicazione, vedere i [limiti del servizio Gateway applicazione](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits).

Hello nella tabella seguente viene mostrata una velocità effettiva delle prestazioni medie per ogni istanza di gateway applicazione con offload SSL abilitato:

| Risposta della pagina di back-end | Small | Media | Large |
| --- | --- | --- | --- |
| 6K |7,5 Mbps |13 Mbps |50 Mbps |
| 100.000 |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> Questi valori sono indicazioni approssimative della velocità effettiva di un gateway applicazione. velocità effettiva di Hello dipende vari dettagli di ambiente, ad esempio la dimensione di pagina Media, percorso delle istanze di back-end e tempo di elaborazione tooserve una pagina. Per dati esatti sulle prestazioni, è consigliabile eseguire propri test. Questi valori vengono forniti solo come indicazioni per la pianificazione della capacità.

## <a name="health-monitoring"></a>Monitoraggio dell’integrità

Gateway applicazione Azure esegue automaticamente di monitoraggio dello stato di hello di istanze di back-end hello tramite probe di integrità di base o personalizzato. Tramite probe di integrità, assicura che l'host solo integro rispondere tootraffic. Per altre informazioni, vedere [Panoramica del monitoraggio dell'integrità del gateway applicazione](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Configurazione e gestione

Quando viene configurato, il gateway applicazione può usare per l'endpoint un IP pubblico, un IP privato o entrambi. Il gateway applicazione viene configurato in una propria subnet all'interno di una rete virtuale. subnet Hello creati o utilizzati per il gateway applicazione non può contenere eventuali altri tipi di risorse, hello solo le risorse che sono consentite nella subnet hello sono altri gateway applicazione. le risorse di back-end, server di back-end hello possono essere contenute all'interno di una subnet diversa in hello toosecure stessa rete virtuale come gateway applicazione hello. Questa subnet che non necessario per le applicazioni back-end hello. Come gateway applicazione hello può raggiungere l'indirizzo ip di hello, gateway applicazione è in grado di tooprovide funzionalità di ADC per i server back-end hello. 

È possibile creare e gestire un gateway applicazione usando API REST, cmdlet di PowerShell, l'interfaccia della riga di comando di Azure o il [portale di Azure](https://portal.azure.com/). Per ulteriori domande sul gateway applicazione visitare [domande frequenti di Gateway applicazione](application-gateway-faq.md) tooview un elenco di comuni domande frequenti.

## <a name="pricing"></a>Prezzi

I prezzi sono basati su una tariffa oraria per istanza del gateway e una tariffa di elaborazione dei dati. All'ora gateway prezzi per hello WAF SKU è diverso da spese SKU Standard. Per informazioni sui prezzi, vedere i [dettagli sui prezzi del gateway applicazione](https://azure.microsoft.com/pricing/details/application-gateway/). L'elaborazione dati rimangono addebiti hello stesso.

## <a name="faq"></a>domande frequenti

Per le domande frequenti sul gateway applicazione, vedere [Domande frequenti sul gateway applicazione](application-gateway-faq.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver imparare gateway applicazione, è possibile [creare un gateway applicazione](application-gateway-create-gateway-portal.md) oppure è possibile [creare un gateway applicazione offload SSL](application-gateway-ssl-arm.md) connessioni HTTPS tooload saldo.

toolearn come toocreate un gateway applicazione utilizzando l'URL di routing basato sul contenuto, andare troppo[creare un gateway applicazione utilizzando il routing basato su URL](application-gateway-create-url-route-arm-ps.md) per ulteriori informazioni.

toolearn su alcuni dei hello altre chiavi rete funzionalità di Azure, vedere [rete Azure](../networking/networking-overview.md).
