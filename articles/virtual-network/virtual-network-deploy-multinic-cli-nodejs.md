---
title: "una macchina virtuale con più schede di rete - CLI di Azure 1.0 aaaCreate | Documenti Microsoft"
description: "Informazioni su come una macchina virtuale con più schede di rete utilizzando toocreate hello Azure CLI 1.0."
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
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="4ec6b-103">Creare una macchina virtuale con più schede di rete utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4ec6b-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="4ec6b-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="4ec6b-105">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="4ec6b-106">i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="4ec6b-107">È possibile completare questa attività usando hello Azure CLI 1.0 (in questo articolo) o hello [CLI di Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="4ec6b-108">valori Hello "" per le variabili di hello nei passaggi hello che seguono creano risorse con le impostazioni da uno scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="4ec6b-109">Modificare i valori hello, come appropriato, per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ec6b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ec6b-110">Prerequisites</span></span>
<span data-ttu-id="4ec6b-111">Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="4ec6b-112">completare queste risorse, toocreate hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ec6b-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="4ec6b-113">Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="4ec6b-114">Nella pagina toohello destra del modello di hello **gruppo di risorse padre**, fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="4ec6b-115">Se necessario, modificare i valori di parametro hello, quindi seguire i passaggi hello nel gruppo di risorse hello toodeploy portale hello anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ec6b-116">Assicurarsi che i nomi degli account di archiviazione siano univoci.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="4ec6b-117">In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="4ec6b-118">Creare macchine virtuali di back-end di hello</span><span class="sxs-lookup"><span data-stu-id="4ec6b-118">Create hello back-end VMs</span></span>
<span data-ttu-id="4ec6b-119">Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="4ec6b-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="4ec6b-120">**Account di archiviazione per dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-120">**Storage account for data disks**.</span></span> <span data-ttu-id="4ec6b-121">Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="4ec6b-122">Verificare che hello distribuire archiviazione premium toosupport località di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="4ec6b-123">**Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-123">**NICs**.</span></span> <span data-ttu-id="4ec6b-124">Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="4ec6b-125">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-125">**Availability set**.</span></span> <span data-ttu-id="4ec6b-126">Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="4ec6b-127">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="4ec6b-127">Step 1 - Start your script</span></span>
<span data-ttu-id="4ec6b-128">È possibile scaricare script bash completo hello utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="4ec6b-129">Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="4ec6b-130">Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="4ec6b-131">Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

3. <span data-ttu-id="4ec6b-132">Recuperare l'ID di hello per hello `BackEnd` subnet in cui verrà creato hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="4ec6b-133">È necessario toodo questo poiché hello NIC associata toobe toothis subnet presenti in un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="4ec6b-134">primo comando precedente viene Hello [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) e [la manipolazione delle stringhe](http://tldp.org/LDP/abs/html/string-manipulation.html) (in particolare, la rimozione di sottostringa).</span><span class="sxs-lookup"><span data-stu-id="4ec6b-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="4ec6b-135">Recuperare l'ID di hello per hello `NSG-RemoteAccess` gruppo.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="4ec6b-136">È necessario toodo questo poiché NIC toobe hello associata toothis NSG si trovano in un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="4ec6b-137">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4ec6b-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="4ec6b-138">Creare un nuovo gruppo di risorse per tutte le risorse back-end.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="4ec6b-139">Utilizzo di hello preavviso di hello `$backendRGName` variabile per nome gruppo di risorse hello e `$location` per hello regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="4ec6b-140">Creare un account di archiviazione premium per hello del sistema operativo e toobe dischi di dati utilizzato dal tuo macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="4ec6b-141">Creare un set di disponibilità per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="4ec6b-142">Passaggio 3: creare le schede NIC hello e macchine virtuali di back-end</span><span class="sxs-lookup"><span data-stu-id="4ec6b-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="4ec6b-143">Avviare un ciclo toocreate più macchine virtuali, in base a hello `numberOfVMs` variabili.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="4ec6b-144">Per ogni macchina virtuale, creare una scheda di rete per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-144">For each VM, create a NIC for database access.</span></span>

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

3. <span data-ttu-id="4ec6b-145">Per ogni macchina virtuale, creare una scheda di rete per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="4ec6b-146">Hello preavviso `--network-security-group` tooassociate utilizzati hello NIC tooan NSG parametro.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

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

4. <span data-ttu-id="4ec6b-147">Creare VM hello.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-147">Create hello VM.</span></span>

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

5. <span data-ttu-id="4ec6b-148">Per ogni macchina virtuale, creare dischi dati di due e il ciclo di hello fine con hello `done` comando.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

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

### <a name="step-4---run-hello-script"></a><span data-ttu-id="4ec6b-149">Passaggio 4: hello Esegui script</span><span class="sxs-lookup"><span data-stu-id="4ec6b-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="4ec6b-150">Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, eseguire nuovamente hello toocreate di script hello terminare le macchine virtuali di database con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="4ec6b-151">Salvare lo script ed eseguirlo dal terminale **Bash** .</span><span class="sxs-lookup"><span data-stu-id="4ec6b-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="4ec6b-152">Verrà visualizzato un output iniziale hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-152">You will see hello initial output, as shown below.</span></span>
   
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
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
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
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
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
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="4ec6b-153">Dopo alcuni minuti, l'esecuzione hello terminerà e verrà visualizzato rest hello dell'output di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4ec6b-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
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
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
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
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

