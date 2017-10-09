---
title: "una macchina virtuale (versione classica) con più schede di rete - CLI di Azure 1.0 aaaCreate | Documenti Microsoft"
description: "Informazioni su come una macchina virtuale (versione classica) con più schede di rete utilizzando toocreate hello Azure interfaccia della riga di comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="a9401-103">Creare una macchina virtuale (versione classica) con più schede di rete utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a9401-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="a9401-104">È possibile creare macchine virtuali (VM) in Azure e collegare più tooeach (NIC) di interfacce di rete delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a9401-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="a9401-105">Più schede di interfaccia rete consentono la separazione dei tipi di traffico tra schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a9401-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="a9401-106">Ad esempio, una che scheda di rete può comunicare con hello Internet, mentre l'altra comunica solo con le risorse interne non connessi toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="a9401-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="a9401-107">Hello possibilità tooseparate il traffico di rete tra più schede di rete è necessario per molti dispositivi virtuali di rete, ad esempio distribuzione delle applicazioni e soluzioni per l'ottimizzazione WAN.</span><span class="sxs-lookup"><span data-stu-id="a9401-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9401-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a9401-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a9401-109">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="a9401-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a9401-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="a9401-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a9401-111">Informazioni su come tooperform questi passaggi tramite hello [il modello di distribuzione di gestione risorse](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9401-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="a9401-112">i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.</span><span class="sxs-lookup"><span data-stu-id="a9401-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9401-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a9401-113">Prerequisites</span></span>
<span data-ttu-id="a9401-114">Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="a9401-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="a9401-115">toocreate queste risorse, completate hello passaggi che seguono.</span><span class="sxs-lookup"><span data-stu-id="a9401-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="a9401-116">Creare una rete virtuale seguendo i passaggi hello hello [creare una rete virtuale](virtual-networks-create-vnet-classic-cli.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="a9401-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="a9401-117">Hello back-end di distribuire le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a9401-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="a9401-118">Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="a9401-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="a9401-119">**Account di archiviazione per dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="a9401-119">**Storage account for data disks**.</span></span> <span data-ttu-id="a9401-120">Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="a9401-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="a9401-121">Verificare che hello distribuire archiviazione premium toosupport località di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9401-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="a9401-122">**Schede di rete**.</span><span class="sxs-lookup"><span data-stu-id="a9401-122">**NICs**.</span></span> <span data-ttu-id="a9401-123">Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.</span><span class="sxs-lookup"><span data-stu-id="a9401-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="a9401-124">**Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="a9401-124">**Availability set**.</span></span> <span data-ttu-id="a9401-125">Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="a9401-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="a9401-126">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="a9401-126">Step 1 - Start your script</span></span>
<span data-ttu-id="a9401-127">È possibile scaricare script bash completo hello utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="a9401-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="a9401-128">Completare hello seguendo i passaggi toochange hello script toowork nell'ambiente in uso:</span><span class="sxs-lookup"><span data-stu-id="a9401-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="a9401-129">Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a9401-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="a9401-130">Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="a9401-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="a9401-131">Passaggio 2 - creare le risorse necessarie per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a9401-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="a9401-132">Creare un nuovo servizio cloud per tutte le macchine virtuali di back-end.</span><span class="sxs-lookup"><span data-stu-id="a9401-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="a9401-133">Utilizzo di hello preavviso di hello `$backendCSName` variabile per nome gruppo di risorse hello e `$location` per hello regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9401-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="a9401-134">Creare un account di archiviazione premium per hello del sistema operativo e toobe dischi di dati utilizzato dal tuo macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a9401-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="a9401-135">Passaggio 3 - creare macchine virtuali con più NIC</span><span class="sxs-lookup"><span data-stu-id="a9401-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="a9401-136">Avviare un ciclo toocreate più macchine virtuali, in base a hello `numberOfVMs` variabili.</span><span class="sxs-lookup"><span data-stu-id="a9401-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="a9401-137">Per ogni macchina virtuale, specificare il nome di hello e indirizzo IP di ogni hello due schede di rete.</span><span class="sxs-lookup"><span data-stu-id="a9401-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="a9401-138">Creare VM hello.</span><span class="sxs-lookup"><span data-stu-id="a9401-138">Create hello VM.</span></span> <span data-ttu-id="a9401-139">Notare l'utilizzo di hello di hello `--nic-config` contenente un elenco di tutte le NIC con indirizzo IP, subnet e nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="a9401-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="a9401-140">Per ogni macchina virtuale, creare due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="a9401-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="a9401-141">Passaggio 4: hello Esegui script</span><span class="sxs-lookup"><span data-stu-id="a9401-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="a9401-142">Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, eseguire nuovamente hello toocreate di script hello terminare le macchine virtuali di database con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="a9401-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="a9401-143">Salvare lo script ed eseguirlo dal terminale **Bash** .</span><span class="sxs-lookup"><span data-stu-id="a9401-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="a9401-144">Verrà visualizzato un output iniziale hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a9401-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="a9401-145">Dopo alcuni minuti, l'esecuzione hello terminerà e verrà visualizzato rest hello dell'output di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a9401-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
