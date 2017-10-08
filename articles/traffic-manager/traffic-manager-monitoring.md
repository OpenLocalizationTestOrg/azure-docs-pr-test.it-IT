---
title: monitoraggio degli endpoint di gestione traffico aaaAzure | Documenti Microsoft
description: "In questo articolo aiuta a comprendere come gestione traffico Usa il monitoraggio degli endpoint e automatica degli endpoint failover toohelp Azure i clienti di distribuire applicazioni a disponibilità elevata"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Monitoraggio degli endpoint di Gestione traffico

Gestione traffico di Azure include il monitoraggio degli endpoint e il failover automatico degli endpoint. Questa funzionalità consente di distribuire le applicazioni a disponibilità elevata resilienti tooendpoint errore, inclusi errori di area di Azure.

## <a name="configure-endpoint-monitoring"></a>Configurare il monitoraggio degli endpoint

tooconfigure monitoraggio degli endpoint, è necessario specificare hello seguendo le impostazioni di profilo di Traffic Manager:

* **Protocollo**. Scegliere HTTP, HTTPS o TCP come protocollo di hello Traffic Manager utilizzato durante il sondaggio toocheck l'endpoint relativa integrità. Il monitoraggio HTTPS non verifica se il certificato SSL sia valido, controlla solo tale hello è presenta un certificato.
* **Porta**. Scegliere porta hello utilizzata per la richiesta di hello.
* **Percorso**. Questa impostazione di configurazione è valida solo per i protocolli HTTP e HTTPS hello, per cui è necessaria l'impostazione del percorso specificando hello. Specificare questa impostazione per hello TCP monitoraggio protocollo genera un errore. Per il protocollo TCP, assegnare hello relativo e nome hello della pagina Web hello o un file hello che hello monitoraggio accessi. Una barra (/) è una voce valida per il percorso relativo hello. Questo valore implica che il file hello trovi nella directory radice di hello (impostazione predefinita).
* **Intervallo sondaggio**. Questo valore specifica la frequenza con cui viene controllata l'integrità di un endpoint dall'agente di sondaggio di Gestione traffico. È possibile specificare due valori qui: 30 secondi (sondaggio normale) e 10 secondi (sondaggio veloce). Se non vengono fornito alcun valore, il profilo di hello imposta il valore predefinito tooa di 30 secondi. Visitare hello [dei prezzi di gestione traffico](https://azure.microsoft.com/pricing/details/traffic-manager) toolearn pagina informazioni sui prezzi probe rapido.
* **Numero di errori tollerati**. Questo valore specifica il numero di errori tollerati da un agente di sondaggio di Gestione traffico prima di contrassegnare l'endpoint come non integro. Il valore può essere compreso tra 0 e 9. Un valore pari a 0 indica un singolo errore di monitoraggio può causare toobe tale endpoint contrassegnato come danneggiato. Se viene specificato alcun valore, utilizza il valore predefinito hello 3.
* **Timeout di monitoraggio**. Questa proprietà specifica la quantità hello di hello ora Traffic Manager agent probe deve attendere prima di considerare che verifica un errore quando un probe di controllo di integrità viene inviato toohello endpoint. Se hello che intervallo probe è too30 secondi, quindi è possibile impostare il valore di Timeout hello compreso tra 5 e 10 secondi. Se non si specifica alcun valore, viene usato il valore predefinito di 10 secondi. Se hello che intervallo probe è too10 secondi, quindi è possibile impostare il valore di Timeout hello compreso tra 5 e 9 secondi. Se non si specifica alcun valore di timeout, viene usato il valore predefinito di 9 secondi.

![Monitoraggio degli endpoint di Gestione traffico](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Figura 1: Monitoraggio degli endpoint di Gestione traffico**

## <a name="how-endpoint-monitoring-works"></a>Funzionamento del monitoraggio degli endpoint

Se hello monitoraggio protocollo è impostato come HTTP o HTTPS, agente di probe di hello Traffic Manager esegue un endpoint di toohello richiesta GET mediante il protocollo di hello, porta e il percorso relativo specificato. Se ottiene una risposta 200-OK, l'endpoint viene considerato integro. Se la risposta hello è un valore diverso o, se viene ricevuta alcuna risposta entro il periodo di timeout hello specificato, quindi hello Traffic Manager probing agente tenta nuovamente di eseguire in base impostazione numero di errori tollerati toohello (nessun tenta nuovamente di eseguire vengono eseguite se questa impostazione è 0) . Se il numero di hello tentativi consecutivi non riusciti è maggiore di impostazione numero di errori tollerati hello, tale endpoint è contrassegnato come danneggiato. 

Se hello monitoraggio protocollo è TCP, l'agente di sondaggio Traffic Manager di hello avvia una richiesta di connessione TCP utilizzando la porta hello specificata. Se l'endpoint di hello risponde toohello richiesta con una connessione di hello tooestablish risposta, che il controllo di integrità è contrassegnato come esito positivo e agente probe Traffic Manager di hello Reimposta connessione TCP hello. Se la risposta hello è un valore diverso o se è stata ricevuta alcuna risposta entro il periodo di timeout hello è specificato, hello Traffic Manager probing agente tenta nuovamente di eseguire in base impostazione numero di errori tollerati toohello (nessun tenta nuovamente di eseguire vengono eseguiti se questa impostazione è 0). Se il numero di hello tentativi consecutivi non riusciti è maggiore di impostazione numero di errori tollerati hello, quindi tale endpoint è contrassegnato come non integro.

In tutti i casi, le ricerche di gestione traffico da più posizioni e determinazione di errori consecutivi hello viene eseguita all'interno di ogni area. Questo significa anche che gli endpoint ricevono probe di integrità da Gestione traffico con una frequenza maggiore rispetto a impostazione hello utilizzata per l'intervallo di probe.

>[!NOTE]
>Per HTTP o HTTPS, il monitoraggio di protocollo, una pratica comune sul lato di endpoint hello è una pagina personalizzata all'interno dell'applicazione, ad esempio, /health.aspx tooimplement. Usando questo percorso per il monitoraggio, è possibile eseguire controlli specifici dell'applicazione, ad esempio il controllo dei contatori delle prestazioni o la verifica della disponibilità del database. In base a questi controlli personalizzati, pagina hello restituisce un codice di stato HTTP appropriato.

Tutti gli endpoint in un profilo di Gestione traffico condividono le impostazioni di monitoraggio. Se è necessario toouse diverse impostazioni di monitoraggio per endpoint diversi, è possibile creare [profili di gestione traffico nidificati](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Stato di endpoint e profili

Gli endpoint e i profili di Gestione traffico possono essere abilitati e disabilitati. Tuttavia, lo stato degli endpoint può cambiare anche a causa di impostazioni e processi automatici di Gestione traffico.

### <a name="endpoint-status"></a>Stato endpoint

È possibile abilitare o disabilitare un endpoint specifico. servizio sottostante Hello, che potrebbe essere ancora integro, non è interessato. I controlli di modifica stato endpoint hello hello disponibilità di endpoint hello in hello profilo di gestione traffico. Quando lo stato di un endpoint è disabilitato, gestione traffico non controlla l'integrità e l'endpoint hello non è incluso in una risposta DNS.

### <a name="profile-status"></a>Stato profilo

Se si utilizza l'impostazione di stato del profilo hello, è possibile abilitare o disabilitare un profilo specifico. Mentre lo stato di endpoint influisce su un singolo endpoint, lo stato del profilo interessa l'intero profilo hello, inclusi tutti gli endpoint. Quando si disabilita un profilo, endpoint hello non vengono verificate per l'integrità e nessun endpoint è incluso in una risposta DNS. Un [NXDOMAIN](https://tools.ietf.org/html/rfc2308) viene restituito il codice di risposta per query DNS hello.

### <a name="endpoint-monitor-status"></a>Endpoint monitor status (Stato monitoraggio endpoint)

Lo stato di monitoraggio endpoint è un valore generato Traffic Manager che mostra lo stato di hello dell'endpoint hello. Questa impostazione non può essere modificata manualmente. monitorare lo stato dell'endpoint di Hello è una combinazione dei risultati di hello di monitoraggio degli endpoint e hello stato endpoint configurato. i valori possibili Hello dello stato di monitoraggio endpoint vengono visualizzati in hello nella tabella seguente:

| Stato profilo | Stato endpoint | Endpoint monitor status (Stato monitoraggio endpoint) | Note |
| --- | --- | --- | --- |
| Disabled |Enabled |Inactive |profilo Hello è stata disabilitata. Anche se lo stato di endpoint hello è attivato, lo stato del profilo hello (disabilitato) ha la precedenza. Gli endpoint nei profili disabilitati non vengono monitorati. Per una query DNS hello, viene restituito un codice di risposta NXDOMAIN. |
| &lt;qualsiasi&gt; |Disabled |Disabled |Hello endpoint è stato disabilitato. Gli endpoint disabilitati non vengono monitorati. endpoint di Hello non è incluso nelle risposte DNS, di conseguenza, non riceve traffico. |
| Enabled |Enabled |Online |endpoint Hello viene monitorato ed è integro. È incluso nelle risposte DNS ed è in grado di ricevere traffico. |
| Enabled |Enabled |Degraded |I controlli di integrità del monitoraggio dell'endpoint hanno esito negativo. endpoint di Hello non è incluso nelle risposte DNS e non riceve traffico. <br>Un'eccezione toothis è se tutti gli endpoint sono danneggiati, nel qual caso tutti gli elementi vengono considerati lo toobe restituite nella risposta query hello).</br>|
| Enabled |Enabled |CheckingEndpoint |Hello endpoint viene monitorato, ma i risultati di hello del primo probe hello non sono ancora stati ricevuti. Verifica endpoint è un stato temporaneo che in genere si verifica immediatamente dopo l'aggiunta o l'abilitazione di un endpoint nel profilo hello. Un endpoint con questo stato viene incluso nelle risposte DNS e può ricevere traffico. |
| Enabled |Enabled |Arrestato |Hello cloud del servizio web app o che hello toois punti endpoint non è in esecuzione. Controllare impostazioni app web o servizio hello cloud. Questa situazione può verificarsi anche se l'endpoint hello è di tipo annidato endpoint e profilo figlio hello è disabilitato o non è attivo. <br>Gli endpoint con stato Interrotto non vengono monitorati. Non è incluso nelle risposte DNS e non riceve traffico. Un'eccezione toothis è se tutti gli endpoint sono danneggiati, nel qual caso tutti gli elementi verranno considerati toobe restituite nella risposta query hello.</br>|

Per informazioni dettagliate su come viene calcolato lo stato del monitoraggio degli endpoint nidificati, vedere [Profili nidificati di Gestione traffico](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Stato monitoraggio profilo

monitorare lo stato del profilo Hello è una combinazione di stato del profilo configurato hello e hello endpoint monitor i valori di stato per tutti gli endpoint. Hello possibili valori sono descritti nella seguente tabella hello:

| Stato profilo (come configurato) | Endpoint monitor status (Stato monitoraggio endpoint) | Stato monitoraggio profilo | Note |
| --- | --- | --- | --- |
| Disabled |&lt;qualsiasi&gt; o un profilo senza endpoint definiti. |Disabled |profilo Hello è stata disabilitata. |
| Enabled |stato di Hello di almeno un endpoint è danneggiato. |Degraded |Esaminare i valori dello stato di hello singoli endpoint toodetermine quali endpoint richiede ulteriore attenzione. |
| Enabled |stato di Hello di almeno un endpoint è Online. Nessun endpoint presenta lo stato Degraded. |Online |il traffico viene accettato dal servizio Hello. Non è necessaria alcuna azione. |
| Enabled |stato di Hello di almeno un endpoint è verifica endpoint. Nessun endpoint presenta lo stato Online o Degraded. |CheckingEndpoints |Questo stato di transizione si verifica quando un profilo viene creato o abilitato. integrità dell'endpoint Hello viene verificata la hello prima volta. |
| Enabled |gli stati di Hello di tutti gli endpoint nel profilo hello sono nello stato disabilitato o arrestato o profilo hello non è endpoint definiti. |Inactive |Nessun endpoint è attivo, ma il profilo di hello è ancora abilitato. |

## <a name="endpoint-failover-and-recovery"></a>Failover e ripristino degli endpoint

Gestione traffico controlla periodicamente lo stato di hello di ogni endpoint, compresi gli endpoint di tipo non integro. Rileva quando un endpoint diventa integro e lo reinserisce nella rotazione.

Un endpoint non è integro quando si verifica uno dei seguenti eventi hello:
- Se hello monitoraggio protocollo è HTTP o HTTPS:
    - Viene ricevuta una risposta non 200, incluso un codice 2xx diverso o un reindirizzamento 301/302.
- Se hello monitoraggio protocollo è TCP: 
    - Una risposta diverso ACK o SYN ACK viene ricevuto nella richiesta di sincronizzazione toohello risposta inviati tramite Gestione traffico tooattempt un tentativo di connessione.
- Timeout. 
- Qualsiasi altro problema di connessione generando hello endpoint non raggiungibile.

Per ulteriori informazioni su come risolvere i problemi relativi ai controlli non riusciti, vedere [Risoluzione dei problemi relativi allo stato Danneggiato di Gestione traffico](traffic-manager-troubleshooting-degraded.md). 

sequenza temporale seguente nella figura 2 Hello è una descrizione dettagliata del processo di endpoint di gestione traffico con hello seguendo le impostazioni di monitoraggio hello: il monitoraggio di protocollo è HTTP, l'intervallo probe è 30 secondi, numero di errori tollerati è 3, valore di timeout è di 10 secondi e TTL del DNS è 30 secondi.

![Sequenza di failover e failback degli endpoint di Gestione traffico](./media/traffic-manager-monitoring/timeline.png)

**Figura 2: Sequenza di failover e ripristino degli endpoint di Gestione traffico**

1. **GET**. Per ogni endpoint, hello sistema di monitoraggio di Traffic Manager esegue una richiesta GET percorso hello specificato nelle impostazioni di monitoraggio hello.
2. **200 OK**. sistema di monitoraggio Hello prevede un toobe messaggio HTTP 200 OK restituito entro 10 secondi. Quando riceve la risposta, esso rileva che il servizio di hello è disponibile.
3. **30 secondi tra i controlli**. controllo di integrità di endpoint Hello viene ripetuto ogni 30 secondi.
4. **Servizio non disponibile**. Hello diventa non disponibile. Gestione traffico non riconoscerà fino al successivo controllo di integrità hello.
5. **Hello tooaccess tentativi monitoraggio percorso**. sistema di monitoraggio Hello esegue una richiesta GET, ma non riceve una risposta entro il periodo di timeout hello di 10 secondi (in alternativa, una risposta non 200 può essere ricevuta). Il sistema esegue quindi altri tre tentativi a intervalli di 30 secondi. Se uno dei tentativi di hello ha esito positivo, il numero di hello di tentativi viene reimpostato.
6. **Stato impostato tooDegraded**. Dopo un quarto errore consecutivo, hello sistema di monitoraggio contrassegna lo stato di endpoint disponibile hello come danneggiato.
7. **Il traffico è tooother deviate endpoint**. Hello Server dei nomi DNS di Traffic Manager vengono aggiornati e gestione traffico non restituisce più endpoint hello nelle query tooDNS di risposta. Le nuove connessioni sono tooother diretto, gli endpoint disponibili. Tuttavia, le risposte DNS precedenti che includono questo endpoint possono essere ancora memorizzate nella cache da server DNS e client DNS ricorsivi. I client continuano endpoint hello toouse fino alla scadenza della cache DNS hello. Scadenza della cache DNS hello client apportare le nuove query DNS e sono endpoint toodifferent diretto. durata della cache di Hello è controllata dall'impostazione di durata (TTL) hello in hello profilo di gestione traffico, ad esempio, 30 secondi.
8. **I controlli di integrità proseguono**. Gestione traffico continua integrità hello toocheck dell'endpoint hello mentre sono in uno stato danneggiato. Gestione traffico rileva se l'endpoint di hello restituisce toohealth.
9. **Il servizio ritorna online**. servizio Hello diventa disponibile. endpoint Hello mantiene lo stato di ridotto in Traffic Manager finché hello sistema di monitoraggio esegue il controllo integrità successivo.
10. **Riprende il traffico tooservice**. Gestione traffico invia una richiesta GET e riceve una risposta di stato 200 OK, servizio Hello ha restituito uno stato integro tooa. Server dei nomi Hello Traffic Manager vengono aggiornati e inizino toohand nome DNS del servizio hello nelle risposte DNS. Traffico restituisce toohello endpoint memorizzato nella cache le risposte DNS che restituiscono altri endpoint scadono e come le connessioni esistenti vengono terminati tooother endpoint.

    > [!NOTE]
    > Poiché gestione traffico funziona hello livello DNS, è possibile influenzare endpoint tooany di connessioni esistenti. Quando indirizza il traffico tra endpoint (o dalle impostazioni del profilo modificate, durante il failover o il failback), gestione traffico indirizza gli endpoint di tooavailable nuove connessioni. Tuttavia, altri endpoint potrebbe continuare tooreceive traffico tramite le connessioni esistenti fino a quando tali sessioni vengono terminate. tooenable toodrain di traffico da connessioni esistenti, le applicazioni devono limitare hello durata della sessione utilizzata con ogni endpoint.

## <a name="traffic-routing-methods"></a>Metodi di routing del traffico

Quando un endpoint ha uno stato danneggiato, non è più restituita nelle query tooDNS di risposta. Viene invece scelto e restituito un endpoint alternativo. metodo di routing del traffico Hello configurata nel profilo di hello determina la modalità di endpoint alternativi hello scelta.

* **Priorità**. gli endpoint formano un elenco con priorità. primo endpoint disponibili Hello nell'elenco di hello viene sempre restituito. Se lo stato di un endpoint è danneggiato, viene restituito l'endpoint disponibile successivo hello.
* **Ponderato**. Qualsiasi endpoint disponibile viene scelto in modo casuale in base a loro assegnati pesi e hello pesi di hello altri endpoint disponibili.
* **Prestazioni**. viene restituito Hello endpoint più vicino toohello utente. Se tale endpoint non è disponibile, un endpoint viene scelto in modo casuale da tutte hello altri endpoint disponibili. Scelta di un endpoint casuale consente di evitare un errore a cascata che può verificarsi quando hello successivo endpoint più vicino in overload. È possibile configurare piani di failover alternativi per il routing del traffico con il metodo Prestazioni usando [profili di Gestione traffico nidificati](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Geografico**. endpoint Hello mappato tooserve hello area geografica in base alla richiesta di query hello che indirizzi IP viene restituito. Se tale endpoint è disponibile, un altro endpoint non sarà selezionato toofailover, poiché un'area geografica può essere mappata endpoint tooone solo in un profilo (altri dettagli sono disponibili in hello [domande frequenti su](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Come procedura consigliata, quando si utilizza il routing geografico, si consiglia ai clienti i profili di Traffic Manager toouse annidati con più di un endpoint come endpoint hello del profilo di hello.

Per altre informazioni, vedere [Metodi di routing del traffico di Gestione traffico](traffic-manager-routing-methods.md).

> [!NOTE]
> Il comportamento di routing del traffico toonormal di un'eccezione si verifica quando tutti gli endpoint idonei hanno uno stato danneggiato. Consente di gestione traffico tenta "best effort" e *risponde come se tutti gli endpoint di stato danneggiato di hello effettivamente sono in uno stato online*. Questo comportamento è in alternativa, preferibili toohello che sarebbe toonot restituire qualsiasi endpoint in hello risposta DNS. Gli endpoint disabilitati o arrestati non vengono monitorati, di conseguenza non sono considerati idonei per il traffico.
>
> Questa condizione è in genere causata dall'errata configurazione del servizio di hello, ad esempio:
>
> * Un elenco di controllo accesso (ACL) blocco hello controlli di integrità di gestione traffico.
> * Una configurazione non corretta di hello monitoraggio porta o protocollo di hello profilo di gestione traffico.
>
> Hello conseguenza di questo comportamento è che, se i controlli di integrità di gestione traffico non sono configurati correttamente, potrebbe essere visualizzato dal traffico hello routing come gestione traffico *è* funziona correttamente. In questo caso il failover degli endpoint non viene tuttavia eseguito, con ripercussioni sulla disponibilità complessiva dell'applicazione. È importante toocheck profilo hello viene visualizzato uno stato Online, non uno stato danneggiato. Uno stato Online indica che hello Traffic Manager di controlli di integrità funzionino come previsto.

Per altre informazioni su come risolvere i problemi relativi ai controlli di integrità non riusciti, vedere [Risoluzione dei problemi relativi allo stato danneggiato di Gestione traffico](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Passaggi successivi

Informazioni sul [funzionamento di Gestione traffico](traffic-manager-how-traffic-manager-works.md)

Altre informazioni su hello [metodi di routing del traffico](traffic-manager-routing-methods.md) supportate da Gestione traffico

Informazioni su come troppo[creare un profilo di Traffic Manager](traffic-manager-manage-profiles.md)

[Risoluzione dei problemi relativi allo stato Degraded](traffic-manager-troubleshooting-degraded.md) di un endpoint di Gestione traffico
