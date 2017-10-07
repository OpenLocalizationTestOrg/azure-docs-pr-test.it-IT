---
title: aaaSet di avvisi per le query nel flusso Analitica | Documenti Microsoft
description: Informazioni sugli avvisi di Analisi di flusso
keywords: configurare avvisi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Impostare gli avvisi per i processi di Analisi di flusso di Azure
## <a name="introduction-monitor-page"></a>Introduzione: Pagina di monitoraggio
Impostare avvisi tootrigger un avviso quando una metrica raggiunge una condizione specificata. Ad esempio, potrebbe impostare un avviso per una condizione hello seguente:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Le regole possono essere configurate in metriche tramite il portale di hello oppure può essere configurate [a livello di programmazione](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sui dati di log operazioni.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Configurare gli avvisi di hello portale di Azure
1. Nel portale di Azure hello, aprire il processo di flusso Analitica hello da toocreate un avviso per. 

2. In hello **processo** pannello, fare clic su hello **monitoraggio** sezione.  

3. In hello **metrica** pannello, fare clic su hello **Aggiungi avviso** comando.

      ![Installazione del portale di Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Immettere un nome e una descrizione.

5. Utilizzare hello selettori toodefine hello condizione in cui hello verrà inviato l'avviso.

6. Informazioni su esiti di avviso hello.

      ![Configurazione di un avviso per un processo di Analisi di flusso di Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Per ulteriori informazioni sulla configurazione di avvisi hello portale di Azure, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-get-started.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

