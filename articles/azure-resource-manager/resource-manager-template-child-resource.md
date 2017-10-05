---
title: Definire una risorsa figlio in un modello di Azure | Microsoft Docs
description: Illustra come impostare il nome e il tipo di una risorsa figlio in un modello di Azure Resource Manager
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="2903d-103">Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2903d-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="2903d-104">Quando si crea un modello, è spesso necessario includere una risorsa figlio correlata a una risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="2903d-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="2903d-105">Il modello, ad esempio, potrebbe includere un'istanza di SQL Server e un database.</span><span class="sxs-lookup"><span data-stu-id="2903d-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="2903d-106">L'istanza di SQL Server è la risorsa padre e il database è la risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="2903d-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="2903d-107">Il formato del tipo della risorsa figlio è: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="2903d-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="2903d-108">Il formato del nome della risorsa figlio è: `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="2903d-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="2903d-109">Il tipo e il nome vengono tuttavia specificati in modo diverso in un modello a seconda che la risorsa sia annidata nella risorsa padre oppure di primo livello.</span><span class="sxs-lookup"><span data-stu-id="2903d-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="2903d-110">Questo argomento illustra come gestire entrambi gli approcci.</span><span class="sxs-lookup"><span data-stu-id="2903d-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="2903d-111">Quando si crea un riferimento completo a una risorsa, l'ordine di combinazione dei segmenti dal tipo e dal nome non è semplicemente una concatenazione dei due elementi.</span><span class="sxs-lookup"><span data-stu-id="2903d-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="2903d-112">Dopo lo spazio dei nomi, usare invece una sequenza di coppie *tipo/nome* dal meno specifico al più specifico:</span><span class="sxs-lookup"><span data-stu-id="2903d-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="2903d-113">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2903d-113">For example:</span></span>

<span data-ttu-id="2903d-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` è corretto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` non è corretto</span><span class="sxs-lookup"><span data-stu-id="2903d-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="2903d-115">Risorsa figlio annidata</span><span class="sxs-lookup"><span data-stu-id="2903d-115">Nested child resource</span></span>
<span data-ttu-id="2903d-116">Il modo più semplice per definire una risorsa figlio consiste nell'annidarla nella risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="2903d-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="2903d-117">L'esempio seguente illustra un database SQL annidato in un'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2903d-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="2903d-118">Per la risorsa figlio, il tipo è impostato su `databases`, ma il tipo di risorsa completo è `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="2903d-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="2903d-119">Non si specifica `Microsoft.Sql/servers/` perché viene ottenuto dal tipo della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="2903d-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="2903d-120">Il nome della risorsa figlio è impostato su `exampledatabase`, ma il nome completo include il nome della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="2903d-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="2903d-121">Non si specifica `exampleserver` perché viene ottenuto dalla risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="2903d-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="2903d-122">Risorsa figlio di primo livello</span><span class="sxs-lookup"><span data-stu-id="2903d-122">Top-level child resource</span></span>
<span data-ttu-id="2903d-123">È possibile definire la risorsa figlio al primo livello.</span><span class="sxs-lookup"><span data-stu-id="2903d-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="2903d-124">Questo approccio potrebbe essere usato se la risorsa padre non viene distribuita nello stesso modello o se si vuole usare `copy` per creare più risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="2903d-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="2903d-125">Con questo approccio, è necessario specificare il tipo di risorsa completo e includere il nome della risorsa padre nel nome della risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="2903d-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="2903d-126">Il database è una risorsa figlio del server anche se sono definiti allo stesso livello nel modello.</span><span class="sxs-lookup"><span data-stu-id="2903d-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2903d-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2903d-127">Next steps</span></span>
* <span data-ttu-id="2903d-128">Per altri suggerimenti su come creare i modelli, vedere [Procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2903d-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="2903d-129">Per un esempio della creazione di più risorse figlio, vedere [Distribuire più istanze delle risorse nei modelli di Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2903d-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
