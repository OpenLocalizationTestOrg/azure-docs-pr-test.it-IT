---
title: Eseguire la replica di macchine virtuali Hyper-V con PowerShell e Azure Resource Manager | Documentazione Microsoft
description: Automatizzare la replica di macchine virtuali in Azure con Azure Site Recovery usando PowerShell e Azure Resource Manager.
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
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="156e9-103">Eseguire la replica tra macchine virtuali Hyper-V locali e Azure con PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="156e9-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="156e9-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="156e9-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="156e9-105">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="156e9-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="156e9-106">Portale classico</span><span class="sxs-lookup"><span data-stu-id="156e9-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="156e9-107">Overview</span><span class="sxs-lookup"><span data-stu-id="156e9-107">Overview</span></span>
<span data-ttu-id="156e9-108">Azure Site Recovery favorisce la strategia di continuità aziendale e ripristino di emergenza gestendo la replica, il failover e il ripristino delle macchine virtuali in diversi scenari di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="156e9-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="156e9-109">Per un elenco completo degli scenari di distribuzione, vedere [Panoramica di Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="156e9-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="156e9-110">Azure PowerShell è un modulo che offre i cmdlet per gestire Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="156e9-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="156e9-111">È possibile utilizzare due tipi di moduli: il modulo Azure Profile o il modulo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="156e9-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="156e9-112">I cmdlet di PowerShell per Site Recovery disponibili con Azure PowerShell per Azure Resource Manager consentono di proteggere e ripristinare i server in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="156e9-113">Questo articolo descrive come usare Windows PowerShell con Azure Resource Manage per distribuire Site Recovery per configurare e orchestrare la protezione dei server in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="156e9-114">L'esempio usato in questo articolo illustra come proteggere, eseguire il failover e ripristinare in Azure le macchine virtuali di un host Hyper-V usando Azure PowerShell con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="156e9-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="156e9-115">I cmdlet di PowerShell per Site Recovery consentono attualmente di configurare i seguenti elementi: da un sito Virtual Machine Manager a un altro, da un sito Virtual Machine Manager ad Azure e da un sito di Hyper-V ad Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="156e9-116">Non è necessario essere un esperto di PowerShell per usare questo articolo, ma si presume che si conoscano i concetti di base, ad esempio moduli, cmdlet e sessioni.</span><span class="sxs-lookup"><span data-stu-id="156e9-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="156e9-117">Per altre informazioni su Windows PowerShell, vedere [Introduzione a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="156e9-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="156e9-118">Altrei informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="156e9-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="156e9-119">I partner Microsoft che fanno parte del programma Cloud Solution Provider (CSP) possono configurare e gestire la protezione dei server dei clienti nelle rispettive sottoscrizioni CSP dei clienti, ovvero le sottoscrizioni tenant.</span><span class="sxs-lookup"><span data-stu-id="156e9-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="156e9-120">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="156e9-120">Before you start</span></span>
<span data-ttu-id="156e9-121">Assicurarsi che siano rispettati i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="156e9-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="156e9-122">Account [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="156e9-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="156e9-123">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="156e9-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="156e9-124">Inoltre, è possibile leggere le informazioni sui [prezzi di Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="156e9-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="156e9-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="156e9-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="156e9-126">Per informazioni su questa versione e su come installarla, vedere [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="156e9-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="156e9-127">Moduli [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/).</span><span class="sxs-lookup"><span data-stu-id="156e9-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="156e9-128">È possibile ottenere le ultime versioni di questi moduli da [PowerShell Gallery](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="156e9-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="156e9-129">Questo articolo descrive come usare Azure Powershell con Azure Resource Manager per configurare e gestire la protezione dei server.</span><span class="sxs-lookup"><span data-stu-id="156e9-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="156e9-130">L'esempio usato in questo articolo illustra come proteggere una macchina virtuale, in esecuzione su un host Hyper-V, in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="156e9-131">I prerequisiti seguenti sono specifici di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="156e9-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="156e9-132">Per un set più completo di requisiti per i diversi scenari di Site Recovery, vedere la documentazione relativa a uno scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="156e9-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="156e9-133">Host Hyper-V che esegue Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 contenente una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="156e9-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="156e9-134">Server Hyper-V connessi a Internet, in modo diretto o tramite proxy.</span><span class="sxs-lookup"><span data-stu-id="156e9-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="156e9-135">Le macchine virtuali da proteggere devono essere conformi ai [prerequisiti per le macchine virtuali](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="156e9-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="156e9-136">Passaggio 1: Accedere al proprio account Azure</span><span class="sxs-lookup"><span data-stu-id="156e9-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="156e9-137">Aprire una console di PowerShell ed eseguire questo comando per accedere all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="156e9-138">Il cmdlet visualizza una pagina Web che richiederà le credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="156e9-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="156e9-139">In alternativa, è anche possibile includere le credenziali dell'account come parametro nel cmdlet `Login-AzureRmAccount` usando il parametro `-Credential`.</span><span class="sxs-lookup"><span data-stu-id="156e9-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="156e9-140">Se si è un partner CSP che opera per conto di un tenant, è necessario specificare il cliente come tenant usando l'ID tenant o il nome di dominio primario del tenant.</span><span class="sxs-lookup"><span data-stu-id="156e9-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="156e9-141">Un account può avere molte sottoscrizioni, è quindi necessario associare la sottoscrizione che si vuole usare all'account.</span><span class="sxs-lookup"><span data-stu-id="156e9-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="156e9-142">Verificare che la sottoscrizione sia registrata per l'uso dei provider di Azure per Servizi di ripristino e Site Recovery usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="156e9-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="156e9-143">Nell'output di questi comandi, se **RegistrationState** è impostato su **Registered**, è possibile procedere con il passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="156e9-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="156e9-144">In caso contrario è necessario registrare il provider mancante nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="156e9-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="156e9-145">Per registrare il provider di Azure per Site Recovery e Servizi di ripristino, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="156e9-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="156e9-146">Verificare che i provider siano stati registrati correttamente usando i comandi `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="156e9-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="156e9-147">Passaggio 2: Configurare l'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="156e9-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="156e9-148">Creare un gruppo di risorse di Azure Resource Manager in cui creare l'insieme di credenziali o usare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="156e9-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="156e9-149">È possibile creare un nuovo gruppo di risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="156e9-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="156e9-150">dove la variabile $ResourceGroupName contiene il nome del gruppo di risorse che si vuole creare e la variabile $Geo contiene l'area di Azure in cui creare il gruppo di risorse (ad esempio, Brasile meridionale).</span><span class="sxs-lookup"><span data-stu-id="156e9-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="156e9-151">È possibile ottenere un elenco dei gruppi di risorse nella sottoscrizione usando il cmdlet `Get-AzureRmResourceGroup` .</span><span class="sxs-lookup"><span data-stu-id="156e9-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="156e9-152">Creare un nuovo insieme di credenziali di Servizi di ripristino di Azure, come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="156e9-153">Per recuperare un elenco di insiemi di credenziali esistenti, usare il cmdlet `Get-AzureRmRecoveryServicesVault`.</span><span class="sxs-lookup"><span data-stu-id="156e9-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="156e9-154">Per eseguire operazioni sulle credenziali di Site Recovery create usando il portale classico o il modulo di PowerShell di gestione dei servizi di Azure, è possibile recuperare un elenco di tali credenziali usando il cmdlet `Get-AzureRmSiteRecoveryVault`.</span><span class="sxs-lookup"><span data-stu-id="156e9-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="156e9-155">Per tutte le nuove operazioni, occorre creare un nuovo insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="156e9-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="156e9-156">Gli insiemi di credenziali di Site Recovery creati prima sono comunque supportati, ma non dispongono delle ultime funzionalità.</span><span class="sxs-lookup"><span data-stu-id="156e9-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="156e9-157">Passaggio 3: Impostare il contesto dell’insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="156e9-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="156e9-158">Impostare il contesto dell’insieme di credenziali eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="156e9-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="156e9-159">Passaggio 4: Creare un sito Hyper-V e generare una nuova chiave di registrazione dell'insieme di credenziali per il sito.</span><span class="sxs-lookup"><span data-stu-id="156e9-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="156e9-160">Creare un nuovo sito Hyper-V, come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="156e9-161">Questo cmdlet avvia un processo di Site Recovery per creare il sito e restituisce un oggetto processo di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="156e9-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="156e9-162">Attendere il completamento del processo e verificare che sia stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="156e9-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="156e9-163">È possibile recuperare l'oggetto processo e quindi controllare lo stato corrente del processo usando il cmdlet Get-AzureRmSiteRecoveryJob.</span><span class="sxs-lookup"><span data-stu-id="156e9-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="156e9-164">Generare e scaricare una chiave di registrazione per il sito come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="156e9-165">Copiare la chiave scaricata nell'host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="156e9-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="156e9-166">La chiave è necessaria per registrare l'host Hyper-V nel sito.</span><span class="sxs-lookup"><span data-stu-id="156e9-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="156e9-167">Passaggio 5: Installare il provider di Azure Site Recovery e l'agente Servizi di ripristino di Azure nell'host Hyper-V</span><span class="sxs-lookup"><span data-stu-id="156e9-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="156e9-168">Scaricare il programma di installazione per l'ultima versione del provider da [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="156e9-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="156e9-169">Eseguire il programma di installazione nell'host Hyper-V e al termine dell'installazione continuare con il passaggio della registrazione.</span><span class="sxs-lookup"><span data-stu-id="156e9-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="156e9-170">Quando richiesto, fornire la chiave di registrazione del sito scaricata e completare la registrazione dell'host Hyper-V nel sito.</span><span class="sxs-lookup"><span data-stu-id="156e9-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="156e9-171">Verificare che l'host Hyper-V sia stato registrato nel sito usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="156e9-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="156e9-172">Passaggio 6: Creare un criterio di replica e associarlo al contenitore di protezione</span><span class="sxs-lookup"><span data-stu-id="156e9-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="156e9-173">Creare un criterio di replica come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="156e9-174">Controllare il processo restituito per assicurarsi che la creazione del criterio di replica sia riuscita.</span><span class="sxs-lookup"><span data-stu-id="156e9-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="156e9-175">L'account di archiviazione specificato deve essere nella stessa area di Azure dell'insieme di credenziali di Servizi di ripristino e avere la replica geografica abilitata.</span><span class="sxs-lookup"><span data-stu-id="156e9-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="156e9-176">Se l'account di archiviazione di ripristino specificato è di tipo Archiviazione di Azure (classico), il failover dei computer protetti ripristina il computer nello IaaS di Azure (classico).</span><span class="sxs-lookup"><span data-stu-id="156e9-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="156e9-177">Se l'account di archiviazione di ripristino specificato è di tipo Archiviazione di Azure (Azure Resource Manager), il failover dei computer protetti ripristina il computer nello IaaS di Azure (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="156e9-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="156e9-178">Ottenere il contenitore di protezione corrispondente al sito come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="156e9-179">Avviare l'associazione del contenitore di protezione al criterio di replica come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="156e9-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="156e9-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="156e9-181">Attendere il completamento del processo di associazione e assicurarsi che sia riuscito.</span><span class="sxs-lookup"><span data-stu-id="156e9-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="156e9-182">Passaggio 7: Abilitare la protezione per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="156e9-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="156e9-183">Ottenere l'entità di protezione corrispondente alla VM da proteggere come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="156e9-184">Avviare la protezione della macchina virtuale come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="156e9-185">L'account di archiviazione specificato deve essere nella stessa area di Azure dell'insieme di credenziali di Servizi di ripristino e avere la replica geografica abilitata.</span><span class="sxs-lookup"><span data-stu-id="156e9-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="156e9-186">Se l'account di archiviazione di ripristino specificato è di tipo Archiviazione di Azure (classico), il failover dei computer protetti ripristina il computer nello IaaS di Azure (classico).</span><span class="sxs-lookup"><span data-stu-id="156e9-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="156e9-187">Se l'account di archiviazione di ripristino specificato è di tipo Archiviazione di Azure (Azure Resource Manager), il failover dei computer protetti ripristina il computer nello IaaS di Azure (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="156e9-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="156e9-188">Se alla VM protetta è collegato più di un disco, specificare il disco del sistema operativo usando il parametro *OSDiskName* .</span><span class="sxs-lookup"><span data-stu-id="156e9-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="156e9-189">Attendere che le macchine virtuali raggiungano uno stato protetto dopo la replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="156e9-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="156e9-190">L’operazione può richiedere un certo tempo a seconda di fattori quali la quantità di dati da replicare e la larghezza di banda upstream disponibile in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="156e9-191">I valori State e StateDescription del processo vengono aggiornati come segue quando la VM raggiunge uno stato protetto.</span><span class="sxs-lookup"><span data-stu-id="156e9-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="156e9-192">Aggiornare le proprietà di ripristino, ad esempio la dimensione del ruolo VM e la rete di Azure a cui associare le schede di interfaccia di rete delle macchine virtuali in caso di failover.</span><span class="sxs-lookup"><span data-stu-id="156e9-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

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
        DisplayName      : Update the virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="156e9-193">Passaggio 8: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="156e9-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="156e9-194">Eseguire un processo di failover di test come segue:</span><span class="sxs-lookup"><span data-stu-id="156e9-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="156e9-195">Verificare che la VM di test sia creata in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="156e9-196">Il processo di failover di test viene sospeso dopo la creazione della VM di test in Azure.</span><span class="sxs-lookup"><span data-stu-id="156e9-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="156e9-197">Il processo viene completato pulendo gli elementi creati alla ripresa del processo, come illustrato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="156e9-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="156e9-198">Completare il failover di test come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="156e9-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="156e9-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="156e9-199">Next Steps</span></span>
<span data-ttu-id="156e9-200">[Altre informazioni](https://msdn.microsoft.com/library/azure/mt637930.aspx) sui cmdlet PowerShell per Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="156e9-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
