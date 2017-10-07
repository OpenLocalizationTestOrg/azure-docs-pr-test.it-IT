---
title: elemento gestita dell'interfaccia utente dell'applicazione TextBox aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.TextBox hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="65850-103">Elemento Microsoft.Common.TextBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="65850-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="65850-104">Un controllo che può essere utilizzati tooedit testo non formattato.</span><span class="sxs-lookup"><span data-stu-id="65850-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="65850-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="65850-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="65850-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="65850-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="65850-108">Schema</span><span class="sxs-lookup"><span data-stu-id="65850-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="65850-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="65850-109">Remarks</span></span>
- <span data-ttu-id="65850-110">Se `constraints.required` è troppo**true**, quindi la casella di testo hello deve contenere un valore toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="65850-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="65850-111">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="65850-111">hello default value is **false**.</span></span>
- <span data-ttu-id="65850-112">`constraints.regex` è un modello di espressione regolare di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="65850-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="65850-113">Se specificato, quindi il valore della casella di testo hello deve corrispondere hello modello toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="65850-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="65850-114">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="65850-114">The default value is **null**.</span></span>
- <span data-ttu-id="65850-115">`constraints.validationMessage`è una stringa di toodisplay quando il valore della casella di testo hello convalida ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="65850-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="65850-116">Se non specificato, hello i messaggi vengono utilizzati la convalida predefinita della casella di testo.</span><span class="sxs-lookup"><span data-stu-id="65850-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="65850-117">valore predefinito di Hello è **null**.</span><span class="sxs-lookup"><span data-stu-id="65850-117">hello default value is **null**.</span></span>
- <span data-ttu-id="65850-118">È possibile toospecify un valore per `constraints.regex` quando `constraints.required` è troppo**false**.</span><span class="sxs-lookup"><span data-stu-id="65850-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="65850-119">In questo scenario, un valore non è stato necessario per toovalidate casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="65850-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="65850-120">Se è specificata, deve corrispondere al criterio di espressione regolare hello.</span><span class="sxs-lookup"><span data-stu-id="65850-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="65850-121">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="65850-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="65850-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65850-122">Next steps</span></span>
* <span data-ttu-id="65850-123">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65850-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="65850-124">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65850-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="65850-125">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="65850-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
