---
title: elemento gestita dell'interfaccia utente dell'applicazione StorageAccountSelector aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Storage.StorageAccountSelector hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="a3e08-103">Elemento Microsoft.Storage.StorageAccountSelector dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="a3e08-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="a3e08-104">Controllo per la selezione di un account di archiviazione nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="a3e08-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="a3e08-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a3e08-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a3e08-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="a3e08-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="a3e08-108">Schema</span><span class="sxs-lookup"><span data-stu-id="a3e08-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="a3e08-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a3e08-109">Remarks</span></span>
- <span data-ttu-id="a3e08-110">L'unicità di `defaultValue.name`, se specificato, viene convalidata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a3e08-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="a3e08-111">Se il nome di account di archiviazione hello non è univoco, l'utente hello deve specificare un nome diverso o scegliere un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="a3e08-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="a3e08-112">il valore predefinito per Hello `defaultValue.type` è **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="a3e08-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="a3e08-113">I tipi non specificati in `constraints.allowedTypes` vengono nascosti e i tipi non specificati in `constraints.excludedTypes` vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="a3e08-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="a3e08-114">`constraints.allowedTypes` e `constraints.excludedTypes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="a3e08-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="a3e08-115">Se `options.hideExisting` è **true**, utente hello non è possibile scegliere un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="a3e08-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="a3e08-116">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="a3e08-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="a3e08-117">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="a3e08-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="a3e08-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3e08-118">Next steps</span></span>
* <span data-ttu-id="a3e08-119">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3e08-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a3e08-120">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3e08-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a3e08-121">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a3e08-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
