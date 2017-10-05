---
title: "Creare una macchina virtuale con più schede di interfaccia di rete - Azure PowerShell | Documentazione Microsoft"
description: "Informazioni su come creare una VM con più schede di interfaccia di rete mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3a11afd8fbd6a5e6b94cf1ebee7ea20665421bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="496b2-103">Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="496b2-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="496b2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="496b2-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="496b2-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="496b2-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="496b2-106">Modello</span><span class="sxs-lookup"><span data-stu-id="496b2-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * <span data-ttu-id="496b2-107">[PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="496b2-107">[PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md)</span></span>
> * [<span data-ttu-id="496b2-108">Interfaccia della riga di comando di Azure (versione classica)</span><span class="sxs-lookup"><span data-stu-id="496b2-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="496b2-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="496b2-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="496b2-110">Questo articolo illustra il modello di distribuzione Resource Manager che Microsoft consiglia di usare per le distribuzioni più recenti in sostituzione del [modello di distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="496b2-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="496b2-111">La procedura seguente usa un gruppo di risorse denominato *IaaSStory* per i server Web e un gruppo di risorse denominato *IaaSStory-BackEnd* per i server di database.</span><span class="sxs-lookup"><span data-stu-id="496b2-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="496b2-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="496b2-112">Prerequisites</span></span>
<span data-ttu-id="496b2-113">Prima di creare i server di database, è necessario creare il gruppo di risorse *IaaSStory* con tutte le risorse richieste per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="496b2-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="496b2-114">Per creare le risorse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="496b2-114">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="496b2-115">Passare alla [pagina del modello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="496b2-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="496b2-116">Nella pagina del modello, a destra del **gruppo di risorse padre**, fare clic su **Distribuisci in Azure**.</span><span class="sxs-lookup"><span data-stu-id="496b2-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="496b2-117">Se necessario, modificare i valori dei parametri, quindi seguire i passaggi nel portale di anteprima di Azure per distribuire il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="496b2-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="496b2-118">Assicurarsi che i nomi degli account di archiviazione siano univoci.</span><span class="sxs-lookup"><span data-stu-id="496b2-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="496b2-119">In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="496b2-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="496b2-120">Creare le macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="496b2-120">Create the back-end VMs</span></span>
<span data-ttu-id="496b2-121">Le macchine virtuali di back-end dipendono dalla creazione delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="496b2-121">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="496b2-122">**Account di archiviazione per i dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="496b2-122">**Storage account for data disks**.</span></span> <span data-ttu-id="496b2-123">Per migliorare le prestazioni, i dischi dati sui server di database utilizzano la tecnologia SSD (Solid State Drive), che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="496b2-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="496b2-124">Verificare che la posizione di Azure distribuita supporti l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="496b2-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="496b2-125">**Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="496b2-125">**NICs**.</span></span> <span data-ttu-id="496b2-126">Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.</span><span class="sxs-lookup"><span data-stu-id="496b2-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="496b2-127">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="496b2-127">**Availability set**.</span></span> <span data-ttu-id="496b2-128">Tutti i server di database vengono aggiunti a un singolo set di disponibilità, per garantire che almeno una delle macchine virtuali sia attiva e in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="496b2-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="496b2-129">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="496b2-129">Step 1 - Start your script</span></span>
<span data-ttu-id="496b2-130">È possibile scaricare lo script di PowerShell completo utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="496b2-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="496b2-131">Attenersi alla procedura seguente per modificare lo script da usare nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="496b2-131">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="496b2-132">Modificare i valori delle variabili indicate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [Prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="496b2-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="496b2-133">Modificare i valori delle variabili indicate di seguito in base ai valori che si desidera usare per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="496b2-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="496b2-134">Recuperare le risorse esistenti necessarie per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="496b2-134">Retrieve the existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="496b2-135">Passaggio 2 - Creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="496b2-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="496b2-136">È necessario creare un nuovo gruppo di risorse, un account di archiviazione per i dischi dati e un set di disponibilità per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="496b2-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="496b2-137">Sono inoltre necessarie credenziali dell'account amministratore locale per ciascuna macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-137">You alos need the local administrator account credentials for each VM.</span></span> <span data-ttu-id="496b2-138">Per creare queste risorse, eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="496b2-138">To create these resources, execute the following steps.</span></span>

1. <span data-ttu-id="496b2-139">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="496b2-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="496b2-140">Creare un nuovo account di archiviazione premium nel gruppo di risorse creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="496b2-140">Create a new premium storage account in the resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="496b2-141">Creare un nuovo set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="496b2-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="496b2-142">Ottenere le credenziali dell'account amministratore locale per ciascuna macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-142">Get the local administrator account credentials to be used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="496b2-143">Passaggio 3 - Creare le schede di rete e le macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="496b2-143">Step 3 - Create the NICs and back-end VMs</span></span>
<span data-ttu-id="496b2-144">È necessario utilizzare un ciclo per creare tutte le macchine virtuali che si desidera e creare le schede di rete e le macchine virtuali necessarie all'interno del ciclo.</span><span class="sxs-lookup"><span data-stu-id="496b2-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="496b2-145">Per creare le schede di rete e le macchine virtuali, eseguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="496b2-145">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="496b2-146">Avviare un ciclo `for` per ripetere i comandi per la creazione di una macchina virtuale e di due schede di rete per il numero di volte necessario, in base al valore della variabile `$numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="496b2-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="496b2-147">Creare la scheda di rete utilizzata per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="496b2-147">Create the NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="496b2-148">Creare la scheda di rete utilizzata per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="496b2-148">Create the NIC used for remote access.</span></span> <span data-ttu-id="496b2-149">Si noti che a questa scheda di rete è associato un NSG.</span><span class="sxs-lookup"><span data-stu-id="496b2-149">Notice how this NIC has an NSG associated to it.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="496b2-150">Creare l'oggetto `vmConfig` .</span><span class="sxs-lookup"><span data-stu-id="496b2-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="496b2-151">Creare due dischi dati per ciascuna macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-151">Create two data disks per VM.</span></span> <span data-ttu-id="496b2-152">Si noti che i dischi dati si trovano nell'account di archiviazione premium creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="496b2-152">Notice that the data disks are in the premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="496b2-153">Configurare il sistema operativo e l'immagine da utilizzare per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-153">Configure the operating system, and image to be used for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="496b2-154">Aggiungere le due schede di rete create in precedenza per l'oggetto `vmConfig` .</span><span class="sxs-lookup"><span data-stu-id="496b2-154">Add the two NICs created above to the `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="496b2-155">Creare il disco del sistema operativo e la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-155">Create the OS disk and create the VM.</span></span> <span data-ttu-id="496b2-156">Si noti il simbolo `}` al termine del ciclo `for`.</span><span class="sxs-lookup"><span data-stu-id="496b2-156">Notice the `}` ending the `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="496b2-157">Passaggio 4 - Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="496b2-157">Step 4 - Run the script</span></span>
<span data-ttu-id="496b2-158">Una volta scaricato e modificato lo script in base alle esigenze, eseguire lo script per creare macchine virtuali del database di back-end con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="496b2-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="496b2-159">Salvare lo script ed eseguirlo dal prompt dei comandi **PowerShell** o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="496b2-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="496b2-160">Verrà visualizzato l'output iniziale, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="496b2-160">You will see the initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="496b2-161">Dopo qualche minuto, inserire le credenziali nella casella di richiesta e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="496b2-161">After a few minutes, fill out the credentials prompt and click **OK**.</span></span> <span data-ttu-id="496b2-162">L'output seguente rappresenta una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="496b2-162">The output below represents a single VM.</span></span> <span data-ttu-id="496b2-163">Si noti che per il completamento dell'intero processo sono stati necessari 8 minuti.</span><span class="sxs-lookup"><span data-stu-id="496b2-163">Notice the entire process took 8 minutes to complete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
