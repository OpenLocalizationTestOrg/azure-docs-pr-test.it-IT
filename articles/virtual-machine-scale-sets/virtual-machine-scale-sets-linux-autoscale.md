---
title: "Set di scalabilità di macchine virtuali Linux aaaAutoscale | Documenti Microsoft"
description: "Impostare il ridimensionamento automatico per un set di scalabilità di macchine virtuali Linux tramite l'interfaccia della riga di comando di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="a6606-103">Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a6606-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="a6606-104">Set di scalabilità di macchine virtuali semplificano automaticamente toodeploy e gestire macchine virtuali identiche come un set.</span><span class="sxs-lookup"><span data-stu-id="a6606-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="a6606-105">I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni.</span><span class="sxs-lookup"><span data-stu-id="a6606-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="a6606-106">vedere, più toolearn [Panoramica set di scalabilità della macchina virtuale](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="a6606-107">Questa esercitazione viene illustrato come imposta di toocreate una scala di macchine virtuali Linux con una versione più recente di hello di Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="a6606-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="a6606-108">esercitazione Hello illustra anche come tooautomatically scala hello computer hello impostato.</span><span class="sxs-lookup"><span data-stu-id="a6606-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="a6606-109">Creare una scala hello e impostare il ridimensionamento per la creazione di un modello di gestione risorse di Azure e la distribuzione utilizzando l'interfaccia CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6606-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="a6606-110">Per altre informazioni sui modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a6606-111">toolearn più sul ridimensionamento automatico del set di scalabilità, vedere [il ridimensionamento automatico e imposta la scala di macchina virtuale](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="a6606-112">In questa esercitazione, si distribuisce seguente hello risorse ed estensioni:</span><span class="sxs-lookup"><span data-stu-id="a6606-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="a6606-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="a6606-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="a6606-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="a6606-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="a6606-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="a6606-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="a6606-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="a6606-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="a6606-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="a6606-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="a6606-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a6606-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="a6606-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="a6606-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="a6606-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="a6606-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="a6606-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="a6606-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="a6606-122">Per altre informazioni sulle risorse di Resource Manager, vedere [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="a6606-123">Prima di iniziare a utilizzare i passaggi di hello in questa esercitazione, [installare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="a6606-124">Passaggio 1: Creare un gruppo di risorse e un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a6606-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="a6606-125">**Accedi tooMicrosoft Azure**</span><span class="sxs-lookup"><span data-stu-id="a6606-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="a6606-126">In un'interfaccia della riga di comando (Bash, Terminal, prompt dei comandi) passare tooResource modalità di gestione, quindi [accedere con l'id aziendale o dell'istituto di istruzione](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Seguire le istruzioni di hello per un tooyour esperienza di accesso interattivo account Azure.</span><span class="sxs-lookup"><span data-stu-id="a6606-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="a6606-127">Se si dispone di un o dell'istituto di istruzione ID e non avere attivata l'autenticazione a due fattori, utilizzare `azure login -u` con toolog di ID hello in senza una sessione interattiva.</span><span class="sxs-lookup"><span data-stu-id="a6606-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="a6606-128">Se non si ha un'identità aziendale o dell'istituto di istruzione, è possibile [crearne una dall'account Microsoft personale](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="a6606-129">**Creare un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="a6606-129">**Create a resource group**</span></span>  
<span data-ttu-id="a6606-130">Tutte le risorse devono essere distribuito tooa gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a6606-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="a6606-131">Per questa esercitazione, denominare il gruppo di risorse hello **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="a6606-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="a6606-132">**La distribuzione di un account di archiviazione nel nuovo gruppo di risorse hello**</span><span class="sxs-lookup"><span data-stu-id="a6606-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="a6606-133">Questo account di archiviazione è in cui è archiviato il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="a6606-134">Creare un account di archiviazione denominato **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="a6606-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="a6606-135">Passaggio 2: Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="a6606-135">Step 2: Create hello template</span></span>
<span data-ttu-id="a6606-136">Un modello di gestione risorse di Azure rende possibile la si toodeploy e gestire le risorse di Azure insieme con una descrizione JSON delle risorse di hello e parametri di distribuzione associati.</span><span class="sxs-lookup"><span data-stu-id="a6606-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="a6606-137">Nell'editor preferito, creare file hello VMSSTemplate.json e aggiungere hello iniziale JSON struttura toosupport hello modello.</span><span class="sxs-lookup"><span data-stu-id="a6606-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="a6606-138">Parametri non sono sempre necessari, ma forniscono un modo tooinput valori quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="a6606-139">Aggiungere i parametri che è stato aggiunto il modello di toohello nell'elemento padre parametri hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="a6606-140">Un nome per la macchina virtuale separata hello che viene utilizzato tooaccess hello macchine nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a6606-141">Un nome per l'account di archiviazione hello in cui è archiviato il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="a6606-142">numero di Hello di istanze di macchine virtuali tooinitially crea nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="a6606-143">Un nome e una password dell'account di amministratore hello in macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="a6606-144">Imposta un prefisso del nome per le risorse di hello scala hello toosupport creati.</span><span class="sxs-lookup"><span data-stu-id="a6606-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="a6606-145">Variabili possono essere utilizzate nei valori di toospecify modello che possono cambiare frequentemente o valori che devono toobe creato da una combinazione di valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="a6606-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="a6606-146">Aggiungere queste variabili che è stato aggiunto il modello di toohello nell'elemento padre variabili hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="a6606-147">I nomi DNS che vengono utilizzati da hello interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="a6606-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="a6606-148">i nomi degli indirizzi IP di Hello e i prefissi di rete virtuale hello e le subnet.</span><span class="sxs-lookup"><span data-stu-id="a6606-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="a6606-149">Hello nomi e gli identificatori di rete virtuale hello, bilanciamento del carico e le interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="a6606-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="a6606-150">Nomi account di archiviazione per gli account di hello associati macchine hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a6606-151">Impostazioni per l'estensione di diagnostica che viene installato nelle macchine virtuali hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="a6606-152">Per ulteriori informazioni su hello estensione di diagnostica, vedere [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6606-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="a6606-153">Aggiungere risorse di account di archiviazione hello nell'elemento padre di risorse hello che è stato aggiunto il modello di toohello.</span><span class="sxs-lookup"><span data-stu-id="a6606-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="a6606-154">Il modello utilizza un hello toocreate ciclo consigliato cinque gli account di archiviazione in cui sono archiviati i dischi del sistema operativo hello e dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="a6606-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="a6606-155">Questo set di account può supportare fino a too100 di macchine virtuali in un set di scalabilità, ossia massimo corrente hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="a6606-156">Ogni account di archiviazione denominato con un indicatore lettera definite nelle variabili hello combinate con il suffisso hello forniti nei parametri hello per modello hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="a6606-157">Aggiungere risorse di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-157">Add hello virtual network resource.</span></span> <span data-ttu-id="a6606-158">Per altre informazioni, vedere [Provider di risorse di rete](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="a6606-159">Aggiungere hello pubbliche risorse indirizzo IP utilizzati da hello bilanciamento del caricano e l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a6606-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="a6606-160">Aggiungere una risorsa di bilanciamento del carico hello utilizzato dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="a6606-161">Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a6606-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="a6606-162">Aggiungere risorse di interfaccia di rete hello utilizzato dalla macchina virtuale separata hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="a6606-163">Poiché le macchine in un set di scalabilità non sono accessibili tramite un indirizzo IP pubblico, una macchina virtuale separata viene creata in hello stesso virtuale macchine di hello tooremotely accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="a6606-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="a6606-164">Aggiungere una macchina virtuale separata hello nella stessa rete set di scalabilità hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="a6606-165">Aggiungere una risorsa del set di scalabilità della macchina virtuale hello e specificare l'estensione diagnostica hello installato in tutte le macchine virtuali nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="a6606-166">Molte delle impostazioni di hello per questa risorsa sono simili alla risorsa di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="a6606-167">Hello principali differenze riguardano elemento capacità hello che specifica il numero di hello di macchine virtuali nel set di scalabilità hello e upgradePolicy che specifica la modalità con cui gli aggiornamenti vengono eseguiti toovirtual macchine.</span><span class="sxs-lookup"><span data-stu-id="a6606-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="a6606-168">Hello set di scalabilità non viene creata finché non vengono creati tutti gli account di archiviazione hello come specificato con l'elemento dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="a6606-169">Aggiungere hello autoscaleSettings risorsa che definisce la modalità in base all'utilizzo del processore nei computer hello nel set di hello hello set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a6606-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="a6606-170">Per questa esercitazione, i valori importanti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6606-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="a6606-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="a6606-171">**metricName**</span></span>  
    <span data-ttu-id="a6606-172">Questo valore è hello stesso come contatore delle prestazioni hello definiti nella variabile wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="a6606-173">Utilizzo di tale variabile, hello estensione di diagnostica raccoglie hello **Processor\PercentProcessorTime** contatore.</span><span class="sxs-lookup"><span data-stu-id="a6606-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="a6606-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="a6606-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="a6606-175">Questo valore è l'identificatore di risorsa hello del set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="a6606-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="a6606-176">**timeGrain**</span></span>  
    <span data-ttu-id="a6606-177">Questo valore è la granularità hello di metriche di hello che vengono raccolti.</span><span class="sxs-lookup"><span data-stu-id="a6606-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="a6606-178">In questo modello, è impostato tooone minuto.</span><span class="sxs-lookup"><span data-stu-id="a6606-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="a6606-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="a6606-179">**statistic**</span></span>  
    <span data-ttu-id="a6606-180">Questo valore determina come le metriche hello vengono combinati tooaccommodate hello azione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="a6606-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="a6606-181">Hello i valori possibili sono: Media, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="a6606-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="a6606-182">In questo modello, verrà raccolti hello totale utilizzo medio della CPU delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="a6606-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="a6606-183">**timeWindow**</span></span>  
    <span data-ttu-id="a6606-184">Questo valore è hello intervallo di tempo in cui vengono raccolti i dati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="a6606-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="a6606-185">Deve essere compreso tra 5 minuti e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="a6606-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="a6606-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="a6606-186">**timeAggregation**</span></span>  
    <span data-ttu-id="a6606-187">il suo valore determina la modalità hello i dati raccolti devono essere combinati nel tempo.</span><span class="sxs-lookup"><span data-stu-id="a6606-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="a6606-188">valore predefinito di Hello è Media.</span><span class="sxs-lookup"><span data-stu-id="a6606-188">hello default value is Average.</span></span> <span data-ttu-id="a6606-189">Hello i valori possibili sono: Media, minimo, massimo, ultimo, totale, conteggio.</span><span class="sxs-lookup"><span data-stu-id="a6606-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="a6606-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="a6606-190">**operator**</span></span>  
    <span data-ttu-id="a6606-191">Questo valore è l'operatore hello toocompare utilizzati hello metrica hello e dati soglia.</span><span class="sxs-lookup"><span data-stu-id="a6606-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="a6606-192">Hello i valori possibili sono: uguale a, diverso da, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="a6606-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="a6606-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="a6606-193">**threshold**</span></span>  
    <span data-ttu-id="a6606-194">Questo valore attiva l'azione di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-194">This value triggers hello scale action.</span></span> <span data-ttu-id="a6606-195">In questo modello, i computer vengono aggiunti toohello scala impostata quando l'utilizzo medio della CPU hello tra le macchine nel set di hello è oltre il 50%.</span><span class="sxs-lookup"><span data-stu-id="a6606-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="a6606-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="a6606-196">**direction**</span></span>  
    <span data-ttu-id="a6606-197">Questo valore determina l'azione eseguita quando viene raggiunto il valore di soglia hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="a6606-198">i valori possibili di Hello sono aumentano o diminuiscono.</span><span class="sxs-lookup"><span data-stu-id="a6606-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="a6606-199">In questo modello, hello numero di macchine virtuali nel set di scalabilità hello viene aumentato se la soglia di hello è oltre il 50% di tempo definito hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="a6606-200">**type**</span><span class="sxs-lookup"><span data-stu-id="a6606-200">**type**</span></span>  
    <span data-ttu-id="a6606-201">Questo valore è di tipo hello di azione che deve essere eseguita e deve essere impostato tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="a6606-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="a6606-202">**value**</span><span class="sxs-lookup"><span data-stu-id="a6606-202">**value**</span></span>  
    <span data-ttu-id="a6606-203">Questo valore è il numero di hello di macchine virtuali che vengono aggiunti o rimossi dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="a6606-204">Questo valore deve essere uguale o maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="a6606-204">This value must be 1 or greater.</span></span> <span data-ttu-id="a6606-205">valore predefinito di Hello è 1.</span><span class="sxs-lookup"><span data-stu-id="a6606-205">hello default value is 1.</span></span> <span data-ttu-id="a6606-206">In questo modello, hello macchine nella scala hello impostare numerose aumenta di 1 quando viene raggiunta la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="a6606-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="a6606-207">**cooldown**</span></span>  
    <span data-ttu-id="a6606-208">Questo valore è quantità hello di toowait tempo dall'ultima azione di scalabilità hello prima che si verifichi l'azione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="a6606-209">Questo valore deve essere compreso tra un minuto e una settimana.</span><span class="sxs-lookup"><span data-stu-id="a6606-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="a6606-210">Salvare il file di modello hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="a6606-211">Passaggio 3: Caricare hello modello toostorage</span><span class="sxs-lookup"><span data-stu-id="a6606-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="a6606-212">è possibile caricare il modello di Hello, purché si conosce il nome di hello e la chiave primaria dell'account di archiviazione hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="a6606-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="a6606-213">Nell'interfaccia della riga di comando (Bash, Terminal, prompt dei comandi) eseguire questi comandi le variabili di ambiente hello tooset necessari tooaccess hello account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a6606-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="a6606-214">È possibile ottenere la chiave hello facendo clic sull'icona chiave hello durante la visualizzazione di risorse di account di archiviazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6606-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="a6606-215">Se si usa il prompt dei comandi di Windows, digitare **set** anziché export.</span><span class="sxs-lookup"><span data-stu-id="a6606-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="a6606-216">Creare il contenitore di hello per archiviare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="a6606-217">Caricare hello modello file toohello nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="a6606-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="a6606-218">Passaggio 4: Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="a6606-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="a6606-219">Ora che è stato creato il modello di hello, è possibile avviare la distribuzione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="a6606-220">Utilizzare questo processo di hello toostart comando:</span><span class="sxs-lookup"><span data-stu-id="a6606-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="a6606-221">Quando preme INVIO, sei valori tooprovide richiesta per le variabili di hello che è assegnato.</span><span class="sxs-lookup"><span data-stu-id="a6606-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="a6606-222">Specificare questi valori:</span><span class="sxs-lookup"><span data-stu-id="a6606-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="a6606-223">Richiede circa 15 minuti per essere distribuito tutti hello risorse toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="a6606-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="a6606-224">È possibile utilizzare anche le risorse di hello del portale hello possibilità toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a6606-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="a6606-225">Usare questo collegamento: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="a6606-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="a6606-226">Passaggio 5: Monitorare le risorse</span><span class="sxs-lookup"><span data-stu-id="a6606-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="a6606-227">Per ottenere informazioni sui set di scalabilità di macchine virtuali, è possibile usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6606-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="a6606-228">portale di Azure Hello: attualmente è possibile ottenere una quantità limitata di informazioni tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="a6606-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="a6606-229">Hello [Esplora inventario risorse di Azure](https://resources.azure.com/) -questo strumento è hello migliore per l'esplorazione dello stato corrente di hello del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a6606-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="a6606-230">Seguire questo percorso e dovrebbe essere vista istanza hello della scala hello imposta creato:</span><span class="sxs-lookup"><span data-stu-id="a6606-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="a6606-231">CLI di Azure - usare questo comando tooget alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="a6606-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="a6606-232">Connessione macchina virtuale di toohello jumpbox esattamente come si farebbe qualsiasi altro computer e quindi è possibile accedere in remoto hello le macchine virtuali in hello scala set toomonitor singoli processi.</span><span class="sxs-lookup"><span data-stu-id="a6606-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a6606-233">Nell'articolo relativo ai [set di scalabilità di macchine virtuali](https://msdn.microsoft.com/library/mt589023.aspx)è disponibile un'API REST completa per ottenere informazioni sui set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a6606-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="a6606-234">Passaggio 6: Rimuovere le risorse di hello</span><span class="sxs-lookup"><span data-stu-id="a6606-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="a6606-235">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre un risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="a6606-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="a6606-236">Non è necessario toodelete ogni risorsa separatamente da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a6606-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="a6606-237">È possibile eliminare il gruppo di risorse hello e tutte le relative risorse vengono eliminate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a6606-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="a6606-238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6606-238">Next steps</span></span>
* <span data-ttu-id="a6606-239">Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma di Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="a6606-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="a6606-240">Informazioni sulle funzionalità di notifica di [utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a6606-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="a6606-241">Informazioni su come troppo[i log di controllo di utilizzare le notifiche degli avvisi di posta elettronica e ai webhook toosend in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a6606-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="a6606-242">Estrarre hello [app demo di scalabilità automatica in Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modello che consente di impostare un hello tooexercise di app Python/bottle funzionalità di scalabilità di macchine virtuali imposta la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="a6606-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

