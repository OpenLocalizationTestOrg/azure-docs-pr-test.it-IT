---
title: 'i metodi di routing del traffico aaaAzure Traffic Manager: | Documenti Microsoft'
description: In questo articolo consente di capire i metodi di routing del traffico diversi hello usati da Gestione traffico
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Metodi di routing di Gestione traffico

Azure Traffic Manager toodetermine metodi di routing del traffico supporta quattro modalità tooroute rete toohello di traffico diversi endpoint del servizio. Gestione traffico applica hello routing del traffico metodo tooeach query DNS che riceve. il metodo di routing del traffico Hello determina quale endpoint restituite nella risposta DNS hello.

In Gestione traffico sono disponibili quattro metodi di routing del traffico:

* **[Priorità](#priority):** selezionare **priorità** quando si desidera toouse un endpoint del servizio principale per tutto il traffico e fornire backup nel caso in cui hello primario o gli endpoint di backup hello non sono disponibili.
* **[Weighted](#weighted):** selezionare **Weighted** quando si desidera toodistribute traffico in un set di endpoint, ovvero in modo uniforme o tooweights secondo, che può essere definito.
* **[Prestazioni](#performance):** selezionare **prestazioni** quando sono disponibili endpoint in aree geografiche diverse e si desideri che gli utenti finali toouse hello endpoint "più vicino" in termini di latenza di rete più bassa hello.
* **[Geografico](#geographic):** selezionare **geografica** in modo che gli utenti sono endpoint toospecific diretto (Azure, esterna o Nested) in base alla quale posizione geografica le query DNS deriva da. Questo consente scenari di tooenable clienti Traffic Manager in cui è importante conoscere l'area geografica dell'utente e il routing in base che. Ne sono esempi la presenza di determinati requisiti sui dati, la localizzazione del contenuto e dell'esperienza dell'utente e la misurazione del traffico da aree diverse.

Tutti i profili di Gestione traffico includono il monitoraggio continuo dell'integrità degli endpoint e il failover automatico degli endpoint. Per altre informazioni, vedere [Informazioni sul monitoraggio di Gestione traffico](traffic-manager-monitoring.md). Un singolo profilo di Gestione traffico può usare un solo metodo di routing del traffico. È possibile selezionare in qualsiasi momento un metodo di routing del traffico diverso per il profilo. Le modifiche vengono applicate entro un minuto e non si verificano periodi di inattività. I metodi di routing del traffico possono essere combinati usando profili nidificati di Gestione traffico. La nidificazione consente più sofisticate e flessibile configurazioni di routing del traffico che soddisfano le esigenze di hello delle applicazioni più grandi e complesse. Per altre informazioni, vedere [nested Traffic Manager profiles](traffic-manager-nested-profiles.md)(Profili nidificati di Gestione traffico).

## <a name = "priority"></a>Metodo di routing del traffico Priorità

Un'organizzazione desidera spesso tooprovide affidabilità dei servizi di distribuendo uno o più servizi di backup nel caso in cui il servizio primario diventa inattivo. metodo di routing del traffico "Priority" Hello consente Azure i clienti tooeasily implementare questo pattern di failover.

![Metodo di routing del traffico "Priorità" di Gestione traffico di Azure][1]

profilo di gestione traffico Hello contiene un elenco con priorità degli endpoint del servizio. Per impostazione predefinita, verrà inviata endpoint (più alta priorità) di tutto il traffico toohello primario. Se l'endpoint primario hello non è disponibile, le route di Traffic Manager hello endpoint secondo toohello di traffico. Se entrambi gli endpoint primario e secondario hello non sono disponibili, hello del traffico toohello terzo, e così via. Disponibilità di endpoint hello è in base allo stato di hello configurato (abilitato o disabilitato) e hello monitoraggio degli endpoint in corso.

### <a name="configuring-endpoints"></a>Configurazione degli endpoint

Con Gestione risorse di Azure, configurare priorità di endpoint hello in modo esplicito utilizzando la proprietà 'priority' hello per ogni endpoint. Questa proprietà accetta un valore compreso tra 1 e 1000, dove i valori più bassi rappresentano una priorità più elevata. Gli endpoint non possono avere lo stesso valore di priorità. L'impostazione di proprietà hello è facoltativa. Se omessa, viene utilizzata una priorità predefinita in base a ordine degli endpoint hello.

##<a name = "weighted"></a>Metodo di routing del traffico Ponderato
metodo di routing del traffico 'Weighted' Hello consente il traffico toodistribute in modo uniforme o toouse un peso predefinito.

![Metodo di routing del traffico "Ponderato" di Gestione traffico di Azure][2]

Nell'hello ponderata routing del traffico (metodo), assegnare a un endpoint tooeach peso nella configurazione del profilo di Traffic Manager hello. peso Hello è un numero intero compreso tra 1 too1000. Questo parametro è facoltativo e, se omesso, viene usato il valore di peso predefinito "1".

Per ogni query DNS ricevuta, viene scelto un endpoint disponibile in modo casuale, probabilità di Hello della scelta di un endpoint si basa su un peso hello endpoint disponibili tooall. Utilizzando hello stesso peso tra tutti i risultati in una distribuzione del traffico anche gli endpoint. L'utilizzo di pesi superiori o inferiori in endpoint specifici provoca toobe tali endpoint ha restituito più o meno frequente nelle risposte DNS hello.

metodo Hello ponderato consente alcuni scenari utili:

* Aggiornamento graduale dell'applicazione: allocare una percentuale di nuovi endpoint di traffico tooroute tooa e aumentare gradualmente il traffico hello più tempo too100%.
* Applicazione migrazione tooAzure: creare un profilo con endpoint di Azure ed esterni. Modificare il peso di hello hello endpoint tooprefer hello nuovi endpoint di.
* Espansione del cloud per capacità aggiuntiva: espandere rapidamente una distribuzione locale nel cloud hello posizionandola dietro a un profilo di Traffic Manager. Quando è necessaria capacità aggiuntiva nel cloud hello, è possibile aggiungere o abilitare più endpoint e specificare la quantità di traffico passa tooeach endpoint.

Hello portale di gestione risorse di Azure supporta la configurazione di hello del routing del traffico ponderato.  È possibile configurare i pesi hello versioni di gestione risorse di Azure PowerShell e CLI hello API REST.

È importante toounderstand che le risposte DNS vengono memorizzate nella cache dai client e per i server DNS ricorsivo di hello che hello client utilizzano nomi DNS tooresolve. Questa memorizzazione ha un impatto sulle distribuzioni del traffico ponderate. Quando il numero di hello del client e server DNS ricorsivo è elevato, la distribuzione del traffico funziona come previsto. Tuttavia, se il numero di hello del client o server DNS ricorsivo è ridotto, la memorizzazione nella cache può distorcere significativamente la distribuzione del traffico hello.

I casi d'uso comuni in cui può verificarsi questa situazione includono:

* Ambienti di sviluppo e test
* Comunicazioni tra applicazioni
* Applicazioni destinate a una base utenti ristretta che condivide un'infrastruttura DNS ricorsiva comune, ad esempio i dipendenti di un'organizzazione che si connettono tramite proxy.

Questi effetti di memorizzazione nella cache DNS sono comuni tooall il traffico basato su DNS routing sistemi, non solo Traffic Manager di Azure. In alcuni casi, in modo esplicito la cancellazione della cache DNS hello possono fornire una soluzione alternativa. In altri casi, può essere più appropriato un metodo di routing del traffico alternativo.

## <a name = "performance"></a>Metodo di routing del traffico Prestazioni

Distribuzione di endpoint in due o più percorsi tra globo hello può migliorare la velocità di risposta hello di molte applicazioni dal routing del traffico toohello percorso tooyou "più vicino". il metodo di routing del traffico "Prestazioni" Hello fornisce questa funzionalità.

![Metodo di routing del traffico "Prestazioni" di Gestione traffico di Azure][3]

endpoint di Hello 'vicino' non è necessariamente più vicino in termini di distanza geografica. Al contrario, il metodo di routing del traffico "Prestazioni" hello determina endpoint più vicino hello misurazione della latenza di rete. Gestione traffico mantiene un tabella di latenza Internet tootrack hello tempo di round trip tra intervalli di indirizzi IP e ogni Data Center di Azure.

Traffic Manager cerca dall'indirizzo IP della richiesta DNS in ingresso hello nella tabella di latenza Internet hello hello origine. Gestione traffico sceglie un endpoint disponibile nel Data Center di Azure che presenta una latenza più bassa di hello per tale intervallo di indirizzi IP, quindi restituisce tale endpoint nella risposta DNS hello hello.

Come spiegato in [Modalità di funzionamento di Gestione traffico](traffic-manager-overview.md#how-traffic-manager-works), le query DNS non vengono ricevute direttamente dai client, Invece, le query DNS provengono da che hello client non siano toouse configurato il servizio DNS ricorsivo hello. Pertanto, hello IP indirizzo utilizzato toodetermine hello 'vicino' endpoint non è l'indirizzo IP del client hello, ma è hello di indirizzo IP del servizio DNS di hello ricorsiva. In pratica, questo indirizzo IP è un proxy valido per il client di hello.


Gestione traffico regolarmente gli aggiornamenti hello tooaccount Internet tabella della latenza delle modifiche in hello Internet globali e nuove aree di Azure. Tuttavia, le prestazioni dell'applicazione variano in base alle variazioni in tempo reale del carico tra hello Internet. Il routing del traffico "Prestazioni" non prende in considerazione il monitoraggio del carico su un determinato endpoint di servizio. Se un endpoint non è più disponibile, non viene incluso nelle risposte alle query DNS.


Toonote punti:

* Se il profilo contiene più endpoint in hello stessa regione di Azure, quindi Traffic Manager distribuisce il traffico in modo uniforme tra gli endpoint disponibili hello in tale area. Se si preferisce una distribuzione del traffico diversa all'interno di un'area, usare i [profili annidati di Gestione traffico](traffic-manager-nested-profiles.md).
* Se tutte abilitate endpoint più vicino hello regione di Azure sono ridotte, gestione traffico consente di spostare gli endpoint toohello traffico nell'area di Azure più vicino successivo hello. Se si desidera toodefine una sequenza di failover preferito, utilizzare [profili di gestione traffico nidificati](traffic-manager-nested-profiles.md).
* Quando si utilizza il metodo di routing del traffico delle prestazioni di hello con endpoint esterni o endpoint nidificato, è necessario posizione hello toospecify di tali endpoint. Scegliere la distribuzione tooyour di hello regione di Azure più vicina. I percorsi sono valori hello è supportati dalla tabella di latenza Internet hello.
* l'algoritmo Hello che sceglie endpoint hello è deterministica. Ripetere le query DNS da hello stesso client vengono indirizzate toohello stesso endpoint. Quando viaggiano, i client solitamente usano server DNS ricorsivi diversi, client di Hello può essere indirizzato tooa diversi endpoint. Routing può essere influenzato anche dal aggiornamenti toohello tabella di latenza Internet. Pertanto, hello prestazioni metodo di routing del traffico non garantisce che un client è sempre indirizzate toohello stesso endpoint.
* Quando viene modificato hello tabella di latenza Internet, è possibile notare che alcuni client diretto tooa diversi endpoint. Ciò riflette un routing più accurato in base ai dati di latenza correnti. Questi aggiornamenti sono l'accuratezza di hello toomaintain essenziale delle prestazioni-routing del traffico come hello che Internet in continua evoluzione.

## <a name = "geographic"></a>Metodo di routing del traffico Geografico

Profili di gestione traffico possono essere configurato toouse hello geografico metodo di routing in modo che gli utenti vengono indirizzati gli endpoint toospecific (Azure, esterna o Nested) in base quale posizione geografica le query DNS deriva da. Questo consente scenari di tooenable clienti Traffic Manager in cui è importante conoscere l'area geografica dell'utente e il routing in base che. Ne sono esempi la presenza di determinati requisiti sui dati, la localizzazione del contenuto e dell'esperienza dell'utente e la misurazione del traffico da aree diverse.
Quando un profilo è configurato per il routing geografico, ogni endpoint associato che è necessario un set di aree geografiche assegnate tooit toohave profilo. Un'area geografica può avere i seguenti livelli di granularità 
- Mondo: qualsiasi area
- Raggruppamento di aree: ad esempio Africa, Medio Oriente, Australia/Pacifico e così via. 
- Paese/area geografica: ad esempio Irlanda, Perù, Regione amministrativa speciale di Hong Kong e così via. 
- Stato/provincia: ad esempio USA-California, Australia-Queensland, Canada-Alberta e così via (nota: questo livello di granularità è supportato solo per gli stati e province di Australia, Canada, Regno Unito e Stati Uniti).

Quando un'area o un set di regioni viene assegnato tooan endpoint, tutte le richieste da tali aree Ottiene indirizzato endpoint toothat solo. Gestione traffico Usa indirizzo IP di origine hello di hello DNS query toodetermine hello area da cui un utente esegue una query da: si tratta in genere l'indirizzo IP hello del resolver DNS locali hello esecuzione query hello per conto di utente hello.  

![Metodo geografico di routing del traffico di Gestione traffico di Azure](./media/traffic-manager-routing-methods/geographic.png)

Gestione traffico legge l'indirizzo IP di origine hello di query DNS hello e decide quale area geografica è stato originato da. Cerca quindi toosee se è presente un endpoint che include questo tooit eseguito il mapping di area geografica. Questa ricerca viene avviata a livello di granularità più bassa hello (stato/provincia in cui è supportato, altrimenti a livello di hello paese/area geografica) e passa tutti modo hello al livello più alto toohello, ovvero di **World**. Hello trovata prima corrispondenza utilizzando questo attraversamento è designato come tooreturn endpoint hello in risposta alla query hello. In caso di corrispondenza con un endpoint di tipo nidificato, viene restituito un endpoint all'interno di tale profilo figlio, in base al suo metodo di routing. Hello punti seguenti è applicabili toothis comportamento:

- Quando il tipo di routing hello è geografico Routing, un'area geografica può essere mappata endpoint tooone solo in un profilo di Traffic Manager. Ciò garantisce che il routing degli utenti sia deterministico e i clienti possano abilitare scenari che richiedono limiti geografici non ambigui.
- Se area dell'utente viene mapping geografiche in due endpoint diversi, gestione traffico seleziona endpoint hello con granularità più bassa hello e non considera il routing delle richieste da tale toohello area altri endpoint. Ad esempio, si consideri un profilo con il tipo di routing geografico e con due endpoint: Endpoint1 ed Endpoint2. Endpoint1 è configurato il traffico tooreceive dall'Irlanda ed Endpoint2 tooreceive traffico da Europe. Se una richiesta proviene da Irlanda, è sempre tooEndpoint1 indirizzato.
- Poiché un'area può essere mappate endpoint tooone solo, gestione traffico restituisce indipendentemente dal fatto endpoint hello sia integro.

    >[!IMPORTANT]
    >È consigliabile che i clienti che utilizzano il metodo di routing geografiche di hello associarlo con gli endpoint di tipo annidate hello con profili figlio contenenti almeno due endpoint all'interno di ognuno.
- Se viene trovata una corrispondenza di endpoint e che l'endpoint è hello **arrestato** stato, gestione traffico restituisce una risposta NODATA. In questo caso, non le altre ricerche è più in alto nella gerarchia di area geografica hello. Questo comportamento è applicabile anche per i tipi annidati endpoint profilo figlio di hello è hello **arrestato** o **disabilitato** stato.
- Se un endpoint viene visualizzato un **disabilitato** stato, non sarà incluso nell'area di hello processo di corrispondenza. Questo comportamento è applicabile anche per i tipi annidati endpoint endpoint hello è hello **disabilitato** stato.
- Se una query proviene da un'area geografica che non ha alcun mapping in quel profilo, Gestione traffico restituisce una risposta NODATA. Pertanto, si consiglia ai clienti di utilizzare routing geografico con un endpoint, in teoria di tipo annidate con almeno due endpoint nel profilo figlio hello, con l'area di hello **World** tooit assegnato. Questo processo assicura anche che tutti gli indirizzi IP che non eseguono il mapping tooa area vengono gestiti.

Come spiegato in [Modalità di funzionamento di Gestione traffico](traffic-manager-how-traffic-manager-works.md), le query DNS non vengono ricevute direttamente dai client, Invece, le query DNS provengono da che hello client non siano toouse configurato il servizio DNS ricorsivo hello. Pertanto, non è hello IP indirizzo utilizzato toodetermine hello area hello indirizzo IP del client, ma è hello di indirizzo IP del servizio DNS di hello ricorsiva. In pratica, questo indirizzo IP è un proxy valido per il client di hello.


## <a name="next-steps"></a>Passaggi successivi

Informazioni su come applicazioni a disponibilità elevata toodevelop utilizzando [monitoraggio degli endpoint di gestione traffico](traffic-manager-monitoring.md)

Informazioni su come troppo[creare un profilo di Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



