---
title: "Creare una VM con più schede di interfaccia di rete - interfaccia della riga di comando 1.0 di Azure| Documentazione Microsoft"
description: "Informazioni su come creare una VM con più schede di interfaccia di rete usando l'interfaccia della riga di comando 1.0 di Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b95bcb38664718bf25ec6981c803415790c6da3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="bb9c4-103">Creare una VM con più schede di interfaccia di rete usando l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="bb9c4-103">Create a VM with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bb9c4-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="bb9c4-105">Questo articolo illustra il modello di distribuzione Resource Manager che Microsoft consiglia di usare per le distribuzioni più recenti in sostituzione del [modello di distribuzione classica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="bb9c4-106">La procedura seguente usa un gruppo di risorse denominato *IaaSStory* per i server Web e un gruppo di risorse denominato *IaaSStory-BackEnd* per i server di database.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span> <span data-ttu-id="bb9c4-107">È possibile completare questa attività usando l'interfaccia della riga di comando di Azure 1.0 (questo articolo) o l'[interfaccia della riga di comando di Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-107">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="bb9c4-108">I valori in "" per le variabili nei passaggi seguenti creano le risorse con le impostazioni usate nello scenario.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="bb9c4-109">Sostituire i valori in base alle esigenze specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-109">Change the values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb9c4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb9c4-110">Prerequisites</span></span>
<span data-ttu-id="bb9c4-111">Prima di creare i server di database, è necessario creare il gruppo di risorse *IaaSStory* con tutte le risorse richieste per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-111">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="bb9c4-112">Per creare le risorse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bb9c4-112">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="bb9c4-113">Passare alla [pagina del modello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-113">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="bb9c4-114">Nella pagina del modello, a destra del **gruppo di risorse padre**, fare clic su **Distribuisci in Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-114">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="bb9c4-115">Se necessario, modificare i valori dei parametri, quindi seguire i passaggi nel portale di anteprima di Azure per distribuire il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-115">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb9c4-116">Assicurarsi che i nomi degli account di archiviazione siano univoci.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="bb9c4-117">In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="bb9c4-118">Creare le macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="bb9c4-118">Create the back-end VMs</span></span>
<span data-ttu-id="bb9c4-119">Le macchine virtuali di back-end dipendono dalla creazione delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb9c4-119">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="bb9c4-120">**Account di archiviazione per i dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-120">**Storage account for data disks**.</span></span> <span data-ttu-id="bb9c4-121">Per migliorare le prestazioni, i dischi dati sui server di database utilizzano la tecnologia SSD (Solid State Drive), che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-121">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="bb9c4-122">Verificare che la posizione di Azure distribuita supporti l'archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-122">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="bb9c4-123">**Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-123">**NICs**.</span></span> <span data-ttu-id="bb9c4-124">Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="bb9c4-125">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-125">**Availability set**.</span></span> <span data-ttu-id="bb9c4-126">Tutti i server di database vengono aggiunti a un singolo set di disponibilità, per garantire che almeno una delle macchine virtuali sia attiva e in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="bb9c4-127">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="bb9c4-127">Step 1 - Start your script</span></span>
<span data-ttu-id="bb9c4-128">È possibile scaricare lo script di bash completo utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-128">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="bb9c4-129">Attenersi alla procedura seguente per modificare lo script da usare nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="bb9c4-130">Modificare i valori delle variabili indicate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [Prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="bb9c4-131">Modificare i valori delle variabili indicate di seguito in base ai valori che si desidera usare per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="bb9c4-132">Recuperare l'ID per la subnet `BackEnd` in cui verranno create le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-132">Retrieve the ID for the `BackEnd` subnet where the VMs will be created.</span></span> <span data-ttu-id="bb9c4-133">È necessario farlo poiché le schede di rete associate a questa subnet si trovano in un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-133">You need to do this since the NICs to be associated to this subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="bb9c4-134">Il primo comando precedente usa [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) e [manipolazione delle stringhe](http://tldp.org/LDP/abs/html/string-manipulation.html) (in particolare, la rimozione di sottostringhe).</span><span class="sxs-lookup"><span data-stu-id="bb9c4-134">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="bb9c4-135">Recuperare l'ID per l’NSG `NSG-RemoteAccess` .</span><span class="sxs-lookup"><span data-stu-id="bb9c4-135">Retrieve the ID for the `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="bb9c4-136">È necessario farlo poiché le schede di rete associate a tale NSG sono in un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-136">You need to do this since the NICs to be associated to this NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="bb9c4-137">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="bb9c4-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="bb9c4-138">Creare un nuovo gruppo di risorse per tutte le risorse back-end.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="bb9c4-139">Si noti l'utilizzo della variabile `$backendRGName` per il nome del gruppo di risorse e `$location` per l'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-139">Notice the use of the `$backendRGName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="bb9c4-140">Creare un account di archiviazione premium per i dischi dati e il sistema operativo da usare per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-140">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="bb9c4-141">Creare un set di disponibilità per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-141">Create an availability set for the VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="bb9c4-142">Passaggio 3 - Creare le schede di rete e le macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="bb9c4-142">Step 3 - Create the NICs and back-end VMs</span></span>

1. <span data-ttu-id="bb9c4-143">Avviare un ciclo per creare più macchine virtuali, in base alle `numberOfVMs` variabili.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-143">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="bb9c4-144">Per ogni macchina virtuale, creare una scheda di rete per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="bb9c4-145">Per ogni macchina virtuale, creare una scheda di rete per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="bb9c4-146">Si noti il parametro `--network-security-group` utilizzato per associare la scheda di rete a un NSG.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-146">Notice the `--network-security-group` parameter, used to associate the NIC to an NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="bb9c4-147">Creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-147">Create the VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="bb9c4-148">Per ogni macchina virtuale, creare due dischi dati e terminare il ciclo con il comando `done` .</span><span class="sxs-lookup"><span data-stu-id="bb9c4-148">For each VM, create two data disks, and end the loop with the `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="bb9c4-149">Passaggio 4 - eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-149">Step 4 - Run the script</span></span>
<span data-ttu-id="bb9c4-150">Una volta scaricato e modificato lo script in base alle esigenze, eseguire lo script per creare macchine virtuali del database di back-end con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-150">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="bb9c4-151">Salvare lo script ed eseguirlo dal terminale **Bash** .</span><span class="sxs-lookup"><span data-stu-id="bb9c4-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="bb9c4-152">Verrà visualizzato l'output iniziale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-152">You will see the initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up the availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up the network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up the network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB1"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB1-DA"
        info:    Looking up the NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="bb9c4-153">Dopo alcuni minuti, l'esecuzione verrà terminata e il resto dell'output verrà visualizzato come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bb9c4-153">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up the network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up the network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB2"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB2-DA"
        info:    Looking up the NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

