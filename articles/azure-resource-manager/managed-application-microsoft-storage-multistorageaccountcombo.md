---
title: elemento gestita dell'interfaccia utente dell'applicazione MultiStorageAccountCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Storage.MultiStorageAccountCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="466c3-103">Elemento Microsoft.Storage.MultiStorageAccountCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="466c3-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="466c3-104">Gruppo di controlli per la creazione di più account di archiviazione, con nomi che iniziano con un prefisso comune.</span><span class="sxs-lookup"><span data-stu-id="466c3-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="466c3-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="466c3-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="466c3-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="466c3-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="466c3-108">Schema</span><span class="sxs-lookup"><span data-stu-id="466c3-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="466c3-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="466c3-109">Remarks</span></span>
- <span data-ttu-id="466c3-110">valore per Hello `defaultValue.prefix` viene concatenato con uno o più numeri interi toogenerate hello sequenza i nomi degli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="466c3-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="466c3-111">Se ad esempio `defaultValue.prefix` è **foobar** e `count` è **2**, vengono generati i nomi degli account di archiviazione **foobar1** e **foobar2**.</span><span class="sxs-lookup"><span data-stu-id="466c3-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="466c3-112">L'unicità dei nomi degli account di archiviazione generati viene convalidata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="466c3-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="466c3-113">i nomi degli account di archiviazione Hello vengono generati in modo lessicografico base `count`.</span><span class="sxs-lookup"><span data-stu-id="466c3-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="466c3-114">Ad esempio, se `count` è 10, quindi i nomi degli account di archiviazione hello terminare con numeri interi a 2 cifre (01, 02, 03, ecc.).</span><span class="sxs-lookup"><span data-stu-id="466c3-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="466c3-115">il valore predefinito per Hello `defaultValue.prefix` è **null**e per `defaultValue.type` è **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="466c3-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="466c3-116">I tipi non specificati in `constraints.allowedTypes` vengono nascosti e i tipi non specificati in `constraints.excludedTypes` vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="466c3-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="466c3-117">`constraints.allowedTypes` e `constraints.excludedTypes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="466c3-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="466c3-118">I nomi account di archiviazione toogenerating aggiunta, `count` è tooset usato il moltiplicatore appropriato per un elemento hello.</span><span class="sxs-lookup"><span data-stu-id="466c3-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="466c3-119">Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="466c3-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="466c3-120">valore predefinito di Hello è **1**.</span><span class="sxs-lookup"><span data-stu-id="466c3-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="466c3-121">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="466c3-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="466c3-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="466c3-122">Next steps</span></span>
* <span data-ttu-id="466c3-123">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="466c3-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="466c3-124">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="466c3-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="466c3-125">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="466c3-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
