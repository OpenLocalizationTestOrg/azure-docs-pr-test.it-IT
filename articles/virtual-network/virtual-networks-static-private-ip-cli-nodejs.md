---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello Azure interfaccia della riga di comando (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="d1a84-103">Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d1a84-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d1a84-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="d1a84-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d1a84-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="d1a84-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d1a84-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="d1a84-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d1a84-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -CLI la prossima generazione per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="d1a84-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d1a84-108">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d1a84-109">È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d1a84-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="d1a84-110">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="d1a84-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="d1a84-111">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d1a84-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="d1a84-112">Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d1a84-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="d1a84-113">una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="d1a84-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d1a84-114">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d1a84-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d1a84-115">Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1a84-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="d1a84-116">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="d1a84-117">Eseguire hello **public-ip di rete di azure creare** toocreate un indirizzo IP pubblico per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1a84-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="d1a84-118">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="d1a84-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="d1a84-119">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="d1a84-120">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="d1a84-121">Nome dell'IP pubblico hello hello risorsa gruppo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="d1a84-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="d1a84-122">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-122">**-n (or --name)**.</span></span> <span data-ttu-id="d1a84-123">Nome dell'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="d1a84-124">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-124">**-l (or --location)**.</span></span> <span data-ttu-id="d1a84-125">Area di Azure in cui verrà creato l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="d1a84-126">Per questo scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="d1a84-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="d1a84-127">Eseguire hello **nic di rete di azure creare** toocreate comando una scheda di rete con un indirizzo IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="d1a84-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="d1a84-128">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="d1a84-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="d1a84-129">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="d1a84-130">**-a (o --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="d1a84-131">Indirizzo IP privato statico per hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="d1a84-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="d1a84-132">**-m (o --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="d1a84-133">Nome della rete virtuale in cui verrà creato hello NIC hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="d1a84-134">**-k (o --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="d1a84-135">Nome della subnet hello in cui verrà creato hello NIC.</span><span class="sxs-lookup"><span data-stu-id="d1a84-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="d1a84-136">Eseguire hello **macchina virtuale di azure creare** comando toocreate hello macchina virtuale con indirizzo IP pubblico hello e scheda di rete creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d1a84-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="d1a84-137">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="d1a84-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="d1a84-138">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="d1a84-139">**-y (o --os-type)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="d1a84-140">Tipo di sistema sia per la macchina virtuale, hello *Windows* o *Linux*.</span><span class="sxs-lookup"><span data-stu-id="d1a84-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="d1a84-141">**-f (o --nic-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="d1a84-142">Nome di hello NIC hello VM utilizzerà.</span><span class="sxs-lookup"><span data-stu-id="d1a84-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="d1a84-143">**-i (o --public-ip-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="d1a84-144">Nome di hello IP pubblico hello VM utilizzerà.</span><span class="sxs-lookup"><span data-stu-id="d1a84-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="d1a84-145">**-F (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="d1a84-146">Nome della rete virtuale in cui verrà creato hello VM hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="d1a84-147">**-j (o --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d1a84-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="d1a84-148">Nome della subnet hello in cui verrà creato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1a84-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="d1a84-149">Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d1a84-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="d1a84-150">IP privato statico di tooview hello informazioni sull'indirizzo di hello macchina virtuale creata con lo script hello precedente, eseguire il comando CLI di Azure seguente hello e osservare i valori hello per *IP privato alloc (metodo)* e *indirizzo IP privato*:</span><span class="sxs-lookup"><span data-stu-id="d1a84-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="d1a84-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="d1a84-152">Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d1a84-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="d1a84-153">Non è possibile rimuovere un indirizzo IP privato statico da un gruppo NIC nell'infrastruttura CLI di Azure per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d1a84-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="d1a84-154">È necessario creare una nuova scheda di rete che utilizza un indirizzo IP dinamico, rimuovere hello NIC precedente da hello macchina virtuale e quindi aggiungere hello toohello NIC nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1a84-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="d1a84-155">toochange hello NIC per hello VM usata int eh comandi precedenti, attenersi alla procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1a84-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="d1a84-156">Eseguire hello **nic di rete di azure creare** comando toocreate una scheda di rete di nuovo utilizzando l'allocazione dell'IP dinamico.</span><span class="sxs-lookup"><span data-stu-id="d1a84-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="d1a84-157">Si noti come non è necessario l'indirizzo IP hello toospecify questo momento.</span><span class="sxs-lookup"><span data-stu-id="d1a84-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="d1a84-158">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="d1a84-159">Eseguire hello **set di macchine virtuali di azure** comando toochange hello scheda di rete utilizzata dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d1a84-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="d1a84-160">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="d1a84-161">Se si desidera, eseguire hello **nic di rete di azure Elimina** comando toodelete hello vecchia interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="d1a84-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="d1a84-162">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="d1a84-163">Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="d1a84-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="d1a84-164">tooadd un statico privato IP indirizzo toohello scheda di rete utilizzata dalla macchina virtuale creata utilizzando lo script hello precedente, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d1a84-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="d1a84-165">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d1a84-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="d1a84-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1a84-166">Next steps</span></span>
* <span data-ttu-id="d1a84-167">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="d1a84-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d1a84-168">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="d1a84-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d1a84-169">Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1a84-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

