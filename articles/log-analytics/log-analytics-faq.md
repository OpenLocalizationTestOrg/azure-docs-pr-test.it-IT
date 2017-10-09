---
title: domande frequenti su Analitica aaaLog | Documenti Microsoft
description: Domande frequenti sul servizio Azure Log Analitica hello toofrequently di risposte.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Domande frequenti su Log Analytics
Queste domande frequenti Microsoft sono relative a Log Analytics in Microsoft Operations Management Suite (OMS). Se si dispone di ulteriori domande su Log Analitica, passare toohello [forum di discussione](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) e inserire le domande. Quando una domanda è frequenti, abbiamo aggiunto toothis articolo in modo che possono essere trovati in modo semplice e rapido.

## <a name="general"></a>Generale

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>D: Log Analitica utilizza hello stesso agente come Centro sicurezza di Azure?

R. A giugno 2017 anticipata, Centro sicurezza di Azure iniziato a utilizzare toocollect e l'archivio dati di Microsoft Monitoring Agent di hello. vedere, più toolearn [domande frequenti sulla migrazione della piattaforma Azure sicurezza Center](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>D: Quali controlli vengono eseguiti da hello Active Directory e soluzioni di valutazione di SQL?

R. Hello nella query seguente mostra una descrizione di tutti i controlli attualmente eseguiti:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Hello risultati possono quindi essere esportati tooExcel per un ulteriore esame.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>D: perché non viene visualizzato *OMS* nella console di System Center Operations Manager?

R: A seconda dell'aggiornamento cumulativo di Operations Manager in uso, viene visualizzato un nodo relativo a *System Center Advisor*, *Operational Insights* o *Log Analytics*.

Hello aggiornamento della stringa di testo troppo*OMS* è incluso in un management pack, che deve toobe importato manualmente. testo di toosee hello corrente e la funzionalità di istruzioni hello hello più recente System Center Operations Manager Update Rollup KB articolo e aggiorna hello console.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>D: Esiste una versione *locale* di Log Analytics?

R: No. Log Analytics elabora e archivia grandi quantità di dati. Come un servizio cloud, Analitica di Log è in grado di tooscale verticale se necessario ed evitare qualsiasi ambiente tooyour di impatto sulle prestazioni.

Questo approccio offre i vantaggi aggiuntivi seguenti:
- Microsoft esegue infrastruttura Log Analitica hello, risparmiando i costi
- Distribuzione regolare di aggiornamenti e correzioni delle funzionalità.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>D: Come riattivare la raccolta dati di Log Analytics?

R: se si trovano in hello disponibile a livello di prezzo e hanno inviato più di 500 MB di dati in un giorno, per il resto di hello del giorno hello arresto della raccolta di dati. Limite giornaliero di raggiungimento hello è una causa comune Log Analitica smette di raccogliere dati o toobe verranno visualizzati i dati mancanti.

Log Analytics crea un evento di tipo *Operazione* quando la raccolta dei dati si avvia e si arresta. 

Eseguire hello seguenti query di ricerca toocheck se si al raggiungimento del limite giornaliero di hello e i dati mancanti:`Type=Operation OperationCategory="Data Collection Status"`

Quando la raccolta dei dati viene arrestata, hello *Statooperazione* è **avviso**. Quando la raccolta dei dati viene avviato, hello *Statooperazione* è **Succeeded**. 

Hello nella tabella seguente vengono descritti i motivi che interrompe la raccolta dei dati e una raccolta di dati tooresume azione suggerita:

| Motivi di interruzione della raccolta dati                       | raccolta di dati tooresume |
| -------------------------------------------------- | ----------------  |
| Limite giornaliero di dati gratuiti raggiunto<sup>1</sup>       | Attendere fino al giorno per raccolta tooautomatically riavvio, hello o<br> Modifica tooa a pagamento a livello di prezzo |
| La sottoscrizione di Azure è in sospeso perché: <br> la versione di prova gratuita è terminata <br> Azure Pass è scaduto <br> Il limite di spesa mensile è stato raggiunto, ad esempio in una sottoscrizione MSDN o in una sottoscrizione di Visual Studio                          | Convertire tooa sottoscrizione a pagamento <br> Convertire tooa sottoscrizione a pagamento <br> Rimuovere il limite oppure attendere fino ripristino del limite |

<sup>1</sup> se l'area di lavoro è nel livello di prezzo gratuito hello, l'utente è limitato toosending 500 MB di dati per ogni servizio toohello giorno. Quando si raggiunge il limite giornaliero di hello, la raccolta dei dati viene arrestata finché non hello giorno successivo. I dati inviati quando la raccolta dati è sospesa non vengono indicizzati e non sono disponibili per la ricerca. Quando la raccolta dei dati riprende, l'elaborazione avviene solo per i nuovi dati inviati. 

Log Analytics usa l'ora UTC e ogni giorno inizia a mezzanotte UTC. Se l'area di lavoro hello raggiunge il limite giornaliero di hello, l'elaborazione verrà ripresa durante hello prima ora di hello giorno UTC.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>D: Come inviare una notifica all'utente quando la raccolta dati si interrompe?

R: utilizzare passaggi hello descritti in [creare una regola di avviso](log-analytics-alerts-creating.md#create-an-alert-rule) toobe una notifica quando si arresta la raccolta dei dati.

Quando si crea avviso hello all'arresto della raccolta dei dati, impostare il:
- **Nome** troppo*interrotta la raccolta dei dati*
- **Gravità** troppo*avviso*
- **Query di ricerca** troppo`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Intervallo di tempo** troppo*2 ore*.
- **Avviso frequenza** toobe un'ora, poiché i dati di utilizzo hello Aggiorna solo una volta ogni ora.
- **Genera l'avviso in base a** toobe *numero di risultati*
- **Numero di risultati** toobe *maggiore di 0*

Utilizzare hello passaggi descritti in [aggiungere regole tooalert azioni](log-analytics-alerts-actions.md) configurare un'azione di posta elettronica, webhook o runbook per la regola di avviso hello.


## <a name="configuration"></a>Configurazione
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>D: È possibile modificare il nome di hello di hello tabella/blob contenitore usato tooread da diagnostica Azure (WAD)?

R. No, non è attualmente possibile tooread da tabelle arbitrari o contenitori in archiviazione di Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>D: Quali indirizzi IP, uso dei servizi Log Analitica hello? Come garantire che il firewall consenta solo servizio Analitica di Log del traffico toohello?

R. servizio Registro Analitica Hello è basato su Azure. Gli indirizzi IP Analitica di log sono in hello [intervalli IP dei data center Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653).

Quando vengono apportate le distribuzioni del servizio, modificare hello gli indirizzi IP effettivi di hello servizio Analitica di Log. Hello DNS nomi tooallow attraverso il firewall sono documentati in [configurare le impostazioni proxy e firewall nel Log Analitica](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>D: Se si usa ExpressRoute per la connessione tooAzure. Il traffico di Log Analytics userà la connessione ExpressRoute?

R. Hello diversi tipi di traffico di ExpressRoute sono descritti in hello [documentazione di ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

Traffico tooLog Analitica Usa il circuito ExpressRoute di peering pubblico hello.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>D: Esiste un modo semplice di toomove un tooanother di area di lavoro esistente Log Analitica Analitica di Log dell'area di lavoro o sottoscrizione di Azure?

R. Hello `Move-AzureRmResource` cmdlet consente di spostare un'area di lavoro Log Analitica e un account di automazione da una sottoscrizione di Azure tooanother. Per altre informazioni, vedere [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Questa modifica può essere effettuata anche nel portale di Azure hello.

Impossibile spostare i dati da un Log Analitica dell'area di lavoro tooanother o modificare l'area hello Analitica di Log vengono archiviati in.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>D: come è possibile aggiungere Log Analitica tooSystem Center Operations Manager?

R: l'aggiornamento cumulativo più recente toohello e l'importazione di management pack consente tooconnect Operations Manager tooLog Analitica.

>[!NOTE]
>tooLog connessione di Operations Manager Hello Analitica è disponibile solo per System Center Operations Manager 2012 SP1 e versioni successive.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>D: come è possibile verificare che un agente sia in grado di toocommunicate con Analitica Log?

R: tooensure che l'agente di hello possa comunicare con OMS, passare a: pannello di controllo, sicurezza e impostazioni, **Microsoft Monitoring Agent**.

In hello **Analitica Log di Azure (OMS)** scheda, cercare un segno di spunta verde. Un'icona segno di spunta verde conferma che l'agente di hello è in grado di toocommunicate con hello servizio OMS.

Un'icona di avviso gialla indica che l'agente hello si è verificati problemi di comunicazione con OMS. Una causa frequente è hello servizio Microsoft Monitoring Agent è stato arrestato. Utilizzare controllo manager toorestart hello servizio.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>D: Come si arresta la comunicazione tra un agente e Log Analytics?

R: In System Center Operations Manager, rimuovere il computer di hello dall'elenco di computer gestiti Advisor hello. Gli aggiornamenti di Operations Manager hello configurazione di hello agente toono più report tooLog Analitica. Per gli agenti connessi direttamente tooLog Analitica, è possibile interromperne le comunicazioni tramite: pannello di controllo, sicurezza e impostazioni, **Microsoft Monitoring Agent**.
In **Analisi dei log di Azure (OMS)**rimuovere tutte le aree di lavoro elencate.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>D: perché viene visualizzato un errore quando si tenta di toomove l'area di lavoro da una sottoscrizione di Azure tooanother?

R: se si utilizza hello portale di Azure, verificare che solo l'area hello è selezionata per lo spostamento di hello. Non selezionare le soluzioni hello - automaticamente sposterà quando si sposta l'area di lavoro hello. 

Verificare di avere l'autorizzazione in entrambe le sottoscrizioni di Azure.

## <a name="agent-data"></a>Dati dell'agente
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>D: La quantità di dati è possibile inviare tramite hello agente tooLog Analitica È prevista una quantità massima di dati per ogni cliente?
R. piano gratuito Hello prevede un limite giornaliero di 500 MB per ogni area di lavoro. Hello standard e i piani premium non esiste alcun limite alla quantità di hello di dati che viene caricati. Come un servizio cloud, è progettato Analitica Log tooautomatically scalabilità volume hello toohandle proveniente da un cliente, anche se è più terabyte al giorno.

agente Log Analitica Hello è stato progettato tooensure dispone di un footprint ridotto. Uno dei clienti ha scritto un blog sui test hello che ha eseguito con l'agente e notevoli fossero. volume di dati Hello varia in base soluzioni hello che attiva. È possibile trovare informazioni dettagliate sul volume di dati hello e vedere suddivisione hello dalla soluzione di hello [utilizzo](log-analytics-usage.md) pagina.

Per ulteriori informazioni, è possibile leggere un [blog di un cliente](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) sul footprint ridotto di hello dell'agente OMS hello.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>D: Quanta larghezza di banda di rete è utilizzata dal hello Microsoft Management Agent (MMA) per inviare dati tooLog Analitica?

R. Larghezza di banda è una funzione quantità hello di dati inviati. Dati sono compressi al momento della trasmissione in rete hello.

### <a name="q-how-much-data-is-sent-per-agent"></a>D: Quanti dati vengono inviati per ogni agente?

R. dipende dalla quantità di Hello di dati inviati per ciascun agente:

* soluzioni Hello che è stata abilitata
* numero di Hello di log e i contatori delle prestazioni raccolti
* volume Hello dei dati nei log hello

Hello disponibile tariffario è tooonboard un buon metodo diversi server e misurare il volume di dati tipico hello. Uso complessivo è indicato nella hello [utilizzo](log-analytics-usage.md) pagina.

Per i computer sono in grado di toorun hello WireData agente, utilizzare hello seguente toosee query vengono inviati la quantità di dati:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Passaggi successivi
* [Introduzione a Log Analitica](log-analytics-get-started.md) toolearn informazioni sul Log Analitica e get attivo e in esecuzione in minuti.
