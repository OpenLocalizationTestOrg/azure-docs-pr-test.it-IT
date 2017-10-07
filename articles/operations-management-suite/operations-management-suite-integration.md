---
title: aaaIntegrating con Operations Management Suite (OMS) | Documenti Microsoft
description: "Inoltre toousing hello funzionalità standard di OMS, è possibile integrarlo con altri tooprovide di applicazioni e servizi di gestione, un ambiente di gestione ibrida, tooprovide gestione personalizzata scenari univoci tooyour ambiente o tooprovide personalizzato esperienza di gestione per i clienti.  In questo articolo viene fornita una panoramica delle opzioni diverse per l'integrazione con OMS e i collegamenti tooarticles fornendo informazioni tecniche dettagliate."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Integrazione con Operations Management Suite (OMS)
Operations Management Suite è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.  Inoltre toousing hello funzionalità standard di OMS, è possibile integrarlo con altri tooprovide di applicazioni e servizi di gestione, un ambiente di gestione ibrida, tooprovide gestione personalizzata scenari univoci tooyour ambiente o tooprovide personalizzato esperienza di gestione per i clienti.  Questo articolo fornisce una panoramica delle diverse opzioni per l'integrazione con OMS servizi e i collegamenti tooarticles fornendo informazioni tecniche dettagliate. 

## <a name="log-analytics"></a>Log Analytics
I dati di gestione raccolti da Log Analytics vengono archiviati in un repository ospitato in Azure.  Tutti i dati archiviati nel repository di hello è disponibile nelle ricerche di log che forniscono analisi rapida tra estremamente grandi quantità di dati.  I requisiti di integrazione potrebbero essere repository hello toopopulate con nuovi dati, rendendoli disponibili per l'analisi, o dati tooextract hello repository tooprovide una nuova visualizzazione o toointegrate con un altro strumento di gestione.

Ogni blocco di dati nel repository di hello viene archiviato come un record.  Quando si popola repository hello, è necessario fornire agli utenti con tipo di record hello usato nella soluzione e una descrizione delle relative proprietà.  Quando si recuperano dati, è necessario queste informazioni sui dati hello in uso.

![Popolamento di repository OMS hello](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Popolare repository Log Analitica hello
Sono disponibili più metodi per il popolamento dei repository OMS hello.  Hello metodo da utilizzare dipende da fattori quali i dati di origine hello in cui si trova, formato hello di hello dati e che i client, è necessario toosupport.  Una volta che i dati vengono archiviati nel repository di hello, influisce in alcun modo modalità di raccolta.

Hello nelle sezioni seguenti vengono descritte hello diverse opzioni per il popolamento dei repository OMS hello.

#### <a name="connected-sources-and-data-sources"></a>Origini dati e origini connesse
Origini collegate sono percorsi hello in cui è possibile recuperare dati per il repository OMS hello.  Origini dati e le soluzioni eseguite Connected Sources e definiscono hello specifica i dati raccolti.  Se l'applicazione scrive dati tooone di queste origini dati, è possibile raccogliere, configurando l'origine dati hello.  Ad esempio, se l'applicazione crea gli eventi Syslog, quindi può essere raccolti dall'origine dati di Syslog hello su un agente Linux.

* [Origini dati in Log Analytics](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Soluzioni
Soluzioni di estendono le funzionalità di hello di OMS.  Una soluzione potrebbe raccogliere dati dall'origine connesso hello o può effettuare analisi su record già raccolti nel repository di hello.  Ogni soluzione fornita da Microsoft dispone di un singolo articolo che fornisce i dettagli di hello sui dati hello da esso raccolti.

* [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>API di raccolta dati HTTP
Hello API dell'agente di raccolta dati di Log Analitica HTTP è un'API REST che consente di repository Log Analitica dei dati toohello tooadd JSON.  Quando si dispone di un'applicazione che non fornisce dati tramite una delle hello altre origini dati o soluzioni, è possibile usare questa API.  Può essere repository hello toopopulate utilizzati da qualsiasi client può chiamare API hello e non si basi su pianificazione raccolta hello di qualsiasi origine dati o di una soluzione.

* [Log Analytics HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) (API di raccolta dati HTTP di Log Analytics)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Recuperare dati dall'archivio di Log Analitica hello
Esistono diversi metodi per il recupero dei dati dal repository OMS hello.  È possibile desidera che gli utenti tooretrieve dati utilizzando la console di OMS hello e fornire loro diversi tipi di analisi e visualizzazioni.  È anche possibile recuperare dati hello da un processo esterno, ad esempio un'altra soluzione di gestione.

#### <a name="log-searches"></a>Ricerche log
Tutti i dati archiviati nel repository OMS hello è disponibile tramite ricerche nei log.  Gli utenti possono eseguire le proprie analisi ad hoc nella console OMS hello oppure creare un dashboard con una visualizzazione per la ricerca di un log specifico.  Le soluzioni possono contenere visualizzazioni personalizzate con le visualizzazioni basate sulle ricerche predefinite.  È possibile utilizzare dati tooaccess di API di ricerca Log hello nel repository OMS hello da uno strumento esterno dell'applicazione o di gestione.  

* [Ricerche nei log in Log Analytics](../log-analytics/log-analytics-log-searches.md)
* [API REST di Log Analytics per la ricerca nei log](../log-analytics/log-analytics-log-search-api.md)
* [Log Analytics cmdlets](https://msdn.microsoft.com/library/mt188224.aspx) (Cmdlet di Log Analytics)

#### <a name="custom-views"></a>Visualizzazioni personalizzate
Hello Progettazione viste consente toocreate visualizzazioni personalizzate nella console OMS hello forniscono agli utenti di visualizzazione e analisi dei dati di hello nella soluzione.  Ogni visualizzazione include un riquadro che viene visualizzato nella pagina principale di hello console hello e qualsiasi numero di parti di visualizzazione che si basano sulle ricerche nei log che definiscono.

* [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) (Progettazione viste di Log Analytics)

#### <a name="power-bi"></a>Power BI
Log Analitica può automaticamente esportare dati dal repository OMS hello in Power BI in modo che è possibile sfruttare le visualizzazioni e gli strumenti di analisi.  Esegue l'esportazione in una pianificazione in modo restino il toodate hello. 

* [Esportare i dati di Log Analitica tooPower BI](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automazione
OMS consente di automatizzare i processi tooreact toocollected dati o tooperform altre funzioni di gestione.  Può raccogliere i dati dall'applicazione e inserirlo nel repository OMS hello oppure è possibile automatizzare correzione hello di un problema noto in risposta toodata trovato nel repository di hello. 

![Automazione](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbook
I runbook in automazione di Azure è possibile eseguire gli script di PowerShell e i flussi di lavoro in hello cloud di Azure.  È possibile usarli toomanage le risorse in Azure o altre risorse che sono accessibili dal cloud hello.  I runbook possono anche essere eseguiti in un datacenter locale tramite un ruolo di lavoro ibrido per runbook.  È possibile avviare un runbook dal portale di Azure hello o da processi esterni mediante una serie di metodi, ad esempio PowerShell o hello API di automazione.

* [Avvio di un Runbook in Automazione di Azure](../automation/automation-starting-a-runbook.md)
* [Azure Automation cmdlets](https://msdn.microsoft.com/library/dn690262.aspx) (Cmdlet di Automazione di Azure)
* [Automation REST API](https://msdn.microsoft.com/library/mt662285.aspx) (API REST di Automazione)
* [Automation .NET](https://msdn.microsoft.com//library/mt465763.aspx) (Automazione .NET)

### <a name="alerts"></a>Avvisi
Ricerche nei log in base tooa pianificazione l'esecuzione automatica delle regole di avviso.  Se i risultati di hello corrispondono particolare avviso risultante di criteri hello può avviare un runbook in automazione di Azure o chiamare un webhook che consente di avviare un processo esterno.  Entrambe queste risposte può includere dettagli dell'avviso hello inclusi dati hello restituiti nella ricerca nei log hello.

* [Avvisi in Log Analytics](../log-analytics/log-analytics-alerts.md)
* [API REST degli avvisi di Log Analytics](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Backup e Site Recovery
Azure Backup e ripristino del sito offrono servizi per la protezione dei dati aziendali e garantire la disponibilità di hello del server e applicazioni.  È possibile sfruttare queste tooperform servizi scenari quali offre servizi di backup per l'applicazione o l'avvio di un failover di una macchina virtuale.

* [Azure Backup cmdlets](https://msdn.microsoft.com/library/mt619253.aspx) (Cmdlet di Backup di Azure)
* [Azure Site Recovery REST API](https://msdn.microsoft.com/library/azure/mt750497.aspx) (API REST di Azure Site Recovery)
* [Azure Site Recovery Cmdlets](https://msdn.microsoft.com/library/mt637930.aspx) (Cmdlet di Azure Site Recovery)

## <a name="custom-solutions"></a>Soluzioni personalizzate
Nell'area di lavoro oppure nell'area di lavoro di un cliente, è possibile incapsulare la logica di integrazione in toorun una soluzione personalizzata.  La soluzione può includere uno dei metodi di integrazione hello in questo articolo in aggiunta tooother risorse tooprovide uno scenario di gestione completa.  risorse Hello nella soluzione hello sono inclusi in modo che quando viene rimosso soluzione hello, tutte le risorse di hello che ha creato vengono rimossi dall'area di lavoro OMS hello e sottoscrizione di Azure.

Ad esempio, la soluzione potrebbe includere un'automazione runbook toogather ed elaborare i dati e popolare repository Log Analitica hello utilizzando hello API dell'agente di raccolta dati di HTTP.  È anche possibile includere una visualizzazione personalizzata che visualizza e analizza i dati raccolti hello.  

* Creazione di soluzioni personalizzate (presto disponibile)    

## <a name="next-steps"></a>Passaggi successivi
* Hello riferimento [OMS SDK](operations-management-suite-sdk.md) per informazioni tecniche sull'automazione di servizi di OMS.  

