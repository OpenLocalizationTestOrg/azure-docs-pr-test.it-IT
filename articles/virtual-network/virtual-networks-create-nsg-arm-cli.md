---
title: Creare i gruppi di sicurezza di rete - interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Informazioni su come creare e distribuire i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure 2.0.
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
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="cd294-103">Creare i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cd294-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cd294-104">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="cd294-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="cd294-105">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="cd294-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="cd294-106">[Interfaccia della riga di comando di Azure 1.0](virtual-networks-create-nsg-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classici e di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="cd294-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="cd294-107">[Interfaccia della riga di comando di Azure 2.0](#Create-the-nsg-for-the-front-end-subnet): interfaccia avanzata per il modello di distribuzione di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="cd294-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="cd294-108">I comandi di esempio dell'interfaccia della riga di comando di Azure 2.0 riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="cd294-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="cd294-109">Creare il gruppo di sicurezza di rete per la subnet `FrontEnd`</span><span class="sxs-lookup"><span data-stu-id="cd294-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="cd294-110">Per creare un gruppo di sicurezza di rete denominato *NSG-FrontEnd* in base allo scenario precedente, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cd294-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="cd294-111">Se questa operazione non è stata ancora eseguita, installare e configurare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure usando il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cd294-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="cd294-112">Creare un gruppo di sicurezza di rete usando il comando [azure network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="cd294-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="cd294-113">Parametri</span><span class="sxs-lookup"><span data-stu-id="cd294-113">Parameters:</span></span>
   
   * <span data-ttu-id="cd294-114">`--resource-group`: nome del gruppo di risorse in cui viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="cd294-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="cd294-115">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="cd294-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="cd294-116">`--location`: area di Azure in cui viene creato il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="cd294-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="cd294-117">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="cd294-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="cd294-118">`--name`: nome per il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="cd294-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="cd294-119">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="cd294-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="cd294-120">L'output previsto include svariate informazioni, tra cui un elenco di tutte le regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="cd294-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="cd294-121">L'esempio seguente mostra le regole predefinite usando un filtro di query JMESPATH con il formato di output `table`:</span><span class="sxs-lookup"><span data-stu-id="cd294-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="cd294-122">Output:</span><span class="sxs-lookup"><span data-stu-id="cd294-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="cd294-123">Creare una regola che consenta l'accesso alla porta 3389 (RDP) da Internet con il comando [azure network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="cd294-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cd294-124">A seconda della shell in uso potrebbe essere necessario modificare il carattere `*` negli argomenti seguenti per non espandere l'argomento prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cd294-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
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
   
    <span data-ttu-id="cd294-125">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-125">Expected output:</span></span>
   
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

    <span data-ttu-id="cd294-126">Parametri</span><span class="sxs-lookup"><span data-stu-id="cd294-126">Parameters:</span></span>

    * <span data-ttu-id="cd294-127">`--resource-group testrg`: il gruppo di risorse da usare.</span><span class="sxs-lookup"><span data-stu-id="cd294-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="cd294-128">Si noti che non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="cd294-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="cd294-129">`--nsg-name NSG-FrontEnd`: nome del gruppo di sicurezza di rete in cui viene creata la regola.</span><span class="sxs-lookup"><span data-stu-id="cd294-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="cd294-130">`--name rdp-rule`: nome per la nuova regola.</span><span class="sxs-lookup"><span data-stu-id="cd294-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="cd294-131">`--access Allow`: livello di accesso per la regola (Deny o Allow).</span><span class="sxs-lookup"><span data-stu-id="cd294-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="cd294-132">`--protocol Tcp`: protocollo (TCP, UDP o *).</span><span class="sxs-lookup"><span data-stu-id="cd294-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="cd294-133">`--direction Inbound`: direzione di connessione (Inbound o Outbound).</span><span class="sxs-lookup"><span data-stu-id="cd294-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="cd294-134">`--priority 100`: priorità per la regola.</span><span class="sxs-lookup"><span data-stu-id="cd294-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="cd294-135">`--source-address-prefix Internet`: prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cd294-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="cd294-136">`--source-port-range "*"`: porta o intervallo di porte di origine.</span><span class="sxs-lookup"><span data-stu-id="cd294-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="cd294-137">Porta che ha aperto la connessione.</span><span class="sxs-lookup"><span data-stu-id="cd294-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="cd294-138">`--destination-address-prefix "*"`: prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cd294-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="cd294-139">`--destination-port-range 3389`: porta o intervallo di porte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cd294-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="cd294-140">Porta che riceve la richiesta di connessione.</span><span class="sxs-lookup"><span data-stu-id="cd294-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="cd294-141">Creare una regola consenta l'accesso alla porta 80 (HTTP) da Internet con il comando **azure network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="cd294-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="cd294-142">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="cd294-143">Associare il gruppo di sicurezza di rete alla subnet **FrontEnd** con il comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="cd294-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="cd294-144">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-144">Expected output:</span></span>
   
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

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="cd294-145">Creare il gruppo di sicurezza di rete per la subnet `BackEnd`</span><span class="sxs-lookup"><span data-stu-id="cd294-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="cd294-146">Per creare un gruppo di sicurezza di rete denominato *NSG-BackEnd* in base allo scenario precedente, seguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="cd294-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="cd294-147">Creare il gruppo di sicurezza di rete `NSG-BackEnd` con **az network nsg create**.</span><span class="sxs-lookup"><span data-stu-id="cd294-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="cd294-148">Come nel passaggio 2 precedente, l'output previsto contiene svariate informazioni, incluse le regole predefinite.</span><span class="sxs-lookup"><span data-stu-id="cd294-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="cd294-149">Creare una regola che consenta l'accesso alla porta 1433 (SQL) dalla subnet `FrontEnd` con il comando **az network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="cd294-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="cd294-150">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-150">Expected output:</span></span>

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

3. <span data-ttu-id="cd294-151">Creare una regola che neghi l'accesso a Internet usando il comando **az network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="cd294-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="cd294-152">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="cd294-153">Associare il gruppo di sicurezza di rete alla subnet `BackEnd` usando il comando **az network vnet subnet set**.</span><span class="sxs-lookup"><span data-stu-id="cd294-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="cd294-154">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cd294-154">Expected output:</span></span>
   
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
