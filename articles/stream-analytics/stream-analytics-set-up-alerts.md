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
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="b2902-104">Impostare gli avvisi per i processi di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="b2902-105">Introduzione: Pagina di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="b2902-105">Introduction: Monitor page</span></span>
<span data-ttu-id="b2902-106">Impostare avvisi tootrigger un avviso quando una metrica raggiunge una condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="b2902-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="b2902-107">Ad esempio, potrebbe impostare un avviso per una condizione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b2902-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="b2902-108">Le regole possono essere configurate in metriche tramite il portale di hello oppure può essere configurate [a livello di programmazione](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sui dati di log operazioni.</span><span class="sxs-lookup"><span data-stu-id="b2902-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="b2902-109">Configurare gli avvisi di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="b2902-110">Nel portale di Azure hello, aprire il processo di flusso Analitica hello da toocreate un avviso per.</span><span class="sxs-lookup"><span data-stu-id="b2902-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="b2902-111">In hello **processo** pannello, fare clic su hello **monitoraggio** sezione.</span><span class="sxs-lookup"><span data-stu-id="b2902-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="b2902-112">In hello **metrica** pannello, fare clic su hello **Aggiungi avviso** comando.</span><span class="sxs-lookup"><span data-stu-id="b2902-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Installazione del portale di Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="b2902-114">Immettere un nome e una descrizione.</span><span class="sxs-lookup"><span data-stu-id="b2902-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="b2902-115">Utilizzare hello selettori toodefine hello condizione in cui hello verrà inviato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="b2902-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="b2902-116">Informazioni su esiti di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="b2902-116">Provide information about where hello alert should go.</span></span>

      ![Configurazione di un avviso per un processo di Analisi di flusso di Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="b2902-118">Per ulteriori informazioni sulla configurazione di avvisi hello portale di Azure, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="b2902-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="b2902-119">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="b2902-119">Get help</span></span>
<span data-ttu-id="b2902-120">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b2902-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2902-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2902-121">Next steps</span></span>
* [<span data-ttu-id="b2902-122">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="b2902-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b2902-123">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="b2902-124">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b2902-125">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b2902-126">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b2902-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

