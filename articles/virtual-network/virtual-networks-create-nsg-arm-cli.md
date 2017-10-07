---
title: -i gruppi di sicurezza di rete aaaCreate 2.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate e distribuire i gruppi di sicurezza di rete utilizzando hello CLI di Azure 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="8f819-103">Creare gruppi di protezione utilizzando hello Azure CLI 2.0 di rete</span><span class="sxs-lookup"><span data-stu-id="8f819-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8f819-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="8f819-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="8f819-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="8f819-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="8f819-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="8f819-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="8f819-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="8f819-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="8f819-108">esempio Hello Azure CLI 2.0 i comandi seguenti prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="8f819-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="8f819-109">Creare hello NSG per hello `FrontEnd` subnet</span><span class="sxs-lookup"><span data-stu-id="8f819-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="8f819-110">un gruppo denominato toocreate *front-end di NSG* a seconda dello scenario hello precedente, attenersi alla seguente procedura hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="8f819-111">Se non hai ancora, installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8f819-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="8f819-112">Creare un gruppo utilizzando hello [rete az creare](/cli/azure/network/nsg#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="8f819-113">Parametri</span><span class="sxs-lookup"><span data-stu-id="8f819-113">Parameters:</span></span>
   
   * <span data-ttu-id="8f819-114">`--resource-group`: Nome del gruppo di risorse hello in cui è stato creato hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="8f819-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="8f819-115">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="8f819-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="8f819-116">`--location`: Azure area in cui hello nuovo gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="8f819-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="8f819-117">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="8f819-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="8f819-118">`--name`: Nome hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="8f819-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="8f819-119">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8f819-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="8f819-120">Hello è previsto output è gran parte delle informazioni tra un elenco di tutte le regole predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="8f819-121">Hello riportato di seguito le regole predefinite di hello con un filtro di query JMESPATH hello `table` formato di output:</span><span class="sxs-lookup"><span data-stu-id="8f819-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="8f819-122">Output:</span><span class="sxs-lookup"><span data-stu-id="8f819-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="8f819-123">Creare una regola che consente accesso tooport 3389 (RDP) da hello Internet con hello [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f819-124">A seconda della shell di hello in uso, potrebbe essere necessario toomodify hello `*` carattere negli argomenti di hello segue in modo da non tooexpand hello argomento prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8f819-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="8f819-125">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="8f819-126">Parametri</span><span class="sxs-lookup"><span data-stu-id="8f819-126">Parameters:</span></span>

    * <span data-ttu-id="8f819-127">`--resource-group testrg`: hello toouse gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f819-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="8f819-128">Si noti che non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8f819-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="8f819-129">`--nsg-name NSG-FrontEnd`: Nome del gruppo di hello in cui hello regola viene creata.</span><span class="sxs-lookup"><span data-stu-id="8f819-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="8f819-130">`--name rdp-rule`: Nome hello nuova regola.</span><span class="sxs-lookup"><span data-stu-id="8f819-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="8f819-131">`--access Allow`: Livello di accesso per la regola di hello (Deny o Consenti).</span><span class="sxs-lookup"><span data-stu-id="8f819-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="8f819-132">`--protocol Tcp`: protocollo (TCP, UDP o *).</span><span class="sxs-lookup"><span data-stu-id="8f819-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="8f819-133">`--direction Inbound`: Direzione di connessione hello (in entrata o in uscita).</span><span class="sxs-lookup"><span data-stu-id="8f819-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="8f819-134">`--priority 100`: Priorità per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="8f819-135">`--source-address-prefix Internet`: prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="8f819-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="8f819-136">`--source-port-range "*"`: porta o intervallo di porte di origine.</span><span class="sxs-lookup"><span data-stu-id="8f819-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="8f819-137">Porta che ha aperto la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="8f819-138">`--destination-address-prefix "*"`: prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="8f819-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="8f819-139">`--destination-port-range 3389`: porta o intervallo di porte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8f819-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="8f819-140">Porta che riceve la richiesta di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="8f819-141">Creare una regola che consente accesso tooport 80 (HTTP) da hello Internet **creare una regola gruppo rete az** comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="8f819-142">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="8f819-143">Associare hello NSG toohello **front-end** subnet con hello [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update) comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="8f819-144">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="8f819-145">Creare hello NSG per hello `BackEnd` subnet</span><span class="sxs-lookup"><span data-stu-id="8f819-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="8f819-146">un gruppo denominato toocreate *back-end di NSG* a seconda dello scenario hello precedente, attenersi alla seguente procedura hello.</span><span class="sxs-lookup"><span data-stu-id="8f819-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="8f819-147">Creare hello `NSG-BackEnd` NSG con **rete az creare**.</span><span class="sxs-lookup"><span data-stu-id="8f819-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="8f819-148">Passaggio 2, precedente, hello previsto output è notevole, incluse le regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="8f819-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="8f819-149">Creare una regola che consente accesso tooport 1433 (SQL) da hello `FrontEnd` subnet con hello **creare una regola gruppo rete az** comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="8f819-150">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="8f819-151">Creare una regola che nega l'accesso toohello Internet utilizzando hello **creare una regola gruppo rete az** comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="8f819-152">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="8f819-153">Associare hello NSG toohello `BackEnd` subnet utilizzando hello **set di subnet di rete virtuale di rete az** comando.</span><span class="sxs-lookup"><span data-stu-id="8f819-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="8f819-154">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="8f819-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
