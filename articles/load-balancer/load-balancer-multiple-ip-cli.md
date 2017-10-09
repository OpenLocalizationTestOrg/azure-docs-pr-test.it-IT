---
title: "bilanciamento del carico su più configurazioni IP mediante Azure CLI aaaLoad | Documenti Microsoft"
description: "Informazioni su come tooassign più gli indirizzi IP tooa virtual machine tramite CLI di Azure | Gestore delle risorse."
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
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="02b72-103">Bilanciamento del carico in più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="02b72-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02b72-104">Portale</span><span class="sxs-lookup"><span data-stu-id="02b72-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="02b72-105">CLI</span><span class="sxs-lookup"><span data-stu-id="02b72-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="02b72-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b72-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="02b72-107">In questo articolo viene descritto come indirizzi di bilanciamento del carico di Azure con più IP toouse su un'interfaccia di rete secondaria (NIC).</span><span class="sxs-lookup"><span data-stu-id="02b72-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="02b72-108">Per questo scenario sono disponibili due VM con Windows, ognuna con una scheda di interfaccia di rete primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="02b72-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="02b72-109">Ognuno di hello secondario schede di rete dispone di due configurazioni IP.</span><span class="sxs-lookup"><span data-stu-id="02b72-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="02b72-110">Ogni macchina virtuale ospita entrambi i siti Web: contoso.com e fabrikam.com. Ogni sito Web è associato tooone delle configurazioni IP hello sulla hello di rete secondaria.</span><span class="sxs-lookup"><span data-stu-id="02b72-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="02b72-111">Utilizziamo bilanciamento del carico di Azure tooexpose due front-end indirizzi IP, una per ogni sito Web, toodistribute traffico toohello rispettiva configurazione IP per il sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="02b72-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="02b72-112">Questo scenario utilizza hello stesso numero di porta tra i server front-end, così come entrambi indirizzi IP del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="02b72-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Immagine dello scenario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="02b72-114">Saldo tooload passaggi su più configurazioni IP</span><span class="sxs-lookup"><span data-stu-id="02b72-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="02b72-115">Attenersi alla procedura hello seguente scenario hello tooachieve descritta in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="02b72-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="02b72-116">[Installare e configurare hello Azure CLI](../cli-install-nodejs.md) hello CLI di Azure seguendo i passaggi di hello nella articolo collegato hello e accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="02b72-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="02b72-117">[Creare un gruppo di risorse](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) denominato *contosofabrikam*, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="02b72-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="02b72-118">[Creare un set di disponibilità](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello due macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="02b72-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="02b72-119">Per questo scenario, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="02b72-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="02b72-120">[Creare una rete virtuale](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) denominata *myVNet* e una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="02b72-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="02b72-121">[Creazione di bilanciamento del carico hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) chiamato *mylb*:</span><span class="sxs-lookup"><span data-stu-id="02b72-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="02b72-122">Creare due indirizzi IP pubblici dinamici per le configurazioni IP front-end di hello del servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="02b72-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="02b72-123">Creare front-end hello due configurazioni IP, *contosofe* e *fabrikamfe* rispettivamente:</span><span class="sxs-lookup"><span data-stu-id="02b72-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="02b72-124">Creare i pool di indirizzi back-end, *contosopool* e *fabrikampool*, un [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP* e le regole di bilanciamento del carico, *HTTPc* e *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="02b72-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="02b72-125">Esempio hello esecuzione comando sotto e verificare troppo output di hello[verificare il servizio di bilanciamento del carico](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) è stato creato correttamente:</span><span class="sxs-lookup"><span data-stu-id="02b72-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="02b72-126">[Creare un indirizzo IP pubblico](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address) denominato *myPublicIp* e un [account di archiviazione](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) denominato *mystorageaccont1* per la prima macchina virtuale VM1, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="02b72-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="02b72-127">[Creare interfacce di rete di hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) per VM1 e aggiungere una seconda configurazione IP, *VM1 ipconfig2*, e [creare hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="02b72-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="02b72-128">Ripetere i passaggi da 10-11 per la seconda macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="02b72-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="02b72-129">Infine, è necessario configurare resource record toopoint toohello front-end rispettivi indirizzo IP del DNS hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="02b72-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="02b72-130">È possibile ospitare i domini nel servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="02b72-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="02b72-131">Per altre informazioni sull'uso del servizio DNS di Azure con Azure Load Balancer, vedere [Uso del servizio DNS di Azure con altri servizi di Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="02b72-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02b72-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02b72-132">Next steps</span></span>
- <span data-ttu-id="02b72-133">Altre informazioni su come il bilanciamento del carico toocombine servizi in Azure in [utilizzando servizi di bilanciamento del carico in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="02b72-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="02b72-134">Informazioni su come è possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi di bilanciamento del carico in [Log analitica per il bilanciamento del carico di Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="02b72-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
