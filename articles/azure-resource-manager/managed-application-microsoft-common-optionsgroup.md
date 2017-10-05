---
title: Elemento OptionsGroup dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Common.OptionsGroup dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="63eed-103">Elemento Microsoft.Common.OptionsGroup dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="63eed-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="63eed-104">Controllo di selezione con una riga di opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="63eed-104">A selection control with a row of available options.</span></span> <span data-ttu-id="63eed-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="63eed-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="63eed-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="63eed-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="63eed-108">Schema</span><span class="sxs-lookup"><span data-stu-id="63eed-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="63eed-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="63eed-109">Remarks</span></span>
- <span data-ttu-id="63eed-110">L'etichetta per `constraints.allowedValues` è il testo visualizzato per un elemento e il rispettivo valore è il valore di output dell'elemento in caso di selezione.</span><span class="sxs-lookup"><span data-stu-id="63eed-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="63eed-111">Se specificato, il valore predefinito deve essere un'etichetta presente in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="63eed-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="63eed-112">Se non è specificato, viene selezionato il primo elemento in `constraints.allowedValues` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="63eed-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="63eed-113">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="63eed-113">The default value is **null**.</span></span>
- <span data-ttu-id="63eed-114">`constraints.allowedValues` deve contenere almeno un elemento.</span><span class="sxs-lookup"><span data-stu-id="63eed-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="63eed-115">Questo elemento non supporta la proprietà `constraints.required`. Per una convalida corretta, è necessario selezionare un elemento.</span><span class="sxs-lookup"><span data-stu-id="63eed-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="63eed-116">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="63eed-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="63eed-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63eed-117">Next steps</span></span>
* <span data-ttu-id="63eed-118">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63eed-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="63eed-119">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63eed-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="63eed-120">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="63eed-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
