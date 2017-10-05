---
title: Configurare avvisi per le query in Analisi di flusso | Microsoft Docs
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
ms.openlocfilehash: 75b1b256eea7295f5a464996e2f34ae301c715fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="a2079-104">Impostare gli avvisi per i processi di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="a2079-105">Introduzione: Pagina di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="a2079-105">Introduction: Monitor page</span></span>
<span data-ttu-id="a2079-106">È possibile configurare avvisi per attivare un avviso quando una metrica raggiunge una condizione specificata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a2079-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="a2079-107">Ad esempio, si potrebbe configurare un avviso per una condizione simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a2079-107">For example, you might set up an alert for a condition like the following:</span></span>

`If there are zero input events in the last 5 minutes, send email notification to sa-admin@example.com`

<span data-ttu-id="a2079-108">Possono essere configurate regole per le metriche tramite il portale o [a livello di codice](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sui dati dei log delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="a2079-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-the-azure-portal"></a><span data-ttu-id="a2079-109">Configurare gli avvisi nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-109">Set up alerts in the Azure portal</span></span>
1. <span data-ttu-id="a2079-110">Nel portale di Azure aprire il processo di Analisi di flusso per cui si intende creare un avviso.</span><span class="sxs-lookup"><span data-stu-id="a2079-110">In the Azure portal, open the Stream Analytics job you want to create an alert for.</span></span> 

2. <span data-ttu-id="a2079-111">Nel pannello **Processo** fare clic sulla sezione **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="a2079-111">In the **Job** blade, click the **Monitoring** section.</span></span>  

3. <span data-ttu-id="a2079-112">Nel pannello **Metrica** fare clic sul comando **Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="a2079-112">In the **Metric** blade, click the **Add alert** command.</span></span>

      ![Installazione del portale di Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="a2079-114">Immettere un nome e una descrizione.</span><span class="sxs-lookup"><span data-stu-id="a2079-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="a2079-115">Usare i selettori per definire la condizione in cui verrà inviato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="a2079-115">Use the selectors to define the condition under which the alert will be sent.</span></span>

6. <span data-ttu-id="a2079-116">Fornire informazioni su dove dovrebbe andare l'avviso.</span><span class="sxs-lookup"><span data-stu-id="a2079-116">Provide information about where the alert should go.</span></span>

      ![Configurazione di un avviso per un processo di Analisi di flusso di Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="a2079-118">Per altre informazioni dettagliate sulla configurazione degli avvisi nel portale di Azure, vedere [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) (Ricevere notifiche di avviso).</span><span class="sxs-lookup"><span data-stu-id="a2079-118">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="a2079-119">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="a2079-119">Get help</span></span>
<span data-ttu-id="a2079-120">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a2079-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2079-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2079-121">Next steps</span></span>
* [<span data-ttu-id="a2079-122">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-122">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a2079-123">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="a2079-124">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a2079-125">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a2079-126">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="a2079-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

