---
title: "Set di scalabilità di macchine virtuali Windows aaaAutoscale | Documenti Microsoft"
description: "Impostare il ridimensionamento automatico per un set di scalabilità di macchine virtuali Windows tramite Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="c862b-103">Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c862b-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="c862b-104">Set di scalabilità di macchine virtuali semplificano automaticamente toodeploy e gestire macchine virtuali identiche come un set.</span><span class="sxs-lookup"><span data-stu-id="c862b-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="c862b-105">I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni.</span><span class="sxs-lookup"><span data-stu-id="c862b-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="c862b-106">Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="c862b-107">Questa esercitazione viene illustrato come un set di scalabilità di macchine virtuali di Windows e automaticamente scala hello macchine in hello toocreate impostato.</span><span class="sxs-lookup"><span data-stu-id="c862b-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="c862b-108">Creare una scala hello e impostare il ridimensionamento per la creazione di un modello di gestione risorse di Azure e la distribuzione con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c862b-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="c862b-109">Per altre informazioni sui modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="c862b-110">toolearn più sul ridimensionamento automatico del set di scalabilità, vedere [il ridimensionamento automatico e imposta la scala di macchina virtuale](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="c862b-111">In questo articolo, si distribuisce seguente hello risorse ed estensioni:</span><span class="sxs-lookup"><span data-stu-id="c862b-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="c862b-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="c862b-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="c862b-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="c862b-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="c862b-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="c862b-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="c862b-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="c862b-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="c862b-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="c862b-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="c862b-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="c862b-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="c862b-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="c862b-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="c862b-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="c862b-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="c862b-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="c862b-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="c862b-121">Per altre informazioni sulle risorse di Resource Manager, vedere [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="c862b-122">Passaggio 1: installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c862b-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="c862b-123">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c862b-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="c862b-124">Passaggio 2: Creare un gruppo di risorse e un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c862b-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="c862b-125">**Creare un gruppo di risorse** : tutte le risorse devono essere distribuito tooa gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c862b-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="c862b-126">Utilizzare [New AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate un gruppo di risorse denominato **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="c862b-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="c862b-127">**Creare un account di archiviazione** : questo account di archiviazione è in cui è archiviato il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="c862b-128">Utilizzare [New AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate un account di archiviazione denominato **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="c862b-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="c862b-129">Passaggio 3: Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="c862b-129">Step 3: Create hello template</span></span>
<span data-ttu-id="c862b-130">Un modello di gestione risorse di Azure rende possibile la si toodeploy e gestire le risorse di Azure insieme con una descrizione JSON delle risorse di hello e parametri di distribuzione associati.</span><span class="sxs-lookup"><span data-stu-id="c862b-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="c862b-131">Nell'editor preferito, creare file hello C:\VMSSTemplate.json e aggiungere hello iniziale JSON struttura toosupport hello modello.</span><span class="sxs-lookup"><span data-stu-id="c862b-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="c862b-132">Parametri non sono sempre necessari, ma forniscono un modo tooinput valori quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="c862b-133">Aggiungere i parametri che è stato aggiunto il modello di toohello nell'elemento padre parametri hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="c862b-134">Un nome per la macchina virtuale separata hello che viene utilizzato tooaccess hello macchine nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="c862b-135">nome Hello hello dell'account di archiviazione in cui è archiviato il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="c862b-136">numero di Hello di macchine virtuali tooinitially creare nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="c862b-137">nome Hello e la password dell'account di amministratore hello in macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="c862b-138">Imposta un prefisso del nome per le risorse di hello scala hello toosupport creati.</span><span class="sxs-lookup"><span data-stu-id="c862b-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="c862b-139">Variabili possono essere utilizzate nei valori di toospecify modello che possono cambiare frequentemente o valori che devono toobe creato da una combinazione di valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="c862b-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="c862b-140">Aggiungere queste variabili che è stato aggiunto il modello di toohello nell'elemento padre variabili hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="c862b-141">I nomi DNS che vengono utilizzati da hello interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="c862b-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="c862b-142">i nomi degli indirizzi IP di Hello e i prefissi di rete virtuale hello e le subnet.</span><span class="sxs-lookup"><span data-stu-id="c862b-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="c862b-143">Hello nomi e gli identificatori di rete virtuale hello, bilanciamento del carico e le interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="c862b-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="c862b-144">Nomi account di archiviazione per gli account di hello associati macchine hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="c862b-145">Impostazioni per l'estensione di diagnostica che viene installato nelle macchine virtuali hello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="c862b-146">Per ulteriori informazioni su hello estensione di diagnostica, vedere [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c862b-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="c862b-147">Aggiungere risorse di account di archiviazione hello nell'elemento padre di risorse hello che è stato aggiunto il modello di toohello.</span><span class="sxs-lookup"><span data-stu-id="c862b-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="c862b-148">Il modello utilizza un hello toocreate ciclo consigliato cinque gli account di archiviazione in cui sono archiviati i dischi del sistema operativo hello e dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c862b-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="c862b-149">Questo set di account può supportare fino a too100 di macchine virtuali in un set di scalabilità, ossia massimo corrente hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="c862b-150">Ogni account di archiviazione denominato con un indicatore lettera definite nelle variabili hello combinate con il prefisso hello forniti nei parametri hello per modello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="c862b-151">Aggiungere risorse di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-151">Add hello virtual network resource.</span></span> <span data-ttu-id="c862b-152">Per altre informazioni, vedere [Provider di risorse di rete](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="c862b-153">Aggiungere hello pubbliche risorse indirizzo IP utilizzati da hello bilanciamento del caricano e l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c862b-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="c862b-154">Aggiungere una risorsa di bilanciamento del carico hello utilizzato dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="c862b-155">Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="c862b-156">Aggiungere risorse di interfaccia di rete hello utilizzato dalla macchina virtuale separata hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="c862b-157">Poiché le macchine in un set di scalabilità non sono accessibili tramite un indirizzo IP pubblico, una macchina virtuale separata viene creata in hello stesso virtuale macchine di hello tooremotely accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="c862b-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="c862b-158">Aggiungere una macchina virtuale separata hello nella stessa rete set di scalabilità hello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="c862b-159">Aggiungere una risorsa del set di scalabilità della macchina virtuale hello e specificare l'estensione diagnostica hello installato in tutte le macchine virtuali nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="c862b-160">Molte delle impostazioni di hello per questa risorsa sono simili alla risorsa di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="c862b-161">Hello principali differenze riguardano hello capacità elemento che specifica il numero di hello di macchine virtuali nel set di scalabilità hello e upgradePolicy che specifica la modalità con cui gli aggiornamenti vengono eseguiti toovirtual macchine.</span><span class="sxs-lookup"><span data-stu-id="c862b-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="c862b-162">Hello set di scalabilità non viene creata finché non vengono creati tutti gli account di archiviazione hello come specificato con l'elemento dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="c862b-163">Aggiungere hello autoscaleSettings risorsa che definisce la modalità in base all'utilizzo del processore hello computer hello in set di scalabilità hello hello set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c862b-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="c862b-164">Per questa esercitazione, i valori importanti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="c862b-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="c862b-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="c862b-165">**metricName**</span></span>  
    <span data-ttu-id="c862b-166">Questo valore è hello stesso come contatore delle prestazioni hello definiti nella variabile wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="c862b-167">Utilizzo di tale variabile, hello estensione di diagnostica raccoglie hello **( totale)\% tempo processore** contatore.</span><span class="sxs-lookup"><span data-stu-id="c862b-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="c862b-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="c862b-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="c862b-169">Questo valore è l'identificatore di risorsa hello del set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="c862b-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="c862b-170">**timeGrain**</span></span>  
    <span data-ttu-id="c862b-171">Questo valore è la granularità hello di metriche di hello che vengono raccolti.</span><span class="sxs-lookup"><span data-stu-id="c862b-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="c862b-172">In questo modello, è impostato tooone minuto.</span><span class="sxs-lookup"><span data-stu-id="c862b-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="c862b-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="c862b-173">**statistic**</span></span>  
    <span data-ttu-id="c862b-174">Questo valore determina come le metriche hello vengono combinati tooaccommodate hello azione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c862b-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="c862b-175">Hello i valori possibili sono: Media, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="c862b-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="c862b-176">In questo modello, verrà raccolti hello totale utilizzo medio della CPU delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="c862b-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="c862b-177">**timeWindow**</span></span>  
    <span data-ttu-id="c862b-178">Questo valore è hello intervallo di tempo in cui vengono raccolti i dati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="c862b-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="c862b-179">Deve essere compreso tra 5 minuti e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="c862b-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="c862b-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="c862b-180">**timeAggregation**</span></span>  
    <span data-ttu-id="c862b-181">il suo valore determina la modalità hello i dati raccolti devono essere combinati nel tempo.</span><span class="sxs-lookup"><span data-stu-id="c862b-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="c862b-182">valore predefinito di Hello è Media.</span><span class="sxs-lookup"><span data-stu-id="c862b-182">hello default value is Average.</span></span> <span data-ttu-id="c862b-183">Hello i valori possibili sono: Media, minimo, massimo, ultimo, totale, conteggio.</span><span class="sxs-lookup"><span data-stu-id="c862b-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="c862b-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="c862b-184">**operator**</span></span>  
    <span data-ttu-id="c862b-185">Questo valore è l'operatore hello toocompare utilizzati hello metrica hello e dati soglia.</span><span class="sxs-lookup"><span data-stu-id="c862b-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="c862b-186">Hello i valori possibili sono: uguale a, diverso da, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="c862b-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="c862b-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="c862b-187">**threshold**</span></span>  
    <span data-ttu-id="c862b-188">Questo valore è hello che attiva l'azione di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="c862b-189">In questo modello, i computer vengono aggiunti toohello scala impostata quando l'utilizzo medio della CPU hello tra le macchine nel set di hello è oltre il 50%.</span><span class="sxs-lookup"><span data-stu-id="c862b-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="c862b-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="c862b-190">**direction**</span></span>  
    <span data-ttu-id="c862b-191">Questo valore determina l'azione eseguita quando viene raggiunto il valore di soglia hello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="c862b-192">i valori possibili di Hello sono aumentano o diminuiscono.</span><span class="sxs-lookup"><span data-stu-id="c862b-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="c862b-193">In questo modello, hello numero di macchine virtuali nel set di scalabilità hello viene aumentato se la soglia di hello è oltre il 50% di tempo definito hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="c862b-194">**type**</span><span class="sxs-lookup"><span data-stu-id="c862b-194">**type**</span></span>  
    <span data-ttu-id="c862b-195">Questo valore è di tipo hello di azione che deve essere eseguita e deve essere impostato tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="c862b-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="c862b-196">**value**</span><span class="sxs-lookup"><span data-stu-id="c862b-196">**value**</span></span>  
    <span data-ttu-id="c862b-197">Questo valore è il numero di hello di macchine virtuali che vengono aggiunti o rimossi dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="c862b-198">Questo valore deve essere uguale o maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="c862b-198">This value must be 1 or greater.</span></span> <span data-ttu-id="c862b-199">valore predefinito di Hello è 1.</span><span class="sxs-lookup"><span data-stu-id="c862b-199">hello default value is 1.</span></span> <span data-ttu-id="c862b-200">In questo modello, hello macchine nella scala hello impostare numerose aumenta di 1 quando viene raggiunta la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="c862b-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="c862b-201">**cooldown**</span></span>  
    <span data-ttu-id="c862b-202">Questo valore è quantità hello di toowait tempo dall'ultima azione di scalabilità hello prima che si verifichi l'azione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="c862b-203">Questo valore deve essere compreso tra un minuto e una settimana.</span><span class="sxs-lookup"><span data-stu-id="c862b-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="c862b-204">Salvare il file di modello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="c862b-205">Passaggio 4: Caricare hello modello toostorage</span><span class="sxs-lookup"><span data-stu-id="c862b-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="c862b-206">è possibile caricare il modello di Hello, purché si conosce il nome di hello e la chiave primaria dell'account di archiviazione hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="c862b-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="c862b-207">Nella finestra di Microsoft Azure PowerShell hello, impostare una variabile che specifica il nome di hello hello dell'account di archiviazione creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="c862b-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="c862b-208">Impostare una variabile che specifica una chiave primaria dell'account di archiviazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="c862b-209">È possibile ottenere la chiave facendo clic sull'icona chiave hello durante la visualizzazione di risorse di account di archiviazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c862b-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="c862b-210">Creare hello oggetto account di archiviazione contesto che viene utilizzato toovalidate operazioni con account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="c862b-211">Creare il contenitore di hello per archiviare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="c862b-212">Caricare hello modello file toohello nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="c862b-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="c862b-213">Passaggio 5: Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="c862b-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="c862b-214">Ora che è stato creato il modello di hello, è possibile avviare la distribuzione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="c862b-215">Utilizzare questo processo di hello toostart comando:</span><span class="sxs-lookup"><span data-stu-id="c862b-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="c862b-216">Quando preme INVIO, sei valori tooprovide richiesta per le variabili di hello che è assegnato.</span><span class="sxs-lookup"><span data-stu-id="c862b-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="c862b-217">Specificare questi valori:</span><span class="sxs-lookup"><span data-stu-id="c862b-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="c862b-218">Richiede circa 15 minuti per essere distribuito tutti hello risorse toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="c862b-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="c862b-219">È possibile utilizzare anche le risorse di hello del portale hello possibilità toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c862b-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="c862b-220">Usare questo collegamento: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="c862b-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="c862b-221">Passaggio 6: Monitorare le risorse</span><span class="sxs-lookup"><span data-stu-id="c862b-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="c862b-222">Per ottenere informazioni sui set di scalabilità di macchine virtuali, è possibile usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c862b-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="c862b-223">portale di Azure Hello: attualmente è possibile ottenere una quantità limitata di informazioni tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="c862b-224">Hello [Esplora inventario risorse di Azure](https://resources.azure.com/) -questo strumento è hello migliore per l'esplorazione dello stato corrente di hello del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="c862b-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="c862b-225">Seguire questo percorso e dovrebbe essere vista istanza hello della scala hello imposta creato:</span><span class="sxs-lookup"><span data-stu-id="c862b-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="c862b-226">sottoscrizioni > {sottoscrizioni dell'utente} > gruppi di risorse > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c862b-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="c862b-227">Azure PowerShell - usare questo comando tooget alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="c862b-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="c862b-228">Or</span><span class="sxs-lookup"><span data-stu-id="c862b-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="c862b-229">Connessione macchina virtuale separata toohello esattamente come si farebbe qualsiasi altro computer e quindi è possibile accedere in remoto hello le macchine virtuali in hello scala set toomonitor singoli processi.</span><span class="sxs-lookup"><span data-stu-id="c862b-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c862b-230">Nell'articolo [Set di scalabilità di macchine virtuali](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="c862b-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="c862b-231">Passaggio 7: Rimuovere le risorse di hello</span><span class="sxs-lookup"><span data-stu-id="c862b-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="c862b-232">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre un risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="c862b-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="c862b-233">Non è necessario toodelete ogni risorsa separatamente da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c862b-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="c862b-234">È possibile eliminare il gruppo di risorse hello e tutte le relative risorse vengono eliminate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c862b-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="c862b-235">Se si desidera tookeep il gruppo di risorse, è possibile eliminare solo set di scalabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="c862b-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="c862b-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c862b-236">Next steps</span></span>
* <span data-ttu-id="c862b-237">Gestire i set di scalabilità hello appena creata utilizzando informazioni hello in [gestire macchine virtuali in un Set di scalabilità della macchina virtuale](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="c862b-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="c862b-238">Altre informazioni sull'aumento delle prestazioni sono disponibili in [Scalabilità automatica verticale con set di scalabilità di macchine virtuali](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="c862b-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="c862b-239">Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="c862b-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="c862b-240">Informazioni sulle funzionalità di notifica di [utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="c862b-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="c862b-241">Informazioni su come troppo[i log di controllo di utilizzare le notifiche degli avvisi di posta elettronica e ai webhook toosend in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="c862b-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

