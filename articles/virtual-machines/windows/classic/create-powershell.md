---
title: una macchina virtuale di Windows con PowerShell aaaCreate | Documenti Microsoft
description: Creare macchine virtuali di Windows Azure PowerShell e il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="f005f-103">Creare una macchina virtuale Windows con PowerShell e hello modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="f005f-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f005f-104">Portale di Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="f005f-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="f005f-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="f005f-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="f005f-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f005f-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f005f-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f005f-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="f005f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f005f-109">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f005f-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f005f-110">Questi passaggi mostrano come toocustomize una serie di Azure PowerShell comandi che creare e preconfigurare una macchina virtuale Azure basato su Windows utilizzando un approccio di blocco predefinito.</span><span class="sxs-lookup"><span data-stu-id="f005f-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="f005f-111">È possibile utilizzare questo processo tooquickly creare un set di comandi per una nuova macchina virtuale basato su Windows ed espandere una distribuzione esistente o toocreate più comando che imposta rapidamente creare un ambiente di pro IT o di sviluppo/test personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f005f-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="f005f-112">Questi passaggi seguono un approccio basato sul completamento di valori predefiniti per la creazione di set di comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f005f-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="f005f-113">Questo approccio può essere utile se si è tooPowerShell nuovo o si desidera tooknow toospecify i valori per la corretta configurazione.</span><span class="sxs-lookup"><span data-stu-id="f005f-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="f005f-114">Gli utenti esperti di PowerShell possono accettare i comandi di hello e sostituire i propri valori per le variabili di hello (righe hello che iniziano con "$").</span><span class="sxs-lookup"><span data-stu-id="f005f-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="f005f-115">Se non è già fatto, utilizzare le istruzioni hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f005f-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="f005f-116">Quindi, aprire un prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f005f-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="f005f-117">Passaggio 1: Aggiungere l'account</span><span class="sxs-lookup"><span data-stu-id="f005f-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="f005f-118">Al prompt di PowerShell hello digitare **Add-AzureAccount** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="f005f-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="f005f-119">Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="f005f-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="f005f-120">Digitare la password dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="f005f-121">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="f005f-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="f005f-122">Passaggio 2: Impostare l'account di archiviazione e la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f005f-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="f005f-123">Impostare la sottoscrizione di Azure e l'account di archiviazione, eseguire questi comandi al prompt dei comandi di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="f005f-124">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con nomi corretti hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="f005f-125">È possibile ottenere il nome di sottoscrizione corretta hello dalla proprietà SubscriptionName hello output di hello hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="f005f-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f005f-126">È possibile ottenere un nome account di archiviazione corretto hello da hello proprietà Label dell'output di hello di hello **Get AzureStorageAccount** comando dopo aver eseguito hello **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="f005f-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="f005f-127">Passaggio 3: Determinare hello family</span><span class="sxs-lookup"><span data-stu-id="f005f-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="f005f-128">Successivamente, è necessario toodetermine hello family o valore dell'etichetta per hello immagine specifica corrispondente toohello desiderato toocreate macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f005f-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="f005f-129">È possibile ottenere l'elenco di hello dei valori di proprietà ImageFamily disponibili con questo comando.</span><span class="sxs-lookup"><span data-stu-id="f005f-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="f005f-130">Di seguito sono riportati alcuni esempi di valori ImageFamily per i computer basati su Windows:</span><span class="sxs-lookup"><span data-stu-id="f005f-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="f005f-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="f005f-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="f005f-132">Windows Server 2008 R2 SP1,</span><span class="sxs-lookup"><span data-stu-id="f005f-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="f005f-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="f005f-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="f005f-134">SQL Server 2012 SP1 Enterprise in Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f005f-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="f005f-135">Se si trova l'immagine di hello che si sta cercando, aprire una nuova istanza dell'editor di testo hello di scelta o hello PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="f005f-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="f005f-136">Copiare l'esempio hello in nuovo file di testo hello o hello PowerShell ISE, sostituendo il valore di proprietà ImageFamily hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="f005f-137">In alcuni casi, il nome di immagine hello è hello proprietà etichetta anziché hello family valore.</span><span class="sxs-lookup"><span data-stu-id="f005f-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="f005f-138">Se non è possibile trovare l'immagine di hello che si sta cercando di utilizzare la proprietà ImageFamily hello, elenco immagini hello tramite la proprietà etichetta con questo comando.</span><span class="sxs-lookup"><span data-stu-id="f005f-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="f005f-139">Se si trova l'immagine a destra hello con questo comando, aprire una nuova istanza dell'editor di testo hello di scelta o hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f005f-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="f005f-140">Copiare l'esempio hello in nuovo file di testo hello o hello PowerShell ISE, sostituendo il valore di etichetta hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="f005f-141">Passaggio 4: compilare il set di comandi</span><span class="sxs-lookup"><span data-stu-id="f005f-141">Step 4: Build your command set</span></span>
<span data-ttu-id="f005f-142">Compilare il resto di hello del comando di impostare copiando set appropriato di hello di blocchi di sotto del nuovo file di testo o hello ISE inserimento dei valori di variabile hello e rimuovendo hello < e > caratteri.</span><span class="sxs-lookup"><span data-stu-id="f005f-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="f005f-143">Vedere hello due [esempi](#examples) alla fine di hello di questo articolo per avere un'idea del risultato finale hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="f005f-144">Avviare il set di comandi scegliendo uno dei due seguenti blocchi di comandi (obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="f005f-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="f005f-145">Opzione 1: specificare un nome di macchina virtuale e una dimensione.</span><span class="sxs-lookup"><span data-stu-id="f005f-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="f005f-146">Opzione 2: specificare un nome, la dimensione e il nome del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="f005f-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="f005f-147">Per i valori di InstanceSize hello per D, di dominio Active Directory o macchine virtuali serie G, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f005f-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f005f-148">Se si dispone di un contratto Enterprise Agreement con Software Assurance e prevede tootake sfruttare hello Windows Server [vantaggio di utilizzare ibrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/), aggiungere il **- LicenseType** toohello parametro  **Nuovo AzureVMConfig** cmdlet, passando il valore di hello **Windows_Server** per hello tipico caso di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="f005f-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="f005f-149">Verificare se che si sta utilizzando un'immagine che è stato caricato; è possibile utilizzare un'immagine dalla raccolta hello standard con il vantaggio di utilizzare ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="f005f-150">Facoltativamente, per un computer Windows autonomo, specificare la password e account di amministratore locale hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="f005f-151">Scegliere una password complessa.</span><span class="sxs-lookup"><span data-stu-id="f005f-151">Choose a strong password.</span></span> <span data-ttu-id="f005f-152">toocheck il livello di attendibilità, vedere [controllo Password: utilizzo di password complesse](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="f005f-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="f005f-153">Facoltativamente, hello tooadd Windows computer tooan dominio Active Directory esistente, specificare l'account amministratore locale hello e password, hello dominio e nome hello e la password di un account di dominio.</span><span class="sxs-lookup"><span data-stu-id="f005f-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="f005f-154">Per altre opzioni di pre-configurazione per le macchine virtuali basate su Windows, vedere la sintassi di hello per hello **Windows** e **WindowsDomain** nei set di parametri [ Aggiungere-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="f005f-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="f005f-155">Facoltativamente, assegnare la macchina virtuale di hello un indirizzo IP specifico, noto come un DIP statico.</span><span class="sxs-lookup"><span data-stu-id="f005f-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="f005f-156">È possibile verificare la disponibilità di uno specifico indirizzo IP con:</span><span class="sxs-lookup"><span data-stu-id="f005f-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="f005f-157">Facoltativamente, assegnare hello tooa specifiche subnet per macchina virtuale in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f005f-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="f005f-158">Facoltativamente, aggiungere una macchina virtuale toohello di dati singolo disco.</span><span class="sxs-lookup"><span data-stu-id="f005f-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="f005f-159">Per un controller di dominio Active Directory, impostare $hcaching troppo "None".</span><span class="sxs-lookup"><span data-stu-id="f005f-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="f005f-160">Facoltativamente, aggiungere hello tooan esistente con bilanciamento del carico set della macchina virtuale per il traffico esterno.</span><span class="sxs-lookup"><span data-stu-id="f005f-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="f005f-161">Infine, scegliere uno di questi blocchi di comando obbligatorio per la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="f005f-162">Opzione 1: Creare una macchina virtuale hello in un servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="f005f-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="f005f-163">nome breve di Hello del servizio cloud hello è nome hello che compare in elenco hello dei servizi Cloud nel portale di Azure hello o nell'elenco di hello di gruppi di risorse nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="f005f-164">Opzione 2: Creare una macchina virtuale hello in un servizio cloud esistente e la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f005f-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="f005f-165">Passaggio 5: eseguire il set di comandi</span><span class="sxs-lookup"><span data-stu-id="f005f-165">Step 5: Run your command set</span></span>
<span data-ttu-id="f005f-166">Esaminare i set di comandi di Azure PowerShell hello compilato in un editor di testo o hello PowerShell ISE composta da più blocchi di comandi del passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="f005f-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="f005f-167">Assicurarsi di aver specificato tutte le variabili di hello necessita e che dispongono di valori corretti di hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="f005f-168">Assicurarsi inoltre che siano stati rimossi tutti i caratteri di hello < e >.</span><span class="sxs-lookup"><span data-stu-id="f005f-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="f005f-169">Se si utilizza un editor di testo, il comando di hello copia impostare toohello Appunti e quindi fare doppio clic su prompt dei comandi di Windows PowerShell aperto.</span><span class="sxs-lookup"><span data-stu-id="f005f-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="f005f-170">Verrà rilasciare il set di comandi hello come una serie di comandi di PowerShell e creare la macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f005f-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="f005f-171">In alternativa, eseguire il comando hello impostato in hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f005f-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="f005f-172">Se si crea nuovamente questa macchina virtuale o una simile, è possibile:</span><span class="sxs-lookup"><span data-stu-id="f005f-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="f005f-173">Salvare questo set di comandi come file di script di PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="f005f-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="f005f-174">Salvare questo comando imposta come un runbook di automazione di Azure in hello **gli account di automazione** sezione di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f005f-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="f005f-175"><a id="examples"></a>Esempi:</span><span class="sxs-lookup"><span data-stu-id="f005f-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="f005f-176">Di seguito sono riportati due esempi di attenendosi alla procedura hello sopra toobuild i set di comandi di PowerShell di Azure che creano le macchine virtuali Azure basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="f005f-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="f005f-177">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="f005f-177">Example 1</span></span>
<span data-ttu-id="f005f-178">È necessario un PowerShell comando impostato toocreate hello iniziale macchina virtuale per un controller di dominio Active Directory:</span><span class="sxs-lookup"><span data-stu-id="f005f-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="f005f-179">Usa immagine di Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f005f-180">Nome hello AZDC1.</span><span class="sxs-lookup"><span data-stu-id="f005f-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="f005f-181">Sia un computer autonomo.</span><span class="sxs-lookup"><span data-stu-id="f005f-181">Is a standalone computer.</span></span>
* <span data-ttu-id="f005f-182">Disponga di un disco dati aggiuntivo di 20 GB.</span><span class="sxs-lookup"><span data-stu-id="f005f-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="f005f-183">È l'indirizzo IP statico hello 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="f005f-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="f005f-184">È nella subnet back-end hello della rete virtuale di hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="f005f-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="f005f-185">Non è nel servizio cloud Azure TailspinToys hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="f005f-186">Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale, con le righe vuote tra ogni blocco per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="f005f-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="f005f-187">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="f005f-187">Example 2</span></span>
<span data-ttu-id="f005f-188">È necessario un PowerShell set di comandi toocreate una macchina virtuale per un server di line-of-business che:</span><span class="sxs-lookup"><span data-stu-id="f005f-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="f005f-189">Usa immagine di Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f005f-190">Nome hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="f005f-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="f005f-191">È un membro del dominio corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="f005f-192">Disponga di un disco dati aggiuntivo di 200 GB.</span><span class="sxs-lookup"><span data-stu-id="f005f-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="f005f-193">È nella subnet front-end hello della rete virtuale di hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="f005f-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="f005f-194">Non è nel servizio cloud Azure TailspinToys hello.</span><span class="sxs-lookup"><span data-stu-id="f005f-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="f005f-195">Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f005f-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="f005f-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f005f-196">Next steps</span></span>
<span data-ttu-id="f005f-197">Se è necessario un disco del sistema operativo sono maggiore di 127 GB, è possibile [espandere l'unità del sistema operativo hello](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f005f-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

