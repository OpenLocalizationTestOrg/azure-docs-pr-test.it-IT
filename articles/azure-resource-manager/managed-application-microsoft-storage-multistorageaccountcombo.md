---
title: Elemento MultiStorageAccountCombo dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Storage.MultiStorageAccountCombo dell'interfaccia utente per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="18623-103">Elemento Microsoft.Storage.MultiStorageAccountCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="18623-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="18623-104">Gruppo di controlli per la creazione di più account di archiviazione, con nomi che iniziano con un prefisso comune.</span><span class="sxs-lookup"><span data-stu-id="18623-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="18623-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="18623-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="18623-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="18623-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="18623-108">Schema</span><span class="sxs-lookup"><span data-stu-id="18623-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="18623-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="18623-109">Remarks</span></span>
- <span data-ttu-id="18623-110">Il valore per `defaultValue.prefix` viene concatenato a uno o più numeri interi per generare la sequenza di nomi di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="18623-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="18623-111">Se ad esempio `defaultValue.prefix` è **foobar** e `count` è **2**, vengono generati i nomi degli account di archiviazione **foobar1** e **foobar2**.</span><span class="sxs-lookup"><span data-stu-id="18623-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="18623-112">L'unicità dei nomi degli account di archiviazione generati viene convalidata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="18623-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="18623-113">I nomi degli account di archiviazione vengono generati in modo lessicografico in base a `count`.</span><span class="sxs-lookup"><span data-stu-id="18623-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="18623-114">Se ad esempio `count` è 10, i nomi degli account di archiviazione terminano con numeri interi a 2 cifre (01, 02, 03 e così via).</span><span class="sxs-lookup"><span data-stu-id="18623-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="18623-115">Il valore predefinito per `defaultValue.prefix` è **null** e quello per `defaultValue.type` è **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="18623-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="18623-116">I tipi non specificati in `constraints.allowedTypes` vengono nascosti e i tipi non specificati in `constraints.excludedTypes` vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="18623-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="18623-117">`constraints.allowedTypes` e `constraints.excludedTypes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="18623-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="18623-118">Oltre a generare nomi di account di archiviazione, `count` viene usato per impostare il moltiplicatore appropriato per l'elemento.</span><span class="sxs-lookup"><span data-stu-id="18623-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="18623-119">Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="18623-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="18623-120">Il valore predefinito è **1**.</span><span class="sxs-lookup"><span data-stu-id="18623-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="18623-121">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="18623-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="18623-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18623-122">Next steps</span></span>
* <span data-ttu-id="18623-123">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18623-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="18623-124">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18623-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="18623-125">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="18623-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
