---
title: una rete virtuale - CLI di Azure 2.0 aaaCreate | Documenti Microsoft
description: Informazioni su come una rete virtuale utilizzando toocreate hello CLI di Azure 2.0.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="07c42-103">Creare una rete virtuale usando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="07c42-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="07c42-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="07c42-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="07c42-105">Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="07c42-106">altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="07c42-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="07c42-107">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="07c42-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="07c42-108">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="07c42-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="07c42-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07c42-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="07c42-110">[Azure CLI 2.0](#create-a-virtual-network) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)'</span><span class="sxs-lookup"><span data-stu-id="07c42-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="07c42-111">È anche possibile creare una rete virtuale tramite Gestione risorse di usare altri strumenti o creare una rete virtuale tramite il modello di distribuzione classica hello selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="07c42-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07c42-112">Portale</span><span class="sxs-lookup"><span data-stu-id="07c42-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="07c42-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07c42-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="07c42-114">CLI</span><span class="sxs-lookup"><span data-stu-id="07c42-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="07c42-115">Modello</span><span class="sxs-lookup"><span data-stu-id="07c42-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="07c42-116">Portale (versione classica)</span><span class="sxs-lookup"><span data-stu-id="07c42-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="07c42-117">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="07c42-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="07c42-118">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="07c42-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="07c42-119">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="07c42-119">Create a virtual network</span></span>

<span data-ttu-id="07c42-120">una rete virtuale utilizzando toocreate hello CLI di Azure 2.0, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07c42-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="07c42-121">Installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="07c42-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="07c42-122">Creare un gruppo di risorse per una rete virtuale usando hello [gruppo az creare](/cli/azure/group#create) con hello `--name` e `--location` argomenti:</span><span class="sxs-lookup"><span data-stu-id="07c42-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="07c42-123">Creare una rete virtuale e subnet:</span><span class="sxs-lookup"><span data-stu-id="07c42-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="07c42-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="07c42-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="07c42-125">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="07c42-125">Parameters used:</span></span>

    - <span data-ttu-id="07c42-126">`--name TestVNet`: Nome di hello toobe di rete virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="07c42-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="07c42-127">`--resource-group TestRG`: # hello Nome gruppo di risorse che controlla la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="07c42-128">`--location centralus`: posizione in cui toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="07c42-129">`--address-prefix 192.168.0.0/16`: hello prefisso dell'indirizzo e blocco.</span><span class="sxs-lookup"><span data-stu-id="07c42-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="07c42-130">`--subnet-name FrontEnd`: nome hello della subnet di hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="07c42-131">`--subnet-prefix 192.168.1.0/24`: hello prefisso dell'indirizzo e blocco.</span><span class="sxs-lookup"><span data-stu-id="07c42-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="07c42-132">toouse di informazioni di base toolist hello in hello successivo comando, è possibile eseguire query tramite rete virtuale hello un [filtro query](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="07c42-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="07c42-133">Che produce hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="07c42-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="07c42-134">Creare una subnet:</span><span class="sxs-lookup"><span data-stu-id="07c42-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="07c42-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="07c42-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="07c42-136">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="07c42-136">Parameters used:</span></span>

    - <span data-ttu-id="07c42-137">`--address-prefix 192.168.2.0/24`: blocco CIDR della subnet.</span><span class="sxs-lookup"><span data-stu-id="07c42-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="07c42-138">`--name BackEnd`: Nome della nuova subnet hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="07c42-139">`--resource-group TestRG`: il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="07c42-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="07c42-140">`--vnet-name TestVNet`: nome hello di hello proprietario rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="07c42-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="07c42-141">Proprietà hello query di hello nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="07c42-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="07c42-142">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="07c42-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="07c42-143">Eseguire query su proprietà hello di subnet hello:</span><span class="sxs-lookup"><span data-stu-id="07c42-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="07c42-144">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="07c42-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="07c42-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07c42-145">Next steps</span></span>

<span data-ttu-id="07c42-146">Informazioni su come tooconnect:</span><span class="sxs-lookup"><span data-stu-id="07c42-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="07c42-147">Una rete virtuale tooa di macchina virtuale (VM) leggendo hello [creare una VM Linux](../virtual-machines/linux/quick-create-cli.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="07c42-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="07c42-148">Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="07c42-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="07c42-149">Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="07c42-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="07c42-150">rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07c42-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="07c42-151">Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="07c42-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
