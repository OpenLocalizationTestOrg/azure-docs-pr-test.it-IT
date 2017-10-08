---
title: aaaMigrate tooResource gestione con PowerShell | Documenti Microsoft
description: Questo articolo descrive la migrazione hello supportata dalla piattaforma IaaS risorse quali macchine virtuali (VM), le reti virtuali (reti virtuali) e gli account di archiviazione da tooAzure classico Resource Manager (ARM) utilizzando i comandi di PowerShell di Azure
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
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="899f4-103">Eseguire la migrazione di risorse IaaS da tooAzure classico Gestione risorse tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="899f4-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="899f4-104">Queste procedure illustrano di funzionamento dei comandi toomigrate infrastruttura come un servizio (IaaS) alle risorse dal modello di distribuzione Azure Resource Manager hello distribuzione classica modello toohello toouse Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="899f4-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="899f4-105">Se si desidera, è anche possibile eseguire la migrazione alle risorse utilizzando hello [Azure interfaccia della riga di comando (CLI di Azure)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="899f4-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="899f4-106">Per informazioni generali sugli scenari di migrazione supportati, vedere [migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="899f4-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="899f4-107">Per istruzioni dettagliate e informazioni dettagliate sulla migrazione, vedere [tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="899f4-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="899f4-108">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="899f4-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="899f4-109">Ecco un ordine di hello tooidentify diagramma di flusso in cui è necessario passaggi toobe eseguite durante un processo di migrazione</span><span class="sxs-lookup"><span data-stu-id="899f4-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Schermata che illustra i passaggi della migrazione hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="899f4-111">Passaggio 1: Pianificare la migrazione</span><span class="sxs-lookup"><span data-stu-id="899f4-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="899f4-112">Ecco alcune procedure consigliate che è consigliabile quando si valutano la migrazione di risorse IaaS da tooResource classico Manager:</span><span class="sxs-lookup"><span data-stu-id="899f4-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="899f4-113">Leggere hello [supportate e non supportate funzionalità e configurazioni](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="899f4-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="899f4-114">Se si dispone di macchine virtuali che utilizzano le configurazioni non supportate o funzionalità, è consigliabile attendere hello e configurazione delle funzionalità supporto toobe annunciato.</span><span class="sxs-lookup"><span data-stu-id="899f4-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="899f4-115">In alternativa, se adatto alle proprie esigenze, rimuovere tale funzionalità o esce da tale migrazione tooenable della configurazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="899f4-116">Se si sono state automatizzate script da distribuire l'infrastruttura e le applicazioni oggi, provare a toocreate una configurazione di test simile utilizzando gli script per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="899f4-117">In alternativa, è possibile impostare gli ambienti di esempio di tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="899f4-118">Gateway applicazione non sono attualmente supportati per la migrazione da tooResource classico Manager.</span><span class="sxs-lookup"><span data-stu-id="899f4-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="899f4-119">toomigrate una rete virtuale classica con un gateway di applicazione, rimuovere gateway hello prima dell'esecuzione di una rete di hello toomove operazione Prepare.</span><span class="sxs-lookup"><span data-stu-id="899f4-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="899f4-120">Dopo aver completato la migrazione di hello, riconnettersi gateway hello in Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="899f4-121">Gateway ExpressRoute connessione tooExpressRoute circuiti in un'altra sottoscrizione non è possibile eseguire la migrazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="899f4-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="899f4-122">In questi casi, è possibile rimuovere gateway ExpressRoute hello, la migrazione della rete virtuale hello e ricreare il gateway di hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="899f4-123">Vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../../expressroute/expressroute-migration-classic-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="899f4-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="899f4-124">Passaggio 2: Installare una versione più recente di hello di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="899f4-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="899f4-125">Esistono due opzioni principali tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) o [installazione guidata piattaforma Web (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="899f4-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="899f4-126">WebPI riceve aggiornamenti mensili.</span><span class="sxs-lookup"><span data-stu-id="899f4-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="899f4-127">PowerShell Gallery riceve aggiornamenti su base continua.</span><span class="sxs-lookup"><span data-stu-id="899f4-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="899f4-128">Questo articolo si basa su Azure PowerShell versione 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="899f4-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="899f4-129">Per istruzioni sull'installazione, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="899f4-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="899f4-130">Passaggio 3: Assicurarsi che sia un amministratore per la sottoscrizione di hello nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="899f4-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="899f4-131">tooperform questa migrazione, è necessario essere aggiunto come coamministratore della sottoscrizione hello in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="899f4-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="899f4-132">Sign in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="899f4-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="899f4-133">Nel menu Hub hello, selezionare **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="899f4-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="899f4-134">Se questa voce non viene visualizzata, selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="899f4-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="899f4-135">Trovare la voce di hello sottoscrizione appropriata, quindi esaminare hello **ruolo MY** campo.</span><span class="sxs-lookup"><span data-stu-id="899f4-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="899f4-136">Per un coamministratore, deve essere il valore di hello _amministratore dell'Account_.</span><span class="sxs-lookup"><span data-stu-id="899f4-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="899f4-137">Se non si è in grado di tooadd un coamministratore, quindi contattare un amministratore del servizio o coamministratore per tooget sottoscrizione hello aggiunti manualmente.</span><span class="sxs-lookup"><span data-stu-id="899f4-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="899f4-138">Passaggio 4: impostare la sottoscrizione e iscriversi per la migrazione</span><span class="sxs-lookup"><span data-stu-id="899f4-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="899f4-139">Avviare prima un prompt di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="899f4-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="899f4-140">Per la migrazione, è necessario tooset dell'ambiente per entrambi classico e Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="899f4-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="899f4-141">Eseguire l'accesso tooyour account per il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="899f4-142">Ottenere le sottoscrizioni disponibili hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="899f4-143">Impostare la sottoscrizione di Azure per hello sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="899f4-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="899f4-144">In questo esempio imposta hello nome predefinito della sottoscrizione troppo**iscrizione Azure**.</span><span class="sxs-lookup"><span data-stu-id="899f4-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="899f4-145">Sostituire nome sottoscrizione di esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="899f4-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="899f4-146">La registrazione è un passaggio da eseguire una sola volta, ma è necessario provvedervi prima di tentare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="899f4-147">Senza registrazione, vedrai hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="899f4-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="899f4-148">*BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="899f4-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="899f4-149">Registrare con provider di risorse di migrazione hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="899f4-150">Attendere cinque minuti per hello toofinish di registrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="899f4-151">È possibile controllare lo stato di hello dell'approvazione hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="899f4-152">Assicurarsi che RegistrationState sia `Registered` prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="899f4-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="899f4-153">Accedi a questo punto tooyour account per il modello classico hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="899f4-154">Ottenere le sottoscrizioni disponibili hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="899f4-155">Impostare la sottoscrizione di Azure per hello sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="899f4-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="899f4-156">In questo esempio imposta sottoscrizione predefinita hello troppo**iscrizione Azure**.</span><span class="sxs-lookup"><span data-stu-id="899f4-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="899f4-157">Sostituire nome sottoscrizione di esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="899f4-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="899f4-158">Passaggio 5: Assicurarsi di disporre di core a sufficienza macchina virtuale di gestione risorse di Azure in hello area della distribuzione corrente o rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="899f4-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="899f4-159">È possibile utilizzare hello seguente PowerShell comando toocheck hello numero corrente di core che nel gestore di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="899f4-160">toolearn più sulle quote di core, vedere [limiti e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="899f4-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="899f4-161">Questo esempio viene verificata la disponibilità di hello in hello **Stati Uniti occidentali** area.</span><span class="sxs-lookup"><span data-stu-id="899f4-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="899f4-162">Sostituire nome dell'area esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="899f4-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="899f4-163">Passaggio 6: Eseguire i comandi toomigrate le risorse IaaS</span><span class="sxs-lookup"><span data-stu-id="899f4-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="899f4-164">Tutte le operazioni descritte di seguito hello sono idempotenti.</span><span class="sxs-lookup"><span data-stu-id="899f4-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="899f4-165">Se si dispone di un problema diverso da una funzionalità non supportata o un errore di configurazione, è consigliabile che si riprova hello preparare, interrompere o l'operazione di commit.</span><span class="sxs-lookup"><span data-stu-id="899f4-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="899f4-166">piattaforma Hello tenta quindi di nuovo l'azione hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="899f4-167">Passaggio 6.1: Opzione 1 - Eseguire la migrazione delle macchine virtuali in un servizio cloud (non in una rete virtuale)</span><span class="sxs-lookup"><span data-stu-id="899f4-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="899f4-168">Ottenere un elenco di servizi cloud tramite hello comando seguente, quindi selezione hello cloud servizio che si desidera toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="899f4-169">Se è hello macchine virtuali nel servizio cloud hello in una rete virtuale o se hanno ruoli web o di lavoro, il comando di hello restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="899f4-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="899f4-170">Ottenere il nome distribuzione hello per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="899f4-171">In questo esempio, è il nome di servizio hello **servizio**.</span><span class="sxs-lookup"><span data-stu-id="899f4-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="899f4-172">Sostituire nome del servizio di esempio hello con il proprio nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="899f4-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="899f4-173">Preparare le macchine virtuali hello nel servizio cloud hello per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="899f4-174">Si dispone di due opzioni toochoose da.</span><span class="sxs-lookup"><span data-stu-id="899f4-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="899f4-175">**Opzione 1. Eseguire la migrazione di hello macchine virtuali tooa piattaforma rete virtuale creata**</span><span class="sxs-lookup"><span data-stu-id="899f4-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="899f4-176">In primo luogo, verificare se è possibile eseguire la migrazione del servizio cloud hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="899f4-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="899f4-177">Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="899f4-178">Se la convalida ha esito positivo, è possibile spostare toohello **Prepare** passaggio:</span><span class="sxs-lookup"><span data-stu-id="899f4-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="899f4-179">**Opzione 2. Eseguire la migrazione tooan rete virtuale esistente nel modello di distribuzione di gestione risorse di hello**</span><span class="sxs-lookup"><span data-stu-id="899f4-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="899f4-180">In questo esempio imposta hello Nome gruppo di risorse troppo**myResourceGroup**, hello nome di rete virtuale troppo**myVirtualNetwork** e hello nome di subnet troppo**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="899f4-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="899f4-181">Sostituire i nomi di hello nell'esempio hello con nomi hello delle proprie risorse.</span><span class="sxs-lookup"><span data-stu-id="899f4-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="899f4-182">In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale di hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="899f4-183">Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="899f4-184">Se la convalida ha esito positivo, è possibile procedere con hello riportata dopo il passaggio di preparazione:</span><span class="sxs-lookup"><span data-stu-id="899f4-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="899f4-185">Dopo l'operazione di preparazione hello ha esito positivo con uno dei precedenti opzioni hello, eseguire una query dello stato di migrazione hello di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="899f4-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="899f4-186">Verificare che siano in hello `Prepared` stato.</span><span class="sxs-lookup"><span data-stu-id="899f4-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="899f4-187">In questo esempio imposta hello nome della macchina virtuale troppo**myVM**.</span><span class="sxs-lookup"><span data-stu-id="899f4-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="899f4-188">Sostituire il nome di esempio hello con il proprio nome di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="899f4-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="899f4-189">Controllare la configurazione di hello hello preparata risorse con PowerShell o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="899f4-190">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="899f4-191">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="899f4-192">Passaggio 6.1: Opzione 2 - Eseguire la migrazione delle macchine virtuali in un una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="899f4-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="899f4-193">macchine virtuali toomigrate in una rete virtuale, la migrazione della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="899f4-194">macchine virtuali Hello eseguire automaticamente la migrazione con la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="899f4-195">Selezione hello rete virtuale che si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="899f4-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="899f4-196">[Eseguire la migrazione di una macchina virtuale classica](migrate-single-classic-to-resource-manager.md) creando una nuova macchina virtuale di gestione delle risorse con i dischi gestiti utilizzando hello (sistema operativo e dati) i file VHD della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="899f4-197">nome della rete virtuale Hello potrebbe essere diverso rispetto a quanto mostrato in hello nuovo portale.</span><span class="sxs-lookup"><span data-stu-id="899f4-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="899f4-198">nuovo portale di Azure Hello Visualizza nome hello come `[vnet-name]` ma il nome di rete virtuale effettivo hello è di tipo `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="899f4-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="899f4-199">Prima della migrazione, nome di rete virtuale effettivo hello di ricerca usando il comando di hello `Get-AzureVnetSite | Select -Property Name` oppure visualizzarlo in hello vecchio portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="899f4-200">In questo esempio imposta hello nome di rete virtuale troppo**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="899f4-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="899f4-201">Sostituire nome di rete virtuale di esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="899f4-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="899f4-202">Se la rete virtuale hello contiene web o ruoli di lavoro o macchine virtuali con configurazioni non supportate, viene visualizzato un messaggio di errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="899f4-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="899f4-203">In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="899f4-204">Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="899f4-205">Se la convalida ha esito positivo, è possibile procedere con hello riportata dopo il passaggio di preparazione:</span><span class="sxs-lookup"><span data-stu-id="899f4-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="899f4-206">Controllare la configurazione di hello hello preparata macchine virtuali con Azure PowerShell o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="899f4-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="899f4-207">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="899f4-208">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="899f4-209">Passaggio 6.2: Eseguire la migrazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="899f4-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="899f4-210">Dopo avere utilizzato la migrazione di macchine virtuali hello, si consiglia di che migrare gli account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="899f4-211">Prima di eseguire la migrazione di account di archiviazione hello, eseguire prima i controlli dei prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="899f4-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="899f4-212">**Eseguire la migrazione di macchine virtuali classiche cui dischi vengono archiviati nell'account di archiviazione hello**</span><span class="sxs-lookup"><span data-stu-id="899f4-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="899f4-213">Comando precedente restituisce RoleName e DiskName proprietà di tutti i dischi di macchina virtuale classici hello nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="899f4-214">RoleName è il nome di hello di hello toowhich di macchina virtuale che è collegato un disco.</span><span class="sxs-lookup"><span data-stu-id="899f4-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="899f4-215">Se il comando precedente restituisce dischi Assicurarsi quindi che toowhich di macchine virtuali sono collegati i dischi vengono migrati prima della migrazione hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="899f4-216">**Eliminare classico scollegati dischi di macchina virtuale archiviati nell'account di archiviazione hello**</span><span class="sxs-lookup"><span data-stu-id="899f4-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="899f4-217">Trovare i dischi di macchina virtuale classici nell'archiviazione hello account tramiti il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="899f4-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="899f4-218">Se il comando sopra restituisce uno o più dischi, eliminare tali dischi tramite il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="899f4-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="899f4-219">**Immagini di macchina virtuale di eliminazione archiviate nell'account di archiviazione hello**</span><span class="sxs-lookup"><span data-stu-id="899f4-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="899f4-220">Comando precedente restituisce tutte le immagini di macchina virtuale hello con disco del sistema operativo archiviato nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="899f4-221">Comando precedente restituisce tutte le immagini di macchina virtuale hello con dischi di dati archiviati nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="899f4-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="899f4-222">Eliminare tutte le immagini VM hello restituite da sopra i comandi usando il comando precedente:</span><span class="sxs-lookup"><span data-stu-id="899f4-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="899f4-223">Convalidare ogni account di archiviazione per la migrazione utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="899f4-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="899f4-224">In questo esempio, nome account di archiviazione hello è **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="899f4-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="899f4-225">Sostituire il nome di esempio hello con nome hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="899f4-226">Passaggio successivo è l'account di archiviazione hello tooPrepare per la migrazione</span><span class="sxs-lookup"><span data-stu-id="899f4-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="899f4-227">Controllare la configurazione di hello hello preparata con Azure PowerShell o hello Azure portale account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="899f4-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="899f4-228">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="899f4-229">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="899f4-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="899f4-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="899f4-230">Next steps</span></span>
* [<span data-ttu-id="899f4-231">Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di</span><span class="sxs-lookup"><span data-stu-id="899f4-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-232">Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="899f4-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-233">Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="899f4-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-234">Utilizzare le risorse IaaS toomigrate CLI da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="899f4-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-235">Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="899f4-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-236">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="899f4-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="899f4-237">Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="899f4-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
