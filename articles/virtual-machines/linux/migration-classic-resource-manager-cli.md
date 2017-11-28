---
title: macchine virtuali di aaaMigrate tooResource Manager utilizzando l'interfaccia CLI di Azure | Documenti Microsoft
description: Questo articolo descrive migrazione supportata dalla piattaforma hello delle risorse da Gestione risorse di tooAzure classico mediante Azure CLI
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
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="bee66-103">Eseguire la migrazione di risorse IaaS da tooAzure classico Resource Manager tramite l'interfaccia CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="bee66-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="bee66-104">Queste procedure illustrano di funzionamento dei comandi toomigrate infrastruttura come un servizio (IaaS) alle risorse dal modello di distribuzione Azure Resource Manager hello distribuzione classica modello toohello toouse Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="bee66-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="bee66-105">articolo Hello richiede hello [CLI di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bee66-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bee66-106">Tutte le operazioni descritte di seguito hello sono idempotenti.</span><span class="sxs-lookup"><span data-stu-id="bee66-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="bee66-107">Se si dispone di un problema diverso da una funzionalità non supportata o un errore di configurazione, è consigliabile che si riprova hello preparare, interrompere o l'operazione di commit.</span><span class="sxs-lookup"><span data-stu-id="bee66-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="bee66-108">piattaforma Hello quindi tenterà nuovamente l'azione hello.</span><span class="sxs-lookup"><span data-stu-id="bee66-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="bee66-109">Ecco un ordine di hello tooidentify diagramma di flusso in cui è necessario passaggi toobe eseguite durante un processo di migrazione</span><span class="sxs-lookup"><span data-stu-id="bee66-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Schermata che illustra i passaggi della migrazione hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="bee66-111">Passaggio 1: Preparare la migrazione</span><span class="sxs-lookup"><span data-stu-id="bee66-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="bee66-112">Ecco alcune procedure consigliate che è consigliabile quando si valutano la migrazione di risorse IaaS da tooResource classico Manager:</span><span class="sxs-lookup"><span data-stu-id="bee66-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="bee66-113">Leggere hello [elenco di configurazioni non supportate o funzionalità](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bee66-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="bee66-114">Se si dispone di macchine virtuali che utilizzano le configurazioni non supportate o funzionalità, è consigliabile attendere hello configurazione delle funzionalità supporto toobe annunciato.</span><span class="sxs-lookup"><span data-stu-id="bee66-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="bee66-115">In alternativa, è possibile rimuovere tale funzionalità o esce da tale migrazione tooenable configurazione se adatto alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="bee66-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="bee66-116">Se si sono state automatizzate script da distribuire l'infrastruttura e le applicazioni oggi, provare a toocreate una configurazione di test simile utilizzando gli script per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="bee66-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="bee66-117">In alternativa, è possibile impostare gli ambienti di esempio di tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bee66-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bee66-118">Gateway applicazione non sono attualmente supportati per la migrazione da tooResource classico Manager.</span><span class="sxs-lookup"><span data-stu-id="bee66-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="bee66-119">toomigrate una rete virtuale classica con un gateway di applicazione, rimuovere gateway hello prima dell'esecuzione di una rete di hello toomove operazione Prepare.</span><span class="sxs-lookup"><span data-stu-id="bee66-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="bee66-120">Dopo aver completato la migrazione di hello, riconnettersi gateway hello in Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bee66-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="bee66-121">Gateway ExpressRoute connessione tooExpressRoute circuiti in un'altra sottoscrizione non è possibile eseguire la migrazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bee66-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="bee66-122">In questi casi, è possibile rimuovere gateway ExpressRoute hello, la migrazione della rete virtuale hello e ricreare il gateway di hello.</span><span class="sxs-lookup"><span data-stu-id="bee66-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="bee66-123">Vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../../expressroute/expressroute-migration-classic-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="bee66-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="bee66-124">Passaggio 2: Impostare la sottoscrizione e registrare il provider di hello</span><span class="sxs-lookup"><span data-stu-id="bee66-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="bee66-125">Per gli scenari di migrazione, è necessario tooset dell'ambiente per entrambi classico e Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="bee66-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="bee66-126">[Installare l'interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) e [selezionare la sottoscrizione](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="bee66-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="bee66-127">Account di accesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="bee66-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="bee66-128">Selezionare hello sottoscrizione di Azure utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="bee66-129">La registrazione è una volta in passaggio ma è necessario toobe eseguita una volta prima di procedere alla migrazione.</span><span class="sxs-lookup"><span data-stu-id="bee66-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="bee66-130">Verrà visualizzato hello seguente messaggio di errore senza registrazione</span><span class="sxs-lookup"><span data-stu-id="bee66-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="bee66-131">*BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione)</span><span class="sxs-lookup"><span data-stu-id="bee66-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="bee66-132">Registrare con provider di risorse di migrazione hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="bee66-133">Si noti che in alcuni casi si verifica il timeout del comando. Tuttavia, la registrazione di hello sarà ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="bee66-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="bee66-134">Attendere cinque minuti per hello toofinish di registrazione.</span><span class="sxs-lookup"><span data-stu-id="bee66-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="bee66-135">È possibile controllare stato hello dell'approvazione hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="bee66-136">Assicurarsi che RegistrationState sia `Registered` prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="bee66-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="bee66-137">Passare ora toohello CLI `asm` modalità.</span><span class="sxs-lookup"><span data-stu-id="bee66-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="bee66-138">Passaggio 3: Assicurarsi di disporre di core a sufficienza macchina virtuale di gestione risorse di Azure in hello area della distribuzione corrente o rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="bee66-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="bee66-139">Per questo passaggio è necessario tooswitch troppo`arm` modalità.</span><span class="sxs-lookup"><span data-stu-id="bee66-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="bee66-140">Eseguire questa operazione con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="bee66-141">È possibile utilizzare hello seguente CLI comando toocheck hello quantità corrente di core che nel gestore di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bee66-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="bee66-142">toolearn più sulle quote di core, vedere [limiti e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="bee66-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="bee66-143">Dopo aver verificato questo passaggio, è possibile passare nuovamente troppo`asm` modalità.</span><span class="sxs-lookup"><span data-stu-id="bee66-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="bee66-144">Passaggio 4: Opzione 1 - Eseguire la migrazione delle macchine virtuali a un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="bee66-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="bee66-145">Ottenere un elenco di servizi cloud tramite hello comando seguente, quindi selezione hello cloud servizio che si desidera toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="bee66-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="bee66-146">Si noti che se hello macchine virtuali nel servizio cloud hello si trovano in una rete virtuale o se hanno ruoli web/di lavoro, si otterrà un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="bee66-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="bee66-147">Eseguire hello dopo il nome di comando tooget hello distribuzione per il servizio cloud hello dall'output di hello dettagliato.</span><span class="sxs-lookup"><span data-stu-id="bee66-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="bee66-148">Nella maggior parte dei casi, il nome di distribuzione hello è hello uguale al nome del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bee66-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="bee66-149">In primo luogo, verificare se è possibile eseguire la migrazione del servizio cloud hello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="bee66-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="bee66-150">Preparare le macchine virtuali hello nel servizio cloud hello per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="bee66-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="bee66-151">Si dispone di due opzioni toochoose da.</span><span class="sxs-lookup"><span data-stu-id="bee66-151">You have two options toochoose from.</span></span>

<span data-ttu-id="bee66-152">Se si desidera toomigrate hello macchine virtuali tooa piattaforma rete virtuale creata, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="bee66-153">Se si desidera tooan toomigrate rete virtuale nel modello di distribuzione di gestione risorse di hello esistente, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="bee66-154">Dopo la preparazione hello operazione ha esito positivo, è possibile esaminare hello output dettagliato tooget hello lo stato di migrazione di macchine virtuali hello e verificare che siano in hello `Prepared` stato.</span><span class="sxs-lookup"><span data-stu-id="bee66-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="bee66-155">Controllare la configurazione di hello hello preparata risorse con CLI o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bee66-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="bee66-156">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="bee66-157">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="bee66-158">Passaggio 4: Opzione 2 - Eseguire la migrazione delle macchine virtuali a una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="bee66-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="bee66-159">Selezione hello rete virtuale che si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bee66-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="bee66-160">Si noti che se la rete virtuale hello contiene ruoli web/di lavoro o macchine virtuali con configurazioni non supportate, si riceverà un messaggio di errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="bee66-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="bee66-161">Ottenere tutte le reti virtuali hello nella sottoscrizione hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="bee66-162">output di Hello sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bee66-162">hello output will look something like this:</span></span>

![Schermata della riga di comando hello con il nome di rete virtuale intera hello evidenziato.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="bee66-164">In hello sopra riportato, hello **virtualNetworkName** è l'intero nome hello **"Gruppo classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="bee66-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="bee66-165">In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale di hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bee66-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="bee66-166">Preparare rete virtuale di hello di propria scelta per la migrazione utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="bee66-167">Controllare la configurazione di hello hello preparata macchine virtuali con CLI o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bee66-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="bee66-168">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="bee66-169">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="bee66-170">Passaggio 5: Eseguire la migrazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="bee66-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="bee66-171">Dopo avere utilizzato la migrazione di macchine virtuali hello, è consigliabile che si esegue la migrazione di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="bee66-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="bee66-172">Preparare account di archiviazione hello per la migrazione tramite hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="bee66-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="bee66-173">Controllare la configurazione di hello hello preparata con CLI o hello Azure portale account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bee66-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="bee66-174">Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="bee66-175">Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="bee66-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="bee66-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bee66-176">Next steps</span></span>

* [<span data-ttu-id="bee66-177">Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di</span><span class="sxs-lookup"><span data-stu-id="bee66-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bee66-178">Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="bee66-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bee66-179">Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="bee66-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bee66-180">Utilizzare le risorse IaaS toomigrate PowerShell da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="bee66-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="bee66-181">Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="bee66-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="bee66-182">Rivedere gli errori di migrazione più comuni</span><span class="sxs-lookup"><span data-stu-id="bee66-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bee66-183">Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico</span><span class="sxs-lookup"><span data-stu-id="bee66-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
