---
title: aaaCollect e analizzare i registri eventi di Windows in OMS Log Analitica | Documenti Microsoft
description: "I registri eventi di Windows sono una delle origini dati più comuni di hello utilizzate dal Log Analitica.  Questo articolo descrive come tooconfigure raccolta dei registri eventi di Windows e i dettagli del record di hello che ha creato nel repository OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Origini dei dati del registro eventi di Windows in Log Analytics
I registri eventi di Windows sono uno dei più comuni di hello [origini dati](log-analytics-data-sources.md) per raccogliere i dati di utilizzo degli agenti di Windows poiché molte applicazioni scrivono toohello registro eventi di Windows.  È possibile raccogliere gli eventi dai registri standard, ad esempio applicazioni e di sistema in toospecifying inoltre qualsiasi log personalizzato creato dalle applicazioni, è necessario toomonitor.

![Eventi Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configurazione dei registri eventi di Windows
Configurare i registri eventi di Windows hello [menu dati nelle impostazioni di registro Analitica](log-analytics-data-sources.md#configuring-data-sources).

Log Analitica raccoglie solo gli eventi dai registri eventi di Windows hello specificati nelle impostazioni di hello.  È possibile aggiungere un registro eventi digitando il nome del log hello hello e facendo clic su  **+** .  Per ogni log, vengono raccolti solo gli eventi di hello con livelli di gravità hello selezionato.  Controllare i livelli di gravità hello per il log di hello specifico che si desidera toocollect.  È possibile fornire eventuali criteri aggiuntivi toofilter eventi.

Mentre si digita il nome di hello di un registro eventi, Log Analitica fornisce suggerimenti di nomi di registro eventi comuni. Se log hello da tooadd non compare nell'elenco di hello, è possibile aggiungerlo digitando nel nome completo di hello del log hello. Nome completo di hello del log hello è possibile trovare il Visualizzatore eventi. Nel Visualizzatore eventi aprire hello *proprietà* pagina per hello log e copia hello stringa hello *nome completo* campo.

![Configurare gli eventi di Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Raccolta dei dati
Log Analitica raccoglie ogni evento che corrisponde a un livello di gravità selezionato da un registro eventi monitorato come evento hello viene creato.  agente Hello registra al suo posto in ogni log di eventi raccolti da.  Se l'agente di hello passa alla modalità offline per un periodo di tempo, quindi Log Analitica raccoglie gli eventi dall'ultimo libero, anche se tali eventi sono stati creati mentre hello agent era offline.  È possibile che per essere raccolti toonot questi eventi, se il registro eventi di hello esegue il wrapping con eventi posteriori venga sovrascritti durante hello agente è offline.

>[!NOTE]
>Log Analytics non raccoglie gli eventi di controllo creati da SQL Server dal *MSSQLSERVER* di origine con l'ID evento 18453 che contiene le parole chiave *Classico* o *Successo del controllo* e la parola chiave *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Proprietà dei record eventi di Windows
Record degli eventi di Windows dispone di un tipo di **evento** e dispone di proprietà hello in hello nella tabella seguente:

| Proprietà | Descrizione |
|:--- |:--- |
| Computer |Nome del computer hello hello eventi raccolti da. |
| EventCategory |Categoria di eventi di hello. |
| EventData |Tutti i dati dell'evento in formato non elaborato. |
| EventID |Numero di eventi di hello. |
| EventLevel |Gravità dell'evento hello in formato numerico. |
| EventLevelName |Gravità dell'evento hello in formato testo. |
| EventLog |Nome del registro eventi di hello hello eventi raccolti da. |
| ParameterXml |Valori dei parametri dell'evento in formato XML. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti di System Center Operations Manager.  Per gli altri agenti, questo valore corrisponde a AOI-<workspace ID> |
| RenderedDescription |Descrizione dell'evento con i valori dei parametri. |
| Sorgente |Origine dell'evento hello. |
| SourceSystem |Tipo di agente hello evento sono stati raccolti da. <br> OpsManager: agente Windows, con connessione diretta o gestita da Operations Manager <br> Linux – Tutti gli agenti Linux  <br> AzureStorage: Diagnostica di Azure |
| TimeGenerated |Data e ora evento hello è stato creato in Windows. |
| UserName |Nome utente dell'account di hello che ha registrato hello evento. |

## <a name="log-searches-with-windows-events"></a>Ricerche nei log con Eventi Windows
Hello nella tabella seguente vengono forniti esempi di ricerche nei log che recuperano i record degli eventi di Windows.

| Query | Descrizione |
|:--- |:--- |
| Tipo=Event |Tutti gli eventi di Windows. |
| Tipo=Event EventLevelName=error |Tutti gli eventi di Windows con livello di gravità dell'errore. |
| Tipo=Event &#124; Measure count() by Source |Numero di eventi di Windows per origine. |
| Tipo=Event EventLevelName=error &#124; Measure count() by Source |Numero di eventi di errore di Windows per origine. |


>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.
>
>| Query | Descrizione |
|:---|:---|
| Evento |Tutti gli eventi di Windows. |
| Event &#124; where EventLevelName == "error" |Tutti gli eventi di Windows con livello di gravità dell'errore. |
| Event &#124; summarize count() by Source |Numero di eventi di Windows per origine. |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |Numero di eventi di errore di Windows per origine. |


## <a name="next-steps"></a>Passaggi successivi
* Configurare altri toocollect Log Analitica [origini dati](log-analytics-data-sources.md) per l'analisi.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.  
* Utilizzare [campi personalizzati](log-analytics-custom-fields.md) record degli eventi di hello tooparse in singoli campi.
* Configurare la [raccolta dei contatori delle prestazioni](log-analytics-data-sources-performance-counters.md) dagli agenti di Windows.
