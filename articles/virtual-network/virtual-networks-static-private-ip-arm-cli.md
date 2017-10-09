---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - CLI di Azure 2.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello Azure interfaccia della riga di comando (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="daa11-103">Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="daa11-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="daa11-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="daa11-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="daa11-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="daa11-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="daa11-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="daa11-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="daa11-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="daa11-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="daa11-108">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="daa11-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="daa11-109">È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="daa11-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="daa11-110">Hello esempio CLI di Azure 2.0 comandi riportati di seguito prevedono un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="daa11-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="daa11-111">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="daa11-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="daa11-112">Specificare un indirizzo IP statico privato durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="daa11-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="daa11-113">una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="daa11-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="daa11-114">Se non hai ancora, installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="daa11-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="daa11-115">Creare un indirizzo IP pubblico per hello VM con hello [az rete public-ip creare](/cli/azure/network/public-ip#create) comando.</span><span class="sxs-lookup"><span data-stu-id="daa11-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="daa11-116">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="daa11-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="daa11-117">È possibile preferibile o necessario toouse valori diversi per gli argomenti in questa e passaggi successivi, a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="daa11-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="daa11-118">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="daa11-119">`--resource-group`: Nome del gruppo di risorse hello toocreate hello IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="daa11-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="daa11-120">`--name`: Nome dell'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="daa11-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="daa11-121">`--location`: Azure area nella quale hello toocreate indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="daa11-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="daa11-122">Eseguire hello [az rete nic creare](/cli/azure/network/nic#create) toocreate comando una scheda di rete con un indirizzo IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="daa11-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="daa11-123">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="daa11-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="daa11-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="daa11-125">Parametri</span><span class="sxs-lookup"><span data-stu-id="daa11-125">Parameters:</span></span>

    * <span data-ttu-id="daa11-126">`--private-ip-address`: Indirizzo IP privato statico per hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="daa11-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="daa11-127">`--vnet-name`: Nome di rete virtuale hello in cui toocreate hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="daa11-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="daa11-128">`--subnet`: Nome della subnet di hello in cui hello toocreate scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="daa11-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="daa11-129">Eseguire hello [macchina virtuale di azure creare](/cli/azure/vm/nic#create) comando toocreate hello macchina virtuale con indirizzo IP pubblico hello e scheda di rete creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="daa11-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="daa11-130">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="daa11-130">hello list shown after hello output explains hello parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="daa11-131">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="daa11-132">I parametri diversi da hello base [creare vm az](/cli/azure/vm#create) parametri.</span><span class="sxs-lookup"><span data-stu-id="daa11-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="daa11-133">`--nics`: Nome di hello toowhich di hello NIC VM è collegato.</span><span class="sxs-lookup"><span data-stu-id="daa11-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="daa11-134">Recuperare le informazioni relative all'indirizzo IP privato statico per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="daa11-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="daa11-135">tooview hello indirizzo IP privato statico che è stato creato, eseguire il comando CLI di Azure seguente hello e osservare i valori hello per *IP privato alloc (metodo)* e *indirizzo IP privato*:</span><span class="sxs-lookup"><span data-stu-id="daa11-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="daa11-136">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="daa11-137">toodisplay hello informazioni IP specifiche di hello NIC per la macchina virtuale, hello query NIC in particolare:</span><span class="sxs-lookup"><span data-stu-id="daa11-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="daa11-138">output di Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="daa11-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="daa11-139">Rimuovere un indirizzo IP statico privato da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="daa11-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="daa11-140">Non è possibile rimuovere un indirizzo IP privato statico da una scheda di interfaccia di rete nell'interfaccia della riga di comando per le distribuzioni di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="daa11-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="daa11-141">È necessario:</span><span class="sxs-lookup"><span data-stu-id="daa11-141">You must:</span></span>
- <span data-ttu-id="daa11-142">Creare una nuova scheda di interfaccia di rete che usa un indirizzo IP dinamico</span><span class="sxs-lookup"><span data-stu-id="daa11-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="daa11-143">Impostare hello NIC in VM hello hello appena creati scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="daa11-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="daa11-144">toochange hello NIC per la macchina virtuale utilizzata in comandi hello precedenti, hello procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="daa11-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="daa11-145">Eseguire hello **nic di rete di azure creare** comando toocreate una scheda di rete di nuovo con un nuovo indirizzo IP di allocazione dell'IP dinamico.</span><span class="sxs-lookup"><span data-stu-id="daa11-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="daa11-146">Si noti che poiché non è specificato alcun indirizzo IP, il metodo di allocazione hello è **dinamica**.</span><span class="sxs-lookup"><span data-stu-id="daa11-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="daa11-147">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="daa11-148">Eseguire hello **set di macchine virtuali di azure** comando toochange hello scheda di rete utilizzata dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="daa11-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="daa11-149">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="daa11-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="daa11-150">Se hello VM è sufficientemente grande toohave più di una scheda di rete, eseguire hello **nic di rete di azure Elimina** comando toodelete hello vecchia interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="daa11-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="daa11-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daa11-151">Next steps</span></span>
* <span data-ttu-id="daa11-152">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="daa11-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="daa11-153">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="daa11-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="daa11-154">Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa11-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

