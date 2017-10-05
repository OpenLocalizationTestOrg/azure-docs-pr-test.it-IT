---
title: Elemento TextBox dell'interfaccia utente dell'applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Common.TextBox dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="070f5-103">Elemento Microsoft.Common.TextBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="070f5-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="070f5-104">Controllo che è possibile usare per modificare il testo non formattato.</span><span class="sxs-lookup"><span data-stu-id="070f5-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="070f5-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="070f5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="070f5-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="070f5-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="070f5-108">Schema</span><span class="sxs-lookup"><span data-stu-id="070f5-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="070f5-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="070f5-109">Remarks</span></span>
- <span data-ttu-id="070f5-110">Se `constraints.required` è impostato su **true**, perché la convalida abbia esito positivo la casella di testo deve contenere un valore.</span><span class="sxs-lookup"><span data-stu-id="070f5-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="070f5-111">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="070f5-111">The default value is **false**.</span></span>
- <span data-ttu-id="070f5-112">`constraints.regex` è un modello di espressione regolare di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="070f5-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="070f5-113">Se specificato, perché la convalida venga abbia esito positivo il valore della casella di testo deve corrispondere al modello.</span><span class="sxs-lookup"><span data-stu-id="070f5-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="070f5-114">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="070f5-114">The default value is **null**.</span></span>
- <span data-ttu-id="070f5-115">`constraints.validationMessage` è una stringa da visualizzare quando il valore della casella di testo non supera la convalida.</span><span class="sxs-lookup"><span data-stu-id="070f5-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="070f5-116">Se non specificata, vengono usati i messaggi di convalida predefiniti della casella di testo.</span><span class="sxs-lookup"><span data-stu-id="070f5-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="070f5-117">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="070f5-117">The default value is **null**.</span></span>
- <span data-ttu-id="070f5-118">È possibile specificare un valore per `constraints.regex` quando `constraints.required` è impostato su **false**.</span><span class="sxs-lookup"><span data-stu-id="070f5-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="070f5-119">In questo scenario non è richiesto un valore perché la convalida della casella di testo abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="070f5-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="070f5-120">Se viene specificato, deve corrispondere al modello di espressione regolare.</span><span class="sxs-lookup"><span data-stu-id="070f5-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="070f5-121">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="070f5-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="070f5-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="070f5-122">Next steps</span></span>
* <span data-ttu-id="070f5-123">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="070f5-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="070f5-124">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="070f5-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="070f5-125">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="070f5-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
