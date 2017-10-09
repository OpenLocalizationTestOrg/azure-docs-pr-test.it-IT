---
title: origini dati aaaConfigure in OMS Log Analitica | Documenti Microsoft
description: Origini dati definiscono i dati di hello che raccoglie Log Analitica dagli agenti e l'altra connessa origini.  In questo articolo viene descritto il concetto di hello di origini dati di utilizzo Log Analitica, spiega in dettaglio hello come tooconfigure e fornisce un riepilogo delle origini dati diverse hello disponibili.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Origini dati in Log Analytics
Raccoglie i dati da origini connesse hello nell'area di lavoro OMS log Analitica e lo archivia nel repository OMS.  Hello i dati raccolti da ogni sono definiti da origini dati che configurano hello.  Dati nel repository OMS hello vengono archiviati come un set di record.  Ogni origine dati crea record di un tipo specifico in cui ogni tipo ha un proprio set di proprietà.

![Raccolta dei dati di Log Analytics](./media/log-analytics-data-sources/overview.png)

Origini dati sono diverse rispetto alle soluzioni OMS che anche raccogliere dati da origini connesse e creare i record nel repository OMS hello.  Soluzioni possono essere aggiunta l'area di lavoro tooyour di hello Solutions Gallery e in genere forniscono gli strumenti di analisi aggiuntive nel portale OMS hello.  

## <a name="summary-of-data-sources"></a>Riepilogo delle origini dati
Nella hello nella tabella seguente sono elencate le origini dati Hello che sono attualmente disponibili nel Log Analitica.  Ognuno presenta un articolo separato tooa collegamento fornire informazioni dettagliate per l'origine dati.

| origine dati | Tipo evento | Descrizione |
|:--- |:--- |:--- |
| [Log personalizzati](log-analytics-data-sources-custom-logs.md) |\<LogName\>_CL |File di testo negli agenti Windows o Linux contenenti le informazioni di log. |
| [Log eventi di Windows](log-analytics-data-sources-windows-events.md) |Evento |Gli eventi raccolti dai log eventi hello nei computer Windows. |
| [Contatori delle prestazioni di Windows](log-analytics-data-sources-performance-counters.md) |Perf |Contatori delle prestazioni raccolti dai computer Windows. |
| [Contatori delle prestazioni di Linux](log-analytics-data-sources-performance-counters.md) |Perf |Contatori delle prestazioni raccolti dai computer Linux. |
| [Log IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Log di Internet Information Services in formato W3C. |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Eventi syslog nei computer Windows o Linux. |

## <a name="configuring-data-sources"></a>Configurazione delle origini dati
Configurare le origini dati da hello **dati** dal menu Registro Analitica **impostazioni**.  Qualsiasi configurazione viene recapitata origini tooall connesso nell'area di lavoro OMS.  Attualmente non è possibile escludere gli agenti da questa configurazione.

![Configurare gli eventi di Windows](./media/log-analytics-data-sources/configure-events.png)

1. Nella console OMS hello fare clic su hello **impostazioni** riquadro o hello **impostazioni** pulsante in alto hello hello.
2. Selezionare **Dati**.
3. Fare clic su tooconfigure di origine dati hello.
4. Seguire la documentazione di hello collegamento toohello per ogni origine dati in hello sopra tabella per informazioni dettagliate per la configurazione.

> [!NOTE]
> Attualmente non è possibile configurare origini dati di Log Analitica in hello portale di Azure.

## <a name="data-collection"></a>Raccolta dei dati
Le configurazioni di origine dati vengono recapitate tooagents che sono direttamente connessi tooLog Analitica entro pochi minuti.  Hello specificato i dati vengono raccolti dall'agente hello e recapitati direttamente tooLog Analitica nell'origine dati di intervalli tooeach specifico.  Vedere la documentazione di hello per ogni origine dati per queste specifiche.

Per gli agenti di System Center Operations Manager (SCOM) in un gruppo di gestione connesso, configurazioni di origine dati vengono convertite in management pack e recapitare il gruppo di gestione toohello ogni 5 minuti per impostazione predefinita.  l'agente Hello Scarica hello management pack come qualsiasi altro e raccoglie hello dati specificato. A seconda di hello di origine dati hello dati sarà inviato tooa i server di gestione che inoltra hello dati toohello Log Analitica o hello agente invierà i dati di hello tooLog Analitica senza passare attraverso il server di gestione di hello. Fare riferimento troppo[dettagli sulla raccolta dei dati per la funzionalità e soluzioni OMS](log-analytics-add-solutions.md#data-collection-details) per informazioni dettagliate.  È possibile leggere informazioni sui dettagli di connessione di SCOM e OMS e modifica la frequenza di hello che la configurazione viene recapitato a [configurare l'integrazione con System Center Operations Manager](log-analytics-om-agents.md).

Se non è possibile tooconnect tooLog Analitica o Operations Manager, agente hello continuerà toocollect dati che apporterà quando viene stabilita una connessione.  Se hello dei dati raggiunge dimensioni massime della cache di hello per client hello o se l'agente di hello non è in grado di tooestablish una connessione entro 24 ore, i dati possono andare perduti.

## <a name="log-analytics-records"></a>Record di Log Analytics
Tutti i dati raccolti da Log Analitica vengono archiviati nel repository OMS hello come record.  I record raccolti da diverse origini dati avranno il proprio set di proprietà e verranno identificati dalla proprietà **Type** .  Vedere la documentazione di hello per ogni origine dati e soluzioni per informazioni dettagliate su ogni tipo di record.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [soluzioni](log-analytics-add-solutions.md) che aggiungere funzionalità tooLog Analitica e inoltre raccogliere i dati nel repository OMS hello.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.  
* Configurare [avvisi](log-analytics-alerts.md) tooproactively ricevere una notifica di dati critici raccolti da origini dati e soluzioni.
