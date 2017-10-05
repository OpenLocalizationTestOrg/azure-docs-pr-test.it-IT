---
title: "Introduzione alla scalabilità automatica in Azure | Documentazione Microsoft"
description: Informazioni su come ridimensionare la risorsa in Azure.
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="d2c4d-103">Introduzione alla scalabilità automatica in Azure</span><span class="sxs-lookup"><span data-stu-id="d2c4d-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="d2c4d-104">Questo articolo descrive come configurare l'impostazione di scalabilità automatica per la risorsa nel portale di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="d2c4d-105">La scalabilità automatica di Monitoraggio di Azure si applica solo a set di scalabilità di macchine virtuali, servizi cloud, piani di servizio app di Azure e ambienti di servizio app.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="d2c4d-106">Individuare le impostazioni di scalabilità automatica nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d2c4d-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="d2c4d-107">È possibile individuare tutte le risorse per le quali è applicabile la scalabilità automatica in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="d2c4d-108">Eseguire i passaggi descritti di seguito per una procedura guidata:</span><span class="sxs-lookup"><span data-stu-id="d2c4d-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="d2c4d-109">Aprire il [portale di Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="d2c4d-110">Fare clic sull'icona di Monitoraggio di Azure nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="d2c4d-111">![Aprire Monitoraggio di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="d2c4d-112">Fare clic su **Scalabilità automatica** per visualizzare tutte le risorse per cui è applicabile, nonché il relativo stato corrente di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="d2c4d-113">![Individuazione della scalabilità automatica nel Monitoraggio di Azure][3]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="d2c4d-114">È possibile usare il riquadro filtro nella parte superiore per ridurre l'ambito dell'elenco e selezionare le risorse in un gruppo di risorse specifico, i tipi di risorse specifici o una determinata risorsa.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="d2c4d-115">Per ogni risorsa verranno indicati il numero di istanze corrente e lo stato di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="d2c4d-116">Lo stato di scalabilità automatica può essere:</span><span class="sxs-lookup"><span data-stu-id="d2c4d-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="d2c4d-117">**Non configurato**: non è stata ancora abilitata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="d2c4d-118">**Configurato**: è stata abilitata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="d2c4d-119">**Disattivato**: è stata disattivata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="d2c4d-120">Creare la prima impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d2c4d-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="d2c4d-121">Verrà ora illustrata una semplice procedura dettagliata per creare la prima impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="d2c4d-122">Aprire il pannello **Scalabilità automatica** in Monitoraggio di Azure e selezionare una risorsa da ridimensionare</span><span class="sxs-lookup"><span data-stu-id="d2c4d-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="d2c4d-123">(la procedura seguente usa un piano di servizio app associato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="d2c4d-124">È possibile [creare la prima app Web ASP.NET in Azure in 5 minuti][4]).</span><span class="sxs-lookup"><span data-stu-id="d2c4d-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="d2c4d-125">Notare che il numero corrente di istanze per il ruolo è 1.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="d2c4d-126">Fare clic su **Abilita scalabilità automatica**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="d2c4d-127">![Impostazione di scalabilità per la nuova app Web][5]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="d2c4d-128">Specificare un nome per il set di scalabilità, quindi scegliere **Aggiungi una regola**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="d2c4d-129">Si notino le opzioni per le regole di scalabilità visualizzate come riquadro contesto sul lato destro.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="d2c4d-130">Per impostazione predefinita viene applicata l'opzione per aumentare il numero di istanze di 1 se la percentuale CPU della risorsa supera il 70 per cento.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="d2c4d-131">Lasciare i valori predefiniti e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="d2c4d-132">![Creare l'impostazione di scalabilità per un'app Web][6]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="d2c4d-133">È stata così creata la prima regola di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-133">You've now created your first scale rule.</span></span> <span data-ttu-id="d2c4d-134">Si noti che l'esperienza utente indica le procedure consigliate e che "È consigliabile includere almeno una regola di riduzione del numero di istanze".</span><span class="sxs-lookup"><span data-stu-id="d2c4d-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="d2c4d-135">A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="d2c4d-135">To do so:</span></span>
  
    <span data-ttu-id="d2c4d-136">a.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-136">a.</span></span> <span data-ttu-id="d2c4d-137">Fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="d2c4d-138">b.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-138">b.</span></span> <span data-ttu-id="d2c4d-139">Impostare **Operatore** a **Minore di**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="d2c4d-140">c.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-140">c.</span></span> <span data-ttu-id="d2c4d-141">Impostare **Soglia** su **20**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="d2c4d-142">d.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-142">d.</span></span> <span data-ttu-id="d2c4d-143">Impostare **Operazione** su **Diminuisci il numero di**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="d2c4d-144">A questo punto si avrà un'impostazione di scalabilità che aumenta/riduce il numero di istanze in base all'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="d2c4d-145">![Scalabilità in base alla CPU][8]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="d2c4d-146">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-146">Click **Save**.</span></span>

<span data-ttu-id="d2c4d-147">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-147">Congratulations!</span></span> <span data-ttu-id="d2c4d-148">A questo punto è stata creata la prima impostazione di scalabilità automatica per l'app Web in base all'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="d2c4d-149">Gli stessi passaggi sono applicabili ai set di scalabilità di macchine virtuali e al ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="d2c4d-150">Altre considerazioni</span><span class="sxs-lookup"><span data-stu-id="d2c4d-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="d2c4d-151">Scalare in base a una pianificazione</span><span class="sxs-lookup"><span data-stu-id="d2c4d-151">Scale based on a schedule</span></span>
<span data-ttu-id="d2c4d-152">Oltre alla scalabilità basata sempre sulla CPU, è possibile impostare la scalabilità in modo diverso per giorni specifici della settimana.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="d2c4d-153">Fare clic su **Aggiungi una condizione di scalabilità**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="d2c4d-154">L'impostazione della modalità e delle regole di scalabilità è uguale alla condizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="d2c4d-155">Selezionare **Ripeti in giorni specifici** per la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="d2c4d-156">Selezionare i giorni e l'ora di inizio/fine per l'applicazione della condizione di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Condizione di scalabilità in base alla pianificazione][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="d2c4d-158">Impostare la scalabilità in modo diverso per date specifiche</span><span class="sxs-lookup"><span data-stu-id="d2c4d-158">Scale differently on specific dates</span></span>
<span data-ttu-id="d2c4d-159">Oltre alla scalabilità basata sempre sulla CPU, è possibile impostare la scalabilità in modo diverso per le date specifiche.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="d2c4d-160">Fare clic su **Aggiungi una condizione di scalabilità**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="d2c4d-161">L'impostazione della modalità e delle regole di scalabilità è uguale alla condizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="d2c4d-162">Selezionare **Specificare le date di inizio/fine** per la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="d2c4d-163">Selezionare i giorni e l'ora di inizio/fine per l'applicazione della condizione di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Condizione di scalabilità in base alle date][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="d2c4d-165">Visualizzare la cronologia di scalabilità della risorsa</span><span class="sxs-lookup"><span data-stu-id="d2c4d-165">View the scale history of your resource</span></span>
<span data-ttu-id="d2c4d-166">Ogni volta che vengono aumentate o ridotte le prestazioni della risorsa, viene registrato un evento nel log attività.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="d2c4d-167">È possibile visualizzare la cronologia della scalabilità della risorsa per le ultime 24 ore passando alla scheda **Cronologia di esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![Cronologia di esecuzione][11]

<span data-ttu-id="d2c4d-169">Per visualizzare la cronologia della scalabilità completa (fino a 90 giorni), selezionare **Fare clic qui per visualizzare altri dettagli**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="d2c4d-170">Si aprirà il log attività con Scalabilità automatica preselezionata per la risorsa e la categoria.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="d2c4d-171">Visualizzare la definizione di scalabilità della risorsa</span><span class="sxs-lookup"><span data-stu-id="d2c4d-171">View the scale definition of your resource</span></span>
<span data-ttu-id="d2c4d-172">Scalabilità automatica è una risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="d2c4d-173">È possibile visualizzare la definizione del piano in JSON passando alla scheda **JSON**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Definizione del piano][12]

<span data-ttu-id="d2c4d-175">È possibile apportare modifiche direttamente in JSON, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="d2c4d-176">Queste modifiche saranno applicate dopo averle salvate.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="d2c4d-177">Disabilitare la scalabilità automatica e ridimensionare le istanze manualmente</span><span class="sxs-lookup"><span data-stu-id="d2c4d-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="d2c4d-178">A volte può essere opportuno disabilitare l'impostazione di scalabilità corrente e ridimensionare la risorsa manualmente.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="d2c4d-179">Fare clic sul pulsante **Disabilita scalabilità automatica** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="d2c4d-180">![Disabilita scalabilità automatica][13]</span><span class="sxs-lookup"><span data-stu-id="d2c4d-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="d2c4d-181">Questa opzione disabilita la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-181">This option disables your configuration.</span></span> <span data-ttu-id="d2c4d-182">Tuttavia, è possibile ritornare dopo aver abilitato nuovamente la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="d2c4d-183">È ora possibile impostare il numero di istanze da ridimensionare manualmente.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Impostare la scalabilità manuale][14]

<span data-ttu-id="d2c4d-185">È sempre possibile impostare nuovamente la scalabilità automatica facendo clic su **Abilita scalabilità automatica** e quindi su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2c4d-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2c4d-186">Next steps</span></span>
- [<span data-ttu-id="d2c4d-187">Creare un avviso di log attività per monitorare tutte le operazioni del motore di scalabilità automatica della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d2c4d-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="d2c4d-188">Creare un avviso di log attività per monitorare tutte le operazioni di scalabilità automatica in riduzione e in aumento non riuscite per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d2c4d-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

