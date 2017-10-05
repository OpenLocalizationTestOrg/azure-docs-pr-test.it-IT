---
title: Elemento StorageAccountSelector dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Storage.StorageAccountSelector dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="337a8-103">Elemento Microsoft.Storage.StorageAccountSelector dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="337a8-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="337a8-104">Controllo per la selezione di un account di archiviazione nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="337a8-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="337a8-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="337a8-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="337a8-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="337a8-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="337a8-108">Schema</span><span class="sxs-lookup"><span data-stu-id="337a8-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="337a8-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="337a8-109">Remarks</span></span>
- <span data-ttu-id="337a8-110">L'unicità di `defaultValue.name`, se specificato, viene convalidata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="337a8-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="337a8-111">Se il nome dell'account di archiviazione non è univoco, l'utente deve specificare un nome diverso o scegliere un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="337a8-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="337a8-112">Il valore predefinito per `defaultValue.type` è **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="337a8-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="337a8-113">I tipi non specificati in `constraints.allowedTypes` vengono nascosti e i tipi non specificati in `constraints.excludedTypes` vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="337a8-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="337a8-114">`constraints.allowedTypes` e `constraints.excludedTypes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="337a8-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="337a8-115">Se `options.hideExisting` è **true**, l'utente non può scegliere un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="337a8-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="337a8-116">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="337a8-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="337a8-117">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="337a8-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="337a8-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="337a8-118">Next steps</span></span>
* <span data-ttu-id="337a8-119">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="337a8-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="337a8-120">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="337a8-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="337a8-121">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="337a8-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
