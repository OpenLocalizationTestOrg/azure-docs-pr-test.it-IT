---
title: Spostare le risorse di Azure in una nuova sottoscrizione o in un gruppo di risorse | Microsoft Docs
description: Usare Azure Resource Manager per spostare risorse a un nuovo gruppo di risorse o a una nuova sottoscrizione.
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="98daa-103">Spostare le risorse in un gruppo di risorse o una sottoscrizione nuovi</span><span class="sxs-lookup"><span data-stu-id="98daa-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="98daa-104">Questo argomento illustra come spostare le risorse in una nuova sottoscrizione o in un nuovo gruppo di risorse nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="98daa-105">È possibile usare il portale, PowerShell, l'interfaccia della riga di comando di Azure o l'API REST per spostare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="98daa-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="98daa-106">Le operazioni di spostamento descritte in questo argomento non richiedono assistenza da parte del supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="98daa-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="98daa-107">Durante lo spostamento di risorse, sia il gruppo di origine che il gruppo di destinazione sono bloccati durante l'operazione.</span><span class="sxs-lookup"><span data-stu-id="98daa-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="98daa-108">Le operazioni di scrittura ed eliminazione sono bloccate nei gruppi di risorse fino al completamento dello spostamento.</span><span class="sxs-lookup"><span data-stu-id="98daa-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="98daa-109">Questo blocco indica che non è possibile aggiungere, aggiornare o eliminare le risorse dei gruppi di risorse, ma non che le risorse sono bloccate.</span><span class="sxs-lookup"><span data-stu-id="98daa-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="98daa-110">Se ad esempio si sposta un Server SQL con il relativo database in un nuovo gruppo di risorse, nelle applicazioni che usano il database non si verificano tempi di inattività,</span><span class="sxs-lookup"><span data-stu-id="98daa-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="98daa-111">poiché rimane possibile leggere e scrivere nel database.</span><span class="sxs-lookup"><span data-stu-id="98daa-111">It can still read and write to the database.</span></span>

<span data-ttu-id="98daa-112">Non è possibile modificare il percorso della risorsa.</span><span class="sxs-lookup"><span data-stu-id="98daa-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="98daa-113">Lo spostamento di una risorsa comporta solo il suo spostamento in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="98daa-114">Il nuovo gruppo di risorse può avere un percorso diverso, ma ciò non modifica la posizione della risorsa.</span><span class="sxs-lookup"><span data-stu-id="98daa-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="98daa-115">In questo articolo viene descritto come spostare le risorse nell'offerta di un account di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="98daa-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="98daa-116">Se si vuole che modificare l'offerta dell'account di Azure, ad esempio effettuando l'aggiornamento da pagamento in base al consumo a pagamento anticipato, pur continuando a lavorare con le risorse esistenti, vedere [Trasferire la sottoscrizione di Azure a un'altra offerta](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="98daa-117">Controllo prima di spostare le risorse</span><span class="sxs-lookup"><span data-stu-id="98daa-117">Checklist before moving resources</span></span>
<span data-ttu-id="98daa-118">Prima di spostare una risorsa è necessario eseguire alcuni passi importanti.</span><span class="sxs-lookup"><span data-stu-id="98daa-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="98daa-119">La verifica di queste condizioni consente di evitare errori.</span><span class="sxs-lookup"><span data-stu-id="98daa-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="98daa-120">Le sottoscrizioni di origine e di destinazione devono trovarsi nello stesso [tenant di Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="98daa-121">Per verificare che entrambe le sottoscrizioni contengano lo stesso ID tenant, usare Azure PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="98daa-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="98daa-122">Per Azure PowerShell usare:</span><span class="sxs-lookup"><span data-stu-id="98daa-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="98daa-123">Per l'interfaccia della riga di comando di Azure 2.0, usare:</span><span class="sxs-lookup"><span data-stu-id="98daa-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="98daa-124">Se gli ID tenant per le sottoscrizioni di origine e di destinazione non sono uguali, è possibile tentare di modificare la directory della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="98daa-125">Tuttavia, questa opzione è disponibile solo per gli amministratori del servizio sono registrati con un account Microsoft (non un account aziendale).</span><span class="sxs-lookup"><span data-stu-id="98daa-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="98daa-126">Per tentare di modificare la directory, accedere al [portale classico](https://manage.windowsazure.com/), selezionare **Impostazioni**, quindi la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="98daa-127">Se l'icona **Modifica directory** è disponibile, selezionarla per modificare l'istanza di Azure Active Directory associata.</span><span class="sxs-lookup"><span data-stu-id="98daa-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![modifica directory](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="98daa-129">Se questa icona non è disponibile, è necessario contattare il supporto per spostare le risorse in un nuovo tenant.</span><span class="sxs-lookup"><span data-stu-id="98daa-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="98daa-130">Il servizio deve abilitare lo spostamento di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="98daa-131">In questo argomento sono elencati i servizi che consentono di spostare risorse e quelli che invece non lo permettono.</span><span class="sxs-lookup"><span data-stu-id="98daa-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="98daa-132">Il provider di risorse della risorsa da spostare deve essere registrato nella sottoscrizione di destinazione,</span><span class="sxs-lookup"><span data-stu-id="98daa-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="98daa-133">altrimenti un errore indica che la **sottoscrizione non è registrata per un tipo di risorsa**.</span><span class="sxs-lookup"><span data-stu-id="98daa-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="98daa-134">Questo problema può verificarsi se si sposta una risorsa in una nuova sottoscrizione, ma la sottoscrizione non è mai stata usata con tale tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="98daa-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="98daa-135">Per informazioni su come controllare lo stato della registrazione e registrare i provider di risorse, vedere [Provider e tipi di risorse](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="98daa-136">Quando chiamare il supporto</span><span class="sxs-lookup"><span data-stu-id="98daa-136">When to call support</span></span>
<span data-ttu-id="98daa-137">È possibile spostare la maggior parte delle risorse tramite le operazioni self-service descritte in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="98daa-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="98daa-138">Usare le operazioni self-service per:</span><span class="sxs-lookup"><span data-stu-id="98daa-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="98daa-139">Spostare le risorse di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="98daa-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="98daa-140">Spostare le risorse classiche in base alle [limitazioni della distribuzione classica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="98daa-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="98daa-141">Chiamare il supporto quando è necessario:</span><span class="sxs-lookup"><span data-stu-id="98daa-141">Call support when you need to:</span></span>

* <span data-ttu-id="98daa-142">Spostare le risorse in un nuovo account di Azure (e tenant di Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="98daa-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="98daa-143">Spostare le risorse classiche ma si verificano problemi relativi alle limitazioni.</span><span class="sxs-lookup"><span data-stu-id="98daa-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="98daa-144">Servizi che abilitano lo spostamento</span><span class="sxs-lookup"><span data-stu-id="98daa-144">Services that enable move</span></span>
<span data-ttu-id="98daa-145">Di seguito sono elencati i servizi che attualmente abilitano lo spostamento in un gruppo di risorse e in una sottoscrizione nuovi:</span><span class="sxs-lookup"><span data-stu-id="98daa-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="98daa-146">Gestione API</span><span class="sxs-lookup"><span data-stu-id="98daa-146">API Management</span></span>
* <span data-ttu-id="98daa-147">App del servizio app (app Web): vedere [Limitazioni del servizio app](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="98daa-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="98daa-148">Application Insights</span></span>
* <span data-ttu-id="98daa-149">Automazione</span><span class="sxs-lookup"><span data-stu-id="98daa-149">Automation</span></span>
* <span data-ttu-id="98daa-150">Batch</span><span class="sxs-lookup"><span data-stu-id="98daa-150">Batch</span></span>
* <span data-ttu-id="98daa-151">Bing Mappe</span><span class="sxs-lookup"><span data-stu-id="98daa-151">Bing Maps</span></span>
* <span data-ttu-id="98daa-152">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="98daa-152">CDN</span></span>
* <span data-ttu-id="98daa-153">Servizi cloud: vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="98daa-154">Servizi cognitivi</span><span class="sxs-lookup"><span data-stu-id="98daa-154">Cognitive Services</span></span>
* <span data-ttu-id="98daa-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="98daa-155">Content Moderator</span></span>
* <span data-ttu-id="98daa-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="98daa-156">Data Catalog</span></span>
* <span data-ttu-id="98daa-157">Data factory</span><span class="sxs-lookup"><span data-stu-id="98daa-157">Data Factory</span></span>
* <span data-ttu-id="98daa-158">Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="98daa-158">Data Lake Analytics</span></span>
* <span data-ttu-id="98daa-159">Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="98daa-159">Data Lake Store</span></span>
* <span data-ttu-id="98daa-160">DNS</span><span class="sxs-lookup"><span data-stu-id="98daa-160">DNS</span></span>
* <span data-ttu-id="98daa-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98daa-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="98daa-162">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="98daa-162">Event Hubs</span></span>
* <span data-ttu-id="98daa-163">Cluster HDInsight - vedere [Limitazioni di HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="98daa-164">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="98daa-164">IoT Hubs</span></span>
* <span data-ttu-id="98daa-165">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="98daa-165">Key Vault</span></span>
* <span data-ttu-id="98daa-166">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="98daa-166">Load Balancers</span></span>
* <span data-ttu-id="98daa-167">App per la logica</span><span class="sxs-lookup"><span data-stu-id="98daa-167">Logic Apps</span></span>
* <span data-ttu-id="98daa-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98daa-168">Machine Learning</span></span>
* <span data-ttu-id="98daa-169">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="98daa-169">Media Services</span></span>
* <span data-ttu-id="98daa-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="98daa-170">Mobile Engagement</span></span>
* <span data-ttu-id="98daa-171">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="98daa-171">Notification Hubs</span></span>
* <span data-ttu-id="98daa-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="98daa-172">Operational Insights</span></span>
* <span data-ttu-id="98daa-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="98daa-173">Operations Management</span></span>
* <span data-ttu-id="98daa-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="98daa-174">Power BI</span></span>
* <span data-ttu-id="98daa-175">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="98daa-175">Redis Cache</span></span>
* <span data-ttu-id="98daa-176">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="98daa-176">Scheduler</span></span>
* <span data-ttu-id="98daa-177">Search</span><span class="sxs-lookup"><span data-stu-id="98daa-177">Search</span></span>
* <span data-ttu-id="98daa-178">Gestione server</span><span class="sxs-lookup"><span data-stu-id="98daa-178">Server Management</span></span>
* <span data-ttu-id="98daa-179">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="98daa-179">Service Bus</span></span>
* <span data-ttu-id="98daa-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="98daa-180">Service Fabric</span></span>
* <span data-ttu-id="98daa-181">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="98daa-181">Storage</span></span>
* <span data-ttu-id="98daa-182">Archiviazione (classica): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="98daa-183">Analisi di flusso: i processi di analisi di flusso non possono essere spostati durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="98daa-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="98daa-184">Server di database SQL: il database e il server devono trovarsi nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="98daa-185">Quando si sposta un server SQL, quindi, vengono spostati anche tutti i relativi database.</span><span class="sxs-lookup"><span data-stu-id="98daa-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="98daa-186">Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="98daa-186">Traffic Manager</span></span>
* <span data-ttu-id="98daa-187">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="98daa-187">Virtual Machines</span></span>
* <span data-ttu-id="98daa-188">Macchine virtuali con certificato archiviato in Key Vault: lo spostamento al nuovo gruppo di risorse nella stessa sottoscrizione è abilitato, ma lo spostamento fra sottoscrizioni non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="98daa-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="98daa-189">Macchine virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="98daa-190">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="98daa-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="98daa-191">Reti virtuali: attualmente non è possibile spostare una rete virtuale con peering fino a quando non viene disabilitato il peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="98daa-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="98daa-192">Dopo che il peering è stato disabilitato, è possibile spostare la rete virtuale e abilitare il peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="98daa-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="98daa-193">Inoltre, è impossibile spostare una rete virtuale in una sottoscrizione diversa se la rete virtuale contiene una qualsiasi subnet con collegamenti di navigazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="98daa-194">Ad esempio, una subnet della rete virtuale ha un collegamento di navigazione delle risorse quando una risorsa redis Microsoft.Cache viene distribuita in questa subnet.</span><span class="sxs-lookup"><span data-stu-id="98daa-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="98daa-195">Gateway VPN</span><span class="sxs-lookup"><span data-stu-id="98daa-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="98daa-196">Servizi che non abilitano lo spostamento</span><span class="sxs-lookup"><span data-stu-id="98daa-196">Services that do not enable move</span></span>
<span data-ttu-id="98daa-197">I servizi che attualmente non abilitano lo spostamento di una risorsa sono:</span><span class="sxs-lookup"><span data-stu-id="98daa-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="98daa-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="98daa-198">AD Domain Services</span></span>
* <span data-ttu-id="98daa-199">Servizio ibrido per l'integrità di AD</span><span class="sxs-lookup"><span data-stu-id="98daa-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="98daa-200">gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="98daa-200">Application Gateway</span></span>
* <span data-ttu-id="98daa-201">Set di disponibilità con macchine virtuali con Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98daa-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="98daa-202">Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="98daa-202">BizTalk Services</span></span>
* <span data-ttu-id="98daa-203">Servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="98daa-203">Container Service</span></span>
* <span data-ttu-id="98daa-204">Express Route</span><span class="sxs-lookup"><span data-stu-id="98daa-204">Express Route</span></span>
* <span data-ttu-id="98daa-205">DevTest Labs: lo spostamento al nuovo gruppo di risorse nella stessa sottoscrizione è abilitato, ma lo spostamento della sottoscrizione incrociato non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="98daa-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="98daa-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="98daa-206">Dynamics LCS</span></span>
* <span data-ttu-id="98daa-207">Immagini create da Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98daa-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="98daa-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98daa-208">Managed Disks</span></span>
* <span data-ttu-id="98daa-209">Applicazioni gestite</span><span class="sxs-lookup"><span data-stu-id="98daa-209">Managed Applications</span></span>
* <span data-ttu-id="98daa-210">Insieme di credenziali delle chiavi di Servizi di ripristino: non spostare anche le risorse di calcolo, rete e archiviazione associate con l'insieme di credenziali di Servizi di ripristino, vedere [Limitazioni dei servizi di ripristino](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="98daa-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="98daa-211">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="98daa-211">Security</span></span>
* <span data-ttu-id="98daa-212">Snapshot creati da Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98daa-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="98daa-213">Gestione dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="98daa-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="98daa-214">Macchine virtuali con Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98daa-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="98daa-215">Reti virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="98daa-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="98daa-216">Impossibile spostare le macchine virtuali create da risorse Marketplace fra sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="98daa-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="98daa-217">La risorsa deve essere sottoposta a deprovisioning nella sottoscrizione corrente e distribuita nuovamente nella nuova sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="98daa-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="98daa-218">Limitazioni del servizio app</span><span class="sxs-lookup"><span data-stu-id="98daa-218">App Service limitations</span></span>
<span data-ttu-id="98daa-219">Quando si usano le app del servizio app non è possibile spostare solo un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="98daa-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="98daa-220">Per spostare le app del servizio app, le opzioni disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="98daa-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="98daa-221">Spostare il piano di servizio app e tutte le altre risorse del servizio app del gruppo di risorse in un nuovo gruppo di risorse che non dispone di risorse del servizio app.</span><span class="sxs-lookup"><span data-stu-id="98daa-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="98daa-222">In base a questo requisito è necessario spostare anche le risorse del servizio app non associate al piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="98daa-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="98daa-223">Spostare le app in un gruppo di risorse diverso, ma mantenere tutti i piani di servizio app nel gruppo di risorse originale.</span><span class="sxs-lookup"><span data-stu-id="98daa-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="98daa-224">Per il corretto funzionamento dell'app non è necessario che il piano di servizio app risieda nello stesso gruppo di risorse in cui si trova l'app stessa.</span><span class="sxs-lookup"><span data-stu-id="98daa-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="98daa-225">Se ad esempio il gruppo di risorse contiene:</span><span class="sxs-lookup"><span data-stu-id="98daa-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="98daa-226">**web-a** che è associata a **plan-a**</span><span class="sxs-lookup"><span data-stu-id="98daa-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="98daa-227">**web-b** che è associata a **plan-b**</span><span class="sxs-lookup"><span data-stu-id="98daa-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="98daa-228">Le opzioni possibili sono:</span><span class="sxs-lookup"><span data-stu-id="98daa-228">Your options are:</span></span>

* <span data-ttu-id="98daa-229">Spostare **web-a**, **plan-a**, **web-b** e **plan-b**</span><span class="sxs-lookup"><span data-stu-id="98daa-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="98daa-230">Spostare **web-a** e **web-b**</span><span class="sxs-lookup"><span data-stu-id="98daa-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="98daa-231">Spostare **web-a**</span><span class="sxs-lookup"><span data-stu-id="98daa-231">Move **web-a**</span></span>
* <span data-ttu-id="98daa-232">Spostare **web-b**</span><span class="sxs-lookup"><span data-stu-id="98daa-232">Move **web-b**</span></span>

<span data-ttu-id="98daa-233">Con tutte le altre combinazioni si lascerebbe dove si trova un tipo di risorsa che non può essere lasciato nella stessa posizione quando si sposta un piano di servizio app (qualsiasi tipo di risorsa del servizio app).</span><span class="sxs-lookup"><span data-stu-id="98daa-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="98daa-234">Se l'app web si trova in un gruppo di risorse diverso rispetto al piano di servizio app corrispondente ma si vuole spostare entrambi gli elementi in un nuovo gruppo di risorse, è necessario eseguire lo spostamento in due fasi.</span><span class="sxs-lookup"><span data-stu-id="98daa-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="98daa-235">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="98daa-235">For example:</span></span>

* <span data-ttu-id="98daa-236">**web-a** si trova in **web-group**</span><span class="sxs-lookup"><span data-stu-id="98daa-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="98daa-237">**plan-a** si trova in **plan-group**</span><span class="sxs-lookup"><span data-stu-id="98daa-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="98daa-238">Si vuole che **web-a** e **plan-a** risiedano in **combined-group**</span><span class="sxs-lookup"><span data-stu-id="98daa-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="98daa-239">Per ottenere questo risultato è necessario eseguire due operazioni di spostamento distinte nell'ordine che segue:</span><span class="sxs-lookup"><span data-stu-id="98daa-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="98daa-240">Spostare **web-a** in **plan-group**</span><span class="sxs-lookup"><span data-stu-id="98daa-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="98daa-241">Spostare **web-a** e **plan-a** in **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="98daa-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="98daa-242">È possibile spostare un certificato del servizio app in un nuovo gruppo di risorse o una nuova sottoscrizione senza problemi.</span><span class="sxs-lookup"><span data-stu-id="98daa-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="98daa-243">Se l'app Web include un certificato SSL acquistato esternamente e caricato nell'app, tuttavia, è necessario eliminare il certificato prima di spostare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="98daa-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="98daa-244">Ad esempio, è possibile eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="98daa-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="98daa-245">Eliminare il certificato caricato dall'App Web</span><span class="sxs-lookup"><span data-stu-id="98daa-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="98daa-246">Spostare l'App Web</span><span class="sxs-lookup"><span data-stu-id="98daa-246">Move the web app</span></span>
3. <span data-ttu-id="98daa-247">Caricare il certificato nell'App Web</span><span class="sxs-lookup"><span data-stu-id="98daa-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="98daa-248">Limitazioni dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="98daa-248">Recovery Services limitations</span></span>
<span data-ttu-id="98daa-249">Lo spostamento non è abilitato per le risorse di archiviazione, di rete o di calcolo usate per configurare il ripristino di emergenza con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="98daa-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="98daa-250">Ad esempio, si supponga di avere configurato la replica delle macchine locali su un account di archiviazione (Storage1) e di desiderare che il computer protetto venga avviato dopo il failover in Azure come macchina virtuale (VM1) collegata a una rete virtuale (Network1).</span><span class="sxs-lookup"><span data-stu-id="98daa-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="98daa-251">Non è possibile spostare una di queste risorse di Azure - Storage1 VM1 e Network1 - nei gruppi di risorse all'interno della stessa sottoscrizione o tra le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="98daa-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="98daa-252">Limitazioni di HDInsight</span><span class="sxs-lookup"><span data-stu-id="98daa-252">HDInsight limitations</span></span>

<span data-ttu-id="98daa-253">È possibile spostare i cluster HDInsight in una nuova sottoscrizione o in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="98daa-254">Non è tuttavia possibile spostare tra sottoscrizioni le risorse di rete collegate al cluster HDInsight, ad esempio la rete virtuale, l'interfaccia di rete o il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="98daa-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="98daa-255">Non è possibile spostare in un nuovo gruppo di risorse un'interfaccia di rete collegata a una macchina virtuale per il cluster.</span><span class="sxs-lookup"><span data-stu-id="98daa-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="98daa-256">Quando si sposta un cluster HDInsight in una nuova sottoscrizione, spostare prima altre risorse, ad esempio l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="98daa-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="98daa-257">Spostare quindi il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98daa-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="98daa-258">Limitazioni della distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="98daa-258">Classic deployment limitations</span></span>
<span data-ttu-id="98daa-259">Le opzioni per lo spostamento delle risorse distribuite con il modello classico variano a seconda che lo spostamento avvenga all'interno di una sottoscrizione o a una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="98daa-260">Stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="98daa-260">Same subscription</span></span>
<span data-ttu-id="98daa-261">Quando si spostano risorse da un gruppo di risorse a un altro gruppo di risorse nella stessa sottoscrizione, sono valide le restrizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="98daa-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="98daa-262">Le reti virtuali (classiche) non possono essere spostate.</span><span class="sxs-lookup"><span data-stu-id="98daa-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="98daa-263">Le macchine virtuali (classiche) devono essere spostate con il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="98daa-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="98daa-264">Il servizio cloud può essere spostato solo quando lo spostamento include tutte le macchine virtuali del servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="98daa-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="98daa-265">È possibile spostare un solo servizio cloud alla volta.</span><span class="sxs-lookup"><span data-stu-id="98daa-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="98daa-266">È possibile spostare un solo account di archiviazione (classico) alla volta.</span><span class="sxs-lookup"><span data-stu-id="98daa-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="98daa-267">Un account di archiviazione (classico) non può essere spostato nella stessa operazione di spostamento che include una macchina virtuale o un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="98daa-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="98daa-268">Per spostare le risorse classiche in un nuovo gruppo di risorse all'interno della stessa sottoscrizione usare le operazioni di spostamento standard tramite il [portale](#use-portal), [Azure PowerShell](#use-powershell), l'[interfaccia della riga di comando di Azure](#use-azure-cli) o l'[API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="98daa-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="98daa-269">Usare le stesse operazioni eseguite per lo spostamento di risorse di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="98daa-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="98daa-270">Nuova sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="98daa-270">New subscription</span></span>
<span data-ttu-id="98daa-271">Quando si spostano risorse in una nuova sottoscrizione, sono valide le restrizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="98daa-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="98daa-272">Tutte le risorse classiche della sottoscrizione vanno spostate nella stessa operazione.</span><span class="sxs-lookup"><span data-stu-id="98daa-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="98daa-273">La sottoscrizione di destinazione non deve contenere nessuna delle altre risorse classiche.</span><span class="sxs-lookup"><span data-stu-id="98daa-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="98daa-274">Lo spostamento può essere richiesto solo tramite un'API REST separata per gli spostamenti di risorse classiche.</span><span class="sxs-lookup"><span data-stu-id="98daa-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="98daa-275">I comandi di spostamento standard di Resource Manager non funzionano quando si spostano risorse classiche a una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="98daa-276">Per spostare le risorse classiche in una nuova sottoscrizione, usare le operazioni REST specifiche per le risorse classiche.</span><span class="sxs-lookup"><span data-stu-id="98daa-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="98daa-277">Per usare REST, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="98daa-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="98daa-278">Controllare se la sottoscrizione di origine può partecipare a un'operazione di spostamento tra sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="98daa-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="98daa-279">Usare l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="98daa-280">Nel corpo della richiesta includere:</span><span class="sxs-lookup"><span data-stu-id="98daa-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="98daa-281">La risposta per l'operazione di convalida ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="98daa-282">Controllare se la sottoscrizione di destinazione può partecipare a un'operazione di spostamento tra sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="98daa-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="98daa-283">Usare l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="98daa-284">Nel corpo della richiesta includere:</span><span class="sxs-lookup"><span data-stu-id="98daa-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="98daa-285">La risposta ha lo stesso formato della convalida della sottoscrizione di origine.</span><span class="sxs-lookup"><span data-stu-id="98daa-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="98daa-286">Se entrambe le sottoscrizioni superano la convalida, spostare tutte le risorse classiche da una sottoscrizione a un'altra usando l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="98daa-287">Nel corpo della richiesta includere:</span><span class="sxs-lookup"><span data-stu-id="98daa-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="98daa-288">Questa operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="98daa-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="98daa-289">Usare il portale</span><span class="sxs-lookup"><span data-stu-id="98daa-289">Use portal</span></span>
<span data-ttu-id="98daa-290">Per spostare le risorse, selezionare il gruppo contenente queste risorse, quindi usare il pulsante **Sposta**.</span><span class="sxs-lookup"><span data-stu-id="98daa-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Spostare le risorse](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="98daa-292">Selezionare se si desidera spostare le risorse in un nuovo gruppo di risorse o in una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98daa-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="98daa-293">Selezionare le risorse da spostare e il gruppo di risorse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="98daa-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="98daa-294">Confermare di dover aggiornare gli script per queste risorse e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="98daa-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="98daa-295">Se si seleziona l'icona del comando Modifica sottoscrizione nel passaggio precedente, è necessario anche selezionare la sottoscrizione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="98daa-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![Selezione della destinazione](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="98daa-297">In **Notifiche**si nota che è in corso l'operazione di spostamento.</span><span class="sxs-lookup"><span data-stu-id="98daa-297">In **Notifications**, you see that the move operation is running.</span></span>

![Visualizzare lo stato dello spostamento](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="98daa-299">Al completamento dell'operazione si riceverà la notifica del risultato.</span><span class="sxs-lookup"><span data-stu-id="98daa-299">When it has completed, you are notified of the result.</span></span>

![Visualizzare il risultato dello spostamento](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="98daa-301">Usare PowerShell</span><span class="sxs-lookup"><span data-stu-id="98daa-301">Use PowerShell</span></span>
<span data-ttu-id="98daa-302">Per spostare le risorse esistenti in un gruppo di risorse o una sottoscrizione diversi, usare il comando `Move-AzureRmResource`.</span><span class="sxs-lookup"><span data-stu-id="98daa-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="98daa-303">Nel primo esempio viene illustrato come spostare una risorsa in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="98daa-304">Nel secondo esempio viene illustrato come spostare più risorse in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="98daa-305">Per eseguire lo spostamento in una nuova sottoscrizione, includere un valore per il parametro `DestinationSubscriptionId`.</span><span class="sxs-lookup"><span data-stu-id="98daa-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="98daa-306">Viene richiesto di confermare che si vuole spostare la risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="98daa-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="98daa-307">Usare l'interfaccia della riga di comando 2.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="98daa-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="98daa-308">Per spostare le risorse esistenti in un gruppo di risorse o una sottoscrizione diversi, usare il comando `az resource move`.</span><span class="sxs-lookup"><span data-stu-id="98daa-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="98daa-309">Fornire gli ID risorsa delle risorse da spostare.</span><span class="sxs-lookup"><span data-stu-id="98daa-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="98daa-310">È possibile ottenere gli ID risorsa con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="98daa-311">L'esempio seguente illustra come spostare un account di archiviazione in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="98daa-312">Nel parametro `--ids` inserire un elenco delimitato da spazi di ID di risorse da spostare.</span><span class="sxs-lookup"><span data-stu-id="98daa-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="98daa-313">Per spostare in una nuova sottoscrizione, inserire il parametro `--destination-subscription-id`.</span><span class="sxs-lookup"><span data-stu-id="98daa-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="98daa-314">Usare l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="98daa-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="98daa-315">Per spostare le risorse esistenti in un gruppo di risorse o una sottoscrizione diversi, usare il comando `azure resource move`.</span><span class="sxs-lookup"><span data-stu-id="98daa-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="98daa-316">Fornire gli ID risorsa delle risorse da spostare.</span><span class="sxs-lookup"><span data-stu-id="98daa-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="98daa-317">È possibile ottenere gli ID risorsa con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="98daa-318">Viene restituito il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="98daa-318">Which returns the following format:</span></span>

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

<span data-ttu-id="98daa-319">L'esempio seguente illustra come spostare un account di archiviazione in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98daa-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="98daa-320">Nel parametro `-i` inserire un elenco delimitato da virgole di ID di risorse da spostare.</span><span class="sxs-lookup"><span data-stu-id="98daa-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="98daa-321">Viene richiesto di confermare che si vuole spostare la risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="98daa-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="98daa-322">Usare l'API REST</span><span class="sxs-lookup"><span data-stu-id="98daa-322">Use REST API</span></span>
<span data-ttu-id="98daa-323">Per spostare le risorse esistenti in un gruppo di risorse o una sottoscrizione diversi, eseguire:</span><span class="sxs-lookup"><span data-stu-id="98daa-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="98daa-324">Nel corpo della richiesta specificare il gruppo di risorse di destinazione e le risorse da spostare.</span><span class="sxs-lookup"><span data-stu-id="98daa-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="98daa-325">Per altre informazioni sull'operazione REST di spostamento, vedere [Spostare le risorse](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="98daa-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98daa-326">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98daa-326">Next steps</span></span>
* <span data-ttu-id="98daa-327">Per informazioni sui cmdlet di PowerShell per la gestione della sottoscrizione, vedere [Uso di Azure PowerShell con Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="98daa-328">Per informazioni sui comandi dell'interfaccia della riga di comando di Azure per la gestione della sottoscrizione, vedere [Uso dell'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="98daa-329">Per informazioni sulle funzionalità del portale per la gestione della sottoscrizione, vedere [Gestire le risorse di Azure mediante il portale](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="98daa-330">Per informazioni sull'organizzazione logica delle risorse, vedere [Uso dei tag per organizzare le risorse di Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="98daa-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
