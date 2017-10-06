---
title: aaaMove risorse di Azure toonew sottoscrizione o la risorsa gruppo | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure toomove risorse tooa nuovo gruppo di risorse o di sottoscrizione.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="97076-103">Gruppo di risorse di spostare risorse toonew o sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="97076-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="97076-104">Questo argomento viene illustrato come toomove risorse tooeither una nuova sottoscrizione o una nuova risorsa gruppo hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="97076-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="97076-105">È possibile utilizzare il portale di hello, PowerShell, CLI di Azure o hello risorsa toomove API REST.</span><span class="sxs-lookup"><span data-stu-id="97076-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="97076-106">operazioni di spostamento Hello in questo argomento sono disponibili tooyou senza assistenza dal supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="97076-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="97076-107">Quando lo spostamento delle risorse, sia il gruppo di origine hello e il gruppo di destinazione hello sono bloccate durante l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="97076-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="97076-108">Scrivere e le operazioni di eliminazione sono bloccati in gruppi di risorse hello fino al completamento di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="97076-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="97076-109">Non è possibile aggiungere, aggiornare o eliminare le risorse in gruppi di risorse hello, ma questo non significa che vengono bloccate risorse hello, significa che questo blocco.</span><span class="sxs-lookup"><span data-stu-id="97076-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="97076-110">Ad esempio, se si sposta un Server SQL e il relativo database tooa nuovo gruppo di risorse, un'applicazione che utilizza database hello non esperienze tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="97076-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="97076-111">Può comunque leggere e scrivere toohello database.</span><span class="sxs-lookup"><span data-stu-id="97076-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="97076-112">È possibile modificare il percorso di hello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="97076-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="97076-113">Lo spostamento di una risorsa solo spostarlo tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="97076-114">nuovo gruppo di risorse Hello può avere un percorso diverso, ma che non modificare il percorso di hello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="97076-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="97076-115">Questo articolo descrive la modalità dell'account offerte toomove risorse all'interno di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="97076-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="97076-116">Se si desidera effettivamente toochange all'account Azure offerta (ad esempio, l'aggiornamento da toopre pagamento a consumo-pay) continuando toowork con le risorse esistenti, vedere [cambiare l'offerta di sottoscrizione di Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="97076-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="97076-117">Controllo prima di spostare le risorse</span><span class="sxs-lookup"><span data-stu-id="97076-117">Checklist before moving resources</span></span>
<span data-ttu-id="97076-118">Esistono tooperform alcuni importanti passaggi prima di spostare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="97076-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="97076-119">La verifica di queste condizioni consente di evitare errori.</span><span class="sxs-lookup"><span data-stu-id="97076-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="97076-120">Hello le sottoscrizioni di origine e di destinazione devono esistere all'interno di hello stesso [tenant Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="97076-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="97076-121">toocheck che entrambe le sottoscrizioni sono hello stesso ID tenant, usare Azure PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="97076-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="97076-122">Per Azure PowerShell usare:</span><span class="sxs-lookup"><span data-stu-id="97076-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="97076-123">Per l'interfaccia della riga di comando di Azure 2.0, usare:</span><span class="sxs-lookup"><span data-stu-id="97076-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="97076-124">Se hello tenant ID per le sottoscrizioni di origine e destinazione hello non sono hello stesso, è possibile tentare directory hello toochange per sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="97076-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="97076-125">Tuttavia, questa opzione è disponibile tooService solo gli amministratori che ha eseguito l'accesso con un account Microsoft (non un account aziendale).</span><span class="sxs-lookup"><span data-stu-id="97076-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="97076-126">modifica della directory di hello, accedi toohello tooattempt [portale classico](https://manage.windowsazure.com/)e selezionare **impostazioni**, selezionare la sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="97076-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="97076-127">Se hello **modifica Directory** icona è disponibile, selezionarlo toochange hello associati di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="97076-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![modifica directory](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="97076-129">Se tale icona non è disponibile, è necessario contattare il supporto toomove hello risorse tooa nuovo tenant.</span><span class="sxs-lookup"><span data-stu-id="97076-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="97076-130">servizio Hello è necessario abilitare le risorse di toomove possibilità hello.</span><span class="sxs-lookup"><span data-stu-id="97076-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="97076-131">In questo argomento sono elencati i servizi che consentono di spostare risorse e quelli che invece non lo permettono.</span><span class="sxs-lookup"><span data-stu-id="97076-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="97076-132">sottoscrizione di destinazione Hello deve essere registrati per il provider di risorse hello della risorsa hello viene spostato.</span><span class="sxs-lookup"><span data-stu-id="97076-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="97076-133">Se non si riceve un errore che informa che hello **sottoscrizione non è registrata per un tipo di risorsa**.</span><span class="sxs-lookup"><span data-stu-id="97076-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="97076-134">Questo problema possono verificarsi durante lo spostamento di una nuova sottoscrizione tooa di risorse, ma tale sottoscrizione non sia mai stato utilizzato con il tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="97076-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="97076-135">toolearn come toocheck hello lo stato della registrazione e registrare i provider di risorse, vedere [tipi e i provider di risorse](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="97076-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="97076-136">Quando il supporto toocall</span><span class="sxs-lookup"><span data-stu-id="97076-136">When toocall support</span></span>
<span data-ttu-id="97076-137">È possibile spostare la maggior parte delle risorse tramite operazioni hello self-service illustrate in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="97076-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="97076-138">Utilizzare hello self-service delle operazioni:</span><span class="sxs-lookup"><span data-stu-id="97076-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="97076-139">Spostare le risorse di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97076-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="97076-140">Spostare le risorse classiche in base toohello [limitazioni di distribuzione classica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="97076-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="97076-141">Chiamare il supporto quando è necessario:</span><span class="sxs-lookup"><span data-stu-id="97076-141">Call support when you need to:</span></span>

* <span data-ttu-id="97076-142">Spostare le risorse tooa nuovo account Azure (e tenant di Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="97076-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="97076-143">Spostare le risorse classiche ma problemi con limitazioni hello.</span><span class="sxs-lookup"><span data-stu-id="97076-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="97076-144">Servizi che abilitano lo spostamento</span><span class="sxs-lookup"><span data-stu-id="97076-144">Services that enable move</span></span>
<span data-ttu-id="97076-145">Per il momento, servizi di hello che consentono lo spostamento tooboth un nuovo gruppo di risorse e la sottoscrizione sono:</span><span class="sxs-lookup"><span data-stu-id="97076-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="97076-146">Gestione API</span><span class="sxs-lookup"><span data-stu-id="97076-146">API Management</span></span>
* <span data-ttu-id="97076-147">App del servizio app (app Web): vedere [Limitazioni del servizio app](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="97076-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="97076-148">Application Insights</span></span>
* <span data-ttu-id="97076-149">Automazione</span><span class="sxs-lookup"><span data-stu-id="97076-149">Automation</span></span>
* <span data-ttu-id="97076-150">Batch</span><span class="sxs-lookup"><span data-stu-id="97076-150">Batch</span></span>
* <span data-ttu-id="97076-151">Bing Mappe</span><span class="sxs-lookup"><span data-stu-id="97076-151">Bing Maps</span></span>
* <span data-ttu-id="97076-152">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="97076-152">CDN</span></span>
* <span data-ttu-id="97076-153">Servizi cloud: vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="97076-154">Servizi cognitivi</span><span class="sxs-lookup"><span data-stu-id="97076-154">Cognitive Services</span></span>
* <span data-ttu-id="97076-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="97076-155">Content Moderator</span></span>
* <span data-ttu-id="97076-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="97076-156">Data Catalog</span></span>
* <span data-ttu-id="97076-157">Data factory</span><span class="sxs-lookup"><span data-stu-id="97076-157">Data Factory</span></span>
* <span data-ttu-id="97076-158">Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="97076-158">Data Lake Analytics</span></span>
* <span data-ttu-id="97076-159">Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="97076-159">Data Lake Store</span></span>
* <span data-ttu-id="97076-160">DNS</span><span class="sxs-lookup"><span data-stu-id="97076-160">DNS</span></span>
* <span data-ttu-id="97076-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="97076-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="97076-162">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="97076-162">Event Hubs</span></span>
* <span data-ttu-id="97076-163">Cluster HDInsight - vedere [Limitazioni di HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="97076-164">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="97076-164">IoT Hubs</span></span>
* <span data-ttu-id="97076-165">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="97076-165">Key Vault</span></span>
* <span data-ttu-id="97076-166">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="97076-166">Load Balancers</span></span>
* <span data-ttu-id="97076-167">App per la logica</span><span class="sxs-lookup"><span data-stu-id="97076-167">Logic Apps</span></span>
* <span data-ttu-id="97076-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="97076-168">Machine Learning</span></span>
* <span data-ttu-id="97076-169">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="97076-169">Media Services</span></span>
* <span data-ttu-id="97076-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="97076-170">Mobile Engagement</span></span>
* <span data-ttu-id="97076-171">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="97076-171">Notification Hubs</span></span>
* <span data-ttu-id="97076-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="97076-172">Operational Insights</span></span>
* <span data-ttu-id="97076-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="97076-173">Operations Management</span></span>
* <span data-ttu-id="97076-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="97076-174">Power BI</span></span>
* <span data-ttu-id="97076-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="97076-175">Redis Cache</span></span>
* <span data-ttu-id="97076-176">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="97076-176">Scheduler</span></span>
* <span data-ttu-id="97076-177">Search</span><span class="sxs-lookup"><span data-stu-id="97076-177">Search</span></span>
* <span data-ttu-id="97076-178">Gestione server</span><span class="sxs-lookup"><span data-stu-id="97076-178">Server Management</span></span>
* <span data-ttu-id="97076-179">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="97076-179">Service Bus</span></span>
* <span data-ttu-id="97076-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="97076-180">Service Fabric</span></span>
* <span data-ttu-id="97076-181">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="97076-181">Storage</span></span>
* <span data-ttu-id="97076-182">Archiviazione (classica): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="97076-183">Analisi di flusso: i processi di analisi di flusso non possono essere spostati durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="97076-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="97076-184">Il server di Database SQL - hello database e server devono risiedere in hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="97076-185">Quando si sposta un server SQL, quindi, vengono spostati anche tutti i relativi database.</span><span class="sxs-lookup"><span data-stu-id="97076-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="97076-186">Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="97076-186">Traffic Manager</span></span>
* <span data-ttu-id="97076-187">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="97076-187">Virtual Machines</span></span>
* <span data-ttu-id="97076-188">Macchine virtuali con certificato archiviato nell'insieme di credenziali chiave - toonew spostamento risorse del gruppo nella stessa sottoscrizione è abilitata, ma spostamento tra sottoscrizioni non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="97076-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="97076-189">Macchine virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="97076-190">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="97076-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="97076-191">Reti virtuali: attualmente non è possibile spostare una rete virtuale con peering fino a quando non viene disabilitato il peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="97076-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="97076-192">Una volta disabilitato, hello rete virtuale può essere spostato correttamente e hello peering di reti virtuali può essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="97076-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="97076-193">Inoltre, una rete virtuale non può essere spostato tooa altra sottoscrizione se hello rete virtuale contiene una qualsiasi subnet con collegamenti di navigazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="97076-194">Ad esempio, una subnet della rete virtuale ha un collegamento di navigazione delle risorse quando una risorsa redis Microsoft.Cache viene distribuita in questa subnet.</span><span class="sxs-lookup"><span data-stu-id="97076-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="97076-195">Gateway VPN</span><span class="sxs-lookup"><span data-stu-id="97076-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="97076-196">Servizi che non abilitano lo spostamento</span><span class="sxs-lookup"><span data-stu-id="97076-196">Services that do not enable move</span></span>
<span data-ttu-id="97076-197">servizi di Hello che attualmente non consentono di spostare una risorsa sono:</span><span class="sxs-lookup"><span data-stu-id="97076-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="97076-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="97076-198">AD Domain Services</span></span>
* <span data-ttu-id="97076-199">Servizio ibrido per l'integrità di AD</span><span class="sxs-lookup"><span data-stu-id="97076-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="97076-200">gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="97076-200">Application Gateway</span></span>
* <span data-ttu-id="97076-201">Set di disponibilità con macchine virtuali con Managed Disks</span><span class="sxs-lookup"><span data-stu-id="97076-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="97076-202">Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="97076-202">BizTalk Services</span></span>
* <span data-ttu-id="97076-203">Servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="97076-203">Container Service</span></span>
* <span data-ttu-id="97076-204">Express Route</span><span class="sxs-lookup"><span data-stu-id="97076-204">Express Route</span></span>
* <span data-ttu-id="97076-205">DevTest Labs - toonew spostamento risorse del gruppo nella stessa sottoscrizione sono abilitata, ma tra spostamento sottoscrizione non sono abilitata.</span><span class="sxs-lookup"><span data-stu-id="97076-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="97076-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="97076-206">Dynamics LCS</span></span>
* <span data-ttu-id="97076-207">Immagini create da Managed Disks</span><span class="sxs-lookup"><span data-stu-id="97076-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="97076-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="97076-208">Managed Disks</span></span>
* <span data-ttu-id="97076-209">Applicazioni gestite</span><span class="sxs-lookup"><span data-stu-id="97076-209">Managed Applications</span></span>
* <span data-ttu-id="97076-210">Insieme di credenziali di servizi di ripristino - anche eseguire hello servizi di ripristino non sposta hello calcolo, rete e archiviazione, le risorse associate all'insieme di credenziali, vedere [limitazioni di servizi di ripristino](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="97076-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="97076-211">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="97076-211">Security</span></span>
* <span data-ttu-id="97076-212">Snapshot creati da Managed Disks</span><span class="sxs-lookup"><span data-stu-id="97076-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="97076-213">Gestione dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="97076-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="97076-214">Macchine virtuali con Managed Disks</span><span class="sxs-lookup"><span data-stu-id="97076-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="97076-215">Reti virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="97076-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="97076-216">Impossibile spostare le macchine virtuali create da risorse Marketplace fra sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="97076-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="97076-217">È necessario toobe deprovisioning nella sottoscrizione corrente hello e distribuito di nuovo nella nuova sottoscrizione hello risorsa</span><span class="sxs-lookup"><span data-stu-id="97076-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="97076-218">Limitazioni del servizio app</span><span class="sxs-lookup"><span data-stu-id="97076-218">App Service limitations</span></span>
<span data-ttu-id="97076-219">Quando si usano le app del servizio app non è possibile spostare solo un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="97076-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="97076-220">le applicazioni di servizio App toomove, le opzioni disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="97076-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="97076-221">Spostare il piano di servizio App hello e tutte le altre risorse del servizio App in tale gruppo tooa nuova risorsa gruppo di risorse che non dispone di risorse del servizio App.</span><span class="sxs-lookup"><span data-stu-id="97076-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="97076-222">Questo requisito significa che è necessario spostare anche hello risorse del servizio App che non sono associati al piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="97076-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="97076-223">Sposta gruppo di risorse diverso tooa hello App, ma Mantieni tutti i piani di servizio App nel gruppo di risorse originale hello.</span><span class="sxs-lookup"><span data-stu-id="97076-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="97076-224">Hello servizio App non è necessario tooreside nel piano hello stesso gruppo di risorse applicazione hello per hello app toofunction correttamente.</span><span class="sxs-lookup"><span data-stu-id="97076-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="97076-225">Se ad esempio il gruppo di risorse contiene:</span><span class="sxs-lookup"><span data-stu-id="97076-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="97076-226">**web-a** che è associata a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="97076-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="97076-227">**web-b** che è associata a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="97076-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="97076-228">Le opzioni possibili sono:</span><span class="sxs-lookup"><span data-stu-id="97076-228">Your options are:</span></span>

* <span data-ttu-id="97076-229">Spostare **web-a**, **plan-a**, **web-b** e **plan-b**</span><span class="sxs-lookup"><span data-stu-id="97076-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="97076-230">Spostare **web-a** e **web-b**</span><span class="sxs-lookup"><span data-stu-id="97076-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="97076-231">Spostare **web-a**</span><span class="sxs-lookup"><span data-stu-id="97076-231">Move **web-a**</span></span>
* <span data-ttu-id="97076-232">Spostare **web-b**</span><span class="sxs-lookup"><span data-stu-id="97076-232">Move **web-b**</span></span>

<span data-ttu-id="97076-233">Con tutte le altre combinazioni si lascerebbe dove si trova un tipo di risorsa che non può essere lasciato nella stessa posizione quando si sposta un piano di servizio app (qualsiasi tipo di risorsa del servizio app).</span><span class="sxs-lookup"><span data-stu-id="97076-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="97076-234">Se l'app web si trova in un gruppo di risorse diverso rispetto al relativo piano di servizio App, ma si desidera toomove entrambi tooa nuovo gruppo di risorse, è necessario eseguire spostamento hello in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="97076-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="97076-235">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="97076-235">For example:</span></span>

* <span data-ttu-id="97076-236">**web-a** si trova in **web-group**</span><span class="sxs-lookup"><span data-stu-id="97076-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="97076-237">**plan-a** si trova in **plan-group**</span><span class="sxs-lookup"><span data-stu-id="97076-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="97076-238">Si desidera **web-a** e **piano-a** tooreside in **gruppo combinati**</span><span class="sxs-lookup"><span data-stu-id="97076-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="97076-239">tooaccomplish questo spostamento, eseguire due operazioni di spostamento separato in hello seguente sequenza:</span><span class="sxs-lookup"><span data-stu-id="97076-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="97076-240">Spostare hello **web-a** troppo**piano gruppo**</span><span class="sxs-lookup"><span data-stu-id="97076-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="97076-241">Spostare **web-a** e **piano-a** troppo**gruppo combinati**.</span><span class="sxs-lookup"><span data-stu-id="97076-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="97076-242">È possibile spostare un certificato di servizio App tooa nuovo gruppo di risorse o di una sottoscrizione senza problemi.</span><span class="sxs-lookup"><span data-stu-id="97076-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="97076-243">Tuttavia, se l'app web include un certificato SSL di acquistata esternamente e caricato toohello app, è necessario eliminare certificato hello prima dell'applicazione web di hello mobile.</span><span class="sxs-lookup"><span data-stu-id="97076-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="97076-244">Ad esempio, è possibile eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="97076-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="97076-245">Eliminare il certificato di hello caricata dall'app web hello</span><span class="sxs-lookup"><span data-stu-id="97076-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="97076-246">Spostare hello web app</span><span class="sxs-lookup"><span data-stu-id="97076-246">Move hello web app</span></span>
3. <span data-ttu-id="97076-247">Caricare hello certificato toohello web app</span><span class="sxs-lookup"><span data-stu-id="97076-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="97076-248">Limitazioni dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="97076-248">Recovery Services limitations</span></span>
<span data-ttu-id="97076-249">Spostamento non è abilitato per l'archiviazione, rete, o risorse di calcolo utilizzato tooset ripristino di emergenza con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97076-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="97076-250">Ad esempio, si supponga di che aver configurato la replica di on-premise macchine tooa account di archiviazione (Storage1) e desidera toocome macchina hello protetto dopo il failover tooAzure come una macchina virtuale (VM1) è associata la rete virtuale tooa (rete1).</span><span class="sxs-lookup"><span data-stu-id="97076-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="97076-251">Non è possibile spostare una di queste risorse Azure - Storage1, VM1, e - rete1 tra risorse gruppi all'interno di hello stessa sottoscrizione o per le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="97076-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="97076-252">Limitazioni di HDInsight</span><span class="sxs-lookup"><span data-stu-id="97076-252">HDInsight limitations</span></span>

<span data-ttu-id="97076-253">È possibile spostare HDInsight cluster tooa nuova sottoscrizione o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="97076-254">Tuttavia, è possibile spostare tra hello sottoscrizioni rete cluster di HDInsight toohello collegato risorse (ad esempio una rete virtuale hello, scheda di rete o servizio di bilanciamento del carico).</span><span class="sxs-lookup"><span data-stu-id="97076-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="97076-255">Inoltre, è possibile spostare il gruppo di risorse nuovo tooa una scheda di rete di macchina virtuale tooa collegato per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="97076-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="97076-256">Quando si sposta una nuova sottoscrizione tooa cluster HDInsight, spostare innanzitutto altre risorse (ad esempio account di archiviazione hello).</span><span class="sxs-lookup"><span data-stu-id="97076-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="97076-257">Spostare quindi il cluster di HDInsight hello da se stesso.</span><span class="sxs-lookup"><span data-stu-id="97076-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="97076-258">Limitazioni della distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="97076-258">Classic deployment limitations</span></span>
<span data-ttu-id="97076-259">salve le opzioni per lo spostamento delle risorse distribuite tramite il modello classico di hello differiscono a seconda se si desidera spostare le risorse di hello all'interno di una sottoscrizione o tooa nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="97076-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="97076-260">Stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="97076-260">Same subscription</span></span>
<span data-ttu-id="97076-261">Quando lo spostamento delle risorse dal gruppo di risorse di una risorsa gruppo tooanother all'interno di hello applicare stessa sottoscrizione, hello seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="97076-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="97076-262">Le reti virtuali (classiche) non possono essere spostate.</span><span class="sxs-lookup"><span data-stu-id="97076-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="97076-263">Macchine virtuali (classico) devono essere spostate con il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="97076-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="97076-264">Servizio cloud può essere spostato solo quando si sposta hello include tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="97076-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="97076-265">È possibile spostare un solo servizio cloud alla volta.</span><span class="sxs-lookup"><span data-stu-id="97076-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="97076-266">È possibile spostare un solo account di archiviazione (classico) alla volta.</span><span class="sxs-lookup"><span data-stu-id="97076-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="97076-267">Account di archiviazione (classico) non può essere spostato in hello stessa operazione con una macchina virtuale o un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="97076-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="97076-268">toomove le risorse classiche tooa nuovo gruppo di risorse interno hello stessa sottoscrizione, utilizzare le operazioni di spostamento standard hello tramite hello [portale](#use-portal), [Azure PowerShell](#use-powershell), [CLI di Azure](#use-azure-cli), o [API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="97076-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="97076-269">Utilizzare hello stesse operazioni quando si utilizza per lo spostamento delle risorse di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="97076-270">Nuova sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="97076-270">New subscription</span></span>
<span data-ttu-id="97076-271">Quando si spostano nuova sottoscrizione di risorse tooa, si applica hello seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="97076-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="97076-272">Tutte le risorse classiche nella sottoscrizione hello devono essere spostate in hello stessa operazione.</span><span class="sxs-lookup"><span data-stu-id="97076-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="97076-273">sottoscrizione di destinazione Hello non deve contenere tutte le altre risorse classiche.</span><span class="sxs-lookup"><span data-stu-id="97076-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="97076-274">spostamento Hello può essere richiesti solo tramite un'API REST separato per gli spostamenti classici.</span><span class="sxs-lookup"><span data-stu-id="97076-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="97076-275">comandi di spostamento Hello standard di gestione delle risorse non funzionano quando sposta le risorse classiche tooa nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="97076-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="97076-276">toomove le risorse classiche tooa nuova sottoscrizione, utilizzare hello le operazioni REST che rappresentano risorse tooclassic specifico.</span><span class="sxs-lookup"><span data-stu-id="97076-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="97076-277">toouse REST, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="97076-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="97076-278">Verifica se la sottoscrizione di origine hello può partecipare a una sottoscrizione tra spostare.</span><span class="sxs-lookup"><span data-stu-id="97076-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="97076-279">Utilizzare hello seguente operazione:</span><span class="sxs-lookup"><span data-stu-id="97076-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="97076-280">Nel corpo della richiesta hello, includere:</span><span class="sxs-lookup"><span data-stu-id="97076-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="97076-281">risposta Hello per l'operazione di convalida hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="97076-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="97076-282">Verifica se la sottoscrizione di destinazione hello può partecipare a una sottoscrizione tra spostare.</span><span class="sxs-lookup"><span data-stu-id="97076-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="97076-283">Utilizzare hello seguente operazione:</span><span class="sxs-lookup"><span data-stu-id="97076-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="97076-284">Nel corpo della richiesta hello, includere:</span><span class="sxs-lookup"><span data-stu-id="97076-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="97076-285">risposta Hello è nel stesso formato delle convalida della sottoscrizione di origine hello hello.</span><span class="sxs-lookup"><span data-stu-id="97076-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="97076-286">Se entrambe le sottoscrizioni superano la convalida, spostare tutte le risorse classiche dalla sottoscrizione di una sottoscrizione tooanother con hello seguente operazione:</span><span class="sxs-lookup"><span data-stu-id="97076-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="97076-287">Nel corpo della richiesta hello, includere:</span><span class="sxs-lookup"><span data-stu-id="97076-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="97076-288">può eseguire l'operazione di Hello per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="97076-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="97076-289">Usare il portale</span><span class="sxs-lookup"><span data-stu-id="97076-289">Use portal</span></span>
<span data-ttu-id="97076-290">risorse toomove, selezionare il gruppo di risorse hello contenente tali risorse, quindi hello **spostare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="97076-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Spostare le risorse](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="97076-292">Selezionare se si sta spostando hello risorse tooa nuovo gruppo di risorse o una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="97076-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="97076-293">Selezionare toomove risorse hello e gruppo di risorse di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="97076-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="97076-294">Confermare che è necessario tooupdate script per le risorse e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="97076-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="97076-295">Se è stata selezionata nel passaggio precedente hello sull'icona di hello Modifica sottoscrizione, è necessario selezionare anche la sottoscrizione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="97076-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![Selezione della destinazione](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="97076-297">In **notifiche**, vedrai che hello spostare l'operazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="97076-297">In **Notifications**, you see that hello move operation is running.</span></span>

![Visualizzare lo stato dello spostamento](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="97076-299">Quando è stata completata, ricevono la notifica del risultato hello.</span><span class="sxs-lookup"><span data-stu-id="97076-299">When it has completed, you are notified of hello result.</span></span>

![Visualizzare il risultato dello spostamento](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="97076-301">Usare PowerShell</span><span class="sxs-lookup"><span data-stu-id="97076-301">Use PowerShell</span></span>
<span data-ttu-id="97076-302">esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `Move-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="97076-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="97076-303">Hello primo esempio viene illustrato come toomove una risorsa tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="97076-304">Hello secondo esempio viene illustrato come toomove più risorse tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="97076-305">toomove tooa nuova sottoscrizione, includere un valore per hello `DestinationSubscriptionId` parametro.</span><span class="sxs-lookup"><span data-stu-id="97076-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="97076-306">Viene richiesto che si desidera hello toomove tooconfirm delle risorse specificate.</span><span class="sxs-lookup"><span data-stu-id="97076-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="97076-307">Usare l'interfaccia della riga di comando 2.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="97076-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="97076-308">esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `az resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="97076-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="97076-309">Fornire hello ID risorsa delle toomove risorse hello.</span><span class="sxs-lookup"><span data-stu-id="97076-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="97076-310">È possibile ottenere l'ID di risorsa con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97076-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="97076-311">Hello di esempio seguente viene illustrato come una risorsa di archiviazione toomove account tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="97076-312">In hello `--ids` parametro, fornire un elenco separato da spazi di toomove gli ID di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="97076-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="97076-313">nuova sottoscrizione tooa toomove, fornire hello `--destination-subscription-id` parametro.</span><span class="sxs-lookup"><span data-stu-id="97076-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="97076-314">Usare l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="97076-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="97076-315">esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `azure resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="97076-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="97076-316">Fornire hello ID risorsa delle toomove risorse hello.</span><span class="sxs-lookup"><span data-stu-id="97076-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="97076-317">È possibile ottenere l'ID di risorsa con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97076-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="97076-318">Restituisce hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="97076-318">Which returns hello following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="97076-319">Hello di esempio seguente viene illustrato come una risorsa di archiviazione toomove account tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97076-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="97076-320">In hello `-i` parametro, fornire un elenco delimitato da virgole di toomove gli ID di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="97076-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="97076-321">Viene richiesto che si desidera toomove hello tooconfirm risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="97076-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="97076-322">Usare l'API REST</span><span class="sxs-lookup"><span data-stu-id="97076-322">Use REST API</span></span>
<span data-ttu-id="97076-323">gruppo risorse tooanother toomove esistente risorse o sottoscrizione, eseguire:</span><span class="sxs-lookup"><span data-stu-id="97076-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="97076-324">Nel corpo della richiesta hello, specificare gruppo di risorse di destinazione hello e toomove risorse hello.</span><span class="sxs-lookup"><span data-stu-id="97076-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="97076-325">Per ulteriori informazioni sull'operazione di resto spostamento hello, vedere [lo spostamento di risorse](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="97076-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97076-326">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97076-326">Next steps</span></span>
* <span data-ttu-id="97076-327">toolearn sui cmdlet di PowerShell per gestire la sottoscrizione, vedere [tramite Azure PowerShell con Gestione risorse di](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="97076-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="97076-328">toolearn sui comandi CLI di Azure per gestire la sottoscrizione, vedere [Using hello CLI di Azure con Gestione risorse di](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="97076-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="97076-329">toolearn sulle funzionalità del portale per gestire la sottoscrizione, vedere [utilizzando le risorse di Azure toomanage portale hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="97076-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="97076-330">toolearn sull'applicazione di una risorsa tooyour organizzazione logica, vedere [tramite tag tooorganize le risorse](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="97076-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
