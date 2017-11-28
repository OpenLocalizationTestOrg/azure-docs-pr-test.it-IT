---
title: elemento gestita dell'interfaccia utente dell'applicazione OptionsGroup aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.OptionsGroup hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="57a03-103">Elemento Microsoft.Common.OptionsGroup dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="57a03-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="57a03-104">Controllo di selezione con una riga di opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="57a03-104">A selection control with a row of available options.</span></span> <span data-ttu-id="57a03-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="57a03-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="57a03-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="57a03-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="57a03-108">Schema</span><span class="sxs-lookup"><span data-stu-id="57a03-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="57a03-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57a03-109">Remarks</span></span>
- <span data-ttu-id="57a03-110">etichetta Hello per `constraints.allowedValues` è hello Visualizza il testo per un elemento e il relativo valore è il valore di output di hello dell'elemento hello quando selezionato.</span><span class="sxs-lookup"><span data-stu-id="57a03-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="57a03-111">Se specificato, valore predefinito di hello deve essere presente in un'etichetta di `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="57a03-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="57a03-112">Se non specificato, hello primo elemento `constraints.allowedValues` è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="57a03-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="57a03-113">valore predefinito di Hello è **null**.</span><span class="sxs-lookup"><span data-stu-id="57a03-113">hello default value is **null**.</span></span>
- <span data-ttu-id="57a03-114">`constraints.allowedValues` deve contenere almeno un elemento.</span><span class="sxs-lookup"><span data-stu-id="57a03-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="57a03-115">Questo elemento non supporta hello `constraints.required` proprietà dell'elemento deve essere selezionato toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="57a03-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="57a03-116">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="57a03-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="57a03-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57a03-117">Next steps</span></span>
* <span data-ttu-id="57a03-118">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57a03-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="57a03-119">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57a03-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="57a03-120">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="57a03-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
