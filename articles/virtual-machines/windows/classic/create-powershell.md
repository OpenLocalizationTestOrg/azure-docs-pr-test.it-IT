---
title: Creare una macchina virtuale Windows con PowerShell | Microsoft Docs
description: Creare macchine virtuali Windows con Azure PowerShell e il modello di distribuzione classica.
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
ms.openlocfilehash: 75c6cf17ee269ae169d9f2f748d0985ca07e454e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="6b906-103">Creare macchine virtuali Windows con il modello di distribuzione classica e PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b906-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b906-104">Portale di Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="6b906-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="6b906-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="6b906-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="6b906-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6b906-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b906-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="6b906-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6b906-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="6b906-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6b906-109">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b906-109">Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="6b906-110">In questi passaggi viene illustrato come personalizzare un set di comandi di Azure PowerShell per la creazione e la preconfigurazione di una macchina virtuale di Azure basata su Windows tramite un approccio con componenti principali.</span><span class="sxs-lookup"><span data-stu-id="6b906-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="6b906-111">È possibile usare questo processo per creare rapidamente un set di comandi per una nuova macchina virtuale basata su Windows ed espandere una distribuzione esistente oppure creare più set di comandi in grado di generare rapidamente un ambiente personalizzato di sviluppo/test o per professionisti IT.</span><span class="sxs-lookup"><span data-stu-id="6b906-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="6b906-112">Questi passaggi seguono un approccio basato sul completamento di valori predefiniti per la creazione di set di comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b906-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="6b906-113">Questo approccio può essere utile se non si è esperti di PowerShell o per sapere semplicemente quali valori specificare per una corretta configurazione.</span><span class="sxs-lookup"><span data-stu-id="6b906-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="6b906-114">Gli utenti esperti di PowerShell possono usare i comandi sostituendo le variabili (le righe che iniziano con "$") con i propri valori.</span><span class="sxs-lookup"><span data-stu-id="6b906-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="6b906-115">Se non è ancora stato installato, attenersi alle istruzioni incluse nell’argomento [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per installare Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="6b906-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="6b906-116">Quindi, aprire un prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b906-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="6b906-117">Passaggio 1: Aggiungere l'account</span><span class="sxs-lookup"><span data-stu-id="6b906-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="6b906-118">Al prompt di PowerShell digitare **Add-AzureAccount** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="6b906-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="6b906-119">Digitare l'indirizzo di posta elettronica associato alla sottoscrizione di Azure e fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="6b906-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="6b906-120">Digitare la password per l'account.</span><span class="sxs-lookup"><span data-stu-id="6b906-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="6b906-121">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="6b906-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="6b906-122">Passaggio 2: Impostare l'account di archiviazione e la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6b906-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="6b906-123">Impostare la sottoscrizione di Azure e l'account di archiviazione eseguendo questi comandi al prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b906-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="6b906-124">Sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >, con i nomi corretti.</span><span class="sxs-lookup"><span data-stu-id="6b906-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="6b906-125">È possibile ottenere il nome della sottoscrizione corretto dalla proprietà SubscriptionName dell'output del comando **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="6b906-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="6b906-126">È possibile ottenere il nome dell'account di archiviazione corretto dalla proprietà Label dell'output del comando **Get-AzureStorageAccount** dopo aver eseguito il comando **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="6b906-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="6b906-127">Passaggio 3: determinare il valore ImageFamily</span><span class="sxs-lookup"><span data-stu-id="6b906-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="6b906-128">Il passaggio successivo prevede la determinazione del valore ImageFamily o Label per l'immagina specifica corrispondente alla macchina virtuale di Azure da creare.</span><span class="sxs-lookup"><span data-stu-id="6b906-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="6b906-129">Con questo comando è possibile ottenere l'elenco di valori ImageFamily disponibili.</span><span class="sxs-lookup"><span data-stu-id="6b906-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="6b906-130">Di seguito sono riportati alcuni esempi di valori ImageFamily per i computer basati su Windows:</span><span class="sxs-lookup"><span data-stu-id="6b906-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="6b906-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="6b906-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="6b906-132">Windows Server 2008 R2 SP1,</span><span class="sxs-lookup"><span data-stu-id="6b906-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="6b906-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="6b906-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="6b906-134">SQL Server 2012 SP1 Enterprise in Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6b906-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="6b906-135">Se si trova l'immagine che si sta cercando, aprire una nuova istanza dell'editor di testo preferito o l'ambiente PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="6b906-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="6b906-136">Copiare quanto segue nel nuovo file di testo o in PowerShell ISE, sostituendo il valore ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="6b906-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="6b906-137">In alcuni casi, il nome dell'immagine si trova nella proprietà Label anziché nel valore ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="6b906-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="6b906-138">Se l'immagine che si sta cercando non viene trovata con la proprietà ImageFamily, elencare le immagini in base alla proprietà Label con questo comando.</span><span class="sxs-lookup"><span data-stu-id="6b906-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="6b906-139">Se si trova l'immagine corretta con questo comando, aprire una nuova istanza dell'editor di testo preferito o l'ambiente PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6b906-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="6b906-140">Copiare quanto segue nel nuovo file di testo o in PowerShell ISE, sostituendo il valore Label.</span><span class="sxs-lookup"><span data-stu-id="6b906-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="6b906-141">Passaggio 4: compilare il set di comandi</span><span class="sxs-lookup"><span data-stu-id="6b906-141">Step 4: Build your command set</span></span>
<span data-ttu-id="6b906-142">Compilare il resto del set di comandi copiando il seguente set appropriato di blocchi nel nuovo file di testo o in ISE, quindi compilare i valori delle variabili rimuovendo i caratteri < e >.</span><span class="sxs-lookup"><span data-stu-id="6b906-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="6b906-143">Vedere i due [esempi](#examples) alla fine di questo articolo per avere un'idea del risultato finale.</span><span class="sxs-lookup"><span data-stu-id="6b906-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="6b906-144">Avviare il set di comandi scegliendo uno dei due seguenti blocchi di comandi (obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="6b906-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="6b906-145">Opzione 1: specificare un nome di macchina virtuale e una dimensione.</span><span class="sxs-lookup"><span data-stu-id="6b906-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="6b906-146">Opzione 2: specificare un nome, la dimensione e il nome del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6b906-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="6b906-147">Per i valori InstanceSize per le macchine virtuali di serie D-, DS- o G-, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b906-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6b906-148">Se si dispone di un contratto Enterprise con Software Assurance e si intende sfruttare il [vantaggio dell'uso ibrido](https://azure.microsoft.com/pricing/hybrid-use-benefit/) di Windows Server, aggiungere il parametro **-LicenseType** al cmdlet **New-AzureVMConfig**, passando il valore **Windows_Server** come caso d'uso tipico.</span><span class="sxs-lookup"><span data-stu-id="6b906-148">If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.</span></span>  <span data-ttu-id="6b906-149">Controllare che si stia usando un'immagine caricata, poiché con il vantaggio dell'uso ibrido non è consentito usare un'immagine standard della raccolta.</span><span class="sxs-lookup"><span data-stu-id="6b906-149">Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="6b906-150">Facoltativamente, per un computer Windows autonomo, specificare l'account amministratore locale e la password.</span><span class="sxs-lookup"><span data-stu-id="6b906-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="6b906-151">Scegliere una password complessa.</span><span class="sxs-lookup"><span data-stu-id="6b906-151">Choose a strong password.</span></span> <span data-ttu-id="6b906-152">Per verificarne il livello di complessità, vedere [Controllo password: utilizzo di password complesse](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b906-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="6b906-153">Facoltativamente, per aggiungere il computer Windows a un dominio di Active Directory esistente, specificare l'account e la password di amministratore locale, il dominio e infine il nome e la password di un account di dominio.</span><span class="sxs-lookup"><span data-stu-id="6b906-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="6b906-154">Per altre opzioni di preconfigurazione per le macchine virtuali basate su Windows, vedere la sintassi per i set di parametri **Windows** e **WindowsDomain** in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="6b906-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="6b906-155">Facoltativamente, assegnare alla macchina virtuale un indirizzo IP specifico, noto come DIP statico.</span><span class="sxs-lookup"><span data-stu-id="6b906-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="6b906-156">È possibile verificare la disponibilità di uno specifico indirizzo IP con:</span><span class="sxs-lookup"><span data-stu-id="6b906-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="6b906-157">Facoltativamente, assegnare la macchina virtuale a una subnet specifica in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b906-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="6b906-158">Facoltativamente, aggiungere un disco dati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b906-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="6b906-159">Per un controller di dominio di Active Directory, impostare $hcaching su "None".</span><span class="sxs-lookup"><span data-stu-id="6b906-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="6b906-160">Facoltativamente, aggiungere la macchina virtuale a un set con carico bilanciato esistente per il traffico esterno.</span><span class="sxs-lookup"><span data-stu-id="6b906-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="6b906-161">Infine, scegliere uno di questi blocchi di comandi richiesti per la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b906-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="6b906-162">Opzione 1: creare la macchina virtuale in un servizio cloud esistente.</span><span class="sxs-lookup"><span data-stu-id="6b906-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="6b906-163">Il nome breve del servizio cloud è il nome visualizzato nell'elenco dei servizi cloud nel portale di Azure o nell'elenco dei gruppi di risorse nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b906-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="6b906-164">Opzione 2: creare la macchina virtuale in un servizio cloud e in una rete virtuale esistenti.</span><span class="sxs-lookup"><span data-stu-id="6b906-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="6b906-165">Passaggio 5: eseguire il set di comandi</span><span class="sxs-lookup"><span data-stu-id="6b906-165">Step 5: Run your command set</span></span>
<span data-ttu-id="6b906-166">Rivedere il set di comandi di Azure PowerShell compilato nell'editor di testo o in PowerShell ISE costituito da più blocchi di comandi del passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="6b906-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="6b906-167">Assicurarsi di aver specificato tutte le variabili necessarie e che siano presenti i valori corretti.</span><span class="sxs-lookup"><span data-stu-id="6b906-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="6b906-168">Assicurarsi inoltre che siano stati rimossi tutti i caratteri < e >.</span><span class="sxs-lookup"><span data-stu-id="6b906-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="6b906-169">Se si usa un editor di testo, copiare il set di comandi negli Appunti, quindi fare clic con il pulsante destro del mouse sul prompt dei comandi aperto di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b906-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="6b906-170">Il set di comandi verrà emesso come una serie di comandi di PowerShell e verrà creata la macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b906-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="6b906-171">In alternativa, eseguire il comando set in PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6b906-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="6b906-172">Se si crea nuovamente questa macchina virtuale o una simile, è possibile:</span><span class="sxs-lookup"><span data-stu-id="6b906-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="6b906-173">Salvare questo set di comandi come file di script di PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="6b906-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="6b906-174">Salvare questo set di comandi come Runbook di automazione di Azure nella sezione **Account di automazione** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b906-174">Save this command set as an Azure Automation runbook in the **Automation Accounts** section of the Azure portal.</span></span>

## <span data-ttu-id="6b906-175"><a id="examples"></a>Esempi:</span><span class="sxs-lookup"><span data-stu-id="6b906-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="6b906-176">Di seguito sono riportati due esempi d'uso dei passaggi precedenti per compilare i set di comandi di Azure PowerShell per la creazione di macchine virtuali Azure basate su Windows.</span><span class="sxs-lookup"><span data-stu-id="6b906-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="6b906-177">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="6b906-177">Example 1</span></span>
<span data-ttu-id="6b906-178">Un set di comandi di PowerShell è necessario per creare la macchina virtuale iniziale per un controller di dominio di Active Directory che:</span><span class="sxs-lookup"><span data-stu-id="6b906-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="6b906-179">Utilizzi l'immagine Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="6b906-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="6b906-180">Sia denominato AZDC1.</span><span class="sxs-lookup"><span data-stu-id="6b906-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="6b906-181">Sia un computer autonomo.</span><span class="sxs-lookup"><span data-stu-id="6b906-181">Is a standalone computer.</span></span>
* <span data-ttu-id="6b906-182">Disponga di un disco dati aggiuntivo di 20 GB.</span><span class="sxs-lookup"><span data-stu-id="6b906-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="6b906-183">Abbia l'indirizzo IP statico 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="6b906-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="6b906-184">Si trovi nella subnet BackEnd della rete virtuale AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="6b906-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="6b906-185">Si trovi nel servizio cloud Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="6b906-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="6b906-186">Ecco il set di comandi corrispondente di Azure PowerShell per creare la macchina virtuale, con righe vuote tra ogni blocco per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="6b906-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
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

### <a name="example-2"></a><span data-ttu-id="6b906-187">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="6b906-187">Example 2</span></span>
<span data-ttu-id="6b906-188">Un set di comandi di PowerShell è necessario per creare una macchina virtuale per un server line-of-business che:</span><span class="sxs-lookup"><span data-stu-id="6b906-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="6b906-189">Utilizzi l'immagine Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="6b906-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="6b906-190">Sia denominato LOB1.</span><span class="sxs-lookup"><span data-stu-id="6b906-190">Has the name LOB1.</span></span>
* <span data-ttu-id="6b906-191">Sia membro del dominio corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6b906-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="6b906-192">Disponga di un disco dati aggiuntivo di 200 GB.</span><span class="sxs-lookup"><span data-stu-id="6b906-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="6b906-193">Si trovi nella subnet FrontEnd della rete virtuale AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="6b906-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="6b906-194">Si trovi nel servizio cloud Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="6b906-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="6b906-195">Ecco il set di comandi corrispondente di Azure PowerShell per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b906-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
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


## <a name="next-steps"></a><span data-ttu-id="6b906-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b906-196">Next steps</span></span>
<span data-ttu-id="6b906-197">Se è necessario un disco del sistema operativo superiore a 127 GB, è possibile [espandere l'unità del sistema operativo](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b906-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

