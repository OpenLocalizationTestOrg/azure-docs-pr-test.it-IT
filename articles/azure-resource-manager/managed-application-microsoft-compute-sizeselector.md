---
title: elemento gestita dell'interfaccia utente dell'applicazione SizeSelector aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Compute.SizeSelector hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="19826-103">Elemento Microsoft.Compute.SizeSelector dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="19826-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="19826-104">Controllo per la selezione di una dimensione per una o più istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="19826-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="19826-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="19826-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="19826-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="19826-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="19826-108">Schema</span><span class="sxs-lookup"><span data-stu-id="19826-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="19826-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="19826-109">Remarks</span></span>
- <span data-ttu-id="19826-110">`recommendedSizes` deve contenere almeno una dimensione.</span><span class="sxs-lookup"><span data-stu-id="19826-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="19826-111">Hello è innanzitutto consigliabile dimensione viene utilizzata come valore predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="19826-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="19826-112">Se una dimensione consigliata non è disponibile nel percorso selezionato hello, dimensioni hello viene ignorata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="19826-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="19826-113">Hello dimensioni consigliate successiva viene invece utilizzata.</span><span class="sxs-lookup"><span data-stu-id="19826-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="19826-114">Qualsiasi dimensione non è specificato in hello `constraints.allowedSizes` è nascosto e di qualsiasi dimensione non è specificato `constraints.excludedSizes` viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="19826-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="19826-115">`constraints.allowedSizes` e `constraints.excludedSizes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="19826-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="19826-116">elenco di Hello di dimensioni disponibili può essere determinato chiamando [elenco delle dimensioni della macchina virtuale disponibile per una sottoscrizione](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="19826-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="19826-117">È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="19826-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="19826-118">I costi di hardware hello toodetermine delle macchine virtuali hello è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="19826-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="19826-119">`imageReference` viene omesso per le immagini proprietarie e viene specificato per le immagini di terze parti.</span><span class="sxs-lookup"><span data-stu-id="19826-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="19826-120">I costi di software hello toodetermine delle macchine virtuali hello è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="19826-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="19826-121">`count`è moltiplicatore di appropriato hello tooset utilizzato per l'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="19826-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="19826-122">Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="19826-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="19826-123">valore predefinito di Hello è **1**.</span><span class="sxs-lookup"><span data-stu-id="19826-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="19826-124">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="19826-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="19826-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19826-125">Next steps</span></span>
* <span data-ttu-id="19826-126">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19826-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="19826-127">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19826-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="19826-128">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="19826-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
