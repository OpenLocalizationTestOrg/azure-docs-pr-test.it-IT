---
title: "Ridimensionare set di scalabilità di macchine virtuali Linux | Microsoft Docs"
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
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="03d10-103">Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="03d10-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="03d10-104">I set di scalabilità di macchine virtuali semplificano la distribuzione e la gestione di macchine virtuali identiche come un set.</span><span class="sxs-lookup"><span data-stu-id="03d10-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="03d10-105">I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni.</span><span class="sxs-lookup"><span data-stu-id="03d10-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="03d10-106">Per altre informazioni, vedere [Panoramica dei set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="03d10-107">Questa esercitazione illustra come creare un set di scalabilità per macchine virtuali Linux con la versione più recente di Linux Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="03d10-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="03d10-108">L'esercitazione mostra inoltre come ridimensionare automaticamente le macchine nel set.</span><span class="sxs-lookup"><span data-stu-id="03d10-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="03d10-109">Per creare il set di scalabilità e configurare il ridimensionamento, creare un modello di Azure Resource Manager e distribuirlo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="03d10-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="03d10-110">Per altre informazioni sui modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="03d10-111">Per altre informazioni sul ridimensionamento automatico dei set di scalabilità, vedere [Ridimensionamento automatico e set di scalabilità di macchine virtuali](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="03d10-112">In questa esercitazione verranno distribuite le risorse e le estensioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="03d10-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="03d10-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="03d10-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="03d10-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="03d10-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="03d10-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="03d10-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="03d10-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="03d10-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="03d10-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="03d10-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="03d10-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="03d10-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="03d10-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="03d10-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="03d10-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="03d10-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="03d10-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="03d10-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="03d10-122">Per altre informazioni sulle risorse di Resource Manager, vedere [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="03d10-123">Prima di iniziare con i passaggi illustrati in questa esercitazione, [installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="03d10-124">Passaggio 1: Creare un gruppo di risorse e un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="03d10-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="03d10-125">**Accedere a Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="03d10-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="03d10-126">Nell'interfaccia della riga di comando (Bash, terminale, prompt dei comandi) passare alla modalità Gestione risorse e quindi [accedere con l'ID aziendale o dell'istituto di istruzione](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Seguire le istruzioni per un'esperienza di accesso interattivo al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="03d10-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="03d10-127">Se si ha un ID aziendale o dell'istituto di istruzione e l'autenticazione a due fattori non è abilitata, usare `azure login -u` con l'ID per eseguire l'accesso senza una sessione interattiva.</span><span class="sxs-lookup"><span data-stu-id="03d10-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="03d10-128">Se non si ha un'identità aziendale o dell'istituto di istruzione, è possibile [crearne una dall'account Microsoft personale](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="03d10-129">**Creare un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="03d10-129">**Create a resource group**</span></span>  
<span data-ttu-id="03d10-130">Tutte le risorse devono essere distribuite in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="03d10-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="03d10-131">Per questa esercitazione, assegnare al gruppo di risorse il nome **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="03d10-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="03d10-132">**Distribuire un account di archiviazione nel nuovo gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="03d10-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="03d10-133">Questo account di archiviazione si deve trovare nella posizione in cui è archiviato il modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="03d10-134">Creare un account di archiviazione denominato **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="03d10-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="03d10-135">Passaggio 2: Creare il modello</span><span class="sxs-lookup"><span data-stu-id="03d10-135">Step 2: Create the template</span></span>
<span data-ttu-id="03d10-136">Un modello di Gestione risorse di Azure permette di distribuire e gestire le risorse di Azure insieme tramite una descrizione JSON delle risorse e dei parametri di distribuzione associati.</span><span class="sxs-lookup"><span data-stu-id="03d10-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="03d10-137">In un editor a scelta creare il file VMSSTemplate.json e aggiungere la struttura JSON iniziale a supporto del modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

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

2. <span data-ttu-id="03d10-138">I parametri non sono sempre obbligatori, ma forniscono un modo per immettere i valori quando il modello viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="03d10-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="03d10-139">Aggiungere questi parametri all'interno dell'elemento padre dei parametri aggiunto al modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="03d10-140">Nome per la macchina virtuale separata usata per accedere alle macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="03d10-141">Nome per l'account di archiviazione in cui è archiviato il modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="03d10-142">Numero di istanze di macchine virtuali da creare inizialmente nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="03d10-143">Nome e password dell'account amministratore nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="03d10-144">Prefisso del nome per le risorse create per supportare il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="03d10-145">Le variabili in un modello possono essere usate per specificare valori che possono subire modifiche frequenti o che devono essere creati da una combinazione di valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="03d10-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="03d10-146">Aggiungere queste variabili all'interno dell'elemento padre delle variabili aggiunto al modello:</span><span class="sxs-lookup"><span data-stu-id="03d10-146">Add these variables under the variables parent element that you added to the template.</span></span>

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

   * <span data-ttu-id="03d10-147">Nomi DNS che vengono usati dalle interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="03d10-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="03d10-148">Prefissi e nomi di indirizzi IP per la rete virtuale e le subnet.</span><span class="sxs-lookup"><span data-stu-id="03d10-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="03d10-149">Nomi e identificatori di rete virtuale, servizio di bilanciamento del carico e rete.</span><span class="sxs-lookup"><span data-stu-id="03d10-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="03d10-150">Nomi di account di archiviazione per gli account associati alle macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="03d10-151">Impostazioni per l'estensione Diagnostica installata nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="03d10-152">Per altre informazioni sull'estensione Diagnostica, vedere [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante il modello di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03d10-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="03d10-153">Aggiungere la risorsa account di archiviazione all'interno dell'elemento padre delle risorse aggiunto al modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="03d10-154">Questo modello usa un ciclo per creare cinque account di archiviazione consigliati in cui sono archiviati i dischi del sistema operativo e i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="03d10-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="03d10-155">Questo set di account può supportare fino a 100 macchine virtuali in un set di scalabilità, ovvero il limite massimo corrente.</span><span class="sxs-lookup"><span data-stu-id="03d10-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="03d10-156">A ogni account di archiviazione è assegnato un nome costituito da un indicatore di lettera definito nelle variabili in combinazione con il suffisso specificato nei parametri per il modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
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

5. <span data-ttu-id="03d10-157">Aggiungere la risorsa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="03d10-157">Add the virtual network resource.</span></span> <span data-ttu-id="03d10-158">Per altre informazioni, vedere [Provider di risorse di rete](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="03d10-159">Aggiungere le risorse indirizzo IP pubblico usate dal servizio di bilanciamento del carico e l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="03d10-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

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

7. <span data-ttu-id="03d10-160">Aggiungere la risorsa servizio di bilanciamento del carico usata dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="03d10-161">Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="03d10-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="03d10-162">Aggiungere la risorsa interfaccia di rete usata dalla macchina virtuale separata.</span><span class="sxs-lookup"><span data-stu-id="03d10-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="03d10-163">Poiché non è possibile accedere tramite un indirizzo IP pubblico alle macchine virtuali di un set di scalabilità, viene creata una macchina virtuale separata nella stessa rete virtuale che verrà usata per accedere in modalità remota alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

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

9. <span data-ttu-id="03d10-164">Aggiungere la macchina virtuale separata nella stessa rete del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-164">Add the separate virtual machine in the same network as the scale set.</span></span>

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

10. <span data-ttu-id="03d10-165">Aggiungere la risorsa set di scalabilità di macchine virtuali e specificare l'estensione di Diagnostica installata in tutte le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="03d10-166">Molte delle impostazioni per questa risorsa sono simili a quelle della risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03d10-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="03d10-167">Le differenze principali sono l'elemento capacity, che specifica il numero di macchine virtuali nel set di scalabilità, e l'elemento upgradePolicy, che specifica la modalità di esecuzione degli aggiornamenti delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="03d10-168">Il set di scalabilità viene creato solo dopo che sono stati creati tutti gli account di archiviazione come specificato nell'elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="03d10-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

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

11. <span data-ttu-id="03d10-169">Aggiungere la risorsa autoscaleSettings che definisce la modalità di regolazione del set di scalabilità in base all'uso dei processori delle macchine virtuali nel set.</span><span class="sxs-lookup"><span data-stu-id="03d10-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

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
    
    <span data-ttu-id="03d10-170">Per questa esercitazione, i valori importanti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="03d10-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="03d10-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="03d10-171">**metricName**</span></span>  
    <span data-ttu-id="03d10-172">Questo valore corrisponde al contatore delle prestazioni definito nella variabile wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="03d10-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="03d10-173">Con questa variabile, l'estensione Diagnostica raccoglie i dati del contatore **Processor\PercentProcessorTime**.</span><span class="sxs-lookup"><span data-stu-id="03d10-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="03d10-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="03d10-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="03d10-175">Questo valore è l'identificatore di risorsa del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="03d10-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="03d10-176">**timeGrain**</span></span>  
    <span data-ttu-id="03d10-177">Questo valore corrisponde alla granularità delle metriche che vengono raccolte.</span><span class="sxs-lookup"><span data-stu-id="03d10-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="03d10-178">In questo modello il valore è impostato su un minuto.</span><span class="sxs-lookup"><span data-stu-id="03d10-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="03d10-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="03d10-179">**statistic**</span></span>  
    <span data-ttu-id="03d10-180">Questo valore determina il modo in cui vengono combinate le metriche per consentire l'azione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="03d10-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="03d10-181">I valori possibili sono: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="03d10-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="03d10-182">In questo modello viene raccolto l'utilizzo medio totale della CPU delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="03d10-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="03d10-183">**timeWindow**</span></span>  
    <span data-ttu-id="03d10-184">Questo valore rappresenta l'intervallo di tempo in cui vengono raccolti i dati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="03d10-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="03d10-185">Deve essere compreso tra 5 minuti e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="03d10-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="03d10-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="03d10-186">**timeAggregation**</span></span>  
    <span data-ttu-id="03d10-187">Questo valore definisce il modo in cui i dati raccolti devono essere combinati nel tempo.</span><span class="sxs-lookup"><span data-stu-id="03d10-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="03d10-188">Il valore predefinito è "Average".</span><span class="sxs-lookup"><span data-stu-id="03d10-188">The default value is Average.</span></span> <span data-ttu-id="03d10-189">I valori possibili sono: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="03d10-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="03d10-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="03d10-190">**operator**</span></span>  
    <span data-ttu-id="03d10-191">Questo valore indica l'operatore usato per confrontare i dati della metrica e la soglia.</span><span class="sxs-lookup"><span data-stu-id="03d10-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="03d10-192">I valori possibili sono: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="03d10-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="03d10-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="03d10-193">**threshold**</span></span>  
    <span data-ttu-id="03d10-194">Questo valore attiva l'azione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="03d10-194">This value triggers the scale action.</span></span> <span data-ttu-id="03d10-195">In questo modello le macchine virtuali vengono aggiunte al set di scalabilità quando l'utilizzo medio della CPU tra le macchine nel set supera il 50%.</span><span class="sxs-lookup"><span data-stu-id="03d10-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="03d10-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="03d10-196">**direction**</span></span>  
    <span data-ttu-id="03d10-197">Questo valore determina l'azione da eseguire quando viene raggiunto il valore di soglia.</span><span class="sxs-lookup"><span data-stu-id="03d10-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="03d10-198">I valori possibili sono Increase o Decrease.</span><span class="sxs-lookup"><span data-stu-id="03d10-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="03d10-199">In questo modello il numero di macchine virtuali nel set di scalabilità viene aumentato se la soglia supera il 50% nell'intervallo di tempo definito.</span><span class="sxs-lookup"><span data-stu-id="03d10-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="03d10-200">**type**</span><span class="sxs-lookup"><span data-stu-id="03d10-200">**type**</span></span>  
    <span data-ttu-id="03d10-201">Questo valore indica il tipo di azione che deve verificarsi e deve essere impostato su ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="03d10-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="03d10-202">**value**</span><span class="sxs-lookup"><span data-stu-id="03d10-202">**value**</span></span>  
    <span data-ttu-id="03d10-203">Questo valore indica il numero di macchine virtuali che vengono aggiunte o rimosse dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="03d10-204">Questo valore deve essere uguale o maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="03d10-204">This value must be 1 or greater.</span></span> <span data-ttu-id="03d10-205">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="03d10-205">The default value is 1.</span></span> <span data-ttu-id="03d10-206">In questo modello il numero di macchine virtuali nel set di scalabilità aumenta di 1 quando viene raggiunta la soglia.</span><span class="sxs-lookup"><span data-stu-id="03d10-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="03d10-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="03d10-207">**cooldown**</span></span>  
    <span data-ttu-id="03d10-208">Questo valore indica il tempo di attesa dopo l'ultima azione di ridimensionamento prima che venga eseguita l'azione successiva.</span><span class="sxs-lookup"><span data-stu-id="03d10-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="03d10-209">Questo valore deve essere compreso tra un minuto e una settimana.</span><span class="sxs-lookup"><span data-stu-id="03d10-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="03d10-210">Salvare il file di modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="03d10-211">Passaggio 3: Caricare il modello nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="03d10-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="03d10-212">È possibile caricare il modello purché si conosca il nome e la chiave primaria dell'account di archiviazione creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="03d10-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="03d10-213">Nell'interfaccia della riga di comando (Bash, terminale, prompt dei comandi), eseguire questi comandi per impostare le variabili di ambiente necessarie per accedere all'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="03d10-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="03d10-214">È possibile ottenere la chiave facendo clic sull'icona della chiave durante la visualizzazione della risorsa account di archiviazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="03d10-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="03d10-215">Se si usa il prompt dei comandi di Windows, digitare **set** anziché export.</span><span class="sxs-lookup"><span data-stu-id="03d10-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="03d10-216">Creare il contenitore per l'archiviazione del modello.</span><span class="sxs-lookup"><span data-stu-id="03d10-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="03d10-217">Caricare il file di modello nel nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="03d10-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="03d10-218">Passaggio 4: Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="03d10-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="03d10-219">Dopo aver creato il modello, è possibile avviare la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="03d10-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="03d10-220">Per avviare il processo, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="03d10-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="03d10-221">Dopo aver premuto INVIO, verrà richiesto di specificare i valori per le variabili assegnate.</span><span class="sxs-lookup"><span data-stu-id="03d10-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="03d10-222">Specificare questi valori:</span><span class="sxs-lookup"><span data-stu-id="03d10-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="03d10-223">La distribuzione di tutte le risorse richiederà circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="03d10-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="03d10-224">Per distribuire le risorse, è anche possibile usare il portale.</span><span class="sxs-lookup"><span data-stu-id="03d10-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="03d10-225">Usare questo collegamento: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="03d10-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="03d10-226">Passaggio 5: Monitorare le risorse</span><span class="sxs-lookup"><span data-stu-id="03d10-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="03d10-227">Per ottenere informazioni sui set di scalabilità di macchine virtuali, è possibile usare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="03d10-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="03d10-228">Portale di Azure: attualmente è possibile ottenere una quantità limitata di informazioni tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="03d10-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="03d10-229">[Esplora risorse di Azure](https://resources.azure.com/) : si tratta dello strumento migliore per esaminare lo stato corrente del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="03d10-230">Seguire questo percorso per passare alla visualizzazione dell'istanza del set di scalabilità creato:</span><span class="sxs-lookup"><span data-stu-id="03d10-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="03d10-231">Interfaccia della riga di comando di Azure. Usare questo comando per ottenere alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="03d10-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="03d10-232">Connettersi alla macchina virtuale jumpbox esattamente come a qualsiasi altra macchina virtuale e quindi accedere in modalità remota alle macchine virtuali nel set di scalabilità per monitorare i singoli processi.</span><span class="sxs-lookup"><span data-stu-id="03d10-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="03d10-233">Nell'articolo relativo ai [set di scalabilità di macchine virtuali](https://msdn.microsoft.com/library/mt589023.aspx)è disponibile un'API REST completa per ottenere informazioni sui set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="03d10-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="03d10-234">Passaggio 6: Rimuovere le risorse</span><span class="sxs-lookup"><span data-stu-id="03d10-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="03d10-235">Poiché vengono applicati addebiti per le risorse usate in Azure, è sempre consigliabile eliminare le risorse che non sono più necessarie.</span><span class="sxs-lookup"><span data-stu-id="03d10-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="03d10-236">Non è necessario eliminare separatamente ogni risorsa da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="03d10-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="03d10-237">È possibile eliminare il gruppo di risorse e tutte le relative risorse automaticamente.</span><span class="sxs-lookup"><span data-stu-id="03d10-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="03d10-238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03d10-238">Next steps</span></span>
* <span data-ttu-id="03d10-239">Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma di Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="03d10-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="03d10-240">Per informazioni sulle funzionalità di notifica, vedere [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md) (Usare le azioni di scalabilità automatica per inviare notifiche di avviso tramite e-mail e webhook in Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="03d10-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="03d10-241">Per informazioni, vedere [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md) (Usare i log di controllo per inviare notifiche di avviso tramite e-mail e webhook in Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="03d10-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="03d10-242">Vedere il modello di [app demo per la scalabilità automatica su Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) che consente di configurare un'app Python/Bottle per applicare la funzionalità di ridimensionamento automatico dei set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03d10-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

