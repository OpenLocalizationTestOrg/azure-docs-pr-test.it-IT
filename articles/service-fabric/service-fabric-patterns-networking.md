---
title: Modelli di rete per Azure Service Fabric | Microsoft Docs
description: "Questo articolo descrive i modelli di rete comuni per Service Fabric e illustra come creare un cluster con le funzionalità di rete di Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="f4d09-103">Modelli di rete di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f4d09-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="f4d09-104">È possibile integrare il cluster di Azure Service Fabric con altre funzionalità di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4d09-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="f4d09-105">Questo articolo illustra come creare cluster che fanno uso delle funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4d09-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="f4d09-106">Rete virtuale o subnet esistente</span><span class="sxs-lookup"><span data-stu-id="f4d09-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="f4d09-107">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="f4d09-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="f4d09-108">Bilanciamento del carico esclusivamente interno</span><span class="sxs-lookup"><span data-stu-id="f4d09-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="f4d09-109">Bilanciamento del carico interno ed esterno</span><span class="sxs-lookup"><span data-stu-id="f4d09-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="f4d09-110">Service Fabric viene eseguito in un set di scalabilità di macchine virtuali standard.</span><span class="sxs-lookup"><span data-stu-id="f4d09-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="f4d09-111">In un cluster di Service Fabric si possono usare tutte le funzionalità che è possibile usare in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f4d09-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="f4d09-112">Le sezioni di rete dei modelli di Azure Resource Manager per i set di scalabilità di macchine virtuali e quelle per Service Fabric sono identiche.</span><span class="sxs-lookup"><span data-stu-id="f4d09-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="f4d09-113">Dopo aver eseguito la distribuzione in una rete virtuale esistente, è facile incorporare altre funzionalità di rete, come Azure ExpressRoute, il gateway VPN di Azure, un gruppo di sicurezza di rete e il peering di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f4d09-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="f4d09-114">Service Fabric si distingue dalle altre funzionalità di rete per un solo aspetto.</span><span class="sxs-lookup"><span data-stu-id="f4d09-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="f4d09-115">Il [portale di Azure](https://portal.azure.com) usa internamente il provider di risorse di Service Fabric per chiamare un cluster e ottenere informazioni sui nodi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f4d09-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="f4d09-116">Il provider di risorse di Service Fabric richiede l'accesso in ingresso accessibile pubblicamente alla porta del gateway HTTP nell'endpoint di gestione. Per impostazione predefinita si tratta della porta 19080.</span><span class="sxs-lookup"><span data-stu-id="f4d09-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="f4d09-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) usa l'endpoint di gestione per gestire il cluster.</span><span class="sxs-lookup"><span data-stu-id="f4d09-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="f4d09-118">Anche il provider di risorse di Service Fabric usa questa porta per richiedere informazioni sul cluster, che vengono visualizzate nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4d09-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="f4d09-119">Se la porta 19080 non è accessibile dal provider di risorse di Service Fabric, nel portale viene visualizzato un messaggio che indica che *non sono stati trovati nodi* e l'elenco dei nodi e delle applicazioni risulta vuoto.</span><span class="sxs-lookup"><span data-stu-id="f4d09-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="f4d09-120">Per visualizzare il cluster nel portale di Azure, il servizio di bilanciamento del carico deve esporre un indirizzo IP pubblico e il gruppo di sicurezza di rete deve consentire il traffico in ingresso dalla porta 19080.</span><span class="sxs-lookup"><span data-stu-id="f4d09-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="f4d09-121">Se la configurazione non soddisfa questi requisiti, lo stato del cluster non viene visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4d09-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="f4d09-122">Modelli</span><span class="sxs-lookup"><span data-stu-id="f4d09-122">Templates</span></span>

<span data-ttu-id="f4d09-123">Tutti i modelli di Service Fabric si trovano in [un unico file scaricabile](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="f4d09-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="f4d09-124">Dovrebbe essere possibile distribuire i modelli così come sono usando i comandi di PowerShell riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f4d09-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="f4d09-125">Se si distribuisce il modello di rete virtuale di Azure esistente o il modello IP pubblico statico, leggere prima la sezione [Configurazione iniziale](#initialsetup) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f4d09-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="f4d09-126">Configurazione iniziale</span><span class="sxs-lookup"><span data-stu-id="f4d09-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="f4d09-127">Rete virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="f4d09-127">Existing virtual network</span></span>

<span data-ttu-id="f4d09-128">L'esempio seguente parte da una rete virtuale esistente denominata ExistingRG-vnet, nel gruppo di risorse **ExistingRG**.</span><span class="sxs-lookup"><span data-stu-id="f4d09-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="f4d09-129">Il nome della subnet è quello predefinito.</span><span class="sxs-lookup"><span data-stu-id="f4d09-129">The subnet is named default.</span></span> <span data-ttu-id="f4d09-130">Queste risorse predefinite vengono create quando si usa il portale di Azure per creare una macchina virtuale (VM) standard.</span><span class="sxs-lookup"><span data-stu-id="f4d09-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="f4d09-131">È possibile creare la rete virtuale e la subnet senza creare la macchina virtuale, ma l'obiettivo principale dell'aggiunta di un cluster a una rete virtuale esistente è fornire la connettività di rete ad altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f4d09-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="f4d09-132">La creazione della macchina virtuale costituisce un buon esempio dell'uso tipico di una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f4d09-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="f4d09-133">Se il cluster di Service Fabric usa soltanto un servizio di bilanciamento del carico interno, senza un indirizzo IP pubblico, è possibile usare la macchina virtuale e il relativo indirizzo IP pubblico come un *jumpbox* protetto.</span><span class="sxs-lookup"><span data-stu-id="f4d09-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="f4d09-134">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="f4d09-134">Static public IP address</span></span>

<span data-ttu-id="f4d09-135">In genere, un indirizzo IP pubblico è una risorsa dedicata che viene gestita separatamente rispetto alla macchina virtuale o alle macchine virtuali a cui è assegnato.</span><span class="sxs-lookup"><span data-stu-id="f4d09-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="f4d09-136">Il provisioning viene effettuato in un gruppo di risorse di rete dedicato e non nel gruppo di risorse stesso del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f4d09-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="f4d09-137">Creare un indirizzo IP pubblico statico denominato staticIP1 nello stesso gruppo di risorse ExistingRG, nel portale di Azure oppure tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f4d09-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="f4d09-138">Modello di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f4d09-138">Service Fabric template</span></span>

<span data-ttu-id="f4d09-139">Negli esempi riportati in questo articolo viene usato il file template.json di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f4d09-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="f4d09-140">Per scaricare il modello dal portale prima di creare un cluster, è possibile usare la procedura guidata standard del portale.</span><span class="sxs-lookup"><span data-stu-id="f4d09-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="f4d09-141">È anche possibile usare uno dei modelli della [raccolta modelli](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), come il [cluster a cinque nodi di Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="f4d09-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="f4d09-142">Rete virtuale o subnet esistente</span><span class="sxs-lookup"><span data-stu-id="f4d09-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="f4d09-143">Impostare il parametro subnet sul nome della subnet esistente e quindi aggiungere due nuovi parametri per fare riferimento alla rete virtuale esistente:</span><span class="sxs-lookup"><span data-stu-id="f4d09-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="f4d09-144">Modificare la variabile `vnetID` in modo che punti alla rete virtuale esistente:</span><span class="sxs-lookup"><span data-stu-id="f4d09-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="f4d09-145">Rimuovere `Microsoft.Network/virtualNetworks` dalle risorse in modo che Azure non crei una nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="f4d09-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="f4d09-146">Impostare come commento la rete virtuale dell'attributo `dependsOn` di `Microsoft.Compute/virtualMachineScaleSets` in modo da non dipendere dalla creazione di una nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="f4d09-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="f4d09-147">Distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="f4d09-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="f4d09-148">Dopo la distribuzione, la rete virtuale dovrebbe includere le nuove macchine virtuali del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="f4d09-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="f4d09-149">Il tipo di nodo del set di scalabilità di macchine virtuali dovrebbe mostrare la rete virtuale esistente e la subnet.</span><span class="sxs-lookup"><span data-stu-id="f4d09-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="f4d09-150">È anche possibile usare il protocollo RDP (Remote Desktop Protocol) per accedere alla macchina virtuale già esistente nella rete virtuale e per effettuare il ping delle nuove macchine virtuali del set di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="f4d09-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="f4d09-151">Per altre informazioni, vedere un [esempio non specifico di Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="f4d09-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="f4d09-152">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="f4d09-152">Static public IP address</span></span>

1. <span data-ttu-id="f4d09-153">Aggiungere i parametri per il gruppo di risorse dell'indirizzo IP statico esistente, il nome e il nome di dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="f4d09-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="f4d09-154">Rimuovere il parametro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="f4d09-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="f4d09-155">L'indirizzo IP statico ne ha già uno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="f4d09-156">Aggiungere una variabile per fare riferimento all'indirizzo IP statico esistente:</span><span class="sxs-lookup"><span data-stu-id="f4d09-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="f4d09-157">Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="f4d09-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="f4d09-158">Impostare come commento l'indirizzo IP dell'attributo `dependsOn` di `Microsoft.Network/loadBalancers` in modo da non dipendere dalla creazione di un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="f4d09-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="f4d09-159">Nella risorsa `Microsoft.Network/loadBalancers` modificare l'elemento `publicIPAddress` di `frontendIPConfigurations` in modo che faccia riferimento l'indirizzo IP statico esistente anziché a uno appena creato:</span><span class="sxs-lookup"><span data-stu-id="f4d09-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="f4d09-160">Nella risorsa `Microsoft.ServiceFabric/clusters` impostare `managementEndpoint` sul nome di dominio completo del DNS dell'indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="f4d09-161">Se si usa un cluster protetto, assicurarsi di modificare *http://* in *https://*.</span><span class="sxs-lookup"><span data-stu-id="f4d09-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="f4d09-162">Si noti che questo passaggio si applica solo ai cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f4d09-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="f4d09-163">Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="f4d09-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="f4d09-164">Distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="f4d09-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="f4d09-165">Dopo la distribuzione, il servizio di bilanciamento del carico è associato all'indirizzo IP statico pubblico dell'altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f4d09-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="f4d09-166">L'endpoint della connessione client di Service Fabric e l'endpoint di [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) puntano al nome di dominio completo del DNS dell'indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="f4d09-167">Bilanciamento del carico esclusivamente interno</span><span class="sxs-lookup"><span data-stu-id="f4d09-167">Internal-only load balancer</span></span>

<span data-ttu-id="f4d09-168">Questo scenario sostituisce il servizio di bilanciamento del carico esterno nel modello di Service Fabric predefinito con un bilanciamento del carico esclusivamente interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="f4d09-169">Per informazioni sulle implicazioni per il portale di Azure e per il provider di risorse di Service Fabric, vedere la sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="f4d09-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="f4d09-170">Rimuovere il parametro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="f4d09-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="f4d09-171">Non è necessario.</span><span class="sxs-lookup"><span data-stu-id="f4d09-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="f4d09-172">Facoltativamente, se si usa un metodo di allocazione statica è possibile aggiungere un parametro per l'indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="f4d09-173">Se si usa un metodo di allocazione dinamica, non è necessario eseguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="f4d09-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="f4d09-174">Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="f4d09-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="f4d09-175">Rimuovere l'indirizzo IP dell'attributo `dependsOn` di `Microsoft.Network/loadBalancers` in modo da non dipendere dalla creazione di un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="f4d09-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="f4d09-176">Dal momento che ora il servizio di bilanciamento del carico dipende dalla subnet della rete virtuale, aggiungere l'attributo `dependsOn` della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="f4d09-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="f4d09-177">Modificare l'impostazione `frontendIPConfigurations` del servizio di bilanciamento del carico passando dall'uso di `publicIPAddress` all'uso di una subnet e di `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="f4d09-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="f4d09-178">`privateIPAddress` usa un indirizzo IP interno statico predefinito.</span><span class="sxs-lookup"><span data-stu-id="f4d09-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="f4d09-179">Per usare un indirizzo IP dinamico, rimuovere l'elemento `privateIPAddress` e modificare `privateIPAllocationMethod` in **dinamico**.</span><span class="sxs-lookup"><span data-stu-id="f4d09-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="f4d09-180">Nella risorsa `Microsoft.ServiceFabric/clusters` modificare `managementEndpoint` in modo che punti all'indirizzo del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="f4d09-181">Se si usa un cluster protetto, assicurarsi di modificare *http://* in *https://*.</span><span class="sxs-lookup"><span data-stu-id="f4d09-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="f4d09-182">Si noti che questo passaggio si applica solo ai cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f4d09-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="f4d09-183">Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="f4d09-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="f4d09-184">Distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="f4d09-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="f4d09-185">Dopo la distribuzione, il servizio di bilanciamento del carico usa l'indirizzo IP privato statico 10.0.0.250.</span><span class="sxs-lookup"><span data-stu-id="f4d09-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="f4d09-186">Se nella stessa rete virtuale è disponibile un altro computer, è possibile passare all'endpoint interno di [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f4d09-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="f4d09-187">Si noti che questo si connette a uno dei nodi del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="f4d09-188">Bilanciamento del carico interno ed esterno</span><span class="sxs-lookup"><span data-stu-id="f4d09-188">Internal and external load balancer</span></span>

<span data-ttu-id="f4d09-189">In questo scenario si inizia con il servizio di bilanciamento del carico esterno a nodo singolo esistente e si aggiunge un servizio di bilanciamento del carico interno per lo stesso tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="f4d09-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="f4d09-190">È possibile assegnare una porta back-end collegata a un pool di indirizzi back-end a un solo servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="f4d09-191">Scegliere a quale servizio di bilanciamento del carico assegnare le porte dell'applicazione e a quale assegnare gli endpoint di gestione (porte 19000 e 19080).</span><span class="sxs-lookup"><span data-stu-id="f4d09-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="f4d09-192">Se si sceglie di inserire gli endpoint di gestione nel servizio di bilanciamento del carico interno, tenere presenti le limitazioni del provider di risorse di Service Fabric illustrate in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f4d09-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="f4d09-193">Nell'esempio usato gli endpoint di gestione rimangono nel servizio di bilanciamento del carico esterno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="f4d09-194">Aggiungere una porta 80 dell'applicazione e posizionarla nel servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="f4d09-195">In un cluster a due tipi di nodo, un tipo di nodo si trova nel servizio di bilanciamento del carico esterno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="f4d09-196">L'altro tipo di nodo si trova nel servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="f4d09-197">Per usare un cluster a due tipi di nodo, nel modello a due tipi di nodo creato nel portale, che include due servizi di bilanciamento del carico, impostare il secondo come servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="f4d09-198">Per altre informazioni, vedere la sezione [Bilanciamento del carico esclusivamente interno](#internallb).</span><span class="sxs-lookup"><span data-stu-id="f4d09-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="f4d09-199">Aggiungere il parametro per l'indirizzo IP statico del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="f4d09-200">Per le note relative all'uso di un indirizzo IP dinamico, vedere le sezioni precedenti di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f4d09-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="f4d09-201">Aggiungere un parametro della porta 80 dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4d09-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="f4d09-202">Per aggiungere versioni interne delle variabili di rete esistenti, copiarle e incollarle e aggiungere "-Int" al nome:</span><span class="sxs-lookup"><span data-stu-id="f4d09-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="f4d09-203">Se si parte dal modello generato nel portale, che usa la porta 80 dell'applicazione, il modello predefinito del portale aggiunge AppPort1 (porta 80) al servizio di bilanciamento del carico esterno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="f4d09-204">In tal caso, rimuovere AppPort1 dall'oggetto `loadBalancingRules` e dai probe del servizio di bilanciamento del carico esterno, in modo che sia possibile aggiungerlo al servizio di bilanciamento del carico interno:</span><span class="sxs-lookup"><span data-stu-id="f4d09-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="f4d09-205">Aggiungere una seconda risorsa `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="f4d09-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="f4d09-206">Ha un aspetto simile al servizio di bilanciamento del carico interno creato nella sezione [Bilanciamento del carico esclusivamente interno](#internallb), ma fa uso delle variabili "-Int" del servizio di bilanciamento del carico e implementa solo la porta 80 dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4d09-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="f4d09-207">Rimuove anche `inboundNatPools`, per mantenere gli endpoint RDP nel servizio di bilanciamento del carico pubblico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="f4d09-208">Per usare il protocollo RDP nel servizio di bilanciamento del carico interno, spostare `inboundNatPools` dal servizio di bilanciamento del carico esterno a quello interno:</span><span class="sxs-lookup"><span data-stu-id="f4d09-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public to Private IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add the probe for the app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="f4d09-209">In `networkProfile` per la risorsa `Microsoft.Compute/virtualMachineScaleSets` aggiungere il pool di indirizzi back-end interno:</span><span class="sxs-lookup"><span data-stu-id="f4d09-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="f4d09-210">Distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="f4d09-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="f4d09-211">Dopo la distribuzione, nel gruppo di risorse vengono visualizzati due servizi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="f4d09-212">Esplorando tali servizi è possibile visualizzare l'indirizzo IP pubblico e gli endpoint di gestione (porte 19000 e 19080) assegnati all'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="f4d09-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="f4d09-213">È anche possibile visualizzare l'indirizzo IP interno statico e l'endpoint dell'applicazione (porta 80) assegnati al servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="f4d09-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="f4d09-214">Entrambi i servizi di bilanciamento del carico usano lo stesso pool back-end del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f4d09-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4d09-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4d09-215">Next steps</span></span>
[<span data-ttu-id="f4d09-216">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="f4d09-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
