---
title: "Informazioni sui modelli di set di scalabilità di macchine virtuali | Microsoft Docs"
description: "Informazioni su come creare un modello di set di scalabilità a validità minima per set di scalabilità di macchine virtuali di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: 65f02c4675eb752dcc82e9a1d1c7f6c2c193fc32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="56771-103">Informazioni sui modelli di set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="56771-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="56771-104">I [modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) sono un ottimo modo di distribuire gruppi di risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="56771-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="56771-105">Questa serie di esercitazioni illustra come creare un modello di set di scalabilità a validità minima e come modificarlo per adattarsi a vari scenari.</span><span class="sxs-lookup"><span data-stu-id="56771-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span></span> <span data-ttu-id="56771-106">Tutti gli esempi provengono da questo [archivio GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="56771-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="56771-107">Questo modello è progettato per essere semplice.</span><span class="sxs-lookup"><span data-stu-id="56771-107">This template is intended to be simple.</span></span> <span data-ttu-id="56771-108">Per esempi più completi di modelli di set di scalabilità, vedere [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) (Archivio GitHub Modelli di avvio rapido di Azure) e cercare le cartelle contenenti la stringa `vmss`.</span><span class="sxs-lookup"><span data-stu-id="56771-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span></span>

<span data-ttu-id="56771-109">Se si ha già familiarità con i modelli, è possibile passare direttamente alla sezione "Passaggi successivi" per informazioni su come modificare questo modello.</span><span class="sxs-lookup"><span data-stu-id="56771-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span></span>

## <a name="review-the-template"></a><span data-ttu-id="56771-110">Rivedere il modello</span><span class="sxs-lookup"><span data-stu-id="56771-110">Review the template</span></span>

<span data-ttu-id="56771-111">Usare GitHub per rivedere il modello di set di scalabilità a validità minima che è possibile usare, ovvero [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="56771-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="56771-112">In questa esercitazione verranno esaminati in dettaglio i diff (`git diff master minimum-viable-scale-set`) per creare il modello di set di scalabilità più semplice che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="56771-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="56771-113">Definire $schema e contentVersion</span><span class="sxs-lookup"><span data-stu-id="56771-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="56771-114">Si definiscono prima gli elementi `$schema` e `contentVersion` del modello.</span><span class="sxs-lookup"><span data-stu-id="56771-114">First, we define `$schema` and `contentVersion` in the template.</span></span> <span data-ttu-id="56771-115">L'elemento `$schema` definisce la versione del linguaggio del modello e viene usato per l'evidenziazione della sintassi di Visual Studio e per funzionalità di convalida simili.</span><span class="sxs-lookup"><span data-stu-id="56771-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="56771-116">L'elemento `contentVersion` non viene usato da Azure.</span><span class="sxs-lookup"><span data-stu-id="56771-116">The `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="56771-117">Però consente di tenere traccia della versione del modello.</span><span class="sxs-lookup"><span data-stu-id="56771-117">Instead, it helps you keep track of the template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="56771-118">Definire i parametri</span><span class="sxs-lookup"><span data-stu-id="56771-118">Define parameters</span></span>
<span data-ttu-id="56771-119">Successivamente, si definiscono due parametri, `adminUsername` e `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="56771-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="56771-120">I parametri sono valori specificati al momento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="56771-120">Parameters are values you specify at the time of deployment.</span></span> <span data-ttu-id="56771-121">Il parametro `adminUsername` è semplicemente un tipo `string`, ma dato che `adminPassword` è un segreto, gli viene assegnato il tipo `securestring`.</span><span class="sxs-lookup"><span data-stu-id="56771-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="56771-122">Successivamente questi parametri vengono passati nella configurazione del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="56771-122">Later, these parameters are passed into the scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="56771-123">Definire le variabili</span><span class="sxs-lookup"><span data-stu-id="56771-123">Define variables</span></span>
<span data-ttu-id="56771-124">I modelli di Resource Manager consentono anche di definire variabili da usare successivamente nel modello.</span><span class="sxs-lookup"><span data-stu-id="56771-124">Resource Manager templates also let you define variables to be used later in the template.</span></span> <span data-ttu-id="56771-125">In questo esempio non vengono usate variabili, quindi l'oggetto JSON è vuoto.</span><span class="sxs-lookup"><span data-stu-id="56771-125">Our example doesn't use any variables, so we've left the JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="56771-126">Definire le risorse</span><span class="sxs-lookup"><span data-stu-id="56771-126">Define resources</span></span>
<span data-ttu-id="56771-127">La sezione successiva del modello riguarda le risorse.</span><span class="sxs-lookup"><span data-stu-id="56771-127">Next is the resources section of the template.</span></span> <span data-ttu-id="56771-128">In questa sezione si definiscono gli elementi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="56771-128">Here, you define what you actually want to deploy.</span></span> <span data-ttu-id="56771-129">A differenza di `parameters` e `variables` (che sono oggetti JSON), `resources` è un elenco JSON di oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="56771-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="56771-130">Tutte le risorse richiedono le proprietà `type`, `name`, `apiVersion` e `location`.</span><span class="sxs-lookup"><span data-stu-id="56771-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="56771-131">La prima risorsa di questo esempio è di tipo `Microsft.Network/virtualNetwork`, nome `myVnet` e apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="56771-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="56771-132">Per determinare la versione più recente dell'API di un tipo di risorsa, vedere [Azure REST API documentation](https://docs.microsoft.com/rest/api/) (Documentazione dell'API REST di Azure).</span><span class="sxs-lookup"><span data-stu-id="56771-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="56771-133">Specificare il percorso</span><span class="sxs-lookup"><span data-stu-id="56771-133">Specify location</span></span>
<span data-ttu-id="56771-134">Per specificare il percorso della rete virtuale, viene usata una [funzione di modello di Resource Manager](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="56771-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="56771-135">Questa funzione deve essere racchiusa tra virgolette e parentesi quadre, nel modo seguente: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="56771-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="56771-136">In questo caso, si usa la funzione `resourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="56771-136">In this case, we use the `resourceGroup` function.</span></span> <span data-ttu-id="56771-137">La funzione non accetta argomenti e restituisce un oggetto JSON con metadati sul gruppo di risorse a cui viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="56771-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span></span> <span data-ttu-id="56771-138">Il gruppo di risorse viene impostato dall'utente al momento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="56771-138">The resource group is set by the user at the time of deployment.</span></span> <span data-ttu-id="56771-139">L'oggetto JSON viene quindi indicizzato con `.location` per ottenere il percorso dall'oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="56771-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="56771-140">Specificare le proprietà di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="56771-140">Specify virtual network properties</span></span>
<span data-ttu-id="56771-141">Ogni risorsa di Resource Manager dispone di una propria sezione `properties` per le configurazioni a essa specifiche.</span><span class="sxs-lookup"><span data-stu-id="56771-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span></span> <span data-ttu-id="56771-142">In questo caso, si specifica che la rete virtuale deve avere una subnet che usa l'intervallo `10.0.0.0/16` di indirizzi IP privati.</span><span class="sxs-lookup"><span data-stu-id="56771-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="56771-143">Un set di scalabilità è sempre contenuto in una subnet.</span><span class="sxs-lookup"><span data-stu-id="56771-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="56771-144">Non può estendersi a più subnet.</span><span class="sxs-lookup"><span data-stu-id="56771-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="56771-145">Aggiungere un elenco dependsOn</span><span class="sxs-lookup"><span data-stu-id="56771-145">Add dependsOn list</span></span>
<span data-ttu-id="56771-146">In aggiunta alle proprietà `type`, `name`, `apiVersion` e `location` necessarie, ogni risorsa può avere un elenco `dependsOn` di stringhe facoltativo.</span><span class="sxs-lookup"><span data-stu-id="56771-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="56771-147">Questo elenco specifica le altre risorse di questa distribuzione che devono essere completate prima di distribuire la risorsa.</span><span class="sxs-lookup"><span data-stu-id="56771-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="56771-148">In questo caso c'è solo un elemento nell'elenco, ovvero la rete virtuale dell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="56771-148">In this case, there is only one element in the list, the virtual network from the previous example.</span></span> <span data-ttu-id="56771-149">Si specifica la dipendenza poiché il set di scalabilità deve disporre di una rete esistente prima di creare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="56771-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span></span> <span data-ttu-id="56771-150">In questo modo, il set di scalabilità può indicare gli indirizzi IP privati delle macchine virtuali dall'intervallo degli indirizzi IP specificato precedentemente nelle proprietà della rete.</span><span class="sxs-lookup"><span data-stu-id="56771-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span></span> <span data-ttu-id="56771-151">Il formato di ogni stringa nell'elenco dependsOn è `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="56771-151">The format of each string in the dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="56771-152">Usare gli stessi `type` e `name` inclusi precedentemente nella definizione delle risorse della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="56771-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="56771-153">Specificare le proprietà del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="56771-153">Specify scale set properties</span></span>
<span data-ttu-id="56771-154">I set di scalabilità hanno molte proprietà per personalizzare le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="56771-154">Scale sets have many properties for customizing the VMs in the scale set.</span></span> <span data-ttu-id="56771-155">Per un elenco completo di queste proprietà, vedere [Scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set) (Documentazione dell'API REST del set di scalabilità).</span><span class="sxs-lookup"><span data-stu-id="56771-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="56771-156">Per questa esercitazione, verranno impostate solo alcune proprietà usate di frequente.</span><span class="sxs-lookup"><span data-stu-id="56771-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="56771-157">Specificare capacità e dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="56771-157">Supply VM size and capacity</span></span>
<span data-ttu-id="56771-158">Il set di scalabilità deve conoscere le dimensioni della macchina virtuale da creare ("nome SKU") e quante macchine virtuali di questo tipo deve creare ("capacità SKU").</span><span class="sxs-lookup"><span data-stu-id="56771-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span></span> <span data-ttu-id="56771-159">Per visualizzare le dimensioni disponibili di macchine virtuali, vedere [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) (Documentazione delle dimensioni di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="56771-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="56771-160">Scegliere un tipo di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="56771-160">Choose type of updates</span></span>
<span data-ttu-id="56771-161">Il set di scalabilità deve inoltre sapere come gestire gli aggiornamenti:</span><span class="sxs-lookup"><span data-stu-id="56771-161">The scale set also needs to know how to handle updates on the scale set.</span></span> <span data-ttu-id="56771-162">Attualmente sono disponibili due opzioni, `Manual` e `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="56771-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="56771-163">Per ulteriori informazioni sulle differenze tra le due opzioni, vedere la documentazione su [come aggiornare un set di scalabilità](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="56771-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="56771-164">Scegliere il sistema operativo delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="56771-164">Choose VM operating system</span></span>
<span data-ttu-id="56771-165">Il set di scalabilità deve conoscere quale sistema operativo installare nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="56771-165">The scale set needs to know what operating system to put on the VMs.</span></span> <span data-ttu-id="56771-166">In questo esempio le macchine virtuali vengono create con un'immagine di Ubuntu 16.04-LTS con patch complete.</span><span class="sxs-lookup"><span data-stu-id="56771-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="56771-167">Specificare computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="56771-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="56771-168">Il set di scalabilità distribuisce più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="56771-168">The scale set deploys multiple VMs.</span></span> <span data-ttu-id="56771-169">Anziché specificare il nome di ogni macchina virtuale, si specifica `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="56771-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="56771-170">Il set di scalabilità aggiunge un indice al prefisso di ogni macchina virtuale. Pertanto, i nomi delle macchine virtuali hanno il formato `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="56771-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="56771-171">In questo frammento di codice vengono anche usati i parametri precedenti per configurare il nome utente e la password dell'amministratore di tutte le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="56771-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span></span> <span data-ttu-id="56771-172">Questa operazione viene eseguita con la funzione di modello `parameters`.</span><span class="sxs-lookup"><span data-stu-id="56771-172">We do this with the `parameters` template function.</span></span> <span data-ttu-id="56771-173">Questa funzione accetta una stringa che specifica il parametro a cui fare riferimento a e restituisce il valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="56771-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="56771-174">Specificare la configurazione di rete delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="56771-174">Specify VM network configuration</span></span>
<span data-ttu-id="56771-175">Infine, è necessario specificare la configurazione di rete per le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="56771-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span></span> <span data-ttu-id="56771-176">In questo caso, è sufficiente specificare l'ID della subnet creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="56771-176">In this case, we only need to specify the ID of the subnet created earlier.</span></span> <span data-ttu-id="56771-177">Questa specifica indica al set di scalabilità di inserire le interfacce di rete in questa subnet.</span><span class="sxs-lookup"><span data-stu-id="56771-177">This tells the scale set to put the network interfaces in this subnet.</span></span>

<span data-ttu-id="56771-178">È possibile ottenere l'ID della rete virtuale che contiene la subnet usando la funzione di modello `resourceId`.</span><span class="sxs-lookup"><span data-stu-id="56771-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span></span> <span data-ttu-id="56771-179">Questa funzione accetta il tipo e il nome di una risorsa e restituisce il relativo identificatore completo della risorsa.</span><span class="sxs-lookup"><span data-stu-id="56771-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span></span> <span data-ttu-id="56771-180">L'ID ha il formato seguente: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="56771-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="56771-181">Tuttavia, l'identificatore della rete virtuale non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="56771-181">However, the identifier of the virtual network is not enough.</span></span> <span data-ttu-id="56771-182">È necessario indicare la subnet specifica in cui devono trovarsi le macchine virtuali del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="56771-182">You must specify the specific subnet that the scale set VMs should be in.</span></span> <span data-ttu-id="56771-183">A tale scopo, concatenare `/subnets/mySubnet` all'ID della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="56771-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span></span> <span data-ttu-id="56771-184">Il risultato è l'ID completo della subnet.</span><span class="sxs-lookup"><span data-stu-id="56771-184">The result is the fully qualified ID of the subnet.</span></span> <span data-ttu-id="56771-185">Eseguire la concatenazione con la funzione `concat`, che accetta una serie di stringhe e restituisce la relativa concatenazione.</span><span class="sxs-lookup"><span data-stu-id="56771-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="56771-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56771-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
