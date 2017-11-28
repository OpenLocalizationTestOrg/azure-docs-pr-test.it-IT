---
title: 'Azure Active Directory Domain Services: Guida all''amministrazione | Microsoft Docs'
description: Un dominio Windows macchina virtuale tooa gestito tramite Azure PowerShell e il modello di distribuzione classica hello.
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="f6eb5-103">Un dominio Windows Server macchina virtuale tooa gestito con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6eb5-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6eb5-104">Portale di Azure classico - Windows</span><span class="sxs-lookup"><span data-stu-id="f6eb5-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="f6eb5-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="f6eb5-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="f6eb5-106">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f6eb5-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f6eb5-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f6eb5-108">Servizi di dominio Active Directory di Azure non supporta attualmente il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="f6eb5-109">Questi passaggi mostrano come toocustomize una serie di Azure PowerShell comandi che creare e preconfigurare una macchina virtuale Azure basato su Windows utilizzando un approccio di blocco predefinito.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="f6eb5-110">Questi passaggi consentono di creare una macchina virtuale Azure basato su Windows e creare un join tooan dominio gestito di servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="f6eb5-111">Questi passaggi seguono un approccio basato sul completamento di valori predefiniti per la creazione di set di comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="f6eb5-112">Questo approccio può essere utile se si tooPowerShell nuovo o si desidera tooknow toospecify i valori per la corretta configurazione.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="f6eb5-113">Gli utenti esperti di PowerShell possono accettare i comandi di hello e sostituire i propri valori per le variabili di hello (righe hello che iniziano con "$").</span><span class="sxs-lookup"><span data-stu-id="f6eb5-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="f6eb5-114">Se non è già fatto, utilizzare le istruzioni hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="f6eb5-115">Quindi, aprire un prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="f6eb5-116">Passaggio 1: Aggiungere l'account</span><span class="sxs-lookup"><span data-stu-id="f6eb5-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="f6eb5-117">Al prompt di PowerShell hello digitare **Add-AzureAccount** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="f6eb5-118">Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="f6eb5-119">Digitare la password dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="f6eb5-120">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="f6eb5-121">Passaggio 2: Impostare l'account di archiviazione e la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f6eb5-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="f6eb5-122">Impostare la sottoscrizione di Azure e l'account di archiviazione, eseguire questi comandi al prompt dei comandi di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="f6eb5-123">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con nomi corretti hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="f6eb5-124">È possibile ottenere il nome di sottoscrizione corretta hello dalla proprietà SubscriptionName hello output di hello hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f6eb5-125">È possibile ottenere un nome account di archiviazione corretto hello da hello proprietà Label dell'output di hello di hello **Get AzureStorageAccount** comando dopo aver eseguito hello **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="f6eb5-126">Passaggio 3: Guida dettagliata - eseguire il provisioning di macchina virtuale hello e aggiungerla dominio gestito toohello</span><span class="sxs-lookup"><span data-stu-id="f6eb5-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="f6eb5-127">Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale, con le righe vuote tra ogni blocco per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="f6eb5-128">Specificare le informazioni su toobe macchina virtuale di Windows hello il provisioning.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="f6eb5-129">Per i valori di InstanceSize hello per D, di dominio Active Directory o macchine virtuali serie G, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6eb5-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="f6eb5-130">Vengono fornite informazioni di dominio gestiti hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="f6eb5-131">Specificare il nome di hello del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="f6eb5-132">Specificare il nome di hello di hello toowhich di rete virtuale hello che VM devono essere unite in join.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="f6eb5-133">Verificare che tale dominio gestito AAD-DS hello è disponibile in questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="f6eb5-134">Selezionare hello VM immagine toobe utilizzato tooprovision hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="f6eb5-135">Configurare hello VM - nome del set di VM toobe di dimensioni e l'immagine di istanza utilizzata.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="f6eb5-136">Ottenere le credenziali di amministratore locale per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="f6eb5-137">Scegliere una password di amministratore locale sicura.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="f6eb5-138">Ottenere le credenziali per un account utente di dominio gestiti degli amministratori di controller di dominio too'AAD gruppo toojoin VM toohello appartenenti.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="f6eb5-139">Non specificare il nome di dominio hello - per istanza, in questo esempio, si specifica "bob" come nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="f6eb5-140">Configurare hello VM - specificare il requisito di join dominio & credenziali necessarie.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="f6eb5-141">Impostare una subnet per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="f6eb5-142">Facoltativo: Scegliere l'indirizzo IP toohello del dominio hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="f6eb5-143">Se si imposta gli indirizzi IP hello di hello toobe gestito dominio servizi di dominio Active Directory di Azure di hello server DNS per la rete virtuale hello, questo passaggio non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="f6eb5-144">A questo punto, hello provisioning dominio macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="f6eb5-145">Script tooprovision una macchina virtuale di Windows e aggiungerla automaticamente tooan dominio gestito di servizi di dominio di Azure ad</span><span class="sxs-lookup"><span data-stu-id="f6eb5-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="f6eb5-146">Questo set di comandi di PowerShell crea una macchina virtuale per un server line-of-business che:</span><span class="sxs-lookup"><span data-stu-id="f6eb5-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="f6eb5-147">Usa immagine di Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f6eb5-148">È una macchina virtuale molto piccola.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="f6eb5-149">Nome hello Contoso100-test.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="f6eb5-150">Viene automaticamente dominio gestito contoso100 di toohello aggiunti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="f6eb5-151">Viene aggiunto toohello stessa rete virtuale hello gestiti dominio.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="f6eb5-152">Ecco hello macchina virtuale Windows di esempio completo script toocreate hello e aggiungerla automaticamente toohello dominio gestito di servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6eb5-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="f6eb5-153">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="f6eb5-153">Related Content</span></span>
* [<span data-ttu-id="f6eb5-154">Guida introduttiva di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="f6eb5-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f6eb5-155">Amministrare un dominio gestito di Servizi di dominio Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6eb5-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
