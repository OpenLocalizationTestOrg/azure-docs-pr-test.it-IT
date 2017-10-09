---
title: "una macchina virtuale (versione classica) con più schede di rete - Azure PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una macchina virtuale (versione classica) con più schede di rete con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="4e395-103">Creare una macchina virtuale (classica) con più schede di interfaccia di rete usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e395-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="4e395-104">È possibile creare macchine virtuali (VM) in Azure e collegare più tooeach (NIC) di interfacce di rete delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4e395-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="4e395-105">Più schede di interfaccia rete consentono la separazione dei tipi di traffico tra schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="4e395-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="4e395-106">Ad esempio, una che scheda di rete può comunicare con hello Internet, mentre l'altra comunica solo con le risorse interne non connessi toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="4e395-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="4e395-107">Hello possibilità tooseparate il traffico di rete tra più schede di rete è necessario per molti dispositivi virtuali di rete, ad esempio distribuzione delle applicazioni e soluzioni per l'ottimizzazione WAN.</span><span class="sxs-lookup"><span data-stu-id="4e395-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e395-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4e395-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4e395-109">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4e395-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4e395-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4e395-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4e395-111">Informazioni su come tooperform questi passaggi tramite hello [il modello di distribuzione di gestione risorse](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4e395-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="4e395-112">i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.</span><span class="sxs-lookup"><span data-stu-id="4e395-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e395-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e395-113">Prerequisites</span></span>

<span data-ttu-id="4e395-114">Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="4e395-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="4e395-115">toocreate queste risorse, completate hello passaggi che seguono.</span><span class="sxs-lookup"><span data-stu-id="4e395-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="4e395-116">Creare una rete virtuale seguendo i passaggi hello hello [creare una rete virtuale](virtual-networks-create-vnet-classic-netcfg-ps.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4e395-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="4e395-117">Creare macchine virtuali di back-end di hello</span><span class="sxs-lookup"><span data-stu-id="4e395-117">Create hello back-end VMs</span></span>
<span data-ttu-id="4e395-118">Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="4e395-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="4e395-119">**Subnet Back-end**.</span><span class="sxs-lookup"><span data-stu-id="4e395-119">**Backend subnet**.</span></span> <span data-ttu-id="4e395-120">server di database Hello faranno parte di una subnet distinta, toosegregate traffico.</span><span class="sxs-lookup"><span data-stu-id="4e395-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="4e395-121">script Hello riportato di seguito prevede tooexist questa subnet in una rete virtuale denominata *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="4e395-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="4e395-122">**Account di archiviazione per dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="4e395-122">**Storage account for data disks**.</span></span> <span data-ttu-id="4e395-123">Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="4e395-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="4e395-124">Verificare che hello distribuire archiviazione premium toosupport località di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e395-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="4e395-125">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4e395-125">**Availability set**.</span></span> <span data-ttu-id="4e395-126">Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="4e395-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="4e395-127">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="4e395-127">Step 1 - Start your script</span></span>
<span data-ttu-id="4e395-128">È possibile scaricare hello completo script di PowerShell utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="4e395-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="4e395-129">Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="4e395-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="4e395-130">Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="4e395-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="4e395-131">Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="4e395-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="4e395-132">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4e395-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="4e395-133">È necessario toocreate un nuovo servizio cloud e uno spazio di archiviazione di account per i dischi dati hello per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4e395-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="4e395-134">È inoltre necessario toospecify un'immagine e un account amministratore locale per hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4e395-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="4e395-135">completare queste risorse, toocreate hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e395-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="4e395-136">Creare un nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="4e395-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="4e395-137">Creare un account di archiviazione premium</span><span class="sxs-lookup"><span data-stu-id="4e395-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="4e395-138">Set di account di archiviazione hello creato in precedenza come account di archiviazione per la sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="4e395-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="4e395-139">Selezionare un'immagine per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e395-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="4e395-140">Impostare le credenziali dell'account amministratore locale hello.</span><span class="sxs-lookup"><span data-stu-id="4e395-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="4e395-141">Passaggio 3 - creare delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4e395-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="4e395-142">È necessario un ciclo di toocreate toouse come più macchine virtuali che desidera e creare hello necessarie schede di rete e le macchine virtuali all'interno di ciclo hello.</span><span class="sxs-lookup"><span data-stu-id="4e395-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="4e395-143">hello toocreate schede di rete e le macchine virtuali, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="4e395-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="4e395-144">Avviare un `for` hello toorepeat ciclo comandi toocreate una macchina virtuale e due schede di rete come numero di volte in base alle esigenze, in base al valore di hello di hello `$numberOfVMs` variabile.</span><span class="sxs-lookup"><span data-stu-id="4e395-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="4e395-145">Creare un `VMConfig` oggetto specificando hello immagine, dimensioni e set di disponibilità per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e395-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="4e395-146">Eseguire il provisioning di hello macchina virtuale come macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="4e395-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="4e395-147">Impostare il valore predefinito di hello NIC e assegnare un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="4e395-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="4e395-148">Aggiungere una seconda scheda di rete per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e395-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="4e395-149">Creare dischi toodata per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4e395-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="4e395-150">Creare ogni macchina virtuale e il ciclo di hello finale.</span><span class="sxs-lookup"><span data-stu-id="4e395-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="4e395-151">Passaggio 4: hello Esegui script</span><span class="sxs-lookup"><span data-stu-id="4e395-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="4e395-152">Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, Run ha script di database di back-end hello toocreate le macchine virtuali con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="4e395-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="4e395-153">Salvare lo script ed eseguirlo da hello **PowerShell** prompt dei comandi o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="4e395-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="4e395-154">Verrà visualizzato un output iniziale hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4e395-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="4e395-155">Immettere le informazioni di hello necessari nella richiesta di credenziali hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e395-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="4e395-156">viene restituito l'output di Hello seguente.</span><span class="sxs-lookup"><span data-stu-id="4e395-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
