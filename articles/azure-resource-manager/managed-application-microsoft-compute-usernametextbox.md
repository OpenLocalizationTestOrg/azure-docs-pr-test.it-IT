---
title: elemento gestita dell'interfaccia utente dell'applicazione UserNameTextBox aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Compute.UserNameTextBox hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="32146-103">Elemento Microsoft.Compute.UserNameTextBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="32146-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="32146-104">Controllo casella di testo con convalida predefinita per i nomi utente di Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="32146-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="32146-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="32146-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="32146-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="32146-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="32146-108">Schema</span><span class="sxs-lookup"><span data-stu-id="32146-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="32146-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="32146-109">Remarks</span></span>
- <span data-ttu-id="32146-110">Se `constraints.required` è troppo**true**, quindi la casella di testo hello deve contenere un valore toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="32146-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="32146-111">valore predefinito di Hello è **true**.</span><span class="sxs-lookup"><span data-stu-id="32146-111">hello default value is **true**.</span></span>
- <span data-ttu-id="32146-112">È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="32146-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="32146-113">`constraints.regex` è un modello di espressione regolare di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="32146-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="32146-114">Se specificato, quindi il valore della casella di testo hello deve corrispondere hello modello toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="32146-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="32146-115">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="32146-115">The default value is **null**.</span></span>
- <span data-ttu-id="32146-116">`constraints.validationMessage`è una stringa di toodisplay caso di convalida hello specificata dal valore della casella di testo hello `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="32146-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="32146-117">Se non specificato, hello i messaggi vengono utilizzati la convalida predefinita della casella di testo.</span><span class="sxs-lookup"><span data-stu-id="32146-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="32146-118">valore predefinito di Hello è **null**.</span><span class="sxs-lookup"><span data-stu-id="32146-118">hello default value is **null**.</span></span>
- <span data-ttu-id="32146-119">Questo elemento dispone di convalida incorporate che è basata sul valore hello specificato per `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="32146-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="32146-120">convalida incorporate Hello è utilizzabile con un'espressione regolare personalizzata.</span><span class="sxs-lookup"><span data-stu-id="32146-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="32146-121">Se un valore per `constraints.regex` viene specificato, entrambi hello predefiniti e vengono attivate le convalide personalizzate.</span><span class="sxs-lookup"><span data-stu-id="32146-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="32146-122">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="32146-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="32146-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32146-123">Next steps</span></span>
* <span data-ttu-id="32146-124">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32146-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="32146-125">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32146-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="32146-126">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="32146-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
