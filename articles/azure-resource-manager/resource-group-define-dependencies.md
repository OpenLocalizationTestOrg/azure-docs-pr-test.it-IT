---
title: Impostare l'ordine di distribuzione per le risorse di Azure | Documentazione Microsoft
description: Descrive come impostare una risorsa come dipendente da un'altra risorsa durante la distribuzione per garantire che le risorse vengano distribuite nell'ordine corretto.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="4d2e6-103">Definire l'ordine per la distribuzione delle risorse nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4d2e6-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="4d2e6-104">Perché una risorsa possa essere distribuita, potrebbe essere necessario che prima di essa esistano altre risorse specifiche.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="4d2e6-105">Ad esempio, un server SQL deve esistere prima che si tenti di distribuire un database SQL.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="4d2e6-106">Per definire questa relazione, si contrassegna una risorsa come dipendente dall'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="4d2e6-107">Una dipendenza viene definita con l'elemento **dependsOn** oppure con la funzione **reference**.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="4d2e6-108">Resource Manager valuta le dipendenze tra le risorse e le distribuisce in base all'ordine di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="4d2e6-109">Quando le risorse non sono interdipendenti, Resource Manager le distribuisce in parallelo.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="4d2e6-110">La definizione delle dipendenze è necessaria solo per le risorse distribuite nello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="4d2e6-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="4d2e6-111">dependsOn</span></span>
<span data-ttu-id="4d2e6-112">All'interno del modello, l'elemento dependsOn consente di definire una risorsa come dipendente da una o più risorse.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="4d2e6-113">Il valore può essere un elenco delimitato da virgole di nomi di risorse.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="4d2e6-114">L'esempio seguente illustra un set di scalabilità di macchine virtuali dipendente da un servizio di bilanciamento del carico e da una rete virtuale. L'esempio illustra anche un ciclo che crea più account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="4d2e6-115">Queste altre risorse non sono visualizzate nell'esempio seguente, ma devono esistere in un altro punto del modello.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="4d2e6-116">Nell'esempio precedente è inclusa una dipendenza per le risorse create tramite il ciclo di copia denominato **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="4d2e6-117">Per avere un esempio, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="4d2e6-118">Quando si definiscono le dipendenze, per evitare ambiguità è possibile includere lo spazio dei nomi del provider di risorse e il tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="4d2e6-119">Ad esempio, per distinguere un bilanciamento del carico e una rete virtuale che hanno lo stesso nome di altre risorse, usare il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="4d2e6-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="4d2e6-120">Anche se si potrebbe essere propensi a usare dependsOn per mappare le relazioni tra le risorse, è importante comprendere il motivo per cui si esegue tale operazione.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="4d2e6-121">Ad esempio, per documentare come le risorse sono interconnesse, dependsOn non è l'approccio giusto.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="4d2e6-122">Non è possibile eseguire query su quali risorse sono state definite nell'elemento dependsOn dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="4d2e6-123">L'uso di dependsOn potrebbe influire sul tempo necessario per la distribuzione perché Resource Manager non esegue la distribuzione simultanea di due risorse con dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="4d2e6-124">Per documentare le relazioni tra le risorse, usare il [collegamento di risorse](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="4d2e6-125">Risorse figlio</span><span class="sxs-lookup"><span data-stu-id="4d2e6-125">Child resources</span></span>
<span data-ttu-id="4d2e6-126">La proprietà delle risorse consente di specificare le risorse figlio correlate alla risorsa definita.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="4d2e6-127">Le risorse figlio possono essere solo definite da cinque livelli.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="4d2e6-128">È importante notare che una relazione implicita non viene creata tra una risorsa figlio e la risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="4d2e6-129">Se è necessario che la risorsa figlio sia distribuita dopo la risorsa padre, è necessario dichiarare in modo esplicito tale dipendenza con la proprietà dependsOn.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="4d2e6-130">Ogni risorsa padre accetta solo determinati tipi di risorse come risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="4d2e6-131">I tipi di risorse accettate sono specificati nel [schema del modello](https://github.com/Azure/azure-resource-manager-schemas) della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="4d2e6-132">Il nome del tipo di risorsa figlio include il nome del tipo di risorsa padre, ad esempio **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** sono entrambi risorse figlio di **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="4d2e6-133">Nell'esempio seguente sono illustrati un server SQL e un database SQL.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="4d2e6-134">Si noti che viene definita una dipendenza esplicita tra il database SQL e il server SQL, anche se il database è un elemento figlio del server.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="4d2e6-135">funzione di riferimento</span><span class="sxs-lookup"><span data-stu-id="4d2e6-135">reference function</span></span>
<span data-ttu-id="4d2e6-136">La [funzione di riferimento](resource-group-template-functions-resource.md#reference) consente un'espressione per derivare il valore da altri nomi JSON e coppie valore o risorse di runtime.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="4d2e6-137">Le Espressioni di riferimento in modo implicito dichiarano che una risorsa dipende da un altro.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="4d2e6-138">Il formato generale è il seguente:</span><span class="sxs-lookup"><span data-stu-id="4d2e6-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="4d2e6-139">Nell'esempio seguente, un endpoint della rete CDN dipende in modo esplicito dal profilo CDN e in modo implicito da un'app Web.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="4d2e6-140">È possibile utilizzare questo elemento o l'elemento dependsOn per specificare le dipendenze, ma non è necessario utilizzare entrambi per la stessa risorsa dipendente.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="4d2e6-141">Quando possibile, usare un riferimento implicito per evitare di aggiungere una dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="4d2e6-142">Per altre informazioni, vedere la [funzione del riferimento](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="4d2e6-143">Raccomandazioni per l'impostazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="4d2e6-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="4d2e6-144">Quando si decidono le dipendenze da impostare, usare le linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d2e6-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="4d2e6-145">Impostare il minor numero possibile di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="4d2e6-146">Impostare una risorsa figlio come dipendente dalla risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="4d2e6-147">Usare la funzione **reference** per impostare dipendenze implicite tra le risorse che devono condividere una proprietà.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="4d2e6-148">Non aggiungere una dipendenza esplicita (**dependsOn**) quando è già stata definita una dipendenza implicita.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="4d2e6-149">Questo approccio riduce il rischio di creare dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="4d2e6-150">Impostare una dipendenza quando una risorsa non può essere **creata** senza le funzionalità di un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="4d2e6-151">Non impostare una dipendenza se le risorse interagiscono solo dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="4d2e6-152">Consentire la propagazione a catena delle dipendenze senza impostarle esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="4d2e6-153">Ad esempio, una macchina virtuale dipende da un'interfaccia di rete virtuale e tale interfaccia dipende da una rete virtuale e indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="4d2e6-154">La macchina virtuale viene quindi distribuita dopo tutte e tre le risorse, ma non deve essere impostata esplicitamente come dipendente da esse.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="4d2e6-155">Questo approccio offre chiarezza nell'ordine delle dipendenze e semplifica la successiva modifica del modello.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="4d2e6-156">Se un valore può essere determinato prima della distribuzione, provare a distribuire le risorse senza una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="4d2e6-157">Se un valore di configurazione richiede il nome di un'altra risorsa, ad esempio, potrebbe non essere necessaria una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="4d2e6-158">Questa indicazione non è sempre valida perché alcune risorse verificano l'esistenza dell'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="4d2e6-159">Se viene visualizzato un errore, aggiungere una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="4d2e6-160">Resource Manager identifica le dipendenze circolari durante la convalida del modello.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="4d2e6-161">Se viene visualizzato un errore che indica la presenza di una dipendenza circolare, valutare il modello per verificare se esistono dipendenze non necessarie che possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="4d2e6-162">Se la rimozione delle dipendenze non è applicabile, è possibile evitare le dipendenze circolari spostando alcune operazioni di distribuzione in risorse figlio distribuite dopo le risorse che hanno la dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="4d2e6-163">Si supponga, ad esempio, di distribuire due macchine virtuali e che sia necessario impostare in ognuna proprietà che fanno riferimento all'altra.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="4d2e6-164">È possibile eseguire la distribuzione nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="4d2e6-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="4d2e6-165">VM 1</span><span class="sxs-lookup"><span data-stu-id="4d2e6-165">vm1</span></span>
2. <span data-ttu-id="4d2e6-166">VM 2</span><span class="sxs-lookup"><span data-stu-id="4d2e6-166">vm2</span></span>
3. <span data-ttu-id="4d2e6-167">L'estensione in VM 1 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="4d2e6-168">L'estensione imposta in VM 1 valori ottenuti da VM 2.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="4d2e6-169">L'estensione in VM 2 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="4d2e6-170">L'estensione imposta in VM 2 valori ottenuti da VM 1.</span><span class="sxs-lookup"><span data-stu-id="4d2e6-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="4d2e6-171">Per informazioni sulla valutazione dell'ordine di distribuzione e la risoluzione degli errori di dipendenza, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d2e6-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d2e6-172">Next steps</span></span>
* <span data-ttu-id="4d2e6-173">Per informazioni sulla risoluzione dei problemi relativi alle dipendenze durante la distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="4d2e6-174">Per informazioni sulla creazione di modelli di Gestione risorse di Azure, vedere [Creazione di modelli](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="4d2e6-175">Per un elenco delle funzioni disponibili in un modello, vedere [Funzioni di modelli](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4d2e6-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

