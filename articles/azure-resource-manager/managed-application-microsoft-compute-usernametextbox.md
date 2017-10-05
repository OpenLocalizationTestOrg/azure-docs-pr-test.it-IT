---
title: Elemento UserNameTextBox dell'interfaccia utente dell'applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Compute.UserNameTextBox dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="2b579-103">Elemento Microsoft.Compute.UserNameTextBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2b579-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="2b579-104">Controllo casella di testo con convalida predefinita per i nomi utente di Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="2b579-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="2b579-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2b579-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2b579-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2b579-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="2b579-108">Schema</span><span class="sxs-lookup"><span data-stu-id="2b579-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="2b579-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2b579-109">Remarks</span></span>
- <span data-ttu-id="2b579-110">Se `constraints.required` è impostato su **true**, perché la convalida abbia esito positivo la casella di testo deve contenere un valore.</span><span class="sxs-lookup"><span data-stu-id="2b579-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="2b579-111">Il valore predefinito è **true**.</span><span class="sxs-lookup"><span data-stu-id="2b579-111">The default value is **true**.</span></span>
- <span data-ttu-id="2b579-112">È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="2b579-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="2b579-113">`constraints.regex` è un modello di espressione regolare di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2b579-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="2b579-114">Se specificato, perché la convalida venga abbia esito positivo il valore della casella di testo deve corrispondere al modello.</span><span class="sxs-lookup"><span data-stu-id="2b579-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="2b579-115">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="2b579-115">The default value is **null**.</span></span>
- <span data-ttu-id="2b579-116">`constraints.validationMessage` è una stringa da visualizzare quando il valore della casella di testo non supera la convalida specificata da `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="2b579-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="2b579-117">Se non specificata, vengono usati i messaggi di convalida predefiniti della casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2b579-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="2b579-118">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="2b579-118">The default value is **null**.</span></span>
- <span data-ttu-id="2b579-119">La convalida predefinita di questo elemento su basa sul valore specificato per `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="2b579-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="2b579-120">È possibile usare la convalida predefinita insieme a un'espressione regolare personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2b579-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="2b579-121">Se si specifica un valore per `constraints.regex`, viene attivata sia la convalida predefinita che quella personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2b579-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2b579-122">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="2b579-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="2b579-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b579-123">Next steps</span></span>
* <span data-ttu-id="2b579-124">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b579-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2b579-125">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b579-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2b579-126">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2b579-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
