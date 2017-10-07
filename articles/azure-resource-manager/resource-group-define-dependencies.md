---
title: ordine di distribuzione aaaSet per le risorse di Azure | Documenti Microsoft
description: Viene descritto come tooset una risorsa come dipendente da un'altra risorsa durante le risorse tooensure distribuzione vengono distribuiti nell'ordine corretto hello.
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="f2e15-103">Definire l'ordine di hello per la distribuzione delle risorse nei modelli di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f2e15-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="f2e15-104">Per una determinata risorsa, possono essere presenti altre risorse che devono essere presente prima di distribuire risorse hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="f2e15-105">Ad esempio, un server SQL deve esistere prima di tentare di toodeploy un database SQL.</span><span class="sxs-lookup"><span data-stu-id="f2e15-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="f2e15-106">Per definire questa relazione, contrassegnare una risorsa come hello dipendente da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="f2e15-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="f2e15-107">Si definisce una dipendenza con hello **dependsOn** elemento, o tramite hello **riferimento** (funzione).</span><span class="sxs-lookup"><span data-stu-id="f2e15-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="f2e15-108">Gestione risorse valuta hello le dipendenze tra le risorse e li distribuisce in base all'ordine dipendenti.</span><span class="sxs-lookup"><span data-stu-id="f2e15-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="f2e15-109">Quando le risorse non sono interdipendenti, Resource Manager le distribuisce in parallelo.</span><span class="sxs-lookup"><span data-stu-id="f2e15-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="f2e15-110">È necessario solo toodefine dipendenze per le risorse distribuite in hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="f2e15-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="f2e15-111">dependsOn</span></span>
<span data-ttu-id="f2e15-112">All'interno di un modello di elemento dependsOn hello consente toodefine una risorsa come dipendente in una o più risorse.</span><span class="sxs-lookup"><span data-stu-id="f2e15-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="f2e15-113">Il valore può essere un elenco delimitato da virgole di nomi di risorse.</span><span class="sxs-lookup"><span data-stu-id="f2e15-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="f2e15-114">Hello esempio seguente viene illustrato un set di scalabilità della macchina virtuale che dipende da un servizio di bilanciamento del carico di rete virtuale e un ciclo che crea più account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f2e15-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="f2e15-115">Queste altre risorse non sono visualizzate nel seguente esempio hello, ma è necessario tooexist in un' posizione nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="f2e15-116">In hello sopra riportato, una dipendenza è incluso nelle risorse hello che vengono create tramite un ciclo di copia denominato **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="f2e15-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="f2e15-117">Per avere un esempio, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f2e15-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="f2e15-118">Quando si definiscono le dipendenze, è possibile includere hello resource provider dello spazio dei nomi e delle risorse tipo tooavoid ambiguità.</span><span class="sxs-lookup"><span data-stu-id="f2e15-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="f2e15-119">Tooclarify, ad esempio, un servizio di bilanciamento del carico e la rete virtuale che può avere hello che nomi identici rispetto alle altre risorse, utilizzare hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="f2e15-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="f2e15-120">Sebbene sia toouse inclinata dependsOn toomap relazioni tra le risorse, è importante toounderstand perché si sta eseguendo.</span><span class="sxs-lookup"><span data-stu-id="f2e15-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="f2e15-121">Ad esempio, come le risorse sono collegate tra loro, toodocument dependsOn non approccio giusto hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="f2e15-122">È possibile eseguire query quali risorse sono state definite nell'elemento dependsOn hello dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f2e15-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="f2e15-123">L'uso di dependsOn potrebbe influire sul tempo necessario per la distribuzione perché Resource Manager non esegue la distribuzione simultanea di due risorse con dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f2e15-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="f2e15-124">toodocument relazioni tra le risorse, utilizzare invece [collegamento delle risorse](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="f2e15-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="f2e15-125">Risorse figlio</span><span class="sxs-lookup"><span data-stu-id="f2e15-125">Child resources</span></span>
<span data-ttu-id="f2e15-126">proprietà di risorse Hello consente toospecify risorse figlio correlate toohello risorsa che viene definita.</span><span class="sxs-lookup"><span data-stu-id="f2e15-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="f2e15-127">Le risorse figlio possono essere solo definite da cinque livelli.</span><span class="sxs-lookup"><span data-stu-id="f2e15-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="f2e15-128">È importante toonote che non è una relazione implicita creata tra una risorsa di figlio e padre hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="f2e15-129">Se è necessario hello toobe risorse figlio distribuiti dopo la risorsa padre hello, è necessario dichiarare in modo esplicito tale dipendenza con proprietà dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="f2e15-130">Ogni risorsa padre accetta solo determinati tipi di risorse come risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="f2e15-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="f2e15-131">Hello accettati vengono specificati i tipi di risorse in hello [schema del modello](https://github.com/Azure/azure-resource-manager-schemas) della risorsa padre hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="f2e15-132">nome di Hello del tipo di risorsa figlio include il nome di hello del tipo di risorsa padre hello, ad esempio **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** sono entrambe le risorse figlio di hello  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="f2e15-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="f2e15-133">Hello di esempio seguente viene illustrato un SQL server e database SQL.</span><span class="sxs-lookup"><span data-stu-id="f2e15-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="f2e15-134">Si noti che una dipendenza esplicita viene definita tra il database SQL hello e SQL server, anche se il database di hello è un elemento figlio di server hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="f2e15-135">funzione di riferimento</span><span class="sxs-lookup"><span data-stu-id="f2e15-135">reference function</span></span>
<span data-ttu-id="f2e15-136">Hello [fanno riferimento a funzione](resource-group-template-functions-resource.md#reference) consente a un'espressione tooderive il relativo valore da altre coppie nome / valore JSON o risorse di runtime.</span><span class="sxs-lookup"><span data-stu-id="f2e15-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="f2e15-137">Le Espressioni di riferimento in modo implicito dichiarano che una risorsa dipende da un altro.</span><span class="sxs-lookup"><span data-stu-id="f2e15-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="f2e15-138">formato generale Hello è:</span><span class="sxs-lookup"><span data-stu-id="f2e15-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="f2e15-139">Nell'esempio seguente di hello, un endpoint rete CDN dipende dal profilo CDN hello in modo esplicito e in modo implicito dipende da un'app web.</span><span class="sxs-lookup"><span data-stu-id="f2e15-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="f2e15-140">È possibile utilizzare questo elemento oppure hello dependsOn elemento toospecify le dipendenze, ma non è necessario toouse entrambi per hello stessa risorsa dipendente.</span><span class="sxs-lookup"><span data-stu-id="f2e15-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="f2e15-141">Se possibile, utilizzare tooavoid un riferimento implicito aggiunta di una dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="f2e15-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="f2e15-142">vedere, più toolearn [fanno riferimento a funzione](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="f2e15-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="f2e15-143">Raccomandazioni per l'impostazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="f2e15-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="f2e15-144">Quando si decide quali tooset dipendenze, usare hello alle linee guida:</span><span class="sxs-lookup"><span data-stu-id="f2e15-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="f2e15-145">Impostare il minor numero possibile di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f2e15-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="f2e15-146">Impostare una risorsa figlio come dipendente dalla risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="f2e15-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="f2e15-147">Hello utilizzare **riferimento** funzione tooset dipendenze implicito tra le risorse che devono tooshare una proprietà.</span><span class="sxs-lookup"><span data-stu-id="f2e15-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="f2e15-148">Non aggiungere una dipendenza esplicita (**dependsOn**) quando è già stata definita una dipendenza implicita.</span><span class="sxs-lookup"><span data-stu-id="f2e15-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="f2e15-149">Questo approccio riduce il rischio di hello di dipendenze non necessari.</span><span class="sxs-lookup"><span data-stu-id="f2e15-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="f2e15-150">Impostare una dipendenza quando una risorsa non può essere **creata** senza le funzionalità di un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="f2e15-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="f2e15-151">Non impostare una dipendenza se le risorse di hello interagiscono solo dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f2e15-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="f2e15-152">Consentire la propagazione a catena delle dipendenze senza impostarle esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="f2e15-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="f2e15-153">Ad esempio, la macchina virtuale dipende da un'interfaccia di rete virtuale e l'interfaccia di rete virtuale hello dipende da una rete virtuale e gli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="f2e15-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="f2e15-154">Pertanto, la macchina virtuale di hello è distribuite dopo che tutte le tre risorse, ma non imposta in modo esplicito macchina virtuale hello come dipendente da tutte e tre le risorse.</span><span class="sxs-lookup"><span data-stu-id="f2e15-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="f2e15-155">Questo approccio è illustrata l'ordine di dipendenza hello e rende più semplice modello di hello toochange in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f2e15-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="f2e15-156">Se un valore può essere determinato prima della distribuzione, provare a distribuire risorse hello senza una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f2e15-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="f2e15-157">Ad esempio, se un valore di configurazione deve nome hello di un'altra risorsa, non è una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f2e15-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="f2e15-158">Questa Guida non sempre funziona perché alcune risorse di verificare l'esistenza hello hello altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="f2e15-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="f2e15-159">Se viene visualizzato un errore, aggiungere una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f2e15-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="f2e15-160">Resource Manager identifica le dipendenze circolari durante la convalida del modello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="f2e15-161">Se si riceve un errore che informa che è presente una dipendenza circolare, valutare il modello toosee se tutte le dipendenze non sono necessari e possono essere rimossi.</span><span class="sxs-lookup"><span data-stu-id="f2e15-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="f2e15-162">Se la rimozione di dipendenze non funziona, è possibile evitare dipendenze circolari spostando alcune operazioni di distribuzione in risorse figlio che vengono distribuite dopo le risorse di hello che dispongono di una dipendenza circolare hello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="f2e15-163">Si supponga, ad esempio, si distribuiscono due macchine virtuali, ma è necessario impostare proprietà su ciascuna di esse che fanno riferimento altri toohello.</span><span class="sxs-lookup"><span data-stu-id="f2e15-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="f2e15-164">È possibile distribuirli in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="f2e15-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="f2e15-165">VM 1</span><span class="sxs-lookup"><span data-stu-id="f2e15-165">vm1</span></span>
2. <span data-ttu-id="f2e15-166">VM 2</span><span class="sxs-lookup"><span data-stu-id="f2e15-166">vm2</span></span>
3. <span data-ttu-id="f2e15-167">L'estensione in VM 1 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="f2e15-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="f2e15-168">estensione Hello imposta valori per vm1 ottenute da vm2.</span><span class="sxs-lookup"><span data-stu-id="f2e15-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="f2e15-169">L'estensione in VM 2 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="f2e15-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="f2e15-170">estensione Hello imposta valori per vm2 ottenute da vm1.</span><span class="sxs-lookup"><span data-stu-id="f2e15-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="f2e15-171">Per informazioni sulla valutazione di ordine di distribuzione hello e risoluzione degli errori di dipendenza, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="f2e15-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2e15-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2e15-172">Next steps</span></span>
* <span data-ttu-id="f2e15-173">toolearn sulla risoluzione dei problemi di dipendenze durante la distribuzione, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="f2e15-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="f2e15-174">toolearn sulla creazione di modelli di gestione risorse di Azure, vedere [creazione di modelli](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f2e15-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="f2e15-175">Per un elenco di funzioni disponibili di hello in un modello, vedere [funzioni di modello](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="f2e15-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

