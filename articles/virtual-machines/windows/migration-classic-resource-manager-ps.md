---
title: Eseguire la migrazione a Resource Manager con PowerShell | Microsoft Docs
description: Questo articolo illustra la migrazione di risorse IaaS supportata dalla piattaforma come macchine virtuali (VM), reti virtuali (VNET) e account di archiviazione dal modello di distribuzione classica ad Azure Resource Manager (ARM) tramite comandi di Azure PowerShell
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="65442-103">Eseguire la migrazione di risorse IaaS dal modello classico al modello di Azure Resource Manager tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65442-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="65442-104">Questi passaggi mostrano come usare i comandi di Azure PowerShell per eseguire la migrazione di risorse IaaS (infrastruttura distribuita come servizio) dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="65442-105">È anche possibile eseguire la migrazione delle risorse usando l' [interfaccia della riga di comando di Azure](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="65442-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="65442-106">Per informazioni di base su scenari di migrazione supportati, vedere [Migrazione di risorse IaaS supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65442-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="65442-107">Per una guida approfondita e la procedura dettagliata di migrazione, vedere [Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="65442-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="65442-108">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="65442-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="65442-109">Ecco un diagramma di flusso per identificare l'ordine di esecuzione dei passaggi durante un processo di migrazione</span><span class="sxs-lookup"><span data-stu-id="65442-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="65442-111">Passaggio 1: Pianificare la migrazione</span><span class="sxs-lookup"><span data-stu-id="65442-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="65442-112">Ecco alcune procedure consigliate per valutare la migrazione delle risorse IaaS dal modello classico al modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="65442-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="65442-113">Leggere con attenzione le [funzionalità e configurazioni supportate e non supportate](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65442-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="65442-114">Se sono disponibili macchine virtuali che usano configurazioni o funzionalità non supportate, è consigliabile attendere l'annuncio del supporto di tali configurazioni o funzionalità.</span><span class="sxs-lookup"><span data-stu-id="65442-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="65442-115">In alternativa, in base alle esigenze è possibile rimuovere tale funzionalità o uscire da tale configurazione per abilitare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="65442-116">Se si hanno script automatizzati che consentono di distribuire subito l'infrastruttura e le applicazioni, provare a creare una configurazione di test simile usando questi script per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="65442-117">In alternativa, è anche possibile configurare ambienti di esempio tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65442-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65442-118">I gateway applicazione non sono attualmente supportati per la migrazione dal modello di distribuzione classica a Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="65442-119">Per eseguire la migrazione di una rete virtuale classica con un gateway applicazione, rimuovere il gateway prima di eseguire un'operazione di preparazione dello spostamento della rete.</span><span class="sxs-lookup"><span data-stu-id="65442-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="65442-120">Dopo aver completato la migrazione, riconnettere il gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="65442-121">Non è possibile eseguire la migrazione automatica di gateway ExpressRoute che si connettono a circuiti ExpressRoute in un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="65442-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="65442-122">In tal caso, rimuovere il gateway ExpressRoute, eseguire la migrazione della rete virtuale e ricreare il gateway.</span><span class="sxs-lookup"><span data-stu-id="65442-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="65442-123">Per altre informazioni, vedere [Eseguire la migrazione di circuiti ExpressRoute e delle reti virtuali associate dalla distribuzione classica al modello di distribuzione Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="65442-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="65442-124">Passaggio 2: Installare la versione più recente di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65442-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="65442-125">Per l'installazione di Azure PowerShell sono previste due opzioni principali: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) e [Installazione guidata piattaforma Web (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="65442-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="65442-126">WebPI riceve aggiornamenti mensili.</span><span class="sxs-lookup"><span data-stu-id="65442-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="65442-127">PowerShell Gallery riceve aggiornamenti su base continua.</span><span class="sxs-lookup"><span data-stu-id="65442-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="65442-128">Questo articolo si basa su Azure PowerShell versione 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="65442-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="65442-129">Per le istruzioni di installazione, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65442-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="65442-130">Passaggio 3: Assicurarsi di essere un amministratore della sottoscrizione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="65442-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="65442-131">Per eseguire la migrazione, è necessario essere aggiunti come coamministratori della sottoscrizione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65442-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="65442-132">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65442-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="65442-133">Nel menu Hub, selezionare **Sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="65442-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="65442-134">Se questa voce non viene visualizzata, selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="65442-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="65442-135">Cercare la voce di sottoscrizione appropriata, quindi esaminare il campo **Ruolo personale**.</span><span class="sxs-lookup"><span data-stu-id="65442-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="65442-136">Per un coamministratore, il valore deve essere _amministratore account_.</span><span class="sxs-lookup"><span data-stu-id="65442-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="65442-137">Se non è possibile aggiungere un coamministratore, contattare un amministratore o un coamministratore del servizio per essere aggiunti alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="65442-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="65442-138">Passaggio 4: impostare la sottoscrizione e iscriversi per la migrazione</span><span class="sxs-lookup"><span data-stu-id="65442-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="65442-139">Avviare prima un prompt di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65442-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="65442-140">Per la migrazione è necessario configurare l'ambiente per il modello classico e di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="65442-141">Accedere con l'account per il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="65442-142">È possibile ottenere le sottoscrizioni disponibili usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="65442-143">Impostare la sottoscrizione di Azure per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="65442-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="65442-144">In questo esempio viene impostato il nome **My Azure Subscription** per la sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="65442-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="65442-145">Sostituire il nome della sottoscrizione di esempio con il nome della propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="65442-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="65442-146">La registrazione è un passaggio da eseguire una sola volta, ma è necessario provvedervi prima di tentare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="65442-147">Senza la registrazione, verrà visualizzato il seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="65442-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="65442-148">*BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="65442-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="65442-149">Registrarsi con il provider di risorse di migrazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="65442-150">Attendere cinque minuti che la registrazione venga completata.</span><span class="sxs-lookup"><span data-stu-id="65442-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="65442-151">È possibile controllare lo stato dell'approvazione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="65442-152">Assicurarsi che RegistrationState sia `Registered` prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="65442-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="65442-153">Accedere ora con l'account per il modello classico.</span><span class="sxs-lookup"><span data-stu-id="65442-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="65442-154">È possibile ottenere le sottoscrizioni disponibili usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="65442-155">Impostare la sottoscrizione di Azure per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="65442-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="65442-156">In questo esempio viene impostato **My Azure Subscription** come sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="65442-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="65442-157">Sostituire il nome della sottoscrizione di esempio con il nome della propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="65442-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="65442-158">Passaggio 5: verificare che siano disponibili sufficienti memorie centrali delle macchine virtuali di Azure Resource Manager nell'area di Azure di cui fa parte la distribuzione corrente o la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="65442-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="65442-159">È possibile usare il comando PowerShell seguente per controllare il numero corrente di memorie centrali in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65442-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="65442-160">Per altre informazioni sulle quote di memoria centrale, vedere [Limiti e Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="65442-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="65442-161">In questo esempio viene verificata la disponibilità nell'area **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="65442-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="65442-162">Sostituire il nome dell'area di esempio con il nome della propria area.</span><span class="sxs-lookup"><span data-stu-id="65442-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="65442-163">Passaggio 6: eseguire i comandi per la migrazione delle risorse IaaS</span><span class="sxs-lookup"><span data-stu-id="65442-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="65442-164">Tutte le operazioni descritte di seguito sono idempotenti.</span><span class="sxs-lookup"><span data-stu-id="65442-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="65442-165">Se vengono rilevati errori diversi da una funzionalità non supportata o un errore di configurazione, è consigliabile provare a ripetere l'operazione di preparazione, interruzione o commit.</span><span class="sxs-lookup"><span data-stu-id="65442-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="65442-166">La piattaforma tenterà di ripetere l'azione.</span><span class="sxs-lookup"><span data-stu-id="65442-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="65442-167">Passaggio 6.1: Opzione 1 - Eseguire la migrazione delle macchine virtuali in un servizio cloud (non in una rete virtuale)</span><span class="sxs-lookup"><span data-stu-id="65442-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="65442-168">Ottenere l'elenco dei servizi cloud con il comando seguente e selezionare il servizio cloud di cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="65442-169">Se le VM nel servizio cloud si trovano in una rete virtuale o hanno ruoli Web o di lavoro, il comando restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="65442-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="65442-170">Ottenere il nome della distribuzione per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="65442-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="65442-171">In questo esempio il nome del servizio è **My Service**.</span><span class="sxs-lookup"><span data-stu-id="65442-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="65442-172">Sostituire il nome del servizio di esempio con il nome del proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="65442-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="65442-173">Preparare le macchine virtuali nel servizio cloud per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="65442-174">È possibile scegliere tra due opzioni.</span><span class="sxs-lookup"><span data-stu-id="65442-174">You have two options to choose from.</span></span>

* <span data-ttu-id="65442-175">**Opzione 1. Eseguire la migrazione delle VM a una rete virtuale creata dalla piattaforma**</span><span class="sxs-lookup"><span data-stu-id="65442-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="65442-176">Per prima cosa, verificare se è possibile eseguire la migrazione del servizio cloud usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="65442-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="65442-177">Il comando precedente visualizza eventuali avvisi ed errori che bloccano la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="65442-178">Se la convalida ha esito positivo, è possibile passare alla fase di **preparazione**:</span><span class="sxs-lookup"><span data-stu-id="65442-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="65442-179">**Opzione 2. Eseguire la migrazione a una rete virtuale esistente nel modello di distribuzione Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="65442-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="65442-180">In questo esempio vengono impostati il nome **myResourceGroup** per il gruppo di risorse, il nome **myVirtualNetwork** per la rete virtuale e il nome **mySubNet** per la subnet.</span><span class="sxs-lookup"><span data-stu-id="65442-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="65442-181">Sostituire i nomi dell'esempio con i nomi delle proprie risorse.</span><span class="sxs-lookup"><span data-stu-id="65442-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="65442-182">Per prima cosa, verificare se sia possibile eseguire la migrazione della rete virtuale usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="65442-183">Il comando precedente visualizza eventuali avvisi ed errori che bloccano la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="65442-184">Se la convalida ha esito positivo, è possibile procedere con il seguente passaggio di preparazione:</span><span class="sxs-lookup"><span data-stu-id="65442-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="65442-185">Dopo aver completato la procedura di preparazione tramite una delle opzioni precedenti, eseguire una query dello stato di migrazione delle VM,</span><span class="sxs-lookup"><span data-stu-id="65442-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="65442-186">verificando che sia `Prepared`.</span><span class="sxs-lookup"><span data-stu-id="65442-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="65442-187">In questo esempio viene impostato il nome **myVM** per la VM.</span><span class="sxs-lookup"><span data-stu-id="65442-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="65442-188">Sostituire il nome di esempio con il nome della propria VM.</span><span class="sxs-lookup"><span data-stu-id="65442-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="65442-189">Controllare la configurazione per le risorse preparate tramite PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65442-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="65442-190">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="65442-191">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="65442-192">Passaggio 6.1: Opzione 2 - Eseguire la migrazione delle macchine virtuali in un una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="65442-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="65442-193">Per eseguire la migrazione delle macchine virtuali in una rete virtuale, migrare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="65442-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="65442-194">Le macchine virtuali migreranno automaticamente con la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="65442-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="65442-195">Selezionare la rete virtuale per cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="65442-196">[Eseguire la migrazione della singola macchina virtuale classica](migrate-single-classic-to-resource-manager.md) creando una nuova macchina virtuale di Resource Manager con dischi gestiti usando i file VHD (sistema operativo e dati) della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="65442-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="65442-197">Il nome della rete virtuale potrebbe essere diverso da quello mostrato nel nuovo portale.</span><span class="sxs-lookup"><span data-stu-id="65442-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="65442-198">Il nuovo portale di Azure visualizza il nome come `[vnet-name]` ma il nome effettivo della rete virtuale è di tipo `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="65442-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="65442-199">Prima della migrazione, controllare il nome effettivo della rete virtuale usando il comando `Get-AzureVnetSite | Select -Property Name` o visualizzarlo nel portale di Azure precedente.</span><span class="sxs-lookup"><span data-stu-id="65442-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="65442-200">In questo esempio viene impostato il nome **myVnet** per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="65442-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="65442-201">Sostituire il nome della rete virtuale di esempio con il nome della propria rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="65442-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="65442-202">Se la rete virtuale contiene ruoli Web o di lavoro, o VM con configurazioni non supportate, viene visualizzato un messaggio di errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="65442-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="65442-203">Per prima cosa, verificare se sia possibile eseguire la migrazione della rete virtuale usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="65442-204">Il comando precedente visualizza eventuali avvisi ed errori che bloccano la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="65442-205">Se la convalida ha esito positivo, è possibile procedere con il seguente passaggio di preparazione:</span><span class="sxs-lookup"><span data-stu-id="65442-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="65442-206">Controllare la configurazione per le macchine virtuali preparate usando Azure PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65442-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="65442-207">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="65442-208">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="65442-209">Passaggio 6.2: Eseguire la migrazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="65442-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="65442-210">Dopo aver completato la migrazione delle macchine virtuali, si consiglia di migrare gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="65442-211">Prima di eseguire la migrazione dell'account di archiviazione, eseguire i controlli dei prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="65442-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="65442-212">**Eseguire la migrazione di macchine virtuali classiche con dischi archiviati nell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="65442-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="65442-213">Il comando precedente restituisce le proprietà RoleName e DiskName di tutti i dischi delle VM classiche nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="65442-214">RoleName è il nome della macchina virtuale a cui il disco è collegato.</span><span class="sxs-lookup"><span data-stu-id="65442-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="65442-215">Se il comando precedente restituisce uno o più dischi, assicurarsi che le macchine virtuali a cui sono collegati tali dischi siano migrate prima della migrazione degli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="65442-216">**Eliminare i dischi di VM classiche archiviati nell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="65442-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="65442-217">Trovare i dischi di VM classiche nello spazio di archiviazione account tramiti il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="65442-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="65442-218">Se il comando sopra restituisce uno o più dischi, eliminare tali dischi tramite il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="65442-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="65442-219">**Eliminare immagini di VM archiviate nell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="65442-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="65442-220">Il comando precedente restituisce tutte le immagini di VM con il disco del sistema operativo archiviato nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="65442-221">Il comando precedente restituisce tutte le immagini di VM con il disco dei dati archiviato nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="65442-222">Eliminare tutte le immagini di VM restituite dal comando precedente tramite il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="65442-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="65442-223">Convalidare ogni account di archiviazione per la migrazione con il comando che segue.</span><span class="sxs-lookup"><span data-stu-id="65442-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="65442-224">In questo esempio il nome dell'account di archiviazione è **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="65442-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="65442-225">Sostituire il nome di esempio con il nome del proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="65442-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="65442-226">Il passaggio successivo consiste nella preparazione dell'account di archiviazione per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="65442-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="65442-227">Controllare la configurazione per l'account di archiviazione preparato tramite Azure PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65442-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="65442-228">Se non si è pronti per la migrazione e si vuole tornare allo stato precedente, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="65442-229">Se la configurazione preparata appare corretta, è possibile procedere ed eseguire il commit delle risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65442-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="65442-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65442-230">Next steps</span></span>
* <span data-ttu-id="65442-231">[Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Panoramica sulla migrazione supportata dalla piattaforma per risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="65442-231">[Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="65442-232">Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65442-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="65442-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Pianificazione della migrazione delle risorse IaaS dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="65442-233">[Planning for migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="65442-234">Usare l'interfaccia della riga di comando per eseguire la migrazione di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65442-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="65442-235">[Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Strumenti della community per assistenza alla migrazione delle risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="65442-235">[Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
* [<span data-ttu-id="65442-236">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="65442-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="65442-237">Esaminare le domande frequenti sulla migrazione delle risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65442-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
