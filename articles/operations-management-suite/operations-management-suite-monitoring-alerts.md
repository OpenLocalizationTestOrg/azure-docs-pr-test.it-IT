---
title: gestione aaaAlert in Microsoft monitoring prodotti | Documenti Microsoft
description: Un avviso indica un problema che richiede attenzione da parte di un amministratore.  In questo articolo vengono descritte le differenze hello come gli avvisi vengono creati e gestiti in System Center Operations Manager (SCOM) e di Log Analitica e procedure consigliate all'utilizzo di due prodotti di hello per una strategia di gestione degli avvisi ibrido.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Gestione degli avvisi di monitoraggio Microsoft
Un avviso indica un problema che richiede attenzione da parte di un amministratore.  Esistono delle differenze ben distinte tra System Center Operations Manager (SCOM) e Log Analytics in Operations Management Suite (OMS) in termini della modalità di creazione, gestione e analisi degli avvisi, ma anche per quanto riguarda la modalità di notifica in caso di rilevamento di un problema critico.

## <a name="alerts-in-operations-manager"></a>Avvisi in Operations Manager
In SCOM vengono generati da singole regole o monitoraggi tooindicate un problema specifico.  Un monitoraggio può generare un avviso quando entra in uno stato di errore durante una regola può generare un avviso tooindicate un problema critico che non è direttamente correlata toohello integrità di un oggetto gestito.  Management Pack includono un'ampia gamma di flussi di lavoro che creano avvisi per un'applicazione hello o un servizio che gestiscono.  Parte del processo di hello di configurazione di un nuovo management pack è ottimizzazione tooensure che non si ricevono avvisi eccessivo per problemi considerati critici.

![Visualizzazione degli avvisi SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM fornisce gestione completa degli avvisi con gli avvisi con uno stato che può essere modificato dagli amministratori di lavoro problema hello tooresolve.  Quando è stato risolto il problema di hello, messaggio per l'amministratore imposta tooclosed di avviso hello in quale momento non verrà più visualizzato nelle visualizzazioni di visualizzazione di avvisi attivi.  Gli avvisi generati dai monitoraggi possono essere risolti automaticamente quando viene restituito uno stato integro tooa monitoraggio hello.

![Stato dell'avviso](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Avvisi in Log Analytics
Un avviso in Log Analytics viene creato da una query di log eseguita automaticamente a intervalli regolari.  È possibile creare una regola di avviso di una qualsiasi query di log.  Se hello query restituisce risultati che soddisfano i criteri di hello specificato, viene creato un avviso.  Potrebbe trattarsi di una query specifica che crea un avviso se viene rilevato un evento specifico oppure è possibile utilizzare una query più generale che ha un aspetto per qualsiasi evento di errore correlati tooa particolare applicazione.

Gli avvisi Analitica di log vengono scritti toohello repository OMS come un evento e possono essere recuperati con una query log.  Lo stato come eventi SCOM non hanno in modo che è possibile indicare quando è stato risolto il problema di hello.

![Avviso OMS](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Quando SCOM viene utilizzato come origine dati per i Log Analitica, gli avvisi SCOM vengono scritti repository OMS toohello non appena vengono creati e modificati.  

![Avviso SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Hello [soluzione Alert Management](http://technet.microsoft.com/library/mt484092.aspx) fornisce un riepilogo di avvisi attivi e diverse query comuni tooretrieve diversi set di avvisi.  In questo modo, l’analisi degli avvisi è più efficace rispetto a un report in SCOM.  È possibile drill-down dai dati toodetailed riepiloghi di hello e creare query ad hoc tooretrieve diversi set di avvisi.

![soluzione Alert Management](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Notifiche
Le notifiche in SCOM inviano posta elettronica di testo nella risposta tooalerts che soddisfano determinati criteri.  È possibile creare sottoscrizioni di notifica diversi che dispongono di utenti diversi di una notifica in base a criteri quali oggetto hello monitorati, hello gravità dell'avviso hello, tipo hello di problema che ha rilevato o hello ora del giorno.

Alcune sottoscrizioni possono essere utilizzato tooimplement una strategia di notifica di completamento per un numero elevato di management pack.

![Avvisi SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Log Analytics può inviarti una notifica tramite posta elettronica per comunicarti che è stato creato un avviso impostando un'azione di notifica di posta elettronica per ogni [regola di avviso](http://technet.microsoft.com/library/mt614775.aspx).  È il possibilità hello di hello SCOM sottoscrivere avvisi toomultiple con una singola regola.  È inoltre necessario toocreate proprie regole di avviso poiché OMS non fornisce qualsiasi preconfigurati.

![Avvisi Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

È completamente non è possibile gestire gli avvisi SCOM in Log Analitica tuttavia poiché è possibile modificare solo nella Console operatore hello.  Log Analytics è però utile come parte di un processo di gestione degli avvisi per fornire gli strumenti di analisi di cui SCOM da solo non dispone.

## <a name="alert-remediation"></a>Correzione tramite avvisi
[Monitoraggio e aggiornamento](http://technet.microsoft.com/library/mt614775.aspx) fa riferimento problema hello corretto tooautomatically tentativo di tooan identificato da un avviso.

SCOM consente toorun diagnostica e ripristini in Monitoraggio tooa risposta immesso uno stato non integro.  In questo caso monitoraggio toohello simultanee creazione hello avviso.  Diagnostica e ripristini in genere vengono implementati come uno script eseguito sull'agente hello.  Ulteriori informazioni su hello toogather una diagnostica tentativi rilevato problema durante i tentativi di ripristino di un problema di hello toocorrect.

Log Analitica consente toostart un [runbook di automazione di Azure](https://azure.microsoft.com/documentation/services/automation/) o chiamare un webhook nell'avviso di Log Analitica tooa di risposta.  I runbook possono includere logica complessa implementata in PowerShell.  script Hello in esecuzione in Azure e possono accedere le risorse di Azure o le risorse esterne disponibili dal cloud hello.  Automazione di Azure in un server nel data center locale sono hello possibilità tooexecute runbook, ma questa funzionalità non è attualmente disponibile all'avvio di runbook hello negli avvisi di risposta tooLog Analitica.

Ripristini in SCOM sia i runbook in OMS possono includere gli script di PowerShell, ma i ripristini toocreate più difficile e gestire perché devono essere contenuti all'interno di un management pack.  I runbook vengono archiviati in Automazione di Azure, che fornisce funzionalità per la creazione, l’esecuzione di test e la gestione dei runbook.

Se si utilizza SCOM come un'origine dati per i Log Analitica, è possibile creare un avviso di Log Analitica utilizzando un tooretrieve query log SCOM avvisi archiviati in hello repository OMS.  In questo modo si toorun un runbook di automazione di Azure nell'avviso SCOM tooa di risposta.  Naturalmente, poiché hello runbook verranno eseguiti in Azure, ciò non sarebbe una strategia valida per i ripristini dei problemi in locale.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni sul supporto di hello [alerts in System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

