---
title: aaaAzure Traffic Manager - domande frequenti | Documenti Microsoft
description: In questo articolo vengono fornite le risposte toofrequently domande frequenti sulla gestione traffico
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
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Domande frequenti (FAQ) su Gestione traffico

## <a name="traffic-manager-basics"></a>Fondamenti di Gestione traffico

### <a name="what-ip-address-does-traffic-manager-use"></a>Quale indirizzo IP viene usato da Gestione traffico?

Come spiegato in [come funziona la gestione traffico](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), gestione traffico opera a livello DNS hello. Invia le risposte DNS del servizio appropriato toodirect client toohello endpoint. I client quindi connettersi endpoint del servizio toohello direttamente, non tramite Traffic Manager.

Di conseguenza, gestione traffico non fornisce un endpoint o l'indirizzo IP per i client tooconnect per. Pertanto, se si desidera l'indirizzo IP statico per il servizio, che deve essere configurato nel servizio di hello, non in Traffic Manager.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Gestione traffico supporta sessioni "permanenti"?

Come spiegato in [come funziona la gestione traffico](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), gestione traffico opera a livello DNS hello. Usa endpoint di servizio appropriato toohello DNS risposte toodirect client. I client si connettono endpoint del servizio toohello direttamente, non tramite Traffic Manager. Pertanto, gestione traffico non vedere il traffico HTTP hello tra hello client e server di hello.

Inoltre, indirizzo IP di origine hello di query DNS hello ricevuti da Gestione traffico appartiene il servizio DNS ricorsivo toohello, non client di hello. Di conseguenza, gestione traffico non contiene modo tootrack singoli client e non può implementare 'sticky' sessioni. Questa limitazione è comune tooall DNS il traffico basato su sistemi di gestione e non è specifico tooTraffic Manager.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Quando si usa Gestione traffico, viene visualizzato un errore HTTP. Perché?

Come spiegato in [come funziona la gestione traffico](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), gestione traffico opera a livello DNS hello. Usa endpoint di servizio appropriato toohello DNS risposte toodirect client. I client quindi connettersi endpoint del servizio toohello direttamente, non tramite Traffic Manager. Gestione traffico non vede il traffico HTTP tra client e server. Ogni errore HTTP visualizzato proviene quindi dall'applicazione. Per l'applicazione hello client tooconnect toohello avere completato tutti i passaggi di risoluzione DNS. Che include qualsiasi interazione con gestione traffico per il flusso del traffico dell'applicazione hello.

Ulteriori indagini pertanto è consigliabile concentrarsi sull'applicazione hello.

intestazione host Hello HTTP inviata dal browser del client hello è l'origine più comune di hello dei problemi. Assicurarsi che un'applicazione hello sia l'intestazione host corretto di hello tooaccept configurato per il nome di dominio hello in uso. Per gli endpoint utilizzando hello servizio App di Azure, vedere [configurazione di un nome di dominio personalizzato per un'app web in Azure App Service tramite Traffic Manager](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>Che cos'è l'impatto sulle prestazioni hello tramite Gestione traffico?

Come spiegato in [come funziona la gestione traffico](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), gestione traffico opera a livello DNS hello. Poiché i client si connettono direttamente gli endpoint del servizio tooyour, non sussiste alcun impatto sulle prestazioni sostenuta quando si utilizza Traffic Manager dopo aver stabilito la connessione di hello.

Poiché Traffic Manager si integra con le applicazioni hello livello DNS, è necessario un toobe di ricerca DNS aggiuntivi inseriti hello catena di risoluzione DNS. impatto di Hello di Traffic Manager nel tempo di risoluzione DNS è minimo. Gestione traffico utilizza una rete globale di server dei nomi e [anycast](https://en.wikipedia.org/wiki/Anycast) rete tooensure DNS query vengono eseguite sempre toohello indirizzato server dei nomi disponibile più vicino. Inoltre, la memorizzazione nella cache delle risposte DNS ovvero hello DNS una latenza aggiuntiva sostenuta tramite Traffic Manager si applica solo tooa frazione di sessioni.

Hello prestazioni metodo instrada il traffico endpoint disponibile più vicino toohello. risultato Hello è tale hello impatto sulle prestazioni complessive associata a questo metodo dovrebbe essere minimo. Un aumento della latenza di DNS deve essere con offset inferiore endpoint toohello latenza di rete.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Quali protocolli di applicazione possono essere usati con Gestione traffico?

Come spiegato in [come funziona la gestione traffico](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), gestione traffico opera a livello DNS hello. Al termine di ricerca DNS hello, i client si connettono endpoint applicazione toohello direttamente, non tramite Traffic Manager. Pertanto, connessione hello è possibile utilizzare qualsiasi protocollo di applicazione. Se si seleziona TCP come hello monitoraggio, gestione traffico del protocollo il monitoraggio dello stato di endpoint può essere eseguito senza utilizzando qualsiasi protocollo di applicazione. Se si sceglie di integrità hello toohave verificata mediante un protocollo di applicazione, è necessario endpoint hello toobe toorespond in grado di tooeither HTTP o HTTPS GET richieste.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>È possibile usare Gestione traffico con un nome di dominio di tipo "naked" (senza www)?

No. standard DNS Hello non consente di limitare CNAME tooco-esiste con altri record DNS di hello stesso nome. contiene sempre due record DNS esistenti; Hello vertice o radice di una zona DNS Hello record SOA e hello autorevole NS. Ciò significa che un record CNAME non è possibile creare al vertice zona hello senza violare gli standard DNS hello.

Gestione traffico richiede un nome DNS di DNS CNAME toomap record hello personale. Ad esempio, si esegue il mapping di www.contoso.com toohello Traffic Manager profilo DNS nome contoso.trafficmanager.net. Inoltre, hello profilo di gestione traffico restituisce un secondo tooindicate DNS CNAME quale endpoint hello client deve connettersi.

toowork questo problema, è consigliabile utilizzare un traffico di toodirect reindirizzamento HTTP da hello naked URL nome di dominio tooa diversi, che è quindi possibile usare Gestione traffico. Ad esempio, hello naked dominio 'contoso.com' possibile reindirizzare gli utenti toohello CNAME 'www.contoso.com' che punta toohello nome DNS di Traffic Manager.

Il supporto completo per i domini naked in Gestione traffico è riportato nel backlog delle funzionalità. È possibile registrare il supporto per questa funzionalità [votandolo sul sito dei commenti della community](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Gestione traffico considera indirizzo di subnet hello client durante la gestione delle query DNS? 
No, attualmente gestione traffico considera solo hello indirizzo IP di origine di query DNS hello riceve, che in genere è l'indirizzo IP hello del resolver DNS hello, quando si eseguono ricerche per i metodi di routing geografico e le prestazioni.  
In particolare, [RFC 7871 – Subnet Client nelle query DNS](https://tools.ietf.org/html/rfc7871) che fornisce un [meccanismo di estensione per il DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) che è possibile passare all'indirizzo di subnet hello client da sistemi di risoluzione che lo supportano, tooDNS server è attualmente non supportato in Traffic Manager. È possibile registrare il supporto per la richiesta di questa funzionalità sul [sito di commenti e suggerimenti della community](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>Cos'è la durata TTL del DNS e che impatto ha sugli utenti?

Quando una query DNS inserita per gestione traffico, imposta un valore in risposta hello chiamato time-to-live (TTL). Questo valore, la cui unità è espresso in secondi, indica ai resolver tooDNS a valle in quanto tempo toocache questa risposta. Mentre i resolver DNS non sono garantiti toocache questo risultato, la memorizzazione nella cache consente loro toorespond tooany le query successive off cache di hello cercarli tooTraffic i server DNS di gestione. Ciò si verifica nelle risposte hello come indicato di seguito:
- una durata maggiore riduce il numero di hello di query che accedono hello server DNS di Traffic Manager, che è possibile ridurre il costo di hello per un cliente, poiché il numero di query gestite è un utilizzo fatturabile.
- una durata superiore possa potenzialmente ridurre hello tempi toodo una ricerca DNS.
- una durata superiore significa anche che i dati non rifletteranno le informazioni di integrità più recente hello ottenuto tramite i relativi agenti eseguiranno il sondaggio Traffic Manager.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Modalità di alto o basso è possibile impostare hello durata (TTL) per le risposte di gestione traffico?

È possibile impostare, in una per ogni livello di profilo, hello toobe TTL DNS come minimo pari a 0 secondi e a un massimo di 2.147.483.647 secondi (hello intervallo massimo conforme con [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). Una durata pari a 0 indica che ai resolver DNS a valle non memorizzati nella cache le risposte alle query e tutte le query sono previsti i server DNS di gestione traffico hello tooreach per la risoluzione.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Metodi geografico di routing del traffico di Gestione traffico

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Quali sono alcuni casi di uso in cui il routing geografico è utile? 
Il tipo di routing geografico utilizzabile in qualsiasi scenario in cui un cliente di Azure deve toodistinguish agli utenti in base alle aree geografiche. Ad esempio, Usa metodo di routing del traffico geografica hello, è possibile assegnare agli utenti di aree specifiche un'esperienza utente diverso rispetto a quelle di altre regioni. Un altro esempio è la necessità di garantire la conformità con requisiti dei dati locali che richiedono di servire gli utenti di una determinata area solo con gli endpoint di tale area.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Quali sono le aree di hello supportate da Gestione traffico per il routing geografica? 
gerarchia di paese/area geografica Hello utilizzato da Gestione traffico è reperibile [qui](traffic-manager-geographic-regions.md). Durante questa pagina viene mantenuta aggiornata con tutte le modifiche, è possibile recuperare anche a livello di codice hello stesse informazioni tramite hello [REST API di gestione traffico di Azure](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>In che modo Gestione traffico determina da dove un utente sta eseguendo una query? 
Gestione traffico esamina hello IP di origine della query hello (è molto probabile che un sistema di risoluzione DNS locale esegue una query hello per conto di utente hello) e utilizza un'interno IP tooregion toodetermine hello posizione della mappa. Questa mappa viene aggiornata a un tooaccount regolarmente per la modifica in hello internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>È garantito che Gestione traffico consente di scegliere correttamente hello esatta area geografica dell'utente hello in ogni caso?
No, gestione traffico non è possibile garantire tale area geografica hello è dedurre dall'indirizzo IP di origine hello di una query DNS corrisponderà sempre il percorso dell'utente toohello scadenza toohello seguenti motivi: 

- In primo luogo, come descritto nella domanda precedente hello, hello è quello di un sistema di risoluzione DNS eseguendo la ricerca hello per conto di utente hello indirizzo IP di origine. Mentre l'area geografica del sistema di risoluzione DNS hello hello è un proxy valido per area geografica dell'utente hello hello, può anche essere diverso a seconda footprint hello del servizio di sistema di risoluzione DNS hello e hello specifico DNS servizio resolver che ha scelto un cliente toouse. Ad esempio, un cliente che si trova in Malaysia possibile specificare in uso di impostazioni del dispositivo in uso un servizio di sistema di risoluzione DNS potrebbe ottenere i cui server DNS Singapore prelevato toohandle risoluzioni query hello per tale utente o dispositivo. In caso, gestione traffico può visualizzare solo IP del resolver hello indirizzo che corrisponde toohello percorso Singapore. Vedere anche hello precedenti domande frequenti relative a indirizzo subnet del client supportano in questa pagina.

- In secondo luogo, gestione traffico Usa una mappa interna toodo hello conversione degli indirizzi IP toogeographic area. Anche se questa mappa viene convalidata e aggiornata in un tooincrease regolarmente la precisione e l'account per natura dell'evoluzione hello hello internet, ancora hello possibilità è che le informazioni non sono una rappresentazione esatta di area geografica hello di tutti indirizzi IP Hello.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Un toobe necessità di endpoint situati fisicamente in hello stessa area hello uno configurate per il routing geografica? 
No, il percorso di hello dell'endpoint hello impone senza restrizioni in cui le regioni possono essere mappate tooit. Ad esempio, un endpoint nell'area Stati Uniti centro Azure può avere tutti gli utenti da tooit India indirizzato.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>È possibile assegnare aree geografiche tooendpoints in un profilo che non è configurato toodo geografica routing? 

Sì, metodo di routing hello di un profilo non è geografico, è possibile utilizzare hello [REST API di gestione traffico di Azure](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign tooendpoints di aree geografiche in quel profilo. Nel caso di hello di profili di tipo routing non geografici, questa configurazione viene ignorata. Se si modifica tale profilo toogeographic routing tipo in un secondo momento, gestione traffico può utilizzare tali mapping.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Motivo per cui viene visualizzato un errore durante il metodo di routing hello toochange di un tooGeographic profilo esistente?

Tutti gli endpoint hello in un profilo con il routing geografica necessario toohave tooit il mapping di almeno un'area. tooconvert un tipo di routing toogeographic profilo esistente, è necessario innanzitutto tooassociate aree geografiche tooall relativi endpoint utilizzando hello [REST API di gestione traffico di Azure](https://docs.microsoft.com/rest/api/trafficmanager/) prima di modificare hello routing digitare toogeographic. Se tramite portale, eliminare innanzitutto endpoint hello, Modifica metodo di routing di hello profilo toogeographic hello e quindi aggiungere gli endpoint hello insieme ai relativi mapping di area geografica. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Perché è decisamente consigliato che i clienti creino profili nidificati anziché endpoint in un profilo con il routing geografico abilitato? 

Un'area è possibile assegnare uno tooonly endpoint all'interno di un profilo se relativo utilizzando il tipo di routing geografico. Se tale endpoint non è un tipo annidato con tooit profilo collegato un figlio, se tale endpoint sarà non integro, Traffic Manager continua toosend traffico tooit dall'alternativa hello di invio non che tutto il traffico non è di meglio. Gestione traffico non non failover tooanother endpoint, anche quando regione hello assegnata un "padre" dell'area di hello toohello endpoint che è stato danneggiato (ad esempio, se un endpoint che include l'area Spagna diventa non integro, che verranno tooanother di failover non assegnato endpoint che dispone di hello area Europa assegnato tooit). Questa operazione viene eseguita tooensure che l'installazione di gestione traffico equivalenti hello geografiche che dispone di un cliente nel proprio profilo. tooget hello vantaggio derivante dall'esecuzione del failover endpoint tooanother quando un endpoint diventa non integro, è consigliabile assegnare profili toonested con più endpoint all'interno di esso anziché singoli endpoint che aree geografiche. In questo modo, se un endpoint hello annidato figlio profilo avrà esito negativo, il traffico può failover tooanother endpoint all'interno di hello stesso nidificato profilo figlio.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Esistono restrizioni sulla versione di hello API che supporta questo tipo di routing?

Sì, solo la versione API 2017-03-01 e supporta più recente hello geografico tipo di routing. Le versioni precedenti di API non possono essere toocreated utilizzati profili di tipo di routing geografico oppure assegnare tooendpoints aree geografiche. Se una versione precedente di API profili tooretrieve utilizzato da una sottoscrizione di Azure, qualsiasi profilo di tipo di routing geografico non viene restituito. Inoltre, quando si usano versioni precedenti dell'API, tutti i profili restituiti che hanno endpoint con un'area geografica assegnata non mostreranno l'area geografica assegnata.



## <a name="traffic-manager-endpoints"></a>Endpoint di Gestione traffico

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>È possibile usare Gestione traffico con endpoint di più sottoscrizioni?

L'uso di endpoint di più sottoscrizioni non è possibile con app Web di Azure. Per le app Web di Azure è necessario che ogni nome di dominio personalizzato usato con app Web venga usato solo all'interno di una singola sottoscrizione. Non è possibile toouse delle App Web più sottoscrizioni con hello stesso nome di dominio.

Per altri tipi di endpoint, è possibile toouse gestione traffico con gli endpoint da più di una sottoscrizione. In Gestione risorse di qualsiasi sottoscrizione è possibile aggiungere endpoint tooTraffic Manager, purché persona hello configurazione profilo di Traffic Manager hello abbia accesso in lettura toohello endpoint. Queste autorizzazioni possono essere concesse tramite il [controllo di accesso in base al ruolo di Azure Resource Manager](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>È possibile usare Gestione traffico con slot di "staging" del servizio cloud?

Sì. Gli slot di "staging" del servizio cloud possono essere configurati come endpoint esterni in Gestione traffico. Controlli di integrità sono comunque addebitato con frequenza di hello gli endpoint di Azure. Poiché il tipo di endpoint esterni hello è in uso, servizio sottostante toohello di modifiche non vengono rilevate automaticamente. Con endpoint esterni, gestione traffico non è possibile rilevare quando hello servizio Cloud viene arrestata o eliminata. Pertanto, hello Traffic Manager continua fatturazione per i controlli di integrità, fino a endpoint hello è disabilitato o eliminato.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Gestione traffico supporta endpoint IPv6?

Attualmente Gestione traffico non fornisce server dei nomi indirizzabili tramite IPv6. Tuttavia, gestione traffico può comunque essere utilizzato dai client di IPv6 tooIPv6 endpoint di connessione. Non esegue un client DNS richiede direttamente tooTraffic Manager. Client hello utilizza invece un servizio DNS ricorsivo. Un client solo IPv6 invia le richieste di servizio DNS ricorsivo toohello tramite IPv6. Servizio ricorsiva hello deve essere in grado di toocontact server dei nomi Traffic Manager hello utilizzo di IPv4.

Gestione traffico risponde con il nome DNS hello dell'endpoint hello. endpoint toosupport IPv6, un AAAA DNS record puntamento hello endpoint DNS nome toohello IPv6 indirizzo deve esistere. I controlli di integrità di Gestione traffico supportano soltanto gli indirizzi IPv4. servizio Hello deve endpoint tooexpose IPv4 hello stesso nome DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>È possibile usare Gestione traffico con più App Web in hello stessa regione?

In genere, gestione traffico è toodirect utilizzato traffico tooapplications distribuiti in aree diverse. Tuttavia, può anche essere utilizzato in un'applicazione dispone di più di una distribuzione in hello stessa area. Hello endpoint Azure Traffic Manager non consente più di un endpoint di App Web da hello stessa regione di Azure toobe aggiunto toohello stesso profilo di Traffic Manager.

##  <a name="traffic-manager-endpoint-monitoring"></a>Monitoraggio degli endpoint di Gestione traffico

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>È Gestione traffico resilienti tooAzure errori area?

Gestione traffico è un componente fondamentale di recapito di hello delle applicazioni a disponibilità elevata in Azure.
toodeliver la disponibilità elevata, gestione traffico deve avere un livello estremamente elevato di disponibilità ed essere resilienti tooregional errore.

Per impostazione predefinita, i componenti di gestione traffico sono resilienti tooa errore completo di qualsiasi area di Azure. Questa capacità di recupero si applica a componenti di gestione traffico tooall: server dei nomi DNS hello, hello API, il livello di archiviazione hello e servizio di monitoraggio degli endpoint hello.

In caso di guasto di hello di un'interruzione di un'intera regione di Azure, gestione traffico è in genere toofunction toocontinue previsto. Le applicazioni distribuite in più aree di Azure possono basarsi su gestione traffico toodirect istanza disponibile di traffico tooan della propria applicazione.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Influenza di gestione traffico scelta hello del percorso del gruppo di risorse

Gestione traffico è un singolo servizio globale. Non è a livello di area. scelta di Hello del percorso del gruppo di risorse non rende i profili di gestione tooTraffic alcuna differenza distribuiti in tale gruppo di risorse.

Gestione risorse di Azure richiede toospecify gruppi di risorse tutti una posizione, che determina il percorso predefinito hello per le risorse distribuite in tale gruppo di risorse. Quando si crea un profilo di Gestione traffico, viene creato in un gruppo di risorse. Tutti i profili di Traffic Manager utilizzare **globale** come posizione, eseguire l'override hello risorsa gruppo predefinito.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Determinazione dello stato corrente di hello di ogni endpoint

Hello monitoraggio dello stato di ogni endpoint corrente, in aggiunta toohello profilo complessivo, viene visualizzato nel hello portale di Azure. Queste informazioni sono anche disponibili tramite hello traffico monitoraggio [API REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [i cmdlet di PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), e [CLI di Azure multipiattaforma](../cli-install-nodejs.md).

Azure non fornisce informazioni cronologiche sull'endpoint ultimi avvisi integrità o hello tooraise possibilità sull'integrità tooendpoint le modifiche.

### <a name="can-i-monitor-https-endpoints"></a>È possibile monitorare gli endpoint HTTPS?

Sì. Gestione traffico supporta il probing su HTTPS. Configurare **HTTPS** come protocollo di hello nella configurazione del monitoraggio hello.

Gestione traffico non prevede alcuna convalida di certificati, tra cui:

* I certificati sul lato server non vengono convalidati
* I certificati SNI sul lato server non sono supportati
* I certificati client non sono supportati

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>È possibile usare Gestione traffico anche se l'applicazione non supporta HTTP o HTTPS?

Sì. È possibile specificare TCP come hello monitoraggio protocollo e gestione traffico è possibile avviare una connessione TCP e attendere una risposta dall'endpoint hello. Se la richiesta di connessione toohello con una connessione di hello tooestablish risposta come endpoint hello, entro il timeout di hello periodo, quindi tale endpoint è contrassegnato come integro.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>Le risposte specifiche sono richieste dall'endpoint hello quando si utilizza TCP monitoraggio?

Quando viene utilizzato TCP monitoraggio, Traffic Manager inizia un handshake TCP a tre vie inviando un SYN richiesta tooendpoint in hello porta specificata. Quindi attende per un periodo di tempo (come specificato nelle impostazioni di timeout hello) per una risposta dall'endpoint hello. Se l'endpoint hello risponde toohello SYN richiesta con una risposta SYN ACK entro il periodo di timeout hello specificato nelle impostazioni di monitoraggio hello, quindi tale endpoint viene considerato integro. Se si riceve risposta SYN ACK hello, hello Traffic Manager Reimposta connessione hello rispondendo con un RST.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Con quale velocità Gestione traffico sposta gli utenti da un endpoint considerato non integro?

Traffic Manager offre più impostazioni che consentono di comportamento del failover toocontrol hello del profilo di gestione traffico come indicato di seguito:
- è possibile specificare che hello Traffic Manager probe hello endpoint più frequentemente impostando hello intervallo di probe a 10 secondi. Ciò assicura che un eventuale endpoint non integro venga rilevato il prima possibile. 
- è possibile specificare la durata del timeout toowait prima di una richiesta di controllo di integrità (valore di timeout minimo è 5 sec).
- è possibile specificare il numero di errori può verificarsi prima che l'endpoint di hello è contrassegnato come danneggiato. Questo valore può essere minimo pari a 0, nella quale endpoint hello case è contrassegnato non integro, non appena si verifica un errore hello controllo di integrità del primo. Tuttavia, utilizzando il valore minimo hello 0 per il numero di hello, che è consentito di errori può causare tooendpoints viene escluso dalla rotazione a causa di errori temporanei tooany che possono verificarsi in fase di hello del sondaggio.
- è possibile specificare hello time-to-live (TTL) per hello DNS risposta toobe minimo pari a 0. In questo modo è indica che ai resolver DNS non è possibile memorizzare nella cache la risposta hello e ogni nuova query Ottiene una risposta che incorpora informazioni più aggiornate sull'integrità di hello che hello Traffic Manager.

Utilizzando queste impostazioni, gestione traffico può fornire i failover meno di 10 secondi dopo che un endpoint diventa non integro e una query DNS viene effettuata profilo corrispondente hello.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Come specificare diverse impostazioni di monitoraggio per i diversi endpoint in un profilo?

Le impostazioni di monitoraggio di Gestione traffico sono configurate a livello di profilo. Se è necessario toouse un'impostazione diversa di monitoraggio per un solo endpoint, può essere eseguita con quell'endpoint come un [annidati profilo](traffic-manager-nested-profiles.md) le cui impostazioni di monitoraggio sono diversi dal profilo padre hello.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Quali intestazione host viene usata per i controlli di integrità degli endpoint?

Gestione traffico usa le intestazioni host nei controlli di integrità HTTP e HTTPS. intestazione host Hello usato da Gestione traffico è il nome di hello della destinazione di endpoint hello configurate nel profilo hello. Impossibile specificare un valore Hello utilizzato nell'intestazione host hello separatamente dalla proprietà di destinazione hello.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Quali sono gli indirizzi IP hello da cui hello controlli di integrità provengono?

Hello elenco seguente contiene gli indirizzi IP hello da cui gestione traffico controlli di integrità possono derivare. È possibile utilizzare questo elenco tooensure che le connessioni in ingresso da questi indirizzi IP consentite in hello endpoint toocheck lo stato di integrità.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Quanti endpoint toomy controlli di integrità è possibile prevedere da Gestione traffico?

numero di Hello di integrità di gestione traffico controlli raggiungere l'endpoint dipende dal seguente hello:
- valore impostato per l'intervallo di monitoraggio hello Hello (indica l'intervallo più piccolo più richieste per l'endpoint di destinazione in un determinato periodo di tempo).
- numero di Hello di percorsi da cui i controlli di integrità hello provengono (hello gli indirizzi IP da dove è possibile prevedere questi controlli è elencato nella precedente domande frequenti su hello).

## <a name="traffic-manager-nested-profiles"></a>Profili annidati di Gestione traffico

### <a name="how-do-i-configure-nested-profiles"></a>Come si configurano i profili nidificati?

Profili di gestione traffico nidificati possono essere configurati tramite Gestione risorse di Azure sia hello e hello classic API REST di Azure, i cmdlet PowerShell di Azure e i comandi CLI di Azure e multipiattaforma. Sono supportate anche tramite il portale di Azure nuova di hello. Non sono supportate nel portale classico hello.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>Quanti livelli di nidificazione supporta Gestione traffico?

È possibile nidificare i profili di too10 livelli. I "loop" non sono consentiti.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>È possibile combinare altri tipi di endpoint con i profili figlio annidati, in hello stesso profilo di gestione traffico?

Sì. Non esistono restrizioni sulla modalità di combinazione di tipi diversi di endpoint all'interno di un profilo.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Come modello di fatturazione hello è applicare per i profili nidificati?

L'uso di profili nidificati non ha alcun impatto negativo sui prezzi.

La fatturazione di Gestione traffico include due componenti: i controlli dell'integrità degli endpoint e milioni di query DNS.

* Controlli dell'integrità degli endpoint: non è previsto alcun addebito per un profilo figlio configurato come endpoint in un profilo padre. Monitoraggio degli endpoint hello nel profilo figlio hello viene fatturato in hello come di consueto.
* Query DNS: ogni query viene conteggiata una sola volta. Una query su un profilo padre che restituisce un endpoint da un profilo per bambini viene conteggiata a fronte profilo padre di hello solo.

Per informazioni dettagliate, vedere hello [pagina dei prezzi di Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>I profili nidificati influiscono sulle prestazioni?

No. Quando si usano i profili annidati non si verifica alcun impatto sulle prestazioni.

Server dei nomi di gestione traffico Hello attraversare gerarchia profilo hello internamente durante l'elaborazione di ogni query DNS. Un profilo di padre tooa query DNS può ricevere una risposta DNS con un endpoint da un profilo per bambini. Viene usato un singolo record CNAME, indipendentemente dal fatto che si usi un profilo singolo o profili annidati. Non è toocreate non è necessario un record CNAME per ciascun profilo nella gerarchia di hello.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>La modalità di calcolo integrità hello di un endpoint di tipo annidato in un profilo padre Traffic Manager

profilo padre Hello non esegue controlli di integrità sul figlio hello direttamente. Integrità hello degli endpoint del profilo figlio hello vengono invece utilizzati toocalculate hello integrità complessiva del profilo figlio hello. Queste informazioni viene propagate hello annidato profilo gerarchia toodetermine hello integrità dell'endpoint hello annidato. profilo padre Hello che utilizza questo toodetermine di integrità aggregato sia il traffico hello può essere figlio toohello diretto.

Hello nella tabella seguente descrive il comportamento di hello di Traffic Manager verifica integrità per un endpoint di tipo annidato.

| Stato di monitoraggio del profilo figlio | Stato di monitoraggio dell'endpoint padre | Note |
| --- | --- | --- |
| Disabilitato. profilo figlio Hello è stata disabilitata. |Arrestato |stato dell'endpoint padre Hello viene arrestato, non è stato disabilitato. stato Disabled Hello è riservato per indicare di aver disabilitato endpoint hello nel profilo padre hello. |
| Danneggiato. Almeno uno degli endpoint del profilo figlio è nello stato Danneggiato. |Online: numero di hello di Online endpoint nel profilo figlio hello è almeno hello valore dell'impostazione MinChildEndpoints.<BR>Verifica endpoint: numero di hello di endpoint con stato Online e nel profilo figlio hello è almeno hello valore dell'impostazione MinChildEndpoints.<BR>Danneggiato: negli altri casi. |Il traffico viene indirizzato tooan endpoint con stato verifica endpoint. Se l'impostazione MinChildEndpoints è troppo elevato, endpoint hello è sempre danneggiato. |
| Online. Almeno uno degli endpoint del profilo figlio è nello stato Online. Nessun endpoint è in stato danneggiato hello. |Vedere sopra. | |
| CheckingEndpoints. Almeno uno degli endpoint del profilo figlio è nello stato CheckingEndpoint. Nessun endpoint è nello stato Online o Danneggiato. |Come sopra. | |
| Inattivo. Tutti gli endpoint del profilo figlio sono nello stato Disabilitato o Arrestato oppure si tratta di un profilo senza endpoint. |Arrestato | |

## <a name="next-steps"></a>Passaggi successivi:
- Altre informazioni sul [monitoraggio degli endpoint e sul failover automatico](../traffic-manager/traffic-manager-monitoring.md)di Gestione traffico.
- Altre informazioni sui [metodi di routing](../traffic-manager/traffic-manager-routing-methods.md)di Gestione traffico.