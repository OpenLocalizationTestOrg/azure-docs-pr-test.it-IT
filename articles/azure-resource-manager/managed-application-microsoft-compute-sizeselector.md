---
title: Elemento SizeSelector dell'interfaccia utente dell'applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Compute.SizeSelector dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="84894-103">Elemento Microsoft.Compute.SizeSelector dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="84894-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="84894-104">Controllo per la selezione di una dimensione per una o più istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="84894-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="84894-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="84894-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="84894-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="84894-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="84894-108">Schema</span><span class="sxs-lookup"><span data-stu-id="84894-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="84894-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="84894-109">Remarks</span></span>
- <span data-ttu-id="84894-110">`recommendedSizes` deve contenere almeno una dimensione.</span><span class="sxs-lookup"><span data-stu-id="84894-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="84894-111">La prima dimensione consigliata viene usata come impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="84894-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="84894-112">Se una dimensione consigliata non è disponibile nella località selezionata, viene ignorata automaticamente</span><span class="sxs-lookup"><span data-stu-id="84894-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="84894-113">e viene usata la dimensione consigliata successiva.</span><span class="sxs-lookup"><span data-stu-id="84894-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="84894-114">Le dimensioni non specificate in `constraints.allowedSizes` vengono nascoste e quelle non specificate in `constraints.excludedSizes` vengono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="84894-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="84894-115">`constraints.allowedSizes` e `constraints.excludedSizes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="84894-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="84894-116">Per determinare l'elenco delle dimensioni disponibili è possibile chiamare l'[elenco di dimensioni di macchina virtuale disponibili per una sottoscrizione](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="84894-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="84894-117">È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="84894-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="84894-118">Viene usato per determinare i costi hardware delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84894-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="84894-119">`imageReference` viene omesso per le immagini proprietarie e viene specificato per le immagini di terze parti.</span><span class="sxs-lookup"><span data-stu-id="84894-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="84894-120">Viene usato per determinare i costi software delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="84894-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="84894-121">`count` viene usato per impostare il moltiplicatore appropriato per l'elemento.</span><span class="sxs-lookup"><span data-stu-id="84894-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="84894-122">Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="84894-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="84894-123">Il valore predefinito è **1**.</span><span class="sxs-lookup"><span data-stu-id="84894-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="84894-124">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="84894-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="84894-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84894-125">Next steps</span></span>
* <span data-ttu-id="84894-126">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84894-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="84894-127">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84894-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="84894-128">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="84894-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
