---
title: "attività di Azure aaaView registra con Log Analitica | Documenti Microsoft"
description: "Per tutte le sottoscrizioni di Azure, è possibile utilizzare hello log attività Azure soluzione tooanalyze e ricerca hello registro attività di Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Visualizzare i log attività di Azure

![Simbolo di Log attività di Azure](./media/log-analytics-activity/activity-log-analytics.png)

Hello soluzione Analitica Log attività consente di analizzare e cercare hello [log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) per tutte le sottoscrizioni di Azure. Hello Log attività di Azure è un log che offre informazioni dettagliate sui hello operazioni eseguite sulle risorse nelle sottoscrizioni dell'utente. Hello Log attività era precedentemente noto come *i log di controllo* o *registri* poiché segnala gli eventi per le sottoscrizioni.

Hello registro attività, consentono di determinare hello *cosa*, *che*, e *quando* per qualsiasi scrittura (PUT, POST, DELETE) effettuate per le risorse di hello nella sottoscrizione. È anche possibile comprendere lo stato di hello di operazioni di hello e altre proprietà pertinenti. non include Hello Log attività di lettura (GET) operazioni o per risorse che utilizzano il modello di distribuzione classica hello.

Quando ci si connette il tooLog log attività Azure Analitica, è possibile:

- Analizzare i log attività hello con visualizzazioni predefinite
- Analizzare e cercare i log attività di più sottoscrizioni di Azure
- Conservare i log attività per più di 90 giorni<sup>1</sup>
- Correlare i log attività con altri dati dell'applicazione e della piattaforma di Azure
- Vedere le attività operative aggregate in base allo stato
- Visualizzare le tendenze delle attività in corso su ognuno dei servizi di Azure
- Segnalare le modifiche alle autorizzazioni in tutte le proprie risorse di Azure
- Identificare i problemi di integrità del servizio o le interruzioni che inficiano il funzionamento delle risorse
- Utilizzare le attività degli utenti toocorrelate ricerca nei Log, operazioni di ridimensionamento automatico, le autorizzazioni e registri tooother di integrità del servizio o metrica dall'ambiente di

<sup>1</sup>per impostazione predefinita, i log attività Azure mantiene Log Analitica per 90 giorni, anche se si è connessi a livello gratuito hello. Oppure, se si dispone di un'impostazione di conservazione dell'area di lavoro inferiore a 90 giorni. Se l'area di lavoro presenta un criterio di conservazione più lungo di 90 giorni, log attività hello vengono mantenuti per il periodo di memorizzazione hello dell'area di lavoro.

Log Analitica raccoglie i log di attività disponibile gratuitamente e archivia i registri di hello per 90 giorni gratuitamente. Se si archiviano i registri per più di 90 giorni, si comporteranno spese di conservazione dei dati per i dati di hello archiviati più di 90 giorni.

Quando ci si trova a livello di prezzo gratuito hello, log attività non si applicano tooyour utilizzo giornaliero dei dati.

## <a name="connected-sources"></a>Origini connesse

A differenza della maggior parte delle soluzioni di Log Analytics, i dati per i log attività non vengono raccolti dagli agenti. Tutti i dati utilizzati dalla soluzione hello proviene direttamente da Azure.

| Origine connessa | Supportato | Descrizione |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti Linux. |
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti in un gruppo di gestione SCOM connesso. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | soluzione Hello non raccoglie informazioni dall'archiviazione di Azure. |

## <a name="prerequisites"></a>Prerequisiti

- tooaccess informazioni del log attività di Azure, è necessario disporre di una sottoscrizione di Azure.

## <a name="configuration"></a>Configurazione

Eseguire hello seguente soluzione Analitica Log attività di passaggi tooconfigure hello per le aree di lavoro.

1. Abilitare soluzioni Analitica Log attività hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Configurare l'area di lavoro attività registri toogo tooyour Analitica di Log.
    1. In hello portale di Azure, selezionare l'area di lavoro e quindi fare clic su **log attività Azure**.
    2. Per ogni sottoscrizione, fare clic sul nome della sottoscrizione hello.  
        ![aggiungere sottoscrizione](./media/log-analytics-activity/add-subscription.png)
    3. In hello *SubscriptionName* pannello, fare clic su **Connetti**.  
        ![connettere sottoscrizione](./media/log-analytics-activity/subscription-connect.png)

Se si aggiunge una soluzione di hello tramite il portale di OMS hello, si noterà hello seguente riquadro. Accedi toohello tooconnect portale Azure un'area di lavoro tooyour sottoscrizione di Azure.  
![esecuzione della valutazione](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Quando si aggiunge l'area di lavoro tooyour soluzione Analitica Log attività hello, hello **log attività Azure** riquadro viene aggiunto il dashboard di panoramica tooyour. Questo riquadro consente di visualizzare un conteggio del numero di hello di record di attività di Azure per hello le sottoscrizioni di Azure hello soluzione ha accesso a.

![Riquadro Log attività di Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Visualizzare i log attività di Azure

Fare clic su hello **log attività Azure** riquadro tooopen hello **log attività Azure** dashboard. dashboard Hello include pannelli hello in hello nella tabella seguente. Ogni pannello elenca backup too10 elementi corrispondenti ai criteri del pannello per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che restituisce tutti i record facendo **tutti** nella parte inferiore di hello del pannello hello oppure facendo clic sull'intestazione di blade hello.

Viene visualizzata solo dati del log attività *dopo* configurati la soluzione toohello toogo log attività, in modo da non visualizzare i dati prima di allora.

| Pannello | Descrizione |
| --- | --- |
| Voci del Log attività di Azure | Mostra un grafico a barre dei primi hello voce di log attività Azure record totali per intervallo di date hello selezionato e Mostra un elenco di hello superiore ai chiamanti di attività 10. Fare clic su hello grafico a barre toorun una ricerca di log per <code>Type=AzureActivity</code>. Fare clic su un toorun elemento chiamante una ricerca nei log la restituzione di tutte le voci di log attività per l'elemento. |
| Log attività per stato | Mostra un grafico ad anello per lo stato del log attività di Azure per intervallo di date hello selezionato. Mostra anche un elenco di un elenco di record di stato dieci superiore hello. Fare clic su una ricerca di log per hello grafico toorun <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Fare clic su un toorun di elemento di stato, una ricerca nei log la restituzione di tutte le voci di log attività per il record di stato. |
| Log attività per risorsa | Mostra hello il numero totale di risorse con i log di attività ed elenca inizio hello conta dieci risorse record per ogni risorsa. Fare clic su una ricerca di log per hello area totale toorun <code>Type=AzureActivity &#124; measure count() by Resource</code>, che mostra tutte le risorse di Azure disponibili toohello soluzione. Fare clic su una risorsa toorun una ricerca nei log la restituzione di tutti i record di attività per tale risorsa. |
| Log attività per provider di risorse | Hello Mostra il numero totale di provider di risorse che producono attività registra ed elenca dieci hello. Fare clic su una ricerca di log per hello area totale toorun <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, che mostra tutti i provider di risorse di Azure. Fare clic su un toorun di provider di risorse restituzione di tutti i record di attività per il provider di hello una ricerca di log. |

![Dashboard Log attività di Azure](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Passaggi successivi

- Creare un [avviso](log-analytics-alerts-creating.md) quando si verifica un'attività specifica.
- Utilizzare [ricerca nei Log](log-analytics-log-searches.md) tooview informazioni dai registri attività.
