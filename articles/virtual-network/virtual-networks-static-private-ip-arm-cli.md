---
title: Configurare indirizzi IP privati per le VM - interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Informazioni su come configurare indirizzi IP privati per le macchine virtuali usando l'interfaccia della riga di comando di Azure 2.0.
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
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="fc6dd-103">Configurare indirizzi IP privati per una macchina virtuale usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="fc6dd-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="fc6dd-104">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="fc6dd-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="fc6dd-105">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="fc6dd-106">[Interfaccia della riga di comando di Azure 1.0](virtual-networks-static-private-ip-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classici e di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="fc6dd-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="fc6dd-107">[Interfaccia della riga di comando di Azure 2.0](#specify-a-static-private-ip-address-when-creating-a-vm): interfaccia avanzata per il modello di distribuzione di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="fc6dd-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="fc6dd-108">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="fc6dd-109">È anche possibile [gestire un indirizzo IP statico privato nel modello di distribuzione classico](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="fc6dd-110">I comandi di esempio dell'interfaccia della riga di comando di Azure 2.0 seguenti prevedono un ambiente semplice già creato.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="fc6dd-111">Se si desidera eseguire i comandi illustrati in questo documento, creare innanzitutto l'ambiente di prova descritto in [creare una rete virtuale](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="fc6dd-112">Specificare un indirizzo IP statico privato durante la creazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6dd-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="fc6dd-113">Per creare una VM denominata *DNS01* nella subnet *FrontEnd* di una rete virtuale denominata *TestVNet* con un indirizzo IP statico privato di *192.168.1.101*, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="fc6dd-114">Se questa operazione non è stata ancora eseguita, installare e configurare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure usando il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="fc6dd-115">Creare un IP pubblico per la VM con il comando [azure network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="fc6dd-116">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fc6dd-117">Potrebbe essere possibile o necessario usare valori diversi per gli argomenti in questo passaggio e nei passaggi successivi, a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="fc6dd-118">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="fc6dd-119">`--resource-group`: nome del gruppo di risorse in cui creare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="fc6dd-120">`--name`: nome dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="fc6dd-121">`--location`: area di Azure in cui creare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="fc6dd-122">Eseguire il comando [az network nic create](/cli/azure/network/nic#create) per creare una scheda di interfaccia di rete con indirizzo IP privato statico.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="fc6dd-123">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="fc6dd-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="fc6dd-125">Parametri</span><span class="sxs-lookup"><span data-stu-id="fc6dd-125">Parameters:</span></span>

    * <span data-ttu-id="fc6dd-126">`--private-ip-address`: indirizzo IP privato statico per la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="fc6dd-127">`--vnet-name`: nome della rete virtuale in cui creare la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="fc6dd-128">`--subnet`: nome della subnet in cui creare la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="fc6dd-129">Eseguire il comando [azure vm create](/cli/azure/vm/nic#create) per creare la VM usando l'indirizzo IP pubblico e il gruppo NIC creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="fc6dd-130">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-130">The list shown after the output explains the parameters used.</span></span>
   
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

    <span data-ttu-id="fc6dd-131">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="fc6dd-132">Parametri diversi dai parametri di base [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="fc6dd-133">`--nics`: nome della scheda di interfaccia di rete a cui è collegata la VM.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="fc6dd-134">Recuperare le informazioni relative all'indirizzo IP privato statico per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6dd-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="fc6dd-135">Per visualizzare l'indirizzo IP privato statico creato, eseguire il comando seguente dell'interfaccia della riga di comando di Azure e osservare i valori di *Private IP alloc-method* e *Private IP address*:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="fc6dd-136">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="fc6dd-137">Per visualizzare informazioni sull'IP specifico della scheda di interfaccia di rete, eseguire una query sulla scheda di interfaccia di rete specifica:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="fc6dd-138">Il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="fc6dd-139">Rimuovere un indirizzo IP statico privato da una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fc6dd-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="fc6dd-140">Non è possibile rimuovere un indirizzo IP privato statico da una scheda di interfaccia di rete nell'interfaccia della riga di comando per le distribuzioni di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="fc6dd-141">È necessario:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-141">You must:</span></span>
- <span data-ttu-id="fc6dd-142">Creare una nuova scheda di interfaccia di rete che usa un indirizzo IP dinamico</span><span class="sxs-lookup"><span data-stu-id="fc6dd-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="fc6dd-143">Impostare la scheda di rete della VM sulla scheda di rete appena creata.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="fc6dd-144">Per cambiare la scheda di interfaccia di rete per la VM usata nei comandi precedenti, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="fc6dd-145">Eseguire il comando **azure network nic create** per creare una nuova scheda di interfaccia di rete usando l'allocazione di IP dinamica con un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="fc6dd-146">Si noti che poiché non è specificato alcun indirizzo IP, il metodo di allocazione è **dinamico**.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="fc6dd-147">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-147">Expected output:</span></span>

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

2. <span data-ttu-id="fc6dd-148">Eseguire il comando **azure vm set** per cambiare il gruppo NIC usato dalla VM.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="fc6dd-149">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fc6dd-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="fc6dd-150">Se le dimensioni della VM consentono di includere più schede di interfacce di rete, eseguire il comando **azure network nic delete** per eliminare la vecchia scheda.</span><span class="sxs-lookup"><span data-stu-id="fc6dd-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="fc6dd-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc6dd-151">Next steps</span></span>
* <span data-ttu-id="fc6dd-152">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="fc6dd-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fc6dd-153">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="fc6dd-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fc6dd-154">Consultare le [API REST dell'indirizzo IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc6dd-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

