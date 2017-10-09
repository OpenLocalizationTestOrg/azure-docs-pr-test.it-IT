---
title: "impostare i modelli di aaaLearn sulla scalabilità di macchine virtuali | Documenti Microsoft"
description: "Informazioni su una scala minima praticabile toocreate Imposta modello per il set di scalabilità di macchine virtuali"
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
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="f7fe3-103">Informazioni sui modelli di set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f7fe3-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="f7fe3-104">[Modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) sono un ottimo modo toodeploy gruppi di risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="f7fe3-105">Questa serie di esercitazioni viene illustrato come modello di set di toocreate una scala minima valida e come toomodify toosuit questo modello vari scenari.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="f7fe3-106">Tutti gli esempi provengono da questo [archivio GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="f7fe3-107">Questo modello è previsto toobe semplice.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-107">This template is intended toobe simple.</span></span> <span data-ttu-id="f7fe3-108">Per esempi più completi della scala impostare i modelli, vedere hello [repository GitHub modelli Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) e cercare le cartelle che contengono la stringa hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="f7fe3-109">Se si ha già familiarità con la creazione di modelli, è possibile ignorare toohello toosee di sezione "Passaggi successivi" come toomodify questo modello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="f7fe3-110">Modello di hello revisione</span><span class="sxs-lookup"><span data-stu-id="f7fe3-110">Review hello template</span></span>

<span data-ttu-id="f7fe3-111">Utilizzare GitHub tooreview modello, di impostare la scala minima valida [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="f7fe3-112">In questa esercitazione verranno esaminati hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimo possibili set di scalabilità di modello di elemento per elemento.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="f7fe3-113">Definire $schema e contentVersion</span><span class="sxs-lookup"><span data-stu-id="f7fe3-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="f7fe3-114">In primo luogo, definiamo `$schema` e `contentVersion` nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="f7fe3-115">Hello `$schema` elemento definisce una versione di hello hello della lingua del modello e viene utilizzato per l'evidenziazione della sintassi di Visual Studio e le funzionalità di convalida simile.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="f7fe3-116">Hello `contentVersion` elemento non viene usato da Azure.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="f7fe3-117">In alternativa, consente di tenere traccia di versione del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="f7fe3-118">Definire i parametri</span><span class="sxs-lookup"><span data-stu-id="f7fe3-118">Define parameters</span></span>
<span data-ttu-id="f7fe3-119">Successivamente, si definiscono due parametri, `adminUsername` e `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="f7fe3-120">I parametri sono i valori specificati in fase di hello della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="f7fe3-121">Hello `adminUsername` parametro è semplicemente un `string` tipo, ma poiché `adminPassword` è un segreto, abbiamo assegnarle tipo `securestring`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="f7fe3-122">In un secondo momento, questi parametri vengono passati in configurazione di set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-122">Later, these parameters are passed into hello scale set configuration.</span></span>

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
## <a name="define-variables"></a><span data-ttu-id="f7fe3-123">Definire le variabili</span><span class="sxs-lookup"><span data-stu-id="f7fe3-123">Define variables</span></span>
<span data-ttu-id="f7fe3-124">Modelli di gestione risorse consentono inoltre di definire variabili toobe utilizzato in un secondo momento nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="f7fe3-125">Questo esempio non utilizza tutte le variabili, in modo sono stati lasciati oggetto JSON hello vuoto.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="f7fe3-126">Definire le risorse</span><span class="sxs-lookup"><span data-stu-id="f7fe3-126">Define resources</span></span>
<span data-ttu-id="f7fe3-127">Di seguito è la sezione relativa alle risorse hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="f7fe3-128">In questo caso, definire i dati effettivamente da toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="f7fe3-129">A differenza di `parameters` e `variables` (che sono oggetti JSON), `resources` è un elenco JSON di oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="f7fe3-130">Tutte le risorse richiedono le proprietà `type`, `name`, `apiVersion` e `location`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="f7fe3-131">La prima risorsa di questo esempio è di tipo `Microsft.Network/virtualNetwork`, nome `myVnet` e apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="f7fe3-132">(toofind hello versione API più recente per un tipo di risorsa, vedere hello [documentazione dell'API REST di Azure](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="f7fe3-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="f7fe3-133">Specificare il percorso</span><span class="sxs-lookup"><span data-stu-id="f7fe3-133">Specify location</span></span>
<span data-ttu-id="f7fe3-134">percorso di hello toospecify per la rete virtuale hello, utilizzare un [funzione di modello di gestione risorse](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="f7fe3-135">Questa funzione deve essere racchiusa tra virgolette e parentesi quadre, nel modo seguente: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="f7fe3-136">In questo caso, utilizziamo hello `resourceGroup` (funzione).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="f7fe3-137">Accetta alcun argomento e restituisce un oggetto JSON con metadati relativi al gruppo di risorse hello che viene distribuita per questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="f7fe3-138">gruppo di risorse Hello viene impostata dall'utente hello in fase di hello della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="f7fe3-139">È quindi indice nell'oggetto JSON con `.location` percorso hello tooget da un oggetto JSON hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="f7fe3-140">Specificare le proprietà di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f7fe3-140">Specify virtual network properties</span></span>
<span data-ttu-id="f7fe3-141">Ogni risorsa di gestione risorse ha il proprio `properties` sezione per la risorsa toohello specifico di configurazioni.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="f7fe3-142">In questo caso, si specifica rete virtuale hello deve avere una subnet con intervallo di indirizzi IP privati hello `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="f7fe3-143">Un set di scalabilità è sempre contenuto in una subnet.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="f7fe3-144">Non può estendersi a più subnet.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-144">It cannot span subnets.</span></span>

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

## <a name="add-dependson-list"></a><span data-ttu-id="f7fe3-145">Aggiungere un elenco dependsOn</span><span class="sxs-lookup"><span data-stu-id="f7fe3-145">Add dependsOn list</span></span>
<span data-ttu-id="f7fe3-146">È inoltre richiesto di toohello `type`, `name`, `apiVersion`, e `location` le proprietà, ogni risorsa possono avere un parametro facoltativo `dependsOn` elenco di stringhe.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="f7fe3-147">Questo elenco specifica le altre risorse di questa distribuzione che devono essere completate prima di distribuire la risorsa.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="f7fe3-148">In questo caso, è presente un solo elemento nell'elenco di hello, rete virtuale di hello dall'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="f7fe3-149">Si specifica questa dipendenza perché hello set di scalabilità è necessario hello rete tooexist prima di creare tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="f7fe3-150">In questo modo, il set di scalabilità di hello può concedere a questi indirizzi IP privati di macchine virtuali dall'intervallo di indirizzi IP hello in precedenza specificato nelle proprietà di rete hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="f7fe3-151">formato Hello di ogni stringa nell'elenco di dependsOn hello è `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="f7fe3-152">Utilizzare hello stesso `type` e `name` utilizzata in precedenza nella definizione di risorsa di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

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
## <a name="specify-scale-set-properties"></a><span data-ttu-id="f7fe3-153">Specificare le proprietà del set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="f7fe3-153">Specify scale set properties</span></span>
<span data-ttu-id="f7fe3-154">Set di scalabilità hanno molte proprietà per la personalizzazione hello macchine virtuali nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="f7fe3-155">Per un elenco completo di queste proprietà, vedere hello [set di scalabilità della documentazione dell'API REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="f7fe3-156">Per questa esercitazione, verranno impostate solo alcune proprietà usate di frequente.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="f7fe3-157">Specificare capacità e dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f7fe3-157">Supply VM size and capacity</span></span>
<span data-ttu-id="f7fe3-158">scala Hello imposta tooknow esigenze le dimensioni della macchina virtuale toocreate ("nome sku") e quanti tali toocreate macchine virtuali ("capacità sku").</span><span class="sxs-lookup"><span data-stu-id="f7fe3-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="f7fe3-159">toosee le dimensioni delle macchine Virtuali sono disponibili, vedere hello [documentazione dimensioni delle macchine Virtuali](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="f7fe3-160">Scegliere un tipo di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="f7fe3-160">Choose type of updates</span></span>
<span data-ttu-id="f7fe3-161">set di scalabilità Hello deve inoltre tooknow modalità di aggiornamento nel set di scalabilità hello toohandle.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="f7fe3-162">Attualmente sono disponibili due opzioni, `Manual` e `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="f7fe3-163">Per ulteriori informazioni sulle differenze tra due hello la hello, vedere la documentazione di hello in [come tooupgrade un set di scalabilità](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="f7fe3-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="f7fe3-164">Scegliere il sistema operativo delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f7fe3-164">Choose VM operating system</span></span>
<span data-ttu-id="f7fe3-165">Hello set di scalabilità esigenze tooknow tooput il sistema operativo nelle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="f7fe3-166">In questo caso, creare macchine virtuali di hello con un'immagine di 16.04 LTS Ubuntu completamente con patch.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

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

### <a name="specify-computernameprefix"></a><span data-ttu-id="f7fe3-167">Specificare computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="f7fe3-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="f7fe3-168">set di scalabilità Hello consente di distribuire più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="f7fe3-169">Anziché specificare il nome di ogni macchina virtuale, si specifica `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="f7fe3-170">Hello set di scalabilità aggiunge un prefisso toohello di indice per ogni macchina virtuale, in modo da dispongono di nomi di macchina virtuale modulo hello `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="f7fe3-171">In hello seguente frammento di codice, utilizziamo parametri hello dalla prima tooset hello amministratore username e password per tutte le macchine virtuali nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="f7fe3-172">Facciamo con hello `parameters` funzione di modello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="f7fe3-173">Questa funzione accetta una stringa che specifica quali tooand toorefer parametro restituisce il valore di hello per tale parametro.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="f7fe3-174">Specificare la configurazione di rete delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f7fe3-174">Specify VM network configuration</span></span>
<span data-ttu-id="f7fe3-175">Infine, è necessario toospecify configurazione di rete hello per le macchine virtuali hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="f7fe3-176">In questo caso, è necessario solo toospecify hello ID di subnet hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="f7fe3-177">In questo modo hello set di scalabilità tooput interfacce di rete hello in questa subnet.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="f7fe3-178">È possibile ottenere hello ID di rete virtuale di hello contenente subnet hello utilizzando hello `resourceId` funzione di modello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="f7fe3-179">Questa funzione accetta il tipo di hello e il nome di una risorsa e restituisce hello identificatore completo della risorsa.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="f7fe3-180">Questo ID è hello:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="f7fe3-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="f7fe3-181">Tuttavia, identificatore hello della rete virtuale hello non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="f7fe3-182">È necessario specificare una subnet specifica hello che hello set di scalabilità di in che macchine virtuali devono trovarsi.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="f7fe3-183">toodo, concatenare `/subnets/mySubnet` toohello ID di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="f7fe3-184">il risultato di Hello è hello completo di ID di subnet hello.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="f7fe3-185">Eseguire questa concatenazione con hello `concat` funzione che accetta una serie di stringhe e restituisce la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="f7fe3-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f7fe3-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7fe3-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
