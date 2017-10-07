---
title: le macchine virtuali Hyper-V con PowerShell e Azure Resource Manager aaaReplicate | Documenti Microsoft
description: Automatizzare la replica di macchine virtuali Hyper-V tooAzure hello con Azure Site Recovery tramite PowerShell e Gestione risorse di Azure.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="f147a-103">Eseguire la replica tra macchine virtuali Hyper-V locali e Azure con PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f147a-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f147a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f147a-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="f147a-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="f147a-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="f147a-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="f147a-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="f147a-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f147a-107">Overview</span></span>
<span data-ttu-id="f147a-108">Azure Site Recovery contribuisce tooyour business emergenza e continuità strategia di ripristino gestendo la replica, il failover e ripristino delle macchine virtuali in un numero di scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f147a-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="f147a-109">Per un elenco completo degli scenari di distribuzione, vedere hello [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f147a-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="f147a-110">Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f147a-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="f147a-111">Può funzionare con due tipi di moduli: hello modulo di Azureprofile, o un modulo di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="f147a-112">I cmdlet di PowerShell per Site Recovery disponibili con Azure PowerShell per Azure Resource Manager consentono di proteggere e ripristinare i server in Azure.</span><span class="sxs-lookup"><span data-stu-id="f147a-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="f147a-113">Questo articolo viene descritto come Windows PowerShell, con Gestione risorse di Azure, toodeploy Site Recovery tooconfigure toouse e orchestrano tooAzure di protezione di server.</span><span class="sxs-lookup"><span data-stu-id="f147a-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="f147a-114">esempio Hello utilizzato in questo articolo mostra come eseguire il failover, tooprotect e ripristinare le macchine virtuali in tooAzure un host Hyper-V, tramite Azure PowerShell con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f147a-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f147a-115">Hello cmdlet PowerShell di ripristino del sito attualmente consentono di hello tooconfigure seguenti: un tooanother del sito di Virtual Machine Manager, un tooAzure sito Virtual Machine Manager e un tooAzure sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f147a-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="f147a-116">Non occorre toobe un toouse esperti di PowerShell in questo articolo, ma è necessario toounderstand hello concetti, ad esempio le sessioni, cmdlet e i moduli.</span><span class="sxs-lookup"><span data-stu-id="f147a-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="f147a-117">Per altre informazioni su Windows PowerShell, vedere [Introduzione a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="f147a-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="f147a-118">Altrei informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f147a-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f147a-119">I partner Microsoft che fanno parte del programma di Provider di soluzioni Cloud (CSP) hello è possono configurare e gestire la protezione dei server dei clienti rispettivi CSP sottoscrizioni (tenant) tootheir clienti.</span><span class="sxs-lookup"><span data-stu-id="f147a-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="f147a-120">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f147a-120">Before you start</span></span>
<span data-ttu-id="f147a-121">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f147a-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="f147a-122">Account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="f147a-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="f147a-123">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f147a-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f147a-124">Inoltre, è possibile leggere le informazioni sui [prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="f147a-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="f147a-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="f147a-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="f147a-126">Per informazioni su questa versione e come tooinstall, vedere [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="f147a-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="f147a-127">Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) moduli.</span><span class="sxs-lookup"><span data-stu-id="f147a-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="f147a-128">È possibile ottenere versioni più recenti di hello di questi moduli da hello [PowerShell gallery](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="f147a-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="f147a-129">Questo articolo illustra come toouse Azure Powershell con Gestione risorse di Azure tooconfigure e gestire la protezione dei server.</span><span class="sxs-lookup"><span data-stu-id="f147a-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="f147a-130">esempio Hello utilizzato in questo articolo illustra come una macchina virtuale, in esecuzione in un host Hyper-V, tooAzure tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f147a-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="f147a-131">Hello seguenti prerequisiti è toothis specifico esempio.</span><span class="sxs-lookup"><span data-stu-id="f147a-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="f147a-132">Per un set più completo di requisiti per hello vari scenari di ripristino del sito, consultare la documentazione del toohello riguardano toothat scenario.</span><span class="sxs-lookup"><span data-stu-id="f147a-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="f147a-133">Host Hyper-V che esegue Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 contenente una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f147a-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="f147a-134">Server Hyper-V connesso toohello Internet, direttamente o tramite un proxy.</span><span class="sxs-lookup"><span data-stu-id="f147a-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="f147a-135">salve le macchine virtuali da tooprotect devono essere conformi ai [prerequisiti per le macchine virtuali](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="f147a-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="f147a-136">Passaggio 1: Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="f147a-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="f147a-137">Aprire la console di PowerShell ed eseguire questo comando toosign in tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="f147a-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="f147a-138">cmdlet di Hello viene visualizzata una pagina web che richiederà le credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="f147a-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="f147a-139">In alternativa, è possibile includere le credenziali dell'account come un parametro toohello `Login-AzureRmAccount` cmdlet utilizzando hello `-Credential` parametro.</span><span class="sxs-lookup"><span data-stu-id="f147a-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="f147a-140">Nel caso di utilizzo per conto di un tenant di partner CSP, specificare come tenant, cliente hello utilizzando il nome di dominio primario tenantID o tenant.</span><span class="sxs-lookup"><span data-stu-id="f147a-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="f147a-141">Un account può disporre di più sottoscrizioni, pertanto è necessario associare la sottoscrizione di hello da toouse con account hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="f147a-142">Verificare che la sottoscrizione sia registrata toouse hello provider di Azure per servizi di ripristino e il ripristino del sito, utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f147a-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="f147a-143">Nell'output di hello di questi comandi, se hello **RegistrationState** è troppo**registrati**, è possibile procedere tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="f147a-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="f147a-144">In caso contrario, è consigliabile registrare provider mancante hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f147a-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="f147a-145">tooregister hello del provider di Azure per il ripristino del sito e i servizi di ripristino, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f147a-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="f147a-146">Verificare che il provider di hello registrato correttamente utilizzando i seguenti comandi hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="f147a-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="f147a-147">Passaggio 2: Configurare hello che insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="f147a-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="f147a-148">Creare un gruppo di risorse di gestione risorse di Azure in cui si crea l'insieme di credenziali hello oppure utilizzare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="f147a-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="f147a-149">È possibile creare un nuovo gruppo di risorse utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f147a-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="f147a-150">dove hello $ResourceGroupName variabile contiene il nome di hello hello del gruppo di risorse da toocreate e variabile hello $Geo contiene hello Azure area nella quale gruppo di risorse hello toocreate (ad esempio, "Brasile meridionale").</span><span class="sxs-lookup"><span data-stu-id="f147a-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="f147a-151">È possibile ottenere un elenco di gruppi di risorse nella sottoscrizione tramite hello `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f147a-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="f147a-152">Creare un nuovo insieme di credenziali di Servizi di ripristino di Azure, come segue:</span><span class="sxs-lookup"><span data-stu-id="f147a-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="f147a-153">È possibile recuperare un elenco di insiemi di credenziali esistenti utilizzando hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f147a-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="f147a-154">Se si desiderano operazioni tooperform su insiemi di credenziali per il ripristino del sito creati tramite portale classico hello o modulo PowerShell di Azure Service Management hello, è possibile recuperare un elenco di tali archivi utilizzando hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f147a-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="f147a-155">Per tutte le nuove operazioni, occorre creare un nuovo insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f147a-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="f147a-156">insiemi di credenziali di Site Recovery Hello creata in precedenza sono supportati, ma non dispone di funzionalità più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="f147a-157">Passaggio 3: Impostare hello contesto insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="f147a-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="f147a-158">Imposta il contesto di insieme di credenziali di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f147a-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="f147a-159">Passaggio 4: Creare un sito Hyper-V e generare una nuova chiave di registrazione dell'insieme di credenziali per il sito hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="f147a-160">Creare un nuovo sito Hyper-V, come segue:</span><span class="sxs-lookup"><span data-stu-id="f147a-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="f147a-161">Questo cmdlet consente di avviare un sito di ripristino del sito processo toocreate hello e restituisce un oggetto processo di ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="f147a-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="f147a-162">Attendere toocomplete processo hello e verificare che il processo di hello è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="f147a-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="f147a-163">È possibile recuperare l'oggetto processo hello e quindi controllare lo stato corrente di hello del processo di hello, tramite il cmdlet Get-AzureRmSiteRecoveryJob hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="f147a-164">Generare e scaricare una chiave di registrazione per il sito di hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="f147a-165">Hello copia scaricato toohello chiave Hyper-V host.</span><span class="sxs-lookup"><span data-stu-id="f147a-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="f147a-166">È necessario il sito toohello host di hello tooregister chiave hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f147a-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="f147a-167">Passaggio 5: Installare il provider di Azure Site Recovery hello e agente di servizi di ripristino di Azure nell'host Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f147a-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="f147a-168">Scaricare la versione più recente di hello del provider di hello dal programma di installazione hello [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="f147a-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="f147a-169">Programma di installazione hello esecuzione sull'host Hyper-V e alla fine hello installazione hello continuare toohello passaggio di registrazione.</span><span class="sxs-lookup"><span data-stu-id="f147a-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="f147a-170">Quando richiesto, specificare hello scaricato chiave di registrazione del sito e completare la registrazione del sito toohello host Hyper-V di hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="f147a-171">Verificare che ospitano hello Hyper-V sia toohello registrato tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f147a-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="f147a-172">Passaggio 6: Creare un criterio di replica e associarlo al contenitore di protezione hello</span><span class="sxs-lookup"><span data-stu-id="f147a-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="f147a-173">Creare un criterio di replica come segue:</span><span class="sxs-lookup"><span data-stu-id="f147a-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="f147a-174">Controllo hello restituito tooensure processo di creazione dei criteri di replica hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f147a-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f147a-175">Hello account di archiviazione specificato deve essere in hello stessa area Azure nell'insieme di credenziali di servizi di ripristino e deve essere abilitata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="f147a-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="f147a-176">Se hello specificato ripristino account di archiviazione è di tipo di archiviazione di Azure (versione classica), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (classico).</span><span class="sxs-lookup"><span data-stu-id="f147a-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="f147a-177">Se hello specificato l'account di archiviazione di ripristino è di tipo di archiviazione di Azure (Azure Resource Manager), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (Gestione risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="f147a-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="f147a-178">Ottenere hello protezione contenitore toohello sito corrispondente, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="f147a-179">Avviare l'associazione hello del contenitore di protezione hello con criteri di replica hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="f147a-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="f147a-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="f147a-181">Attendere toocomplete processo di associazione hello e verificare che siano stati completati.</span><span class="sxs-lookup"><span data-stu-id="f147a-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="f147a-182">Passaggio 7: Abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f147a-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="f147a-183">Ottenere hello protezione entità corrispondente toohello macchina virtuale che si desidera tooprotect, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="f147a-184">Iniziare a proteggere hello macchina virtuale, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="f147a-185">Hello account di archiviazione specificato deve essere in hello stessa area Azure nell'insieme di credenziali di servizi di ripristino e deve essere abilitata la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="f147a-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="f147a-186">Se hello specificato ripristino account di archiviazione è di tipo di archiviazione di Azure (versione classica), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (classico).</span><span class="sxs-lookup"><span data-stu-id="f147a-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="f147a-187">Se hello specificato l'account di archiviazione di ripristino è di tipo di archiviazione di Azure (Azure Resource Manager), il failover di hello protetto macchine Ripristina hello macchina tooAzure IaaS (Gestione risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="f147a-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="f147a-188">Se hello macchina virtuale che si sta proteggendo ha più di un disco collegato tooit, specificare disco del sistema operativo hello utilizzando hello *OSDiskName* parametro.</span><span class="sxs-lookup"><span data-stu-id="f147a-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="f147a-189">Attendere hello macchine virtuali tooreach uno stato protetto dopo la replica iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="f147a-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="f147a-190">Questo può richiedere alcuni minuti, a seconda di fattori, ad esempio quantità hello di toobe dati replicati e hello tooAzure larghezza di banda disponibile a monte.</span><span class="sxs-lookup"><span data-stu-id="f147a-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="f147a-191">lo stato del processo Hello e StateDescription vengono aggiornati come indicato di seguito, al momento hello VM raggiungere uno stato protetto.</span><span class="sxs-lookup"><span data-stu-id="f147a-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="f147a-192">Aggiornare le proprietà di ripristino, ad esempio hello dimensioni del ruolo VM e hello rete Azure tooattach hello del network interface card tooupon failover della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f147a-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="f147a-193">Passaggio 8: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="f147a-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="f147a-194">Eseguire un processo di failover di test come segue:</span><span class="sxs-lookup"><span data-stu-id="f147a-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="f147a-195">Verificare che il test hello che creazione macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="f147a-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="f147a-196">(processo di failover di test hello viene sospeso, dopo la creazione di test hello VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="f147a-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="f147a-197">Hello del processo termina con la pulizia artefatti hello creato dopo il ripristino processo hello, come illustrato nel passaggio successivo hello.)</span><span class="sxs-lookup"><span data-stu-id="f147a-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="f147a-198">Hello completa test failover, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f147a-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="f147a-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f147a-199">Next Steps</span></span>
<span data-ttu-id="f147a-200">[Altre informazioni](https://msdn.microsoft.com/library/azure/mt637930.aspx) sui cmdlet PowerShell per Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f147a-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
