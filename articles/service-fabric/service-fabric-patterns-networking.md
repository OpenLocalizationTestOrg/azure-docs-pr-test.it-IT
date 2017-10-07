---
title: modelli aaaNetworking per Azure Service Fabric | Documenti Microsoft
description: "Descrive i modelli di rete comuni per l'infrastruttura di servizio e come toocreate un cluster con funzionalità di rete di Azure."
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
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="c2d96-103">Modelli di rete di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2d96-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="c2d96-104">È possibile integrare il cluster di Azure Service Fabric con altre funzionalità di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d96-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="c2d96-105">In questo articolo viene illustrata la modalità toocreate cluster hello tale uso seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="c2d96-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="c2d96-106">Rete virtuale o subnet esistente</span><span class="sxs-lookup"><span data-stu-id="c2d96-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="c2d96-107">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="c2d96-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="c2d96-108">Bilanciamento del carico esclusivamente interno</span><span class="sxs-lookup"><span data-stu-id="c2d96-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="c2d96-109">Bilanciamento del carico interno ed esterno</span><span class="sxs-lookup"><span data-stu-id="c2d96-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="c2d96-110">Service Fabric viene eseguito in un set di scalabilità di macchine virtuali standard.</span><span class="sxs-lookup"><span data-stu-id="c2d96-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="c2d96-111">In un cluster di Service Fabric si possono usare tutte le funzionalità che è possibile usare in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c2d96-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="c2d96-112">Nelle sezioni di rete Hello dei modelli di Azure Resource Manager hello per set di scalabilità di macchine virtuali e Service Fabric sono identiche.</span><span class="sxs-lookup"><span data-stu-id="c2d96-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="c2d96-113">Dopo aver distribuito tooan rete virtuale esistente, è facile tooincorporate altre funzionalità, come Azure ExpressRoute, Gateway VPN di Azure, un gruppo di sicurezza di rete e peering di rete virtuale di rete.</span><span class="sxs-lookup"><span data-stu-id="c2d96-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="c2d96-114">Service Fabric si distingue dalle altre funzionalità di rete per un solo aspetto.</span><span class="sxs-lookup"><span data-stu-id="c2d96-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="c2d96-115">Hello [portale di Azure](https://portal.azure.com) internamente utilizza hello Service Fabric risorsa toocall tooa cluster tooget informazioni sul provider sui nodi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c2d96-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="c2d96-116">provider di risorse di Service Fabric Hello richiede l'accesso in ingresso accessibile pubblicamente toohello HTTP gateway (porta 19080, per impostazione predefinita) nell'endpoint di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="c2d96-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) utilizza hello toomanage endpoint di gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c2d96-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="c2d96-118">provider di risorse di Service Fabric Hello utilizza anche queste informazioni di tooquery porta sul cluster, toodisplay in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d96-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="c2d96-119">Se la porta 19080 non è accessibile dal provider di risorse di Service Fabric hello, ad esempio un messaggio *non trovati nodi* viene visualizzato nel portale di hello e l'elenco di nodo e un'applicazione viene visualizzata vuota.</span><span class="sxs-lookup"><span data-stu-id="c2d96-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="c2d96-120">Se si desidera toosee il cluster in hello portale di Azure, servizio di bilanciamento del carico deve esporre un indirizzo IP pubblico e il gruppo di sicurezza di rete deve consentire il traffico in ingresso porta 19080.</span><span class="sxs-lookup"><span data-stu-id="c2d96-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="c2d96-121">Se il programma di installazione non soddisfa questi requisiti, hello portale di Azure non vengono visualizzati lo stato di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="c2d96-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="c2d96-122">Modelli</span><span class="sxs-lookup"><span data-stu-id="c2d96-122">Templates</span></span>

<span data-ttu-id="c2d96-123">Tutti i modelli di Service Fabric si trovano in [un unico file scaricabile](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="c2d96-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="c2d96-124">Dovrebbe essere in grado di toodeploy modelli hello come-utilizzando i seguenti comandi PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="c2d96-125">Se si sta distribuendo hello modello di rete virtuale di Azure esistente o hello statico pubblico IP template, leggere prima hello [Initial setup](#initialsetup) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c2d96-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="c2d96-126">Configurazione iniziale</span><span class="sxs-lookup"><span data-stu-id="c2d96-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="c2d96-127">Rete virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="c2d96-127">Existing virtual network</span></span>

<span data-ttu-id="c2d96-128">Nell'esempio seguente di hello, iniziare con una rete virtuale esistente denominata ExistingRG-vnet, in hello **ExistingRG** gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c2d96-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="c2d96-129">subnet Hello è denominato default.</span><span class="sxs-lookup"><span data-stu-id="c2d96-129">hello subnet is named default.</span></span> <span data-ttu-id="c2d96-130">Queste risorse predefiniti vengono create quando si utilizza hello toocreate portale Azure una standard macchina virtuale (VM).</span><span class="sxs-lookup"><span data-stu-id="c2d96-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="c2d96-131">È possibile creare la rete virtuale hello e subnet senza hello VM di creazione, ma l'obiettivo principale di aggiunta di una rete virtuale esistente cluster tooan hello è tooother di connettività di rete tooprovide macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c2d96-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="c2d96-132">Creazione hello VM fornisce un buon esempio di come una rete virtuale esistente in genere viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="c2d96-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="c2d96-133">Se il cluster di Service Fabric utilizza solo un bilanciamento del carico interno, senza un indirizzo IP pubblico, è possibile utilizzare hello macchina virtuale e il relativo indirizzo IP pubblico come sicuro *passare casella*.</span><span class="sxs-lookup"><span data-stu-id="c2d96-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="c2d96-134">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="c2d96-134">Static public IP address</span></span>

<span data-ttu-id="c2d96-135">In genere, un indirizzo IP pubblico statico è una risorsa dedicata che è gestita separatamente dal hello per le VM di cui è assegnato.</span><span class="sxs-lookup"><span data-stu-id="c2d96-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="c2d96-136">Si è effettuato il provisioning in un gruppo di risorse di rete dedicata (come tooin anziché hello Service Fabric gruppo di risorse cluster stesso).</span><span class="sxs-lookup"><span data-stu-id="c2d96-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="c2d96-137">Creare un indirizzo IP pubblico statico denominato staticIP1 in hello stesso gruppo di risorse ExistingRG, hello portale di Azure o tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2d96-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="c2d96-138">Modello di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2d96-138">Service Fabric template</span></span>

<span data-ttu-id="c2d96-139">Negli esempi di hello in questo articolo, utilizziamo template.json Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="c2d96-140">È possibile utilizzare hello standard portale toodownload hello il modello procedura guidata dal portale hello prima di creare un cluster.</span><span class="sxs-lookup"><span data-stu-id="c2d96-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="c2d96-141">È inoltre possibile utilizzare uno dei modelli di hello in hello [raccolta di modelli](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), ad esempio hello [cluster di Service Fabric cinque](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="c2d96-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="c2d96-142">Rete virtuale o subnet esistente</span><span class="sxs-lookup"><span data-stu-id="c2d96-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="c2d96-143">Modificare nome toohello del parametro hello subnet di una subnet esistente hello e quindi aggiungere due nuovi parametri tooreference hello rete virtuale esistente:</span><span class="sxs-lookup"><span data-stu-id="c2d96-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

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


2. <span data-ttu-id="c2d96-144">Hello modifica `vnetID` rete virtuale di variabile toopoint toohello esistente:</span><span class="sxs-lookup"><span data-stu-id="c2d96-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="c2d96-145">Rimuovere `Microsoft.Network/virtualNetworks` dalle risorse in modo che Azure non crei una nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="c2d96-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="c2d96-146">Commento di rete virtuale di hello dall'hello `dependsOn` attributo di `Microsoft.Compute/virtualMachineScaleSets`, pertanto non dipendono dalla creazione di una nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="c2d96-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="c2d96-147">Distribuire il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="c2d96-148">Dopo la distribuzione, è necessario includere la rete virtuale le macchine virtuali del set di scalabilità di nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="c2d96-149">tipo di nodo set di scalabilità di Hello macchina virtuale deve visualizzare subnet e la rete virtuale esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="c2d96-150">È anche possibile usare Remote Desktop Protocol (RDP) tooaccess hello macchina virtuale che era già in una rete virtuale hello e impostare la scala di nuovo hello tooping su macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="c2d96-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="c2d96-151">Per un altro esempio, vedere [uno che non sia tooService specifico dell'infrastruttura](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c2d96-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="c2d96-152">Indirizzo IP pubblico statico</span><span class="sxs-lookup"><span data-stu-id="c2d96-152">Static public IP address</span></span>

1. <span data-ttu-id="c2d96-153">Aggiungere parametri per nome hello di hello esistente al gruppo di risorse IP statico, nome e il nome di dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="c2d96-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="c2d96-154">Rimuovere hello `dnsName` parametro.</span><span class="sxs-lookup"><span data-stu-id="c2d96-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="c2d96-155">l'indirizzo IP statico hello già dispone di uno.</span><span class="sxs-lookup"><span data-stu-id="c2d96-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="c2d96-156">Aggiungere un variabile tooreference hello indirizzo IP statico esistente:</span><span class="sxs-lookup"><span data-stu-id="c2d96-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="c2d96-157">Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="c2d96-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="c2d96-158">Commento di indirizzo IP hello hello `dependsOn` attributo di `Microsoft.Network/loadBalancers`, pertanto non dipendono dalla creazione di un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="c2d96-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="c2d96-159">In hello `Microsoft.Network/loadBalancers` risorsa, hello modifica `publicIPAddress` elemento `frontendIPConfigurations` tooreference hello indirizzo IP statico esistente anziché uno appena creato:</span><span class="sxs-lookup"><span data-stu-id="c2d96-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="c2d96-160">In hello `Microsoft.ServiceFabric/clusters` risorse, modifica `managementEndpoint` toohello FQDN DNS dell'indirizzo IP statico hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="c2d96-161">Se si utilizza un cluster protetto, assicurarsi di modificare *http://* troppo*https://*.</span><span class="sxs-lookup"><span data-stu-id="c2d96-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="c2d96-162">(Si noti che questo passaggio si applica solo i cluster di infrastruttura tooService.</span><span class="sxs-lookup"><span data-stu-id="c2d96-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="c2d96-163">Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="c2d96-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="c2d96-164">Distribuire il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="c2d96-165">Dopo la distribuzione, è possibile notare che il servizio di bilanciamento del carico associato toohello pubblica indirizzo IP statico da hello altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c2d96-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="c2d96-166">endpoint di connessione client di Service Fabric Hello e [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello punto endpoint FQDN DNS dell'indirizzo IP statico hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="c2d96-167">Bilanciamento del carico esclusivamente interno</span><span class="sxs-lookup"><span data-stu-id="c2d96-167">Internal-only load balancer</span></span>

<span data-ttu-id="c2d96-168">Questo scenario sostituisce bilanciamento del carico esterno hello nel modello di Service Fabric hello predefinito con un bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="c2d96-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="c2d96-169">Per influisce hello portale di Azure e per provider di risorse di Service Fabric hello, vedere la precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="c2d96-170">Rimuovere hello `dnsName` parametro.</span><span class="sxs-lookup"><span data-stu-id="c2d96-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="c2d96-171">Non è necessario.</span><span class="sxs-lookup"><span data-stu-id="c2d96-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="c2d96-172">Facoltativamente, se si usa un metodo di allocazione statica è possibile aggiungere un parametro per l'indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="c2d96-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="c2d96-173">Se si utilizza un metodo di allocazione dinamica, non è necessario toodo questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="c2d96-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="c2d96-174">Rimuovere `Microsoft.Network/publicIPAddresses` dalle risorse in modo che Azure non crei un nuovo indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="c2d96-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="c2d96-175">Rimuovere l'indirizzo IP hello `dependsOn` attributo di `Microsoft.Network/loadBalancers`, pertanto non dipendono dalla creazione di un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="c2d96-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="c2d96-176">Aggiungere la rete virtuale hello `dependsOn` attributo perché il servizio di bilanciamento del carico hello ora dipende dalla subnet hello dalla rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

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

5. <span data-ttu-id="c2d96-177">Modifica del bilanciamento carico di hello `frontendIPConfigurations` impostazione dall'utilizzo di un `publicIPAddress`, toousing una subnet e `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="c2d96-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="c2d96-178">`privateIPAddress` usa un indirizzo IP interno statico predefinito.</span><span class="sxs-lookup"><span data-stu-id="c2d96-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="c2d96-179">toouse un indirizzo IP dinamico, rimuovere hello `privateIPAddress` elemento e quindi modificare `privateIPAllocationMethod` troppo**dinamica**.</span><span class="sxs-lookup"><span data-stu-id="c2d96-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

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

6. <span data-ttu-id="c2d96-180">In hello `Microsoft.ServiceFabric/clusters` risorse, modifica `managementEndpoint` indirizzo di bilanciamento del carico interno toohello toopoint.</span><span class="sxs-lookup"><span data-stu-id="c2d96-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="c2d96-181">Se si utilizza un cluster protetto, assicurarsi di modificare *http://* troppo*https://*.</span><span class="sxs-lookup"><span data-stu-id="c2d96-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="c2d96-182">(Si noti che questo passaggio si applica solo i cluster di infrastruttura tooService.</span><span class="sxs-lookup"><span data-stu-id="c2d96-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="c2d96-183">Se si usa un set di scalabilità di macchine virtuali, ignorare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="c2d96-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="c2d96-184">Distribuire il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="c2d96-185">Dopo la distribuzione, il servizio di bilanciamento del carico Usa indirizzo IP hello 10.0.0.250 statico privato.</span><span class="sxs-lookup"><span data-stu-id="c2d96-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="c2d96-186">Se si dispone di un altro computer nella stessa rete virtuale, è possibile passare toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span><span class="sxs-lookup"><span data-stu-id="c2d96-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="c2d96-187">Si noti che si connette tooone dei nodi di hello bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="c2d96-188">Bilanciamento del carico interno ed esterno</span><span class="sxs-lookup"><span data-stu-id="c2d96-188">Internal and external load balancer</span></span>

<span data-ttu-id="c2d96-189">In questo scenario, iniziare con bilanciamento del carico esterno a nodo singolo tipo esistente hello e aggiungere un servizio di bilanciamento del carico interno per hello stesso tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="c2d96-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="c2d96-190">Un pool di indirizzi back-end tooa porta back-end collegata può essere assegnato solo tooa singolo bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c2d96-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="c2d96-191">Scegliere a quale servizio di bilanciamento del carico assegnare le porte dell'applicazione e a quale assegnare gli endpoint di gestione (porte 19000 e 19080).</span><span class="sxs-lookup"><span data-stu-id="c2d96-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="c2d96-192">Se si inserisce l'endpoint di gestione di hello su servizio di bilanciamento del carico interno hello, tenere hello presente risorsa Service Fabric restrizioni provider in precedenza in hello articolo.</span><span class="sxs-lookup"><span data-stu-id="c2d96-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="c2d96-193">Nell'esempio hello che utilizziamo, gli endpoint di gestione di hello rimangono sul servizio di bilanciamento del carico esterno hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="c2d96-194">Inoltre aggiungere una porta di porta 80 dell'applicazione e posizionalo nel servizio di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="c2d96-195">In un cluster di tipo di nodo due, un tipo di nodo è nel servizio di bilanciamento del carico esterno hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="c2d96-196">Hello altro tipo di nodo è nel servizio di bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="c2d96-197">toouse un cluster di tipo di nodo due, in hello creare portale del tipo di nodo due modello (incluso in due servizi di bilanciamento del carico), passare hello secondo carico bilanciamento tooan bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="c2d96-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="c2d96-198">Per ulteriori informazioni, vedere hello [bilanciamento del carico solo per uso interno](#internallb) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2d96-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="c2d96-199">Aggiungi parametro di indirizzo IP del servizio di bilanciamento carico di interno statico hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="c2d96-200">(Per le note correlate toousing un indirizzo IP dinamico, vedere le sezioni precedenti di questo articolo).</span><span class="sxs-lookup"><span data-stu-id="c2d96-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="c2d96-201">Aggiungere un parametro della porta 80 dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c2d96-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="c2d96-202">tooadd versioni interne di hello esistente rete variabili, copiare e incollare i controlli e aggiungere "-Int" nome toohello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

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

4. <span data-ttu-id="c2d96-203">Se si avvia con modello generato portale hello che utilizza la porta 80 dell'applicazione, modello di portale predefinito hello aggiunge AppPort1 (porta 80) nel servizio di bilanciamento del carico esterno hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="c2d96-204">In questo caso, rimuovere AppPort1 dal servizio di bilanciamento del carico esterno hello `loadBalancingRules` probe e, pertanto è possibile aggiungere il servizio di bilanciamento del carico interno toohello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

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
        } /* Remove AppPort1 from hello external load balancer.
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
        } /* Remove AppPort1 from hello external load balancer.
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

5. <span data-ttu-id="c2d96-205">Aggiungere una seconda risorsa `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="c2d96-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="c2d96-206">Ottenere un risultato simile bilanciamento del carico interno toohello creato in hello [bilanciamento del carico solo per uso interno](#internallb) sezione, ma Usa hello "-Int" caricare le variabili di sistema di bilanciamento e implementa solo hello applicazione la porta 80.</span><span class="sxs-lookup"><span data-stu-id="c2d96-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="c2d96-207">Verranno rimossi anche `inboundNatPools`, gli endpoint RDP tookeep nel servizio di bilanciamento del carico pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="c2d96-208">Se si desidera RDP nel servizio di bilanciamento del carico interno hello, spostare `inboundNatPools` da hello toothis bilanciamento di carico esterno interno il bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="c2d96-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
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
                                /* Switch from Public tooPrivate IP address
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
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
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
                    /* Add hello probe for hello app port. */
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

6. <span data-ttu-id="c2d96-209">In `networkProfile` per hello `Microsoft.Compute/virtualMachineScaleSets` risorse, aggiungere il pool di indirizzi back-end interno hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

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

7. <span data-ttu-id="c2d96-210">Distribuire il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="c2d96-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="c2d96-211">Dopo la distribuzione, è possibile visualizzare due servizi di bilanciamento del carico nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="c2d96-212">Se si seleziona servizi di bilanciamento del carico hello, è possibile visualizzare l'indirizzo IP pubblico hello e indirizzo IP pubblico di gestione endpoint (porte 19000 e 19080) assegnato toohello.</span><span class="sxs-lookup"><span data-stu-id="c2d96-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="c2d96-213">È inoltre possibile visualizzare hello statico interno IP applicazione e l'indirizzo endpoint (porta 80) assegnato toohello interno il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c2d96-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="c2d96-214">Entrambi di caricamento Usa bilanciamento del carico scalabilità della macchina virtuale stessa hello impostare pool back-end.</span><span class="sxs-lookup"><span data-stu-id="c2d96-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2d96-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2d96-215">Next steps</span></span>
[<span data-ttu-id="c2d96-216">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="c2d96-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
