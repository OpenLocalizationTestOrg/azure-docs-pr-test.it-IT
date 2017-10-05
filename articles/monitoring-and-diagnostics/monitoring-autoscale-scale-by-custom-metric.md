---
title: "Introduzione alla scalabilità automatica in base a una metrica personalizzata in Azure | Microsoft Docs"
description: Informazioni su come ridimensionare la risorsa in base a una metrica personalizzata in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: de8f7acadc282e4b81c657b1723f00fd3e5fd4f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="9706e-103">Introduzione alla scalabilità automatica in base a una metrica personalizzata in Azure</span><span class="sxs-lookup"><span data-stu-id="9706e-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="9706e-104">Questo articolo descrive come ridimensionare la risorsa in base a una metrica personalizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9706e-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="9706e-105">La scalabilità automatica di Monitoraggio di Azure si applica solo a set di scalabilità di macchine virtuali (VMSS), servizi cloud, piani di servizio app e ambienti di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9706e-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="9706e-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9706e-106">Lets get started</span></span>
<span data-ttu-id="9706e-107">In questo articolo si presuppone che l'utente abbia un'app Web con Application Insights configurato.</span><span class="sxs-lookup"><span data-stu-id="9706e-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="9706e-108">Se non è già stato fatto, è possibile [configurare Application Insights per il sito Web ASP.NET][1].</span><span class="sxs-lookup"><span data-stu-id="9706e-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="9706e-109">Aprire il [portale di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="9706e-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="9706e-110">Fare clic sull'icona di Monitoraggio di Azure nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9706e-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="9706e-111">![Avviare Monitoraggio di Azure][3]</span><span class="sxs-lookup"><span data-stu-id="9706e-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="9706e-112">Fare clic sull'impostazione Scalabilità automatica per visualizzare tutte le risorse per le quali è applicabile la scalabilità automatica, insieme allo stato corrente ![Individuare l'impostazione Scalabilità automatica in Monitoraggio di Azure][4]</span><span class="sxs-lookup"><span data-stu-id="9706e-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="9706e-113">Aprire il pannello 'Scalabilità automatica' in Monitoraggio di Azure e selezionare una risorsa da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="9706e-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="9706e-114">Nota: la procedura seguente usa un piano di servizio app associato a un'app Web con Application Insights configurato.</span><span class="sxs-lookup"><span data-stu-id="9706e-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="9706e-115">Nel pannello delle impostazioni di scalabilità automatica per la risorsa si noti che il numero di istanze corrente è 1.</span><span class="sxs-lookup"><span data-stu-id="9706e-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="9706e-116">Fare clic su 'Abilita scalabilità automatica'.</span><span class="sxs-lookup"><span data-stu-id="9706e-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="9706e-117">![Impostazione di scalabilità per la nuova app Web][5]</span><span class="sxs-lookup"><span data-stu-id="9706e-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="9706e-118">Specificare un nome per l'impostazione di scalabilità, quindi scegliere "Add a rule" (Aggiungi una regola).</span><span class="sxs-lookup"><span data-stu-id="9706e-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="9706e-119">Si notino le opzioni per le regole di scalabilità visualizzate come riquadro contesto sul lato destro.</span><span class="sxs-lookup"><span data-stu-id="9706e-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="9706e-120">Per impostazione predefinita viene applicata l'opzione per aumentare il numero di istanze di 1 se la percentuale CPU della risorsa supera il 70%.</span><span class="sxs-lookup"><span data-stu-id="9706e-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="9706e-121">Impostare l'origine della metrica nella parte superiore su "Application Insights", selezionare la risorsa Application Insights nell'elenco a discesa 'Risorsa' e quindi selezionare la metrica personalizzata in base a ciò che si vuole ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="9706e-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="9706e-122">![Ridimensionare in base a una metrica personalizzata][6]</span><span class="sxs-lookup"><span data-stu-id="9706e-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="9706e-123">Analogamente al passaggio precedente, aggiungere una regola di scalabilità che ridurrà il numero di istanze di 1 se la metrica personalizzata è al di sotto di una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="9706e-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="9706e-124">![Scalabilità in base alla CPU][7]</span><span class="sxs-lookup"><span data-stu-id="9706e-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="9706e-125">Impostare i limiti per le istanze.</span><span class="sxs-lookup"><span data-stu-id="9706e-125">Set the you instance limits.</span></span> <span data-ttu-id="9706e-126">Se ad esempio si vogliono ridimensionare da 2 a 5 istanze a seconda delle fluttuazioni della metrica personalizzata, impostare il valore minimo su 2, quello massimo su 5 e quello predefinito su 2</span><span class="sxs-lookup"><span data-stu-id="9706e-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="9706e-127">Nota: se si verifica un problema relativo alla metrica delle risorse e la capacità corrente è inferiore alla capacità predefinita, per assicurare la disponibilità della risorsa, la funzionalità di scalabilità automatica aumenterà il numero di istanze fino al valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="9706e-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="9706e-128">Se la capacità corrente è già superiore alla capacità predefinita, la funzionalità di scalabilità automatica non ridurrà il numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="9706e-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="9706e-129">Fare clic su 'Salva'</span><span class="sxs-lookup"><span data-stu-id="9706e-129">Click on 'Save'</span></span>

<span data-ttu-id="9706e-130">A questo punto</span><span class="sxs-lookup"><span data-stu-id="9706e-130">Congratulations.</span></span> <span data-ttu-id="9706e-131">A questo punto è stata creata l'impostazione di scalabilità automatica per l'app Web in base a una metrica personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9706e-131">You now now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="9706e-132">Nota: gli stessi passaggi sono applicabili ai set di scalabilità di macchine virtuali e al ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9706e-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
