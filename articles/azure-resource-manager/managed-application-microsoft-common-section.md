---
title: elemento gestita dell'interfaccia utente dell'applicazione sezione aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.Section hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="f4a25-103">Elemento Microsoft.Common.Section dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="f4a25-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="f4a25-104">Controllo che raggruppa uno o più elementi sotto un'intestazione.</span><span class="sxs-lookup"><span data-stu-id="f4a25-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="f4a25-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f4a25-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f4a25-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="f4a25-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="f4a25-108">Schema</span><span class="sxs-lookup"><span data-stu-id="f4a25-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f4a25-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="f4a25-109">Remarks</span></span>
- <span data-ttu-id="f4a25-110">`elements` deve contenere almeno un elemento e può contenere tutti i tipi di elementi, ad eccezione di `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="f4a25-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="f4a25-111">Questo elemento non supporta hello `toolTip` proprietà.</span><span class="sxs-lookup"><span data-stu-id="f4a25-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f4a25-112">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="f4a25-112">Sample output</span></span>
<span data-ttu-id="f4a25-113">i valori di elementi nell'output di hello tooaccess `elements`, utilizzare hello [basics()](managed-application-createuidefinition-functions.md#basics) o [steps()](managed-application-createuidefinition-functions.md#steps) funzioni e la notazione del punto:</span><span class="sxs-lookup"><span data-stu-id="f4a25-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="f4a25-114">Gli elementi di tipo `Microsoft.Common.Section` stessi non hanno valori di output.</span><span class="sxs-lookup"><span data-stu-id="f4a25-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4a25-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4a25-115">Next steps</span></span>
* <span data-ttu-id="f4a25-116">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4a25-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f4a25-117">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4a25-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f4a25-118">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f4a25-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
