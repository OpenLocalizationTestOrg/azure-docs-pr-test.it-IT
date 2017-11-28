---
title: "Bilanciamento del carico in più configurazioni IP tramite l'interfaccia della riga di comando di Azure | Microsoft Docs"
description: "Informazioni su come assegnare più indirizzi IP a una macchina virtuale usando l'interfaccia della riga di comando di Azure | Resource Manager"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="27742-103">Bilanciamento del carico in più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="27742-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27742-104">Portale</span><span class="sxs-lookup"><span data-stu-id="27742-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="27742-105">CLI</span><span class="sxs-lookup"><span data-stu-id="27742-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="27742-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27742-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="27742-107">Questo articolo descrive come usare Azure Load Balancer con più indirizzi IP su una scheda di interfaccia di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="27742-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="27742-108">Per questo scenario sono disponibili due VM con Windows, ognuna con una scheda di interfaccia di rete primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="27742-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="27742-109">Ogni scheda di interfaccia di rete secondaria dispone di due configurazioni di IP.</span><span class="sxs-lookup"><span data-stu-id="27742-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="27742-110">Ogni macchina virtuale ospita entrambi i siti Web: contoso.com e fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="27742-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="27742-111">Ogni sito Web è associato a una delle configurazioni IP della scheda di interfaccia di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="27742-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="27742-112">Azure Load Balancer viene usato per esporre due indirizzi IP front-end, uno per ogni sito Web, per distribuire il traffico alla rispettiva configurazione IP per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="27742-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="27742-113">Questo scenario usa lo stesso numero di porta per entrambi i front-end, nonché per entrambi gli indirizzi IP del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="27742-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Immagine dello scenario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="27742-115">Procedura per il bilanciamento del carico in più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="27742-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="27742-116">Per ottenere lo scenario descritto in questo articolo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="27742-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="27742-117">[Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) seguendo la procedura riportata nell'articolo collegato e accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="27742-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="27742-118">[Creare un gruppo di risorse](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) denominato *contosofabrikam*, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="27742-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="27742-119">[Creare un set di disponibilità](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) per le due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="27742-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="27742-120">Per questo scenario, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="27742-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="27742-121">[Creare una rete virtuale](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) denominata *myVNet* e una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="27742-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="27742-122">[Creare il servizio di bilanciamento del carico](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) denominato *mylb*:</span><span class="sxs-lookup"><span data-stu-id="27742-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="27742-123">Creare due indirizzi IP pubblici dinamici per le configurazioni IP front-end del servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="27742-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="27742-124">Creare le due configurazioni IP front-end, rispettivamente *contosofe* e *fabrikamfe*:</span><span class="sxs-lookup"><span data-stu-id="27742-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="27742-125">Creare i pool di indirizzi back-end, *contosopool* e *fabrikampool*, un [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP* e le regole di bilanciamento del carico, *HTTPc* e *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="27742-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="27742-126">Eseguire questo comando e controllare l'output per verificare che il [servizio di bilanciamento del carico](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sia stato creato correttamente:</span><span class="sxs-lookup"><span data-stu-id="27742-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="27742-127">[Creare un indirizzo IP pubblico](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address) denominato *myPublicIp* e un [account di archiviazione](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) denominato *mystorageaccont1* per la prima macchina virtuale VM1, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="27742-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="27742-128">[Creare le interfacce di rete](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) per VM1 e aggiungere una seconda configurazione IP, *VM1-ipconfig2*, e [creare la VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms), come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="27742-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="27742-129">Ripetere i passaggi da 10-11 per la seconda macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="27742-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="27742-130">Infine, è necessario configurare i record risorsa DNS in modo che puntino all'indirizzo IP front-end corrispondente di Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="27742-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="27742-131">È possibile ospitare i domini nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="27742-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="27742-132">Per altre informazioni sull'uso del servizio DNS di Azure con Azure Load Balancer, vedere [Uso del servizio DNS di Azure con altri servizi di Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="27742-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27742-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27742-133">Next steps</span></span>
- <span data-ttu-id="27742-134">Altre informazioni su come combinare i servizi di bilanciamento del carico di Azure sono disponibili in [Uso dei servizi di bilanciamento del carico in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="27742-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="27742-135">Informazioni su come è possibile usare diversi tipi di log in Azure per gestire e risolvere i problemi di bilanciamento del carico sono disponibili in [Analisi dei log per Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="27742-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
