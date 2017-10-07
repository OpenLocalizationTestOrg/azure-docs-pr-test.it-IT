---
title: aaaSet di gestione temporanea di ambienti per le app web in Azure App Service | Documenti Microsoft
description: Informazioni su come toouse staging pubblicazione per le app web in Azure App Service.
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
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="07ae2-103">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="07ae2-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="07ae2-104">Quando si distribuisce l'app web, l'app web su Linux, back-end per dispositivi mobili e app per le API troppo[servizio App](http://go.microsoft.com/fwlink/?LinkId=529714), è possibile distribuire uno slot di distribuzione separata tooa anziché slot di produzione predefinito hello durante l'esecuzione in hello **Standard**o **Premium** modalità del piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="07ae2-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="07ae2-105">Gli slot di distribuzione sono in realtà app dal vivo con nomi host specifici.</span><span class="sxs-lookup"><span data-stu-id="07ae2-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="07ae2-106">Gli elementi di contenuto e le configurazioni di App possono essere scambiati tra i due slot di distribuzione, compreso hello slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="07ae2-107">Distribuzione di slot di distribuzione di applicazione tooa ha hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="07ae2-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="07ae2-108">È possibile convalidare modifiche all'applicazione in uno slot di distribuzione di gestione temporanea prima di scambiarlo con lo slot di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="07ae2-109">Distribuzione di uno slot tooa app prima che lo scambio alla produzione assicura che tutte le istanze di slot hello sono riscaldate prima viene scambiato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="07ae2-110">Ciò consente di evitare i tempi di inattività al momento della distribuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="07ae2-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="07ae2-111">Hello reindirizzamento del traffico è seamless e nessuna richiesta viene eliminata in seguito a operazioni di scambio.</span><span class="sxs-lookup"><span data-stu-id="07ae2-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="07ae2-112">L'intero flusso di lavoro può essere automatizzata tramite la configurazione di [scambio automatico](#Auto-Swap) quando non è necessario spazio di pre-swapping convalida.</span><span class="sxs-lookup"><span data-stu-id="07ae2-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="07ae2-113">Dopo uno scambio, slot hello con app con installazione di appoggio in precedenza può hello precedente dell'applicazione di produzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="07ae2-114">Se le modifiche di hello scambiate nello slot di produzione hello non corrisponda a quello desiderato, è possibile eseguire hello che stesso scambio immediatamente il backup tooget "ultimo noto buona sito".</span><span class="sxs-lookup"><span data-stu-id="07ae2-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="07ae2-115">Ciascuna modalità di piano App Service supporta un numero diverso di slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="07ae2-116">supporta la modalità dell'app toofind numero hello di slot, vedere [prezzi del servizio App](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="07ae2-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="07ae2-117">Quando l'applicazione ha più slot, è possibile modificare la modalità hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="07ae2-118">Gli slot non di produzione non sono scalabili.</span><span class="sxs-lookup"><span data-stu-id="07ae2-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="07ae2-119">La gestione delle risorse collegate non è supportata per gli slot non di produzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="07ae2-120">In hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715) solo, è possibile evitare il potenziale impatto su uno slot di produzione spostando temporaneamente hello slot non di produzione tooa servizio App piano modalità diversa.</span><span class="sxs-lookup"><span data-stu-id="07ae2-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="07ae2-121">Si noti che lo slot non di produzione hello deve condividere nuovamente hello stessa modalità con lo slot di produzione hello prima che è possibile scambiare gli slot di due hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="07ae2-122">Aggiungere uno slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-122">Add a deployment slot</span></span>
<span data-ttu-id="07ae2-123">app Hello deve essere eseguita in hello **Standard** o **Premium** modalità in ordine per si tooenable più slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="07ae2-124">In hello [portale Azure](https://portal.azure.com/), Apri l'app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="07ae2-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="07ae2-125">Scegliere hello **gli slot di distribuzione** opzione, quindi fare clic su **Aggiungi Slot**.</span><span class="sxs-lookup"><span data-stu-id="07ae2-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Aggiungi nuovo slot di distribuzione][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="07ae2-127">Se l'applicazione hello non sia già in hello **Standard** o **Premium** modalità, si riceverà un messaggio che indica la modalità di hello è supportato per l'abilitazione della pubblicazione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="07ae2-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="07ae2-128">A questo punto, si dispone di hello opzione tooselect **aggiornamento** e passare toohello **scala** scheda dell'app prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="07ae2-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="07ae2-129">In hello **aggiungere uno slot** pannello, assegnare un nome di uno slot hello e selezionare se tooclone configurazione delle app da un altro slot di distribuzione esistente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="07ae2-130">Fare clic su hello toocontinue di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="07ae2-130">Click hello check mark toocontinue.</span></span>
   
    ![Origine della configurazione][ConfigurationSource1]
   
    <span data-ttu-id="07ae2-132">Hello prima volta che si aggiunge uno slot, si avrà solo due opzioni: configurazione clone dallo slot di hello predefinito nell'ambiente di produzione o non è affatto.</span><span class="sxs-lookup"><span data-stu-id="07ae2-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="07ae2-133">Dopo aver creato gli slot diverse, sarà in grado di tooclone configurazione da uno slot diverso da hello nell'ambiente di produzione:</span><span class="sxs-lookup"><span data-stu-id="07ae2-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Origini della configurazione][MultipleConfigurationSources]
4. <span data-ttu-id="07ae2-135">Nel pannello della risorsa dell'applicazione, fare clic su **gli slot di distribuzione**, quindi fare clic su un tooopen slot di distribuzione pannello della risorsa che dello slot, con un set di configurazione come qualsiasi altra app e sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="07ae2-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="07ae2-136">Hello nome dello slot hello viene visualizzato nella parte superiore di hello di hello pannello tooremind che si sta visualizzando hello slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Titolo slot di distribuzione][StagingTitle]
5. <span data-ttu-id="07ae2-138">Fare clic su URL app hello nel pannello hello dello slot.</span><span class="sxs-lookup"><span data-stu-id="07ae2-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="07ae2-139">Si noti lo slot di distribuzione hello ha il proprio nome host ed è anche un'applicazione in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="07ae2-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="07ae2-140">lo slot di distribuzione toohello accesso pubblico toolimit, vedere [App del servizio Web App: slot di distribuzione di produzione toonon accesso web blocco](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="07ae2-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="07ae2-141">Non è presente alcun contenuto dopo la creazione dello slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="07ae2-142">È possibile distribuire slot toohello da un repository di completamente diverso, o un ramo del repository diversi.</span><span class="sxs-lookup"><span data-stu-id="07ae2-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="07ae2-143">È inoltre possibile modificare hello configurazione dello slot.</span><span class="sxs-lookup"><span data-stu-id="07ae2-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="07ae2-144">Hello utilizzare pubblicazione le credenziali di distribuzione o del profilo associate hello slot di distribuzione per gli aggiornamenti del contenuto.</span><span class="sxs-lookup"><span data-stu-id="07ae2-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="07ae2-145">Ad esempio, è possibile [pubblicare toothis slot con git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="07ae2-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="07ae2-146">Configurazione per gli slot di distribuzione ##</span><span class="sxs-lookup"><span data-stu-id="07ae2-146">Configuration for deployment slots</span></span>
<span data-ttu-id="07ae2-147">Quando si clona una configurazione da un altro slot di distribuzione, configurazione clonato hello è modificabile.</span><span class="sxs-lookup"><span data-stu-id="07ae2-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="07ae2-148">Inoltre, alcuni elementi di configurazione seguirà contenuto hello in uno scambio (non slot specifico) mentre altri elementi di configurazione verranno mantenuta nel hello stesso slot dopo uno scambio (slot specifico).</span><span class="sxs-lookup"><span data-stu-id="07ae2-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="07ae2-149">Hello elenchi seguenti vengono illustrati configurazione hello che verrà modificata durante lo scambio di slot.</span><span class="sxs-lookup"><span data-stu-id="07ae2-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="07ae2-150">**Impostazioni che vengono scambiate**:</span><span class="sxs-lookup"><span data-stu-id="07ae2-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="07ae2-151">Impostazioni generali, quali la versione del framework, 32/64 bit, i socket Web</span><span class="sxs-lookup"><span data-stu-id="07ae2-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="07ae2-152">Impostazioni dell'App (può essere configurato toostick tooa slot)</span><span class="sxs-lookup"><span data-stu-id="07ae2-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="07ae2-153">Stringhe di connessione (può essere configurato toostick tooa slot)</span><span class="sxs-lookup"><span data-stu-id="07ae2-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="07ae2-154">Mapping dei gestori</span><span class="sxs-lookup"><span data-stu-id="07ae2-154">Handler mappings</span></span>
* <span data-ttu-id="07ae2-155">Impostazioni di monitoraggio e diagnostica</span><span class="sxs-lookup"><span data-stu-id="07ae2-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="07ae2-156">Contenuto WebJobs</span><span class="sxs-lookup"><span data-stu-id="07ae2-156">WebJobs content</span></span>

<span data-ttu-id="07ae2-157">**Impostazioni che non vengono scambiate**:</span><span class="sxs-lookup"><span data-stu-id="07ae2-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="07ae2-158">Endpoint di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="07ae2-158">Publishing endpoints</span></span>
* <span data-ttu-id="07ae2-159">Nomi di dominio personalizzati</span><span class="sxs-lookup"><span data-stu-id="07ae2-159">Custom Domain Names</span></span>
* <span data-ttu-id="07ae2-160">Certificati e associazioni SSL</span><span class="sxs-lookup"><span data-stu-id="07ae2-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="07ae2-161">Impostazioni di scalabilità</span><span class="sxs-lookup"><span data-stu-id="07ae2-161">Scale settings</span></span>
* <span data-ttu-id="07ae2-162">Utilità di pianificazione WebJobs</span><span class="sxs-lookup"><span data-stu-id="07ae2-162">WebJobs schedulers</span></span>

<span data-ttu-id="07ae2-163">app impostazione o connessione stringa toostick tooa slot (non invertito), hello accesso tooconfigure **le impostazioni dell'applicazione** pannello per una specificato slot, quindi seleziona hello **impostazione Slot** casella per hello elementi di configurazione che è necessario utilizzare slot hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="07ae2-164">Si noti che il contrassegno di un elemento di configurazione come slot specifico ha l'effetto di hello definizione di tale elemento come non sostituibili tra tutti gli slot di distribuzione hello associati hello app.</span><span class="sxs-lookup"><span data-stu-id="07ae2-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Impostazioni di slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="07ae2-166">Swap degli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-166">Swap deployment slots</span></span> 
<span data-ttu-id="07ae2-167">È possibile scambiare gli slot di distribuzione di hello **Panoramica** o **gli slot di distribuzione** visualizzazione del pannello della risorsa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07ae2-168">Prima che lo scambio di un'app da uno slot di distribuzione nell'ambiente di produzione, assicurarsi che tutte le impostazioni specifiche di slot non sono configurate esattamente come si desidera toohave nella destinazione dello scambio hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="07ae2-169">tooswap gli slot di distribuzione, fare clic su hello **scambiare** pulsante nella barra dei comandi di hello dell'applicazione hello o nella barra dei comandi hello di uno slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Pulsante Swap][SwapButtonBar]

2. <span data-ttu-id="07ae2-171">Verificare che tale destinazione hello scambio origine e lo scambio siano impostate correttamente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="07ae2-172">In genere, destinazione dello scambio hello è slot di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="07ae2-173">Fare clic su **OK** operazione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="07ae2-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="07ae2-174">Al termine dell'operazione di hello, gli slot di distribuzione hello sono stati invertiti.</span><span class="sxs-lookup"><span data-stu-id="07ae2-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Scambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="07ae2-176">Per hello **scambio con anteprima** Scambia tipo, vedere [scambio con anteprima (scambio multifase)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="07ae2-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="07ae2-177">Scambio con anteprima (swap multifase)</span><span class="sxs-lookup"><span data-stu-id="07ae2-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="07ae2-178">Lo scambio con anteprima o swap multifase semplifica la convalida degli elementi di configurazione di uno slot specifico, ad esempio le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="07ae2-179">Per i carichi di lavoro mission-critical, si desidera toovalidate che hello app si comporta come previsto quando viene applicata la configurazione dello slot di produzione hello, ed è necessario eseguire tale convalida *prima* app hello viene scambiato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="07ae2-180">Lo scambio con anteprima è ciò che serve.</span><span class="sxs-lookup"><span data-stu-id="07ae2-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="07ae2-181">Lo scambio con anteprima non è supportato nelle applicazioni Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="07ae2-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="07ae2-182">Quando si utilizza hello **scambio con anteprima** opzione (vedere [scambiare gli slot di distribuzione](#Swap)), servizio App hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="07ae2-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="07ae2-183">Non è compromessa mantiene hello destinazione slot invariato così carico di lavoro esistente in tale slot (ad esempio produzione).</span><span class="sxs-lookup"><span data-stu-id="07ae2-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="07ae2-184">Si applica agli elementi di configurazione di hello di hello slot toohello origine slot di destinazione, incluse le stringhe di connessione specifica slot hello e le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="07ae2-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="07ae2-185">Riavvia i processi di lavoro hello nello slot di origine hello utilizzando tali elementi di configurazione menzionati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07ae2-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="07ae2-186">Quando si completa scambio hello: slot di origine remota warmed hello passa in uno slot di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="07ae2-187">slot di destinazione Hello viene spostato in uno slot di origine hello come uno scambio manuale.</span><span class="sxs-lookup"><span data-stu-id="07ae2-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="07ae2-188">Quando si annulla swap hello: consente di riapplicare gli elementi di configurazione hello dello slot di origine di hello origine slot toohello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="07ae2-189">È possibile visualizzare l'anteprima esattamente come applicazione hello comporterà con la configurazione dello slot di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="07ae2-190">Dopo aver completato la convalida, è completare lo scambio di hello in un passaggio separato.</span><span class="sxs-lookup"><span data-stu-id="07ae2-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="07ae2-191">Questo passaggio è hello vantaggio che lo slot di origine hello già riscaldato con la configurazione desiderata hello e i client non subiscono alcun tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="07ae2-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="07ae2-192">Esempi per cmdlet di Azure PowerShell disponibili per lo scambio multifase hello sono inclusi in hello cmdlet PowerShell di Azure per sezione slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="07ae2-193">Configurare lo scambio automatico</span><span class="sxs-lookup"><span data-stu-id="07ae2-193">Configure Auto Swap</span></span>
<span data-ttu-id="07ae2-194">Semplifica lo scambio automatico DevOps scenari in cui si desidera toocontinuously distribuisce l'app con zero a freddo e tempi di inattività per i clienti finali dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="07ae2-195">Quando uno slot di distribuzione è configurato per lo scambio automatico nell'ambiente di produzione, ogni volta che si esegue il push slot toothat di aggiornamento di codice, il servizio App automaticamente scambiare app hello nell'ambiente di produzione dopo che è già stato riscaldato nello slot di hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07ae2-196">Quando si abilita scambio automatico per uno slot, verificare che la configurazione dello slot di hello è esattamente configurazione hello per lo slot di destinazione di hello (in genere slot di produzione di hello).</span><span class="sxs-lookup"><span data-stu-id="07ae2-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="07ae2-197">Lo scambio automatico non è supportato nelle applicazioni Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="07ae2-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="07ae2-198">La configurazione dello scambio automatico per uno slot è semplice.</span><span class="sxs-lookup"><span data-stu-id="07ae2-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="07ae2-199">Attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="07ae2-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="07ae2-200">In **Slot di distribuzione** selezionare uno slot non di produzione e scegliere **Impostazioni applicazione** nel pannello delle risorse di questo slot.</span><span class="sxs-lookup"><span data-stu-id="07ae2-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="07ae2-201">Selezionare **su** per **scambio automatico**, selezionare uno slot di destinazione desiderato hello **Slot di scambio automatico**, fare clic su **salvare** nella barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="07ae2-202">Assicurarsi di configurazione per lo slot di hello è esattamente hello destinata agli slot di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="07ae2-203">Hello **notifiche** scheda lampeggia una verde **successo** al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="07ae2-204">tootest scambio automatico per l'app, è possibile selezionare prima uno slot di destinazione non di produzione in **Slot di scambio automatico** toobecome familiarità con la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="07ae2-205">Eseguire uno slot di distribuzione toothat push di codice.</span><span class="sxs-lookup"><span data-stu-id="07ae2-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="07ae2-206">Verrà eseguito lo scambio automatico dopo un breve periodo di tempo e aggiornamento hello verrà riflesse nell'URL di slot di destinazione.</span><span class="sxs-lookup"><span data-stu-id="07ae2-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="07ae2-207">toorollback un'app di produzione dopo lo scambio</span><span class="sxs-lookup"><span data-stu-id="07ae2-207">toorollback a production app after swap</span></span>
<span data-ttu-id="07ae2-208">Se vengono rilevati errori nell'ambiente di produzione dopo uno scambio di slot, il rollup slot hello tootheir indietro pre-swap stati per lo scambio di slot hello due stesso immediatamente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="07ae2-209">Riscaldamento personalizzato prima dello scambio</span><span class="sxs-lookup"><span data-stu-id="07ae2-209">Custom warm-up before swap</span></span>
<span data-ttu-id="07ae2-210">Alcune app potrebbero richiedere azioni di riscaldamento personalizzate.</span><span class="sxs-lookup"><span data-stu-id="07ae2-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="07ae2-211">Hello `applicationInitialization` consente di elemento di configurazione in Web. config è toospecify l'inizializzazione personalizzata azioni toobe eseguita prima che venga ricevuta una richiesta.</span><span class="sxs-lookup"><span data-stu-id="07ae2-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="07ae2-212">operazione di scambio Hello attenderà questo toocomplete riscaldamento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="07ae2-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="07ae2-213">Di seguito è riportato un frammento web.config di esempio.</span><span class="sxs-lookup"><span data-stu-id="07ae2-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="07ae2-214">toodelete uno slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-214">toodelete a deployment slot</span></span>
<span data-ttu-id="07ae2-215">Nel Pannello di hello per uno slot di distribuzione, pannello dello slot di distribuzione hello aperto, fare clic su **Panoramica** (pagina predefinita di hello), fare clic su **eliminare** nella barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Per eliminare uno slot di distribuzione][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="07ae2-217">Cmdlet Azure PowerShell per gli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="07ae2-218">Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell, incluso il supporto per la gestione di slot di distribuzione in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="07ae2-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="07ae2-219">Per informazioni sull'installazione e configurazione di Azure PowerShell e sull'autenticazione di Azure PowerShell con la sottoscrizione di Azure, vedere [come tooinstall e configurare Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07ae2-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="07ae2-220">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="07ae2-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="07ae2-221">Creare uno slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="07ae2-222">Avviare uno scambio con revisione (scambio multifase) e applicare slot toosource configurazione dello slot di destinazione</span><span class="sxs-lookup"><span data-stu-id="07ae2-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="07ae2-223">Annullare uno scambio (scambio con anteprima) in sospeso e ripristinare la configurazione dello slot di origine</span><span class="sxs-lookup"><span data-stu-id="07ae2-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="07ae2-224">Swap degli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="07ae2-225">Eliminare slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="07ae2-226">Comandi dell'interfaccia della riga di comando di Azure per gli slot di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07ae2-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="07ae2-227">Hello CLI di Azure fornisce comandi multipiattaforma per l'utilizzo di Azure, incluso il supporto per la gestione di slot di distribuzione di servizio App.</span><span class="sxs-lookup"><span data-stu-id="07ae2-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="07ae2-228">Per istruzioni sull'installazione e configurazione hello CLI di Azure, incluse le informazioni su come tooconnect CLI di Azure tooyour sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07ae2-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="07ae2-229">comandi di hello toolist disponibili per il servizio App di Azure in hello CLI di Azure, chiamare `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="07ae2-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="07ae2-230">Per i comandi dell'[interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) relativi agli slot di distribuzione, vedere [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="07ae2-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="07ae2-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="07ae2-231">azure site list</span></span>
<span data-ttu-id="07ae2-232">Per informazioni sulle App hello nella sottoscrizione corrente hello, chiamare **elenco del sito azure**, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="07ae2-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="07ae2-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="07ae2-233">azure site create</span></span>
<span data-ttu-id="07ae2-234">toocreate uno slot di distribuzione, chiamare **sito azure creare** e specificare il nome di hello di un'app esistente e il nome di hello di hello slot toocreate, come in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="07ae2-235">controllo del codice sorgente per hello nuovo slot di, utilizzare hello tooenable **- git** opzione, come in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="07ae2-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="07ae2-236">azure site swap</span></span>
<span data-ttu-id="07ae2-237">toomake hello dell'applicazione di produzione hello slot di distribuzione aggiornato, utilizzare hello **scambio sito azure** comando tooperform un'operazione di scambio, come in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="07ae2-238">applicazione di produzione Hello non verifichino tempi di inattività, né verrà sottoposta ad a un avvio a freddo.</span><span class="sxs-lookup"><span data-stu-id="07ae2-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="07ae2-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="07ae2-239">azure site delete</span></span>
<span data-ttu-id="07ae2-240">toodelete uno slot di distribuzione che non è più necessario, utilizzare hello **eliminazione sito azure** comando, come in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="07ae2-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="07ae2-241">Verificare il funzionamento di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="07ae2-241">See a web app in action.</span></span> <span data-ttu-id="07ae2-242">[provare il servizio app](https://azure.microsoft.com/try/app-service/) immediatamente e creare un'app iniziale temporanea, senza necessità di fornire una carta di credito e senza impegni.</span><span class="sxs-lookup"><span data-stu-id="07ae2-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="07ae2-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07ae2-243">Next Steps</span></span>
<span data-ttu-id="07ae2-244">[Azure App Service Web App: consente di bloccare gli slot di distribuzione di produzione toonon di accesso web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp introduzione del servizio in Linux](./app-service-linux-intro.md)
[versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="07ae2-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
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

