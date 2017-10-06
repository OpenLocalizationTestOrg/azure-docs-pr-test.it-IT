---
title: "aaaGet avviato con scalabilità automatica in Azure | Documenti Microsoft"
description: Informazioni su come tooscale la risorsa in Azure.
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
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="49410-103">Introduzione alla scalabilità automatica in Azure</span><span class="sxs-lookup"><span data-stu-id="49410-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="49410-104">Questo articolo viene descritto come tooset backup delle impostazioni di scalabilità automatica per la risorsa nel portale di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="49410-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="49410-105">Azure scalabilità automatica di monitoraggio si applica solo set di scalabilità macchina toovirtual, servizi cloud, i piani di servizio App di Azure e gli ambienti del servizio App.</span><span class="sxs-lookup"><span data-stu-id="49410-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="49410-106">Individuare le impostazioni di scalabilità automatica hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="49410-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="49410-107">È possibile individuare tutte le risorse di hello per cui è applicabile in Monitor di Azure.</span><span class="sxs-lookup"><span data-stu-id="49410-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="49410-108">Utilizzare hello alla procedura seguente per una procedura dettagliata:</span><span class="sxs-lookup"><span data-stu-id="49410-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="49410-109">Aprire hello [portale di Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="49410-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="49410-110">Fare clic sull'icona di monitoraggio di Azure di hello nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="49410-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="49410-111">![Aprire Monitoraggio di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="49410-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="49410-112">Fare clic su **scalabilità automatica** tooview tutte le risorse di hello per la cui scalabilità automatica è applicabile, nonché il relativo stato corrente di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="49410-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="49410-113">![Individuazione della scalabilità automatica nel Monitoraggio di Azure][3]</span><span class="sxs-lookup"><span data-stu-id="49410-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="49410-114">È possibile utilizzare il riquadro di filtro hello in hello tooscope alto verso il basso hello elencano tooselect le risorse in un determinato gruppo di risorse, tipi di risorsa specifico o una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="49410-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="49410-115">Per ogni risorsa, si trova il numero di istanze correnti di hello e stato scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="49410-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="49410-116">Hello stato scalabilità automatica può essere:</span><span class="sxs-lookup"><span data-stu-id="49410-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="49410-117">**Non configurato**: non è stata ancora abilitata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="49410-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="49410-118">**Configurato**: è stata abilitata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="49410-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="49410-119">**Disattivato**: è stata disattivata la scalabilità automatica per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="49410-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="49410-120">Creare la prima impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="49410-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="49410-121">Verrà ora passano attraverso un toocreate semplice procedura dettagliata la prima impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="49410-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="49410-122">Aprire hello **scalabilità automatica** pannello in Monitor di Azure e selezionare una risorsa che si desidera tooscale.</span><span class="sxs-lookup"><span data-stu-id="49410-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="49410-123">(hello procedura seguente utilizza un piano di servizio App associato a un'app web.</span><span class="sxs-lookup"><span data-stu-id="49410-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="49410-124">È possibile [creare la prima app Web ASP.NET in Azure in 5 minuti][4]).</span><span class="sxs-lookup"><span data-stu-id="49410-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="49410-125">Si noti che il numero di istanze correnti di hello è 1.</span><span class="sxs-lookup"><span data-stu-id="49410-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="49410-126">Fare clic su **Abilita scalabilità automatica**.</span><span class="sxs-lookup"><span data-stu-id="49410-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="49410-127">![Impostazione di scalabilità per la nuova app Web][5]</span><span class="sxs-lookup"><span data-stu-id="49410-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="49410-128">Specificare un nome per la scala hello impostazione e quindi fare clic su **aggiungere una regola**.</span><span class="sxs-lookup"><span data-stu-id="49410-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="49410-129">Notare le opzioni della regola scala hello aperti come un riquadro contesto sul lato destro hello.</span><span class="sxs-lookup"><span data-stu-id="49410-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="49410-130">Per impostazione predefinita, consente di impostare l'istanza del conteggio di 1 se la percentuale di CPU della risorsa hello hello supera il 70% di hello opzione tooscale.</span><span class="sxs-lookup"><span data-stu-id="49410-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="49410-131">Lasciare i valori predefiniti e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="49410-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="49410-132">![Creare l'impostazione di scalabilità per un'app Web][6]</span><span class="sxs-lookup"><span data-stu-id="49410-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="49410-133">È stata così creata la prima regola di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="49410-133">You've now created your first scale rule.</span></span> <span data-ttu-id="49410-134">Si noti che hello UX consiglia di procedure consigliate e indica che ", è consigliabile toohave almeno una scala nella regola."</span><span class="sxs-lookup"><span data-stu-id="49410-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="49410-135">toodo in modo:</span><span class="sxs-lookup"><span data-stu-id="49410-135">toodo so:</span></span>
  
    <span data-ttu-id="49410-136">a.</span><span class="sxs-lookup"><span data-stu-id="49410-136">a.</span></span> <span data-ttu-id="49410-137">Fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="49410-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="49410-138">b.</span><span class="sxs-lookup"><span data-stu-id="49410-138">b.</span></span> <span data-ttu-id="49410-139">Impostare **operatore** troppo**minore**.</span><span class="sxs-lookup"><span data-stu-id="49410-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="49410-140">c.</span><span class="sxs-lookup"><span data-stu-id="49410-140">c.</span></span> <span data-ttu-id="49410-141">Impostare **soglia** troppo**20**.</span><span class="sxs-lookup"><span data-stu-id="49410-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="49410-142">d.</span><span class="sxs-lookup"><span data-stu-id="49410-142">d.</span></span> <span data-ttu-id="49410-143">Impostare **operazione** troppo**ridurre il numero da**.</span><span class="sxs-lookup"><span data-stu-id="49410-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="49410-144">A questo punto si avrà un'impostazione di scalabilità che aumenta/riduce il numero di istanze in base all'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="49410-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="49410-145">![Scalabilità in base alla CPU][8]</span><span class="sxs-lookup"><span data-stu-id="49410-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="49410-146">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="49410-146">Click **Save**.</span></span>

<span data-ttu-id="49410-147">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="49410-147">Congratulations!</span></span> <span data-ttu-id="49410-148">Ora è stato creato correttamente il primo tooautoscale di impostazione di scala app web in base all'utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="49410-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="49410-149">stessi passaggi Hello sono applicabili tooget avviato con una scala di macchina virtuale ruolo del servizio cloud o di set.</span><span class="sxs-lookup"><span data-stu-id="49410-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="49410-150">Altre considerazioni</span><span class="sxs-lookup"><span data-stu-id="49410-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="49410-151">Scalare in base a una pianificazione</span><span class="sxs-lookup"><span data-stu-id="49410-151">Scale based on a schedule</span></span>
<span data-ttu-id="49410-152">Inoltre tooscale basato sulla CPU, è possibile impostare la scala in modo diverso per specifici giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="49410-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="49410-153">Fare clic su **Aggiungi una condizione di scalabilità**.</span><span class="sxs-lookup"><span data-stu-id="49410-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="49410-154">Impostazione delle regole di modalità e hello scala hello è hello stesso come condizione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="49410-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="49410-155">Selezionare **ripetere giorni specifici** per la pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="49410-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="49410-156">Selezionare i giorni hello e l'ora di inizio e fine hello per quando condizione scala hello deve essere applicato.</span><span class="sxs-lookup"><span data-stu-id="49410-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Condizione di scalabilità in base alla pianificazione][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="49410-158">Impostare la scalabilità in modo diverso per date specifiche</span><span class="sxs-lookup"><span data-stu-id="49410-158">Scale differently on specific dates</span></span>
<span data-ttu-id="49410-159">Inoltre tooscale basato sulla CPU, è possibile impostare la scala in modo diverso per date specifiche.</span><span class="sxs-lookup"><span data-stu-id="49410-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="49410-160">Fare clic su **Aggiungi una condizione di scalabilità**.</span><span class="sxs-lookup"><span data-stu-id="49410-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="49410-161">Impostazione delle regole di modalità e hello scala hello è hello stesso come condizione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="49410-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="49410-162">Selezionare **specificare date di inizio e fine** per la pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="49410-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="49410-163">Selezionare le date di inizio e fine hello e l'ora di inizio e fine hello per quando condizione scala hello deve essere applicato.</span><span class="sxs-lookup"><span data-stu-id="49410-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Condizione di scalabilità in base alle date][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="49410-165">Visualizzare la cronologia di scala hello della risorsa</span><span class="sxs-lookup"><span data-stu-id="49410-165">View hello scale history of your resource</span></span>
<span data-ttu-id="49410-166">Ogni volta che la risorsa viene ridimensionata verso l'alto o verso il basso, viene registrato un evento nel registro attività hello.</span><span class="sxs-lookup"><span data-stu-id="49410-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="49410-167">È possibile visualizzare cronologia scala hello della risorsa per hello nelle ultime 24 ore passando toohello **cronologia di esecuzione** scheda.</span><span class="sxs-lookup"><span data-stu-id="49410-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Cronologia di esecuzione][11]

<span data-ttu-id="49410-169">Se si desidera una cronologia completa di scala di hello tooview (per backup too90 giorni), selezionare **fare clic qui toosee ulteriori dettagli**.</span><span class="sxs-lookup"><span data-stu-id="49410-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="49410-170">log attività Hello apre con pre-selezionata per la risorsa e una categoria di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="49410-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="49410-171">Definizione della vista hello scala della risorsa</span><span class="sxs-lookup"><span data-stu-id="49410-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="49410-172">Scalabilità automatica è una risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49410-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="49410-173">È possibile visualizzare definizione scala hello in JSON passando toohello **JSON** scheda.</span><span class="sxs-lookup"><span data-stu-id="49410-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Definizione del piano][12]

<span data-ttu-id="49410-175">È possibile apportare modifiche direttamente in JSON, se necessario.</span><span class="sxs-lookup"><span data-stu-id="49410-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="49410-176">Queste modifiche saranno applicate dopo averle salvate.</span><span class="sxs-lookup"><span data-stu-id="49410-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="49410-177">Disabilitare la scalabilità automatica e ridimensionare le istanze manualmente</span><span class="sxs-lookup"><span data-stu-id="49410-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="49410-178">Potrebbero esserci volte quando si desidera che l'impostazione di scala corrente toodisable e ridimensionare manualmente la risorsa.</span><span class="sxs-lookup"><span data-stu-id="49410-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="49410-179">Fare clic su hello **disabilitare la scalabilità automatica** pulsante nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="49410-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="49410-180">![Disabilita scalabilità automatica][13]</span><span class="sxs-lookup"><span data-stu-id="49410-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="49410-181">Questa opzione disabilita la configurazione.</span><span class="sxs-lookup"><span data-stu-id="49410-181">This option disables your configuration.</span></span> <span data-ttu-id="49410-182">Tuttavia, è possibile tornare tooit dopo aver abilitato la scalabilità automatica nuovamente.</span><span class="sxs-lookup"><span data-stu-id="49410-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="49410-183">È ora possibile impostare il numero di hello di istanze che si desidera tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="49410-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Impostare la scalabilità manuale][14]

<span data-ttu-id="49410-185">È sempre possibile tornare tooAutoscale facendo **abilitare la scalabilità automatica** e quindi **salvare**.</span><span class="sxs-lookup"><span data-stu-id="49410-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49410-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49410-186">Next steps</span></span>
- [<span data-ttu-id="49410-187">Creare un avviso di Log attività toomonitor tutte le operazioni del motore di scalabilità automatica per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="49410-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="49410-188">Creare un avviso di Log attività toomonitor non riuscita. le operazioni di scala/scalabilità di scalabilità automatica per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="49410-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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

