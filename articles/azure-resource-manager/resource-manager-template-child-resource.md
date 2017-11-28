---
title: la risorsa aaaDefine figlio nel modello di Azure | Documenti Microsoft
description: Viene illustrato come tooset hello tipo di risorsa e il nome per la risorsa figlio in un modello di gestione risorse di Azure
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="773f0-103">Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="773f0-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="773f0-104">Quando si crea un modello, spesso necessario tooinclude una risorsa figlio risorsa padre tooa correlati.</span><span class="sxs-lookup"><span data-stu-id="773f0-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="773f0-105">Il modello, ad esempio, potrebbe includere un'istanza di SQL Server e un database.</span><span class="sxs-lookup"><span data-stu-id="773f0-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="773f0-106">Hello SQL server è risorsa padre hello e database hello è la risorsa figlio hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="773f0-107">formato Hello hello figlio del tipo di risorsa è:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="773f0-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="773f0-108">formato Hello hello figlio del nome di risorsa è:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="773f0-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="773f0-109">È tuttavia specificare hello tipo e il nome in un modello in modo diverso in base è annidata all'interno di risorsa padre hello oppure autonomamente al primo livello hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="773f0-110">Questo argomento viene illustrato come si avvicina toohandle entrambi.</span><span class="sxs-lookup"><span data-stu-id="773f0-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="773f0-111">Quando si crea una risorsa di riferimento completo tooa, hello ordine toocombine segmenti dal tipo hello e nome non è semplicemente una concatenazione di due hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="773f0-112">Dopo aver hello dello spazio dei nomi, utilizzare invece una sequenza di *nome/tipo* le coppie meno specifico toomost specifico:</span><span class="sxs-lookup"><span data-stu-id="773f0-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="773f0-113">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="773f0-113">For example:</span></span>

<span data-ttu-id="773f0-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` è corretto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` non è corretto</span><span class="sxs-lookup"><span data-stu-id="773f0-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="773f0-115">Risorsa figlio annidata</span><span class="sxs-lookup"><span data-stu-id="773f0-115">Nested child resource</span></span>
<span data-ttu-id="773f0-116">toodefine modo più semplice di Hello una risorsa figlio è toonest in risorsa padre hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="773f0-117">Hello esempio seguente viene illustrato un database SQL annidato in un Server SQL.</span><span class="sxs-lookup"><span data-stu-id="773f0-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="773f0-118">Per una risorsa figlio hello tipo hello è troppo`databases` ma il tipo di risorsa completo `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="773f0-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="773f0-119">Non si specifica `Microsoft.Sql/servers/` perché si presuppone dal tipo di risorsa padre hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="773f0-120">nome di risorsa figlio Hello impostato troppo`exampledatabase` ma il nome completo di hello include il nome del padre hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="773f0-121">Non si specifica `exampleserver` perché si presuppone dalla risorsa padre hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="773f0-122">Risorsa figlio di primo livello</span><span class="sxs-lookup"><span data-stu-id="773f0-122">Top-level child resource</span></span>
<span data-ttu-id="773f0-123">È possibile definire la risorsa figlio hello al primo livello hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="773f0-124">È possibile utilizzare questo approccio se risorsa padre hello non viene distribuito nella hello stesso modello o se desidera toouse `copy` toocreate più risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="773f0-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="773f0-125">Con questo approccio, è necessario fornire il tipo di risorsa completo hello e includono nome della risorsa padre di hello nel nome di risorsa figlio hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="773f0-126">database Hello è un server di toohello risorse figlio, anche se sono definiti in hello stesso livello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="773f0-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="773f0-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="773f0-127">Next steps</span></span>
* <span data-ttu-id="773f0-128">Per indicazioni su come toocreate modelli, vedere [procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="773f0-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="773f0-129">Per un esempio della creazione di più risorse figlio, vedere [Distribuire più istanze delle risorse nei modelli di Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="773f0-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
