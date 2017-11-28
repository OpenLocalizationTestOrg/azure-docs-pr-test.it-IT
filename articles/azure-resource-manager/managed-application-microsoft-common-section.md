---
title: Elemento Section dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Common.Section dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="94943-103">Elemento Microsoft.Common.Section dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="94943-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="94943-104">Controllo che raggruppa uno o più elementi sotto un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="94943-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="94943-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="94943-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="94943-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="94943-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="94943-108">Schema</span><span class="sxs-lookup"><span data-stu-id="94943-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="94943-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="94943-109">Remarks</span></span>
- <span data-ttu-id="94943-110">`elements` deve contenere almeno un elemento e può contenere tutti i tipi di elementi, ad eccezione di `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="94943-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="94943-111">Questo elemento non supporta la proprietà `toolTip`.</span><span class="sxs-lookup"><span data-stu-id="94943-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="94943-112">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="94943-112">Sample output</span></span>
<span data-ttu-id="94943-113">Per accedere ai valori di output degli elementi in `elements`, usare le funzioni [basics()](managed-application-createuidefinition-functions.md#basics) o [steps()](managed-application-createuidefinition-functions.md#steps) e la notazione punto:</span><span class="sxs-lookup"><span data-stu-id="94943-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="94943-114">Gli elementi di tipo `Microsoft.Common.Section` stessi non hanno valori di output.</span><span class="sxs-lookup"><span data-stu-id="94943-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94943-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94943-115">Next steps</span></span>
* <span data-ttu-id="94943-116">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94943-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="94943-117">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94943-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="94943-118">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="94943-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
