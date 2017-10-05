---
title: Domande frequenti su Azure IoT Suite | Microsoft Docs
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="c3610-103">Domande frequenti su IoT Suite</span><span class="sxs-lookup"><span data-stu-id="c3610-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="c3610-104">Vedere anche le [domande frequenti](iot-suite-faq-cf.md) specifiche della factory connessa.</span><span class="sxs-lookup"><span data-stu-id="c3610-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="c3610-105">Dove è possibile visualizzare il codice sorgente per la soluzione preconfigurata?</span><span class="sxs-lookup"><span data-stu-id="c3610-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="c3610-106">Il codice sorgente è memorizzato nei repository di GitHub seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3610-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="c3610-107">[Soluzione preconfigurata per il monitoraggio remoto][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="c3610-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="c3610-108">[Soluzione preconfigurata di manutenzione predittiva][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="c3610-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="c3610-109">Soluzione preconfigurata di factory connessa</span><span class="sxs-lookup"><span data-stu-id="c3610-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="c3610-110">Come eseguire l'aggiornamento alla versione più recente della soluzione preconfigurata per il monitoraggio remoto che usa le funzionalità di gestione del dispositivo hub IoT?</span><span class="sxs-lookup"><span data-stu-id="c3610-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="c3610-111">Se la soluzione preconfigurata viene distribuita dal sito https://www.azureiotsuite.com/, viene sempre distribuita una nuova istanza della versione più recente della soluzione.</span><span class="sxs-lookup"><span data-stu-id="c3610-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="c3610-112">Se la soluzione preconfigurata viene distribuita tramite la riga di comando, è possibile aggiornare una distribuzione esistente con il nuovo codice.</span><span class="sxs-lookup"><span data-stu-id="c3610-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="c3610-113">Vedere [Distribuzione cloud][lnk-cloud-deployment] nel [repository][lnk-remote-monitoring-github] GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3610-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c3610-114">Come aggiungere il supporto per un nuovo metodo del dispositivo alla soluzione preconfigurata di monitoraggio remoto?</span><span class="sxs-lookup"><span data-stu-id="c3610-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="c3610-115">Vedere la sezione [Aggiungere il supporto per un nuovo metodo al simulatore][lnk-add-method] nell'articolo [Personalizzare una soluzione preconfigurata][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="c3610-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="c3610-116">Perché il dispositivo simulato ignora le modifiche alle proprietà desiderate?</span><span class="sxs-lookup"><span data-stu-id="c3610-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="c3610-117">Nella soluzione preconfigurata per il monitoraggio remoto, il codice del dispositivo simulato usa le proprietà desiderate **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** per aggiornare le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="c3610-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="c3610-118">Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="c3610-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="c3610-119">Perché il dispositivo non è visualizzato nell'elenco dei dispositivi nel dashboard della soluzione?</span><span class="sxs-lookup"><span data-stu-id="c3610-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="c3610-120">L'elenco dei dispositivi nel dashboard della soluzione usa una query per restituire l'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="c3610-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="c3610-121">Attualmente, una query non può restituire più di 10.000 dispositivi.</span><span class="sxs-lookup"><span data-stu-id="c3610-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="c3610-122">Provare ad applicare alla query criteri di ricerca più restrittivi.</span><span class="sxs-lookup"><span data-stu-id="c3610-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="c3610-123">Che differenza c'è tra eliminare un gruppo di risorse nel portale di Azure e fare clic per eliminare una soluzione preconfigurata in azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="c3610-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="c3610-124">Se si elimina la soluzione preconfigurata in [azureiotsuite.com][lnk-azureiotsuite], si eliminano anche tutte le risorse di cui è stato eseguito il provisioning al momento della creazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="c3610-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="c3610-125">Se sono state aggiunte altre risorse al gruppo, anche queste ultime vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="c3610-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="c3610-126">Se si elimina il gruppo di risorse nel [portale di Azure][lnk-azure-portal], si eliminano solo le risorse presenti in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="c3610-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="c3610-127">È anche necessario eliminare l'applicazione Azure Active Directory associata alla soluzione preconfigurata nel [portale di Azure classico][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="c3610-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="c3610-128">Di quante istanze dell'hub IoT è possibile eseguire il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="c3610-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="c3610-129">Per impostazione predefinita, è possibile eseguire il provisioning di [10 hub IoT per ogni sottoscrizione][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="c3610-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="c3610-130">È possibile creare un [ticket di supporto di Azure][link-azuresupportticket] per aumentare questo limite.</span><span class="sxs-lookup"><span data-stu-id="c3610-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="c3610-131">Di conseguenza, poiché ogni soluzione preconfigurata effettua il provisioning di un nuovo hub IoT, è possibile effettuare il provisioning solo di un massimo di 10 soluzioni preconfigurate in una determinata sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c3610-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="c3610-132">Di quante istanze di Azure Cosmos DB è possibile effettuare il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="c3610-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="c3610-133">Cinquanta.</span><span class="sxs-lookup"><span data-stu-id="c3610-133">Fifty.</span></span> <span data-ttu-id="c3610-134">Anche se è possibile creare un [ticket di supporto di Azure][link-azuresupportticket] per aumentare questo limite, per impostazione predefinita è possibile effettuare il provisioning solo di 50 istanze di Cosmos DB per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c3610-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="c3610-135">Di quante API di Bing Maps gratuite è possibile eseguire il provisioning in una sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="c3610-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="c3610-136">Due.</span><span class="sxs-lookup"><span data-stu-id="c3610-136">Two.</span></span> <span data-ttu-id="c3610-137">È possibile creare solo due Transazioni sito Web interno - Livello 1 per Bing Maps per i piani aziendali in una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3610-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="c3610-138">Per impostazione predefinita, il provisioning della soluzione per il monitoraggio remoto viene effettuato con il piano Transazioni sito Web interno - Livello 1.</span><span class="sxs-lookup"><span data-stu-id="c3610-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="c3610-139">Di conseguenza, è possibile eseguire il provisioning di un massimo di due soluzioni per il monitoraggio remoto in una sottoscrizione senza modifiche.</span><span class="sxs-lookup"><span data-stu-id="c3610-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="c3610-140">Se si usa la distribuzione di soluzioni di monitoraggio remoto con una mappa statica, come si aggiunge una mappa di Bing interattiva?</span><span class="sxs-lookup"><span data-stu-id="c3610-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="c3610-141">È possibile ottenere la chiave QueryKey di Bing Maps API for Enterprise dal [portale di Azure][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="c3610-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="c3610-142">Passare al gruppo di risorse in cui si trova Bing Maps API for Enterprise nel [portale di Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c3610-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="c3610-143">Fare clic su **All Settings** (Tutte le impostazioni) e quindi su **Key Management** (Gestione chiavi).</span><span class="sxs-lookup"><span data-stu-id="c3610-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="c3610-144">Vengono visualizzate le due chiavi **MasterKey** e **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="c3610-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="c3610-145">Copiare il valore per **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="c3610-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="c3610-146">Se non si ha un account Bing Maps API for Enterprise,</span><span class="sxs-lookup"><span data-stu-id="c3610-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="c3610-147">è possibile crearne uno nel [portale di Azure][lnk-azure-portal]. A questo scopo fare clic su +Nuovo, cercare Bing Maps API for Enterprise e seguire le istruzioni per la creazione.</span><span class="sxs-lookup"><span data-stu-id="c3610-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="c3610-148">Ottenere il codice più recente da [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="c3610-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="c3610-149">Eseguire una distribuzione locale o cloud in base alle indicazioni per la distribuzione da riga di comando nella cartella /docs/ del repository.</span><span class="sxs-lookup"><span data-stu-id="c3610-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="c3610-150">Dopo aver eseguito una distribuzione locale o cloud, cercare nella cartella radice il file *.user.config creato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c3610-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="c3610-151">Aprire il file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="c3610-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="c3610-152">Modificare la riga seguente in modo da includere il valore copiato da **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="c3610-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="c3610-153">È possibile creare una soluzione preconfigurata se è disponibile Microsoft Azure per DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="c3610-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="c3610-154">Al momento non è possibile creare una soluzione preconfigurata con un account [Microsoft Azure for DreamSpark][lnk-dreamspark],</span><span class="sxs-lookup"><span data-stu-id="c3610-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="c3610-155">ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="c3610-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="c3610-156">È possibile creare una soluzione preconfigurata se si dispone di una sottoscrizione di Cloud Solution Provider?</span><span class="sxs-lookup"><span data-stu-id="c3610-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="c3610-157">È possibile attualmente creare una soluzione preconfigurata con una sottoscrizione di Cloud Solution Provider,</span><span class="sxs-lookup"><span data-stu-id="c3610-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="c3610-158">ma è possibile creare facilmente un [account di valutazione gratuito per][lnk-30daytrial] che consente di creare una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="c3610-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="c3610-159">Come si elimina un tenant AAD?</span><span class="sxs-lookup"><span data-stu-id="c3610-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="c3610-160">Vedere il post del blog di Eric Golpe relativo alla [procedura dettagliata di eliminazione di un tenant di Azure AD][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="c3610-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="c3610-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3610-161">Next steps</span></span>

<span data-ttu-id="c3610-162">È anche possibile esplorare alcune altre funzionalità delle soluzioni preconfigurate di IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="c3610-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="c3610-163">[Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="c3610-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="c3610-164">Panoramica della soluzione preconfigurata di factory connessa</span><span class="sxs-lookup"><span data-stu-id="c3610-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="c3610-165">[Sicurezza IoT sin dall'inizio][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="c3610-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
