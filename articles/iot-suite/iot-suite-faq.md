---
title: domande frequenti di IoT Suite aaaAzure | Documenti Microsoft
description: Domande frequenti su IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="431b4-103">Domande frequenti su IoT Suite</span><span class="sxs-lookup"><span data-stu-id="431b4-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="431b4-104">Vedere anche, specifici di factory connesso hello [domande frequenti su](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="431b4-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="431b4-105">Dove trovare il codice sorgente hello per le soluzioni hello preconfigurato</span><span class="sxs-lookup"><span data-stu-id="431b4-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="431b4-106">codice di origine Hello è archiviato in hello repository GitHub seguente:</span><span class="sxs-lookup"><span data-stu-id="431b4-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="431b4-107">[Soluzione preconfigurata per il monitoraggio remoto][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="431b4-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="431b4-108">[Soluzione preconfigurata di manutenzione predittiva][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="431b4-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* <span data-ttu-id="431b4-109">[Connected factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) (Soluzione preconfigurata di connected factory)</span><span class="sxs-lookup"><span data-stu-id="431b4-109">[Connected factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory)</span></span>

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="431b4-110">Come posso aggiornare toohello ultima versione di hello remoto monitoraggio preconfigurato soluzione che utilizza hello funzionalità di gestione dei dispositivi IoT Hub?</span><span class="sxs-lookup"><span data-stu-id="431b4-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="431b4-111">Se si distribuisce una soluzione preconfigurata dal sito https://www.azureiotsuite.com/ hello, distribuisce sempre una nuova istanza della versione più recente di hello della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="431b4-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="431b4-112">Se si distribuisce una soluzione preconfigurata tramite la riga di comando hello, è possibile aggiornare una distribuzione esistente con il nuovo codice.</span><span class="sxs-lookup"><span data-stu-id="431b4-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="431b4-113">Vedere [distribuzione Cloud] [ lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="431b4-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="431b4-114">Come è possibile aggiungere il supporto per un nuovo dispositivo metodo toohello soluzione preconfigurata di monitoraggio remoto?</span><span class="sxs-lookup"><span data-stu-id="431b4-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="431b4-115">Vedere la sezione hello [aggiungere il supporto per un nuovo simulatore toohello metodo] [ lnk-add-method] in hello [personalizzare una soluzione preconfigurata] [ lnk-customize] articolo.</span><span class="sxs-lookup"><span data-stu-id="431b4-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="431b4-116">Ignora le modifiche di proprietà desiderato, il dispositivo simulato Hello perché?</span><span class="sxs-lookup"><span data-stu-id="431b4-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="431b4-117">In hello monitoraggio remoto preconfigurato soluzione, il codice di dispositivo simulato hello utilizza solo hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** le proprietà desiderate hello tooupdate segnalato proprietà.</span><span class="sxs-lookup"><span data-stu-id="431b4-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="431b4-118">Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="431b4-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="431b4-119">Il dispositivo non viene visualizzato nell'elenco di hello dei dispositivi nel dashboard di soluzione hello, perché?</span><span class="sxs-lookup"><span data-stu-id="431b4-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="431b4-120">elenco Hello dei dispositivi nel dashboard di soluzione hello utilizza un elenco di hello tooreturn query di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="431b4-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="431b4-121">Attualmente, una query non può restituire più di 10.000 dispositivi.</span><span class="sxs-lookup"><span data-stu-id="431b4-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="431b4-122">Provare a eseguire i criteri di ricerca hello per le query più restrittiva.</span><span class="sxs-lookup"><span data-stu-id="431b4-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="431b4-123">Qual è la differenza hello tra l'eliminazione di un gruppo di risorse in Azure nel portale e facendo clic su delete su una soluzione preconfigurata in azureiotsuite.com hello?</span><span class="sxs-lookup"><span data-stu-id="431b4-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="431b4-124">Se si elimina una soluzione di hello preconfigurato in [azureiotsuite.com][lnk-azureiotsuite], si eliminano tutte le risorse di hello che ha effettuato il provisioning durante la creazione di soluzioni hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="431b4-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="431b4-125">Se è stato aggiunto gruppo di risorse toohello risorse aggiuntive, vengono eliminate anche tali risorse.</span><span class="sxs-lookup"><span data-stu-id="431b4-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="431b4-126">Se si elimina il gruppo di risorse hello in hello [portale di Azure][lnk-azure-portal], si eliminano solo risorse di hello in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="431b4-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="431b4-127">È inoltre necessario associata alla soluzione hello preconfigurato in hello un'applicazione Azure Active Directory hello toodelete [portale di Azure classico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="431b4-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="431b4-128">Di quante istanze dell'hub IoT è possibile eseguire il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="431b4-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="431b4-129">Per impostazione predefinita, è possibile eseguire il provisioning di [10 hub IoT per ogni sottoscrizione][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="431b4-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="431b4-130">È possibile creare un [ticket di supporto tecnico di Azure] [ link-azuresupportticket] tooraise questo limite.</span><span class="sxs-lookup"><span data-stu-id="431b4-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="431b4-131">Di conseguenza, poiché ogni disposizioni soluzione preconfigurata un nuovo IoT Hub, è possibile solo effettuare il provisioning di too10 preconfigurato soluzioni in una specifica sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="431b4-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="431b4-132">Di quante istanze di Azure Cosmos DB è possibile effettuare il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="431b4-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="431b4-133">Cinquanta.</span><span class="sxs-lookup"><span data-stu-id="431b4-133">Fifty.</span></span> <span data-ttu-id="431b4-134">È possibile creare un [ticket di supporto tecnico di Azure] [ link-azuresupportticket] tooraise questo limite, ma per impostazione predefinita, è possibile fornire solo 50 istanze DB Cosmos per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="431b4-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="431b4-135">Di quante API di Bing Maps gratuite è possibile eseguire il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="431b4-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="431b4-136">Due.</span><span class="sxs-lookup"><span data-stu-id="431b4-136">Two.</span></span> <span data-ttu-id="431b4-137">È possibile creare solo due Transazioni sito Web interno - Livello 1 per Bing Maps per i piani aziendali in una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="431b4-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="431b4-138">soluzione di monitoraggio remoto Hello viene eseguito il provisioning per impostazione predefinita con piano hello interna 1 livello di transazioni.</span><span class="sxs-lookup"><span data-stu-id="431b4-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="431b4-139">Di conseguenza, è possibile fornire solo backup tootwo soluzioni in una sottoscrizione senza modifiche di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="431b4-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="431b4-140">Se si usa la distribuzione di soluzioni di monitoraggio remoto con una mappa statica, come si aggiunge una mappa di Bing interattiva?</span><span class="sxs-lookup"><span data-stu-id="431b4-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="431b4-141">È possibile ottenere la chiave QueryKey di Bing Maps API for Enterprise dal [portale di Azure][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="431b4-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="431b4-142">Passare il gruppo di risorse in cui l'API di Bing Maps per Enterprise è in hello toohello [portale di Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="431b4-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="431b4-143">Fare clic su **All Settings** (Tutte le impostazioni) e quindi su **Key Management** (Gestione chiavi).</span><span class="sxs-lookup"><span data-stu-id="431b4-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="431b4-144">Vengono visualizzate le due chiavi **MasterKey** e **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="431b4-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="431b4-145">Copiare il valore di hello per **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="431b4-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="431b4-146">Se non si ha un account Bing Maps API for Enterprise,</span><span class="sxs-lookup"><span data-stu-id="431b4-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="431b4-147">Crearne una nel hello [portale di Azure] [ lnk-azure-portal] facendo clic su + nuova, la ricerca di API di Bing Maps per l'organizzazione e seguire richiede toocreate.</span><span class="sxs-lookup"><span data-stu-id="431b4-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="431b4-148">Verso il basso il codice più recente di hello da hello [Azure IoT-remoto Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="431b4-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="431b4-149">Esecuzione locale o nel cloud di distribuzione seguente Guida alla distribuzione della riga di comando hello nella cartella /docs/ hello nel repository di hello.</span><span class="sxs-lookup"><span data-stu-id="431b4-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="431b4-150">Dopo aver eseguito una variabile locale o cloud di distribuzione, cercare nella cartella radice per hello *. file User. config creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="431b4-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="431b4-151">Aprire il file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="431b4-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="431b4-152">Il valore di hello tooinclude copiato nelle righe seguenti hello di modifica del **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="431b4-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="431b4-153">È possibile creare una soluzione preconfigurata se è disponibile Microsoft Azure per DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="431b4-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="431b4-154">Al momento non è possibile creare una soluzione preconfigurata con un account [Microsoft Azure for DreamSpark][lnk-dreamspark],</span><span class="sxs-lookup"><span data-stu-id="431b4-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="431b4-155">ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="431b4-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="431b4-156">È possibile creare una soluzione preconfigurata se si dispone di una sottoscrizione di Cloud Solution Provider?</span><span class="sxs-lookup"><span data-stu-id="431b4-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="431b4-157">È possibile attualmente creare una soluzione preconfigurata con una sottoscrizione di Cloud Solution Provider,</span><span class="sxs-lookup"><span data-stu-id="431b4-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="431b4-158">ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="431b4-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="431b4-159">Come si elimina un tenant AAD?</span><span class="sxs-lookup"><span data-stu-id="431b4-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="431b4-160">Vedere il post del blog di Eric Golpe relativo alla [procedura dettagliata di eliminazione di un tenant di Azure AD][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="431b4-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="431b4-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="431b4-161">Next steps</span></span>

<span data-ttu-id="431b4-162">È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:</span><span class="sxs-lookup"><span data-stu-id="431b4-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="431b4-163">[Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="431b4-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="431b4-164">Panoramica della soluzione preconfigurata di connected factory</span><span class="sxs-lookup"><span data-stu-id="431b4-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="431b4-165">[Sicurezza di IoT da hello messa a terra][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="431b4-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
