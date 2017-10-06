---
title: "una macchina virtuale con più schede di rete - Azure PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una macchina virtuale con più schede di rete con PowerShell."
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
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="936a4-103">Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="936a4-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="936a4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="936a4-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="936a4-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="936a4-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="936a4-106">Modello</span><span class="sxs-lookup"><span data-stu-id="936a4-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * <span data-ttu-id="936a4-107">[PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="936a4-107">[PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md)</span></span>
> * [<span data-ttu-id="936a4-108">Interfaccia della riga di comando di Azure (versione classica)</span><span class="sxs-lookup"><span data-stu-id="936a4-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="936a4-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="936a4-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="936a4-110">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="936a4-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="936a4-111">i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.</span><span class="sxs-lookup"><span data-stu-id="936a4-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="936a4-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="936a4-112">Prerequisites</span></span>
<span data-ttu-id="936a4-113">Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="936a4-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="936a4-114">completare queste risorse, toocreate hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="936a4-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="936a4-115">Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="936a4-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="936a4-116">Nella pagina toohello destra del modello di hello **gruppo di risorse padre**, fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="936a4-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="936a4-117">Se necessario, modificare i valori di parametro hello, quindi seguire i passaggi hello nel gruppo di risorse hello toodeploy portale hello anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="936a4-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="936a4-118">Assicurarsi che i nomi degli account di archiviazione siano univoci.</span><span class="sxs-lookup"><span data-stu-id="936a4-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="936a4-119">In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="936a4-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="936a4-120">Creare macchine virtuali di back-end di hello</span><span class="sxs-lookup"><span data-stu-id="936a4-120">Create hello back-end VMs</span></span>
<span data-ttu-id="936a4-121">Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="936a4-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="936a4-122">**Account di archiviazione per dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="936a4-122">**Storage account for data disks**.</span></span> <span data-ttu-id="936a4-123">Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="936a4-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="936a4-124">Verificare che hello distribuire archiviazione premium toosupport località di Azure.</span><span class="sxs-lookup"><span data-stu-id="936a4-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="936a4-125">**Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="936a4-125">**NICs**.</span></span> <span data-ttu-id="936a4-126">Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.</span><span class="sxs-lookup"><span data-stu-id="936a4-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="936a4-127">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="936a4-127">**Availability set**.</span></span> <span data-ttu-id="936a4-128">Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="936a4-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="936a4-129">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="936a4-129">Step 1 - Start your script</span></span>
<span data-ttu-id="936a4-130">È possibile scaricare hello completo script di PowerShell utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="936a4-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="936a4-131">Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="936a4-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="936a4-132">Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="936a4-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="936a4-133">Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="936a4-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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
3. <span data-ttu-id="936a4-134">Recuperare le risorse esistenti di hello necessari per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="936a4-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="936a4-135">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="936a4-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="936a4-136">È necessario un nuovo gruppo di risorse, un account di archiviazione per i dischi dati hello, toocreate e un gruppo di disponibilità per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="936a4-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="936a4-137">Le credenziali dell'account amministratore locale hello è alos necessario per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="936a4-138">esecuzione di queste risorse, toocreate hello i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="936a4-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="936a4-139">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="936a4-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="936a4-140">Creare un nuovo account di archiviazione premium, nel gruppo di risorse hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="936a4-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="936a4-141">Creare un nuovo set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="936a4-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="936a4-142">Ottenere l'amministratore locale hello toobe le credenziali di account utilizzato per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="936a4-143">Passaggio 3: creare le schede NIC hello e macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="936a4-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="936a4-144">È necessario un ciclo di toocreate toouse come più macchine virtuali che desidera e creare hello necessarie schede di rete e le macchine virtuali all'interno di ciclo hello.</span><span class="sxs-lookup"><span data-stu-id="936a4-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="936a4-145">hello toocreate schede di rete e le macchine virtuali, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="936a4-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="936a4-146">Avviare un `for` hello toorepeat ciclo comandi toocreate una macchina virtuale e due schede di rete come numero di volte in base alle esigenze, in base al valore di hello di hello `$numberOfVMs` variabile.</span><span class="sxs-lookup"><span data-stu-id="936a4-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="936a4-147">Creare hello che NIC utilizzato per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="936a4-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="936a4-148">Creare hello che NIC utilizzato per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="936a4-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="936a4-149">Si noti come questa scheda di rete ha un tooit di gruppo associata.</span><span class="sxs-lookup"><span data-stu-id="936a4-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="936a4-150">Creare l'oggetto `vmConfig` .</span><span class="sxs-lookup"><span data-stu-id="936a4-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="936a4-151">Creare due dischi dati per ciascuna macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-151">Create two data disks per VM.</span></span> <span data-ttu-id="936a4-152">Notare che i dischi dati hello in account di archiviazione premium hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="936a4-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

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

6. <span data-ttu-id="936a4-153">Configurare hello del sistema operativo e immagine toobe utilizzato per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="936a4-154">Aggiungere hello due schede di rete creati in precedenza toohello `vmConfig` oggetto.</span><span class="sxs-lookup"><span data-stu-id="936a4-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="936a4-155">Creare disco del sistema operativo hello e hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="936a4-156">Hello preavviso `}` finale hello `for` ciclo.</span><span class="sxs-lookup"><span data-stu-id="936a4-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="936a4-157">Passaggio 4: hello Esegui script</span><span class="sxs-lookup"><span data-stu-id="936a4-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="936a4-158">Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, Run ha script di database di back-end hello toocreate le macchine virtuali con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="936a4-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="936a4-159">Salvare lo script ed eseguirlo da hello **PowerShell** prompt dei comandi o **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="936a4-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="936a4-160">Verrà visualizzato l'output di hello iniziale, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="936a4-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="936a4-161">Dopo alcuni minuti, compilare la richiesta di credenziali hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="936a4-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="936a4-162">output di Hello seguente rappresenta una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="936a4-162">hello output below represents a single VM.</span></span> <span data-ttu-id="936a4-163">Si noti hello intero processo ha impiegato toocomplete 8 minuti.</span><span class="sxs-lookup"><span data-stu-id="936a4-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

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
