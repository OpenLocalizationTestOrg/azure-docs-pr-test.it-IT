---
title: Migrazione di macchine virtuali in Azure Resource Manager tramite l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo illustra la migrazione supportata dalla piattaforma di risorse dal modello classico al modello di Azure Resource Manager tramite l'interfaccia della riga di comando di Azure
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="c6a58-103">Eseguire la migrazione di risorse IaaS dal modello classico al modello di Azure Resource Manager tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c6a58-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="c6a58-104">Questi passaggi mostrano come usare i comandi dell'interfaccia della riga di comando di Azure per eseguire la migrazione dalle risorse IaaS (infrastruttura distribuita come servizio) dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6a58-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c6a58-105">L'articolo richiede l' [interfaccia della riga di comando di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c6a58-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c6a58-106">Tutte le operazioni descritte di seguito sono idempotenti.</span><span class="sxs-lookup"><span data-stu-id="c6a58-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="c6a58-107">Se vengono rilevati errori diversi da una funzionalità non supportata o un errore di configurazione, è consigliabile provare a ripetere l'operazione di preparazione, interruzione o commit.</span><span class="sxs-lookup"><span data-stu-id="c6a58-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="c6a58-108">La piattaforma proverà di nuovo a eseguire l'azione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="c6a58-109">Ecco un diagramma di flusso per identificare l'ordine di esecuzione dei passaggi durante un processo di migrazione</span><span class="sxs-lookup"><span data-stu-id="c6a58-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="c6a58-111">Passaggio 1: Preparare la migrazione</span><span class="sxs-lookup"><span data-stu-id="c6a58-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="c6a58-112">Ecco alcune procedure consigliate per valutare la migrazione delle risorse IaaS dal modello classico al modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c6a58-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="c6a58-113">Leggere [l'elenco di configurazioni e funzionalità non supportate](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6a58-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="c6a58-114">Se sono disponibili macchine virtuali che usano configurazioni o funzionalità non supportate, è consigliabile attendere l'annuncio del supporto di tali configurazioni o funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c6a58-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="c6a58-115">In alternativa, è possibile rimuovere tale funzionalità o uscire da tale configurazione per abilitare la migrazione se ciò soddisfa le esigenze.</span><span class="sxs-lookup"><span data-stu-id="c6a58-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="c6a58-116">Se si hanno script automatizzati che consentono di distribuire subito l'infrastruttura e le applicazioni, provare a creare una configurazione di test simile usando questi script per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="c6a58-117">In alternativa, è anche possibile configurare ambienti di esempio tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a58-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6a58-118">I gateway applicazione non sono attualmente supportati per la migrazione dal modello di distribuzione classica a Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6a58-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="c6a58-119">Per eseguire la migrazione di una rete virtuale classica con un gateway applicazione, rimuovere il gateway prima di eseguire un'operazione di preparazione dello spostamento della rete.</span><span class="sxs-lookup"><span data-stu-id="c6a58-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="c6a58-120">Dopo aver completato la migrazione, riconnettere il gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6a58-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="c6a58-121">Non è possibile eseguire la migrazione automatica di gateway ExpressRoute che si connettono a circuiti ExpressRoute in un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="c6a58-122">In tal caso, rimuovere il gateway ExpressRoute, eseguire la migrazione della rete virtuale e ricreare il gateway.</span><span class="sxs-lookup"><span data-stu-id="c6a58-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="c6a58-123">Per altre informazioni, vedere [Eseguire la migrazione di circuiti ExpressRoute e delle reti virtuali associate dalla distribuzione classica al modello di distribuzione Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c6a58-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="c6a58-124">Passaggio 2: Impostare la sottoscrizione e registrare il provider</span><span class="sxs-lookup"><span data-stu-id="c6a58-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="c6a58-125">Per gli scenari di migrazione è necessario configurare l'ambiente per il modello classico e di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6a58-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="c6a58-126">[Installare l'interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) e [selezionare la sottoscrizione](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c6a58-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="c6a58-127">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="c6a58-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="c6a58-128">Selezionare la sottoscrizione di Azure usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="c6a58-129">La registrazione è un passaggio da eseguire un'unica volta, tuttavia deve essere eseguita prima di tentare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="c6a58-130">Senza la registrazione verrà visualizzato il seguente messaggio di errore</span><span class="sxs-lookup"><span data-stu-id="c6a58-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="c6a58-131">*BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="c6a58-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="c6a58-132">Registrarsi con il provider di risorse di migrazione utilizzando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="c6a58-133">Si noti che in alcuni casi si verifica il timeout del comando.</span><span class="sxs-lookup"><span data-stu-id="c6a58-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="c6a58-134">Tuttavia, la registrazione verrà completata.</span><span class="sxs-lookup"><span data-stu-id="c6a58-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="c6a58-135">Attendere cinque minuti che la registrazione venga completata.</span><span class="sxs-lookup"><span data-stu-id="c6a58-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="c6a58-136">È possibile controllare lo stato dell'approvazione con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="c6a58-137">Assicurarsi che RegistrationState sia `Registered` prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="c6a58-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="c6a58-138">Passare ora dall'interfaccia della riga di comando alla modalità `asm` .</span><span class="sxs-lookup"><span data-stu-id="c6a58-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="c6a58-139">Passaggio 3: Verificare che siano disponibili sufficienti memorie centrali delle macchine virtuali di Azure Resource Manager nell'area di Azure di cui fa parte la distribuzione corrente o la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a58-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="c6a58-140">Per questo passaggio è necessario passare alla modalità `arm` .</span><span class="sxs-lookup"><span data-stu-id="c6a58-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="c6a58-141">A tale scopo, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="c6a58-142">È possibile usare il comando dell'interfaccia della riga di comando seguente per controllare la quantità corrente di memorie centrali in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6a58-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="c6a58-143">Per altre informazioni sulle quote di memoria centrale, vedere [Limiti e Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="c6a58-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="c6a58-144">Dopo aver verificato questo passaggio, è possibile passare nuovamente alla modalità `asm` .</span><span class="sxs-lookup"><span data-stu-id="c6a58-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="c6a58-145">Passaggio 4: Opzione 1 - Eseguire la migrazione delle macchine virtuali a un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c6a58-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="c6a58-146">Ottenere l'elenco dei servizi cloud con il comando seguente e selezionare il servizio cloud di cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="c6a58-147">Si noti che se le VM nel servizio cloud si trovano in una rete virtuale o hanno ruoli Web/di lavoro, verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c6a58-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="c6a58-148">Eseguire il comando seguente per ottenere il nome della distribuzione per il servizio cloud dall'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="c6a58-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="c6a58-149">Nella maggior parte dei casi, il nome della distribuzione corrisponde al nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="c6a58-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="c6a58-150">Per prima cosa, verificare se è possibile eseguire la migrazione del servizio cloud usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6a58-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="c6a58-151">Preparare le macchine virtuali nel servizio cloud per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="c6a58-152">È possibile scegliere tra due opzioni.</span><span class="sxs-lookup"><span data-stu-id="c6a58-152">You have two options to choose from.</span></span>

<span data-ttu-id="c6a58-153">Se si vuole eseguire la migrazione delle VM a una rete virtuale creata dalla piattaforma, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="c6a58-154">Se si vuole eseguire la migrazione a una rete virtuale esistente nel modello di distribuzione Resource Manager, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="c6a58-155">Dopo aver completato l'operazione di preparazione, è possibile osservare l'output dettagliato per ottenere lo stato di migrazione delle VM, verificando che sia `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="c6a58-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="c6a58-156">Controllare la configurazione per le risorse preparate tramite l'interfaccia della riga di comando o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a58-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="c6a58-157">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="c6a58-158">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="c6a58-159">Passaggio 4: Opzione 2 - Eseguire la migrazione delle macchine virtuali a una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c6a58-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="c6a58-160">Selezionare la rete virtuale per cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="c6a58-161">Si noti che se la rete virtuale contiene ruoli Web/di lavoro o VM con configurazioni non supportate, verrà visualizzato un messaggio di errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="c6a58-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="c6a58-162">Ottenere tutte le reti virtuali nella sottoscrizione con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="c6a58-163">Verrà visualizzato un risultato simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c6a58-163">The output will look something like this:</span></span>

![Schermata della riga di comando con evidenziato l'intero nome della rete virtuale.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="c6a58-165">Nell'esempio precedente il valore **virtualNetworkName** è l'intero nome **"Gruppo classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="c6a58-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="c6a58-166">Per prima cosa, verificare se sia possibile eseguire la migrazione della rete virtuale usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c6a58-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="c6a58-167">Preparare la rete virtuale scelta per la migrazione con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="c6a58-168">Controllare la configurazione per le macchine virtuali preparate tramite l'interfaccia della riga di comando o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a58-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="c6a58-169">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="c6a58-170">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="c6a58-171">Passaggio 5: Eseguire la migrazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c6a58-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="c6a58-172">Dopo aver completato la migrazione delle macchine virtuali, si consiglia di migrare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c6a58-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="c6a58-173">Preparare l'account di archiviazione per la migrazione con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="c6a58-174">Controllare la configurazione per l'account di archiviazione preparato tramite l'interfaccia della riga di comando o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a58-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="c6a58-175">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="c6a58-176">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a58-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="c6a58-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6a58-177">Next steps</span></span>

* <span data-ttu-id="c6a58-178">[Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Panoramica sulla migrazione supportata dalla piattaforma per risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="c6a58-178">[Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* [<span data-ttu-id="c6a58-179">Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6a58-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="c6a58-180">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Pianificazione della migrazione delle risorse IaaS dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="c6a58-180">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* [<span data-ttu-id="c6a58-181">Usare PowerShell per eseguire la migrazione di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6a58-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="c6a58-182">[Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Strumenti della community per assistenza alla migrazione delle risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="c6a58-182">[Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="c6a58-183">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="c6a58-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c6a58-184">Esaminare le domande frequenti sulla migrazione delle risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6a58-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
