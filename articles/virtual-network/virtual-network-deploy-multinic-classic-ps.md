---
title: "Creare una VM (classica) con più schede di interfaccia di rete - Azure PowerShell | Microsoft Docs"
description: "Informazioni su come creare una VM (classica) con più schede di interfaccia di rete mediante PowerShell."
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
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="cbdd2-103">Creare una macchina virtuale (classica) con più schede di interfaccia di rete usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbdd2-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="cbdd2-104">È possibile creare macchine virtuali (VM) in Azure e collegare più interfacce di rete (NIC) a ciascuna delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="cbdd2-105">Più schede di interfaccia rete consentono la separazione dei tipi di traffico tra schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="cbdd2-106">Ad esempio, una scheda di interfaccia di rete può comunicare con Internet, mentre un'altra comunica solo con le risorse interne non connesse a Internet.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="cbdd2-107">La possibilità di separare il traffico di rete tra più schede di interfaccia di rete è necessaria per molte appliance virtuali di rete, ad esempio soluzioni di ottimizzazione WAN e di distribuzione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbdd2-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cbdd2-109">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="cbdd2-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="cbdd2-111">Informazioni su come seguire questa procedura con il [modello di distribuzione Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="cbdd2-112">La procedura seguente usa un gruppo di risorse denominato *IaaSStory* per i server Web e un gruppo di risorse denominato *IaaSStory-BackEnd* per i server di database.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbdd2-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cbdd2-113">Prerequisites</span></span>

<span data-ttu-id="cbdd2-114">Prima di creare i server di database, è necessario creare il gruppo di risorse *IaaSStory* con tutte le risorse richieste per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="cbdd2-115">Per creare le risorse, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="cbdd2-116">Creare una rete virtuale seguendo la procedura riportata nell'articolo [Creare una rete virtuale](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="cbdd2-117">Creare le macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="cbdd2-117">Create the back-end VMs</span></span>
<span data-ttu-id="cbdd2-118">Le macchine virtuali di back-end dipendono dalla creazione delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbdd2-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="cbdd2-119">**Subnet Back-end**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-119">**Backend subnet**.</span></span> <span data-ttu-id="cbdd2-120">I server del database formeranno parte di una subnet distinta, per separare il traffico.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="cbdd2-121">Lo script seguente prevede che questa subnet sia presente in una rete virtuale denominata *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="cbdd2-122">**Account di archiviazione per dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-122">**Storage account for data disks**.</span></span> <span data-ttu-id="cbdd2-123">Per migliorare le prestazioni, i dischi dati sui server di database utilizzano la tecnologia SSD (Solid State Drive), che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="cbdd2-124">Verificare la posizione di Azure che viene distribuita per supportare l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="cbdd2-125">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-125">**Availability set**.</span></span> <span data-ttu-id="cbdd2-126">Tutti i server di database vengono aggiunti a un singolo set di disponibilità, per garantire che almeno una delle macchine virtuali sia attiva e in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="cbdd2-127">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="cbdd2-127">Step 1 - Start your script</span></span>
<span data-ttu-id="cbdd2-128">È possibile scaricare lo script di PowerShell completo utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="cbdd2-129">Attenersi alla procedura seguente per modificare lo script da usare nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="cbdd2-130">Modificare i valori delle variabili indicate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [Prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="cbdd2-131">Modificare i valori delle variabili indicate di seguito in base ai valori che si desidera usare per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="cbdd2-132">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cbdd2-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="cbdd2-133">È necessario creare un nuovo servizio cloud e un account di archiviazione per i dischi di dati per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="cbdd2-134">È inoltre necessario specificare un'immagine e un account amministratore locale per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="cbdd2-135">Per creare le risorse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cbdd2-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="cbdd2-136">Creare un nuovo servizio cloud</span><span class="sxs-lookup"><span data-stu-id="cbdd2-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="cbdd2-137">Creare un account di archiviazione premium</span><span class="sxs-lookup"><span data-stu-id="cbdd2-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="cbdd2-138">Impostare l'account di archiviazione creato in precedenza come account di archiviazione corrente per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="cbdd2-139">Selezionare un'immagine per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="cbdd2-140">Impostare le credenziali dell'account amministratore locale</span><span class="sxs-lookup"><span data-stu-id="cbdd2-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="cbdd2-141">Passaggio 3 - creare delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cbdd2-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="cbdd2-142">È necessario utilizzare un ciclo per creare tutte le macchine virtuali che si desidera e creare le schede di rete e le macchine virtuali necessarie all'interno del ciclo.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="cbdd2-143">Per creare le schede di rete e le macchine virtuali, eseguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="cbdd2-144">Avviare un `for` ciclo per ripetere i comandi per la creazione di una macchina virtuale e di due schede di rete tutte le volte che lo si ritiene necessario, in base al valore della `$numberOfVMs` variabile.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="cbdd2-145">Creare un `VMConfig` oggetto che specifica l'immagine, le dimensioni e il set di disponibilità per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="cbdd2-146">Eseguire il provisioning della macchina virtuale come macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="cbdd2-147">Impostare il valore predefinito NIC e assegnare un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="cbdd2-148">Aggiungere una seconda scheda di rete per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="cbdd2-149">Creare dischi di dati per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-149">Create to data disks for each VM.</span></span>

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

7. <span data-ttu-id="cbdd2-150">Creare ogni macchina virtuale e terminare il ciclo.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="cbdd2-151">Passaggio 4 - eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-151">Step 4 - Run the script</span></span>
<span data-ttu-id="cbdd2-152">Una volta scaricato e modificato lo script in base alle esigenze, eseguire lo script per creare macchine virtuali del database di back-end con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="cbdd2-153">Salvare lo script ed eseguirlo dal prompt dei comandi **PowerShell** o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="cbdd2-154">Verrà visualizzato l'output iniziale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="cbdd2-155">Compilare le informazioni necessarie nella richiesta di credenziali e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="cbdd2-156">Viene restituito l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
