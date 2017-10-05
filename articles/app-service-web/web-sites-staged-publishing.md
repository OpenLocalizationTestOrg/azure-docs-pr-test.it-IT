---
title: Configurare ambienti di staging per le app Web nel Servizio app di Azure | Documentazione Microsoft
description: Informazioni su come utilizzare la pubblicazione per fasi per le app Web in Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="4d6fe-103">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="4d6fe-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="4d6fe-104">Quando si distribuisce l'app Web, il back-end per dispositivi mobili, l'app Web su Linux e l'App per le API al [servizio app](http://go.microsoft.com/fwlink/?LinkId=529714), è possibile eseguire la distribuzione in uno slot di distribuzione distinto, invece che in quello predefinito, se la modalità del piano di servizio app usata è **Standard** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="4d6fe-105">Gli slot di distribuzione sono in realtà app dal vivo con nomi host specifici.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="4d6fe-106">È possibile scambiare il contenuto dell'app e gli elementi delle configurazioni tra i due slot di distribuzione, incluso lo slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="4d6fe-107">La distribuzione dell'applicazione in uno slot di distribuzione presenta i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="4d6fe-108">È possibile convalidare le modifiche alle app in uno slot di distribuzione temporaneo prima di scambiarlo con quello di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="4d6fe-109">La distribuzione preliminare di un'app in uno slot e la successiva implementazione in un ambiente di produzione garantiscono che tutte le istanze dello slot vengano effettivamente eseguite prima di passare alla fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="4d6fe-110">Ciò consente di evitare i tempi di inattività al momento della distribuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="4d6fe-111">Il reindirizzamento del traffico è lineare e nessuna richiesta viene eliminata in seguito alle operazioni di scambio.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="4d6fe-112">L'intero flusso di lavoro può essere automatizzata tramite la configurazione di [scambio automatico](#Auto-Swap) quando non è necessario spazio di pre-swapping convalida.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="4d6fe-113">Dopo uno scambio, lo slot con l'app gestita temporaneamente include l'app di produzione precedente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="4d6fe-114">Se le modifiche applicate nello slot di produzione non risultano corrette, è possibile ripetere immediatamente lo scambio dei due slot per recuperare l'ultimo sito con i dati corretti.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="4d6fe-115">Ciascuna modalità di piano App Service supporta un numero diverso di slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="4d6fe-116">Per conoscere il numero di slot supportati dalla modalità della propria app, vedere [Tariffe del servizio app](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="4d6fe-117">Se l'app dispone di più slot, non è possibile cambiare la modalità.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="4d6fe-118">Gli slot non di produzione non sono scalabili.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="4d6fe-119">La gestione delle risorse collegate non è supportata per gli slot non di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="4d6fe-120">Solo nel [portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715) , è possibile evitare questo impatto potenziale su uno slot di produzione spostando temporaneamente lo slot non di produzione in una modalità di piano servizio app differente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="4d6fe-121">Si noti che lo slot non di produzione deve ancora una volta condividere la stessa modalità dello slot di produzione per potere eseguire lo scambio tra i due slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="4d6fe-122">Aggiungere uno slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-122">Add a deployment slot</span></span>
<span data-ttu-id="4d6fe-123">Per abilitare più slot di distribuzione, l'app deve essere in esecuzione in modalità **Standard** o **Premium**.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="4d6fe-124">Nel [Portale di Azure](https://portal.azure.com/) aprire il pannello della [risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources) dell'app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="4d6fe-125">Scegliere l'opzione **Slot di distribuzione**, quindi fare clic su **Aggiungi slot**.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Aggiungi nuovo slot di distribuzione][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="4d6fe-127">Se l'app non è già in modalità **Standard** o **Premium**, si riceverà un messaggio di errore che indica le modalità supportate per l'abilitazione della pubblicazione per fasi.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="4d6fe-128">A questo punto è possibile selezionare **Aggiorna** e spostarsi alla scheda **Scalabilità** dell'app prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="4d6fe-129">Nel pannello **Aggiungi uno slot** assegnare un nome allo slot e selezionare se clonare la configurazione dell'app da uno slot di distribuzione esistente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="4d6fe-130">Fare clic sul segno di spunta per continuare.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-130">Click the check mark to continue.</span></span>
   
    ![Origine della configurazione][ConfigurationSource1]
   
    <span data-ttu-id="4d6fe-132">La prima volta che si aggiunge uno slot, sono disponibili solo due opzioni: clonare la configurazione dallo slot predefinito in produzione oppure no.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="4d6fe-133">Dopo aver creato vari slot, sarà possibile clonare la configurazione da uno slot diverso da quello in produzione:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Origini della configurazione][MultipleConfigurationSources]
4. <span data-ttu-id="4d6fe-135">Nel pannello delle risorse dell'app fare clic su **Slot di distribuzione**, quindi fare clic su uno slot di distribuzione per aprire il pannello delle risorse dello slot, con un set di metriche e una configurazione come qualsiasi altra app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="4d6fe-136">Il nome dello slot è indicato in alto nel pannello per ricordare all'utente che sta visualizzando lo slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Titolo slot di distribuzione][StagingTitle]
5. <span data-ttu-id="4d6fe-138">Fare clic sull'URL dell'app nel pannello dello slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="4d6fe-139">Tenere presente che lo slot di distribuzione dispone di un nome host specifico ed è inoltre un'app attiva.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="4d6fe-140">Per limitare l'accesso pubblico allo slot di distribuzione, vedere [Blocco dell'accesso Web agli slot di distribuzione non di produzione nell'app Web del servizio app](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="4d6fe-141">Non è presente alcun contenuto dopo la creazione dello slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="4d6fe-142">È possibile distribuire lo slot da un'area diversa dell'archivio o da un altro archivio.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="4d6fe-143">È anche possibile modificare la configurazione dello slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="4d6fe-144">Usare le credenziali del profilo di pubblicazione o di distribuzione associate allo slot di distribuzione per gli aggiornamenti dei contenuti.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="4d6fe-145">È ad esempio possibile [pubblicare in questo slot con git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="4d6fe-146">Configurazione per gli slot di distribuzione ##</span><span class="sxs-lookup"><span data-stu-id="4d6fe-146">Configuration for deployment slots</span></span>
<span data-ttu-id="4d6fe-147">Quando si clona la configurazione da un altro slot di distribuzione, la configurazione clonata è modificabile.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="4d6fe-148">Inoltre, alcuni elementi della configurazione seguiranno il contenuto nello scambio (non specifici dello slot) mentre altri elementi della configurazione resteranno nello stesso slot dopo uno scambio (specifici dello slot).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="4d6fe-149">Negli elenchi seguenti sono riportati gli elementi di configurazione che verranno modificati al momento dello scambio degli slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="4d6fe-150">**Impostazioni che vengono scambiate**:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="4d6fe-151">Impostazioni generali, quali la versione del framework, 32/64 bit, i socket Web</span><span class="sxs-lookup"><span data-stu-id="4d6fe-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="4d6fe-152">Impostazioni app (possono essere configurate per adattarsi a uno slot)</span><span class="sxs-lookup"><span data-stu-id="4d6fe-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="4d6fe-153">Stringhe di connessione (possono essere configurate per adattarsi a uno slot)</span><span class="sxs-lookup"><span data-stu-id="4d6fe-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="4d6fe-154">Mapping dei gestori</span><span class="sxs-lookup"><span data-stu-id="4d6fe-154">Handler mappings</span></span>
* <span data-ttu-id="4d6fe-155">Impostazioni di monitoraggio e diagnostica</span><span class="sxs-lookup"><span data-stu-id="4d6fe-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="4d6fe-156">Contenuto WebJobs</span><span class="sxs-lookup"><span data-stu-id="4d6fe-156">WebJobs content</span></span>

<span data-ttu-id="4d6fe-157">**Impostazioni che non vengono scambiate**:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="4d6fe-158">Endpoint di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-158">Publishing endpoints</span></span>
* <span data-ttu-id="4d6fe-159">Nomi di dominio personalizzati</span><span class="sxs-lookup"><span data-stu-id="4d6fe-159">Custom Domain Names</span></span>
* <span data-ttu-id="4d6fe-160">Certificati e associazioni SSL</span><span class="sxs-lookup"><span data-stu-id="4d6fe-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="4d6fe-161">Impostazioni di scalabilità</span><span class="sxs-lookup"><span data-stu-id="4d6fe-161">Scale settings</span></span>
* <span data-ttu-id="4d6fe-162">Utilità di pianificazione WebJobs</span><span class="sxs-lookup"><span data-stu-id="4d6fe-162">WebJobs schedulers</span></span>

<span data-ttu-id="4d6fe-163">Per configurare un'impostazione app o una stringa di connessione in modo da adattarla a uno (non scambiata), accedere al pannello **Impostazioni applicazione** di uno slot specifico, quindi selezionare la casella **Impostazione slot** per gli elementi di configurazione che devono adattarsi allo slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="4d6fe-164">Si noti che contrassegnando un elemento della configurazione come specifico dello slot, si determina che non può essere scambiato tra tutti gli slot di distribuzione associati all'app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Impostazioni di slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="4d6fe-166">Swap degli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-166">Swap deployment slots</span></span> 
<span data-ttu-id="4d6fe-167">È possibile scambiare gli slot di distribuzione nella visualizzazione **Panoramica** o **Slot di distribuzione** del pannello delle risorse dell'app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6fe-168">Prima di scambiare un'app da uno slot di distribuzione alla produzione, accertarsi che tutte le impostazioni non specifiche dello slot siano configurate esattamente nel modo desiderato nello slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="4d6fe-169">Per scambiare gli slot di distribuzione, fare clic sul pulsante **Scambia** nella barra dei comandi dell'app o di uno slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Pulsante Swap][SwapButtonBar]

2. <span data-ttu-id="4d6fe-171">Assicurarsi che l'origine e la destinazione dello scambio siano impostati correttamente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="4d6fe-172">In genere, la destinazione dello scambio è lo slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="4d6fe-173">Fare clic su **OK** per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="4d6fe-174">Una volta terminata l'operazione, gli slot di distribuzione sono stati scambiati.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Scambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="4d6fe-176">Per il tipo **Scambio con anteprima** vedere [Scambio con anteprima (swap multifase)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="4d6fe-177">Scambio con anteprima (swap multifase)</span><span class="sxs-lookup"><span data-stu-id="4d6fe-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="4d6fe-178">Lo scambio con anteprima o swap multifase semplifica la convalida degli elementi di configurazione di uno slot specifico, ad esempio le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="4d6fe-179">Per i carichi di lavoro mission-critical, è possibile convalidare il comportamento previsto dell'app quando viene applicata la configurazione dello slot di produzione ed è necessario eseguire questa convalida *prima* dello scambio dell'app in produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="4d6fe-180">Lo scambio con anteprima è ciò che serve.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="4d6fe-181">Lo scambio con anteprima non è supportato nelle applicazioni Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="4d6fe-182">Quando si usa l'opzione **Scambio con anteprima** (vedere [Swap degli slot di distribuzione](#Swap)), il servizio app effettua le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="4d6fe-183">Mantiene invariato lo slot di destinazione in modo che non interessi il carico di lavoro esistente in questo slot, ad esempio, la produzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="4d6fe-184">Applica gli elementi di configurazione dello slot di destinazione allo slot di origine, incluse le impostazioni delle app e le stringhe di connessione specifiche dello slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="4d6fe-185">Riavvia i processi di lavoro nello slot di origine usando questi elementi di configurazione menzionati.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="4d6fe-186">Al completamento dello scambio: lo slot di origine pre-riscaldato viene spostato nello slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="4d6fe-187">Lo slot di destinazione viene spostato nello slot di origine come in uno scambio manuale.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="4d6fe-188">In caso di annullamento dello scambio: gli elementi di configurazione dello slot di origine vengono riapplicati allo slot di origine.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="4d6fe-189">È possibile visualizzare in anteprima il funzionamento esatto dell'app con la configurazione dello slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="4d6fe-190">Al termine della convalida, completare lo scambio in un passaggio separato.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="4d6fe-191">Questo passaggio ha anche il vantaggio che lo slot di origine è già riscaldato con la configurazione desiderata e i client non subiranno tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="4d6fe-192">Degli esempi per i cmdlet PowerShell di Azure disponibili per lo swap multifase sono inclusi nei cmdlet PowerShell di Azure per la sezione relativa agli slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="4d6fe-193">Configurare lo scambio automatico</span><span class="sxs-lookup"><span data-stu-id="4d6fe-193">Configure Auto Swap</span></span>
<span data-ttu-id="4d6fe-194">Lo scambio automatico semplifica gli scenari DevOps nei quali si vuole distribuire continuamente l'app senza avvio a freddo e senza tempi di inattività per i clienti finali dell'app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="4d6fe-195">Quando uno slot di distribuzione viene configurato per lo scambio automatico in produzione, ogni volta che si esegue il push dell'aggiornamento del codice in tale slot, il servizio app eseguirà automaticamente lo scambio dell'app in produzione dopo che è stato eseguito il riscaldamento nello slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6fe-196">AZURE.IMPORTANTE Quando si abilita lo scambio automatico per uno slot, assicurarsi che la configurazione dello slot corrisponda esattamente alla configurazione dello slot desiderata per lo slot di destinazione (in genere lo slot di produzione).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="4d6fe-197">Lo scambio automatico non è supportato nelle applicazioni Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="4d6fe-198">La configurazione dello scambio automatico per uno slot è semplice.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="4d6fe-199">Attenersi ai passaggi indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="4d6fe-199">Follow the steps below:</span></span>

1. <span data-ttu-id="4d6fe-200">In **Slot di distribuzione** selezionare uno slot non di produzione e scegliere **Impostazioni applicazione** nel pannello delle risorse di questo slot.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="4d6fe-201">Selezionare **On** per **Scambio automatico**, scegliere lo slot di destinazione desiderato in **Slot scambio automatico**, quindi fare clic su **Salva** nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="4d6fe-202">Assicurarsi che la configurazione dello slot corrisponda esattamente alla configurazione desiderata per lo slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="4d6fe-203">Dopo il completamento dell'operazione, nella scheda **Notifiche** verrà visualizzata la scritta verde lampeggiante **OPERAZIONE RIUSCITA**.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="4d6fe-204">Per verificare lo scambio automatico per l'app, è possibile selezionare prima uno slot di destinazione non di produzione in **Scambia automaticamente slot** per acquisire familiarità con la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="4d6fe-205">Eseguire un push del codice in tale slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="4d6fe-206">Lo scambio automatico verrà eseguito poco dopo e l'aggiornamento verrà riflesso nell'URL dello slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="4d6fe-207">Per eseguire il rollback di un'app di produzione dopo lo scambio</span><span class="sxs-lookup"><span data-stu-id="4d6fe-207">To rollback a production app after swap</span></span>
<span data-ttu-id="4d6fe-208">Se vengono identificati errori nel sito di produzione dopo lo scambio di uno slot, ripristinare i due slot allo stato precedente scambiandoli immediatamente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="4d6fe-209">Riscaldamento personalizzato prima dello scambio</span><span class="sxs-lookup"><span data-stu-id="4d6fe-209">Custom warm-up before swap</span></span>
<span data-ttu-id="4d6fe-210">Alcune app potrebbero richiedere azioni di riscaldamento personalizzate.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="4d6fe-211">L'elemento di configurazione `applicationInitialization` in web.config consente di specificare le azioni di inizializzazione personalizzate da eseguire prima che venga ricevuta una richiesta.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="4d6fe-212">L'operazione di scambio attenderà il completamento del riscaldamento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="4d6fe-213">Di seguito è riportato un frammento web.config di esempio.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="4d6fe-214">Per eliminare uno slot di distribuzione##</span><span class="sxs-lookup"><span data-stu-id="4d6fe-214">To delete a deployment slot</span></span>
<span data-ttu-id="4d6fe-215">Nel pannello di uno slot di distribuzione aprire il pannello dello slot di distribuzione, fare clic su **Panoramica** (la pagina predefinita), quindi fare clic su **Elimina** nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Per eliminare uno slot di distribuzione][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="4d6fe-217">Cmdlet Azure PowerShell per gli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="4d6fe-218">Azure PowerShell è un modulo che fornisce i cmdlet per gestire Azure tramite Windows PowerShell, tra cui il supporto per la gestione degli slot di distribuzione in Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="4d6fe-219">Per informazioni sull'installazione e la configurazione di Azure PowerShell e sull'autenticazione di Azure PowerShell con l'abbonamento di Microsoft Azure, vedere l'argomento relativo alla [procedura di installazione e configurazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="4d6fe-220">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="4d6fe-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="4d6fe-221">Creare uno slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="4d6fe-222">Avviare uno scambio con anteprima (swap multifase) e applicare la configurazione dello slot di destinazione allo slot di origine</span><span class="sxs-lookup"><span data-stu-id="4d6fe-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="4d6fe-223">Annullare uno scambio (scambio con anteprima) in sospeso e ripristinare la configurazione dello slot di origine</span><span class="sxs-lookup"><span data-stu-id="4d6fe-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="4d6fe-224">Swap degli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="4d6fe-225">Eliminare slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="4d6fe-226">Comandi dell'interfaccia della riga di comando di Azure per gli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4d6fe-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="4d6fe-227">L'interfaccia della riga di comando di Azure fornisce comandi multipiattaforma che è possibile usare con Azure, incluso il supporto per la gestione degli slot di distribuzione del servizio app.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="4d6fe-228">Per istruzioni sull'installazione e la configurazione dell'interfaccia della riga di comando di Azure, incluse le informazioni su come collegarla alla sottoscrizione di Azure, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="4d6fe-229">Per l'elenco dei comandi disponibili per il servizio app di Azure, chiamare `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="4d6fe-230">Per i comandi dell'[interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) relativi agli slot di distribuzione, vedere [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="4d6fe-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="4d6fe-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="4d6fe-231">azure site list</span></span>
<span data-ttu-id="4d6fe-232">Per informazioni sulle app nell'attuale sottoscrizione, chiamare **azure site list**, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="4d6fe-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="4d6fe-233">azure site create</span></span>
<span data-ttu-id="4d6fe-234">Per creare uno slot di distribuzione, chiamare **azure site create** e specificare il nome di un'app esistente e il nome dello slot da creare, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="4d6fe-235">Per abilitare il controllo del codice sorgente per il nuovo slot, utilizzare l'opzione **- git** , come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="4d6fe-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="4d6fe-236">azure site swap</span></span>
<span data-ttu-id="4d6fe-237">Per applicare lo slot di distribuzione aggiornato al sito di produzione, utilizzare il comando **azure site swap** per eseguire un'operazione di scambio, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="4d6fe-238">L'app di produzione non sarà caratterizzata da tempi di inattività, né subirà un avvio a freddo.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="4d6fe-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="4d6fe-239">azure site delete</span></span>
<span data-ttu-id="4d6fe-240">Per eliminare uno slot di distribuzione non più necessario, usare il comando **azure site delete** , come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="4d6fe-241">Verificare il funzionamento di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-241">See a web app in action.</span></span> <span data-ttu-id="4d6fe-242">[provare il servizio app](https://azure.microsoft.com/try/app-service/) immediatamente e creare un'app iniziale temporanea, senza necessità di fornire una carta di credito e senza impegni.</span><span class="sxs-lookup"><span data-stu-id="4d6fe-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4d6fe-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d6fe-243">Next Steps</span></span>
<span data-ttu-id="4d6fe-244">[Blocco dell'accesso Web agli slot di distribuzione non di produzione nell'app Web del servizio app di Azure](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduzione al servizio app in Linux](./app-service-linux-intro.md)
[Versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="4d6fe-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

