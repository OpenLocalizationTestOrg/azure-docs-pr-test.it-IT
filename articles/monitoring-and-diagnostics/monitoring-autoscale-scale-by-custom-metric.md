---
title: "aaaGet avviata con scalabilità automatica da metrica personalizzata in Azure | Documenti Microsoft"
description: Informazioni su come tooscale la risorsa in base alla metrica personalizzata in Azure.
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
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="40c59-103">Introduzione alla scalabilità automatica in base a una metrica personalizzata in Azure</span><span class="sxs-lookup"><span data-stu-id="40c59-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="40c59-104">Questo articolo viene descritto come tooscale la risorsa da una metrica personalizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40c59-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="40c59-105">Azure ridimensionamento automatico di monitoraggio si applica solo tooVirtual set di scalabilità macchina (VMSS), servizi cloud, piani di servizio app e gli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="40c59-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="40c59-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="40c59-106">Lets get started</span></span>
<span data-ttu-id="40c59-107">In questo articolo si presuppone che l'utente abbia un'app Web con Application Insights configurato.</span><span class="sxs-lookup"><span data-stu-id="40c59-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="40c59-108">Se non è già stato fatto, è possibile [configurare Application Insights per il sito Web ASP.NET][1].</span><span class="sxs-lookup"><span data-stu-id="40c59-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="40c59-109">Aprire il [portale di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="40c59-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="40c59-110">Fare clic sull'icona di monitoraggio di Azure nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="40c59-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="40c59-111">![Avviare Monitoraggio di Azure][3]</span><span class="sxs-lookup"><span data-stu-id="40c59-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="40c59-112">Fare clic su impostazioni tooview tutte le risorse di hello per cui automaticamente la scala è applicabile, e il relativo stato corrente di scalabilità automatica di scalabilità automatica ![individuare il ridimensionamento automatico in monitor di Azure][4]</span><span class="sxs-lookup"><span data-stu-id="40c59-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="40c59-113">Aprire Pannello 'Autoscale' in Monitoraggio di Azure e selezionare una risorsa che si desidera tooscale</span><span class="sxs-lookup"><span data-stu-id="40c59-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="40c59-114">Nota: procedura hello utilizza un piano di servizio app associato a un'app web che ha configurati informazioni di app.</span><span class="sxs-lookup"><span data-stu-id="40c59-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="40c59-115">Nel Pannello di impostazione hello scala per la risorsa hello, si noti che il numero di istanze correnti di hello è 1.</span><span class="sxs-lookup"><span data-stu-id="40c59-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="40c59-116">Fare clic su 'Abilita scalabilità automatica'.</span><span class="sxs-lookup"><span data-stu-id="40c59-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="40c59-117">![Impostazione di scalabilità per la nuova app Web][5]</span><span class="sxs-lookup"><span data-stu-id="40c59-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="40c59-118">Fornire un nome per l'impostazione di scala di hello e hello fare clic su "Aggiungi una regola di".</span><span class="sxs-lookup"><span data-stu-id="40c59-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="40c59-119">Si noti hello regola le opzioni della scala che viene visualizzata come riquadro contesto sul lato destro di hello.</span><span class="sxs-lookup"><span data-stu-id="40c59-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="40c59-120">Per impostazione predefinita, imposta l'istanza 1 conteggio se hello CPU percetage della risorsa hello è superiore al 70% di hello opzione tooscale.</span><span class="sxs-lookup"><span data-stu-id="40c59-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="40c59-121">Origine della metrica hello modifica nella parte superiore di hello troppo "Application Insights", selezionare hello risorse insights app nell'elenco a discesa 'Resource' hello e metrica personalizzata di hello quindi in base in cui si desidera tooscale.</span><span class="sxs-lookup"><span data-stu-id="40c59-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="40c59-122">![Ridimensionare in base a una metrica personalizzata][6]</span><span class="sxs-lookup"><span data-stu-id="40c59-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="40c59-123">Passaggio di toohello simile precedente, aggiungere una regola di scala che scalabilità e ridurre il numero di scala hello di 1 se la metrica personalizzata hello è inferiore alla soglia.</span><span class="sxs-lookup"><span data-stu-id="40c59-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="40c59-124">![Scalabilità in base alla CPU][7]</span><span class="sxs-lookup"><span data-stu-id="40c59-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="40c59-125">Impostare i limiti dell'istanza hello.</span><span class="sxs-lookup"><span data-stu-id="40c59-125">Set hello you instance limits.</span></span> <span data-ttu-id="40c59-126">Ad esempio, se si desidera tooscale tra 2 e 5 istanze a seconda delle fluttuazioni metrica personalizzata hello, impostare 'minimo' troppo '2', 'massimo' troppo '5' e 'default' troppo '2'</span><span class="sxs-lookup"><span data-stu-id="40c59-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="40c59-127">Nota: nel caso in cui si verifica un problema durante la lettura delle metriche delle risorse hello e capacità corrente hello è di sotto di capacità predefinita hello, quindi la disponibilità di hello tooensure della risorsa di hello, scalabilità automatica verranno scalabilità toohello predefinita.</span><span class="sxs-lookup"><span data-stu-id="40c59-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="40c59-128">Se la capacità corrente hello è superiore alla capacità predefinita, la scalabilità automatica non verranno scalare.</span><span class="sxs-lookup"><span data-stu-id="40c59-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="40c59-129">Fare clic su 'Salva'</span><span class="sxs-lookup"><span data-stu-id="40c59-129">Click on 'Save'</span></span>

<span data-ttu-id="40c59-130">A questo punto</span><span class="sxs-lookup"><span data-stu-id="40c59-130">Congratulations.</span></span> <span data-ttu-id="40c59-131">È ora la scala, l'impostazione di app web in base a una metrica personalizzata tooauto scala creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="40c59-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="40c59-132">Nota: hello stessi passaggi sono applicabili tooget avviato con un ruolo del servizio VMSS o cloud.</span><span class="sxs-lookup"><span data-stu-id="40c59-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
