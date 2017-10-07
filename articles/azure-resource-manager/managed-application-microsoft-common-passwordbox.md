---
title: elemento gestita dell'interfaccia utente dell'applicazione PasswordBox aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.PasswordBox hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="8516d-103">Elemento Microsoft.Common.PasswordBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="8516d-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="8516d-104">Un controllo che può essere utilizzati tooprovide e confermare una password.</span><span class="sxs-lookup"><span data-stu-id="8516d-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="8516d-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8516d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8516d-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="8516d-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="8516d-108">Schema</span><span class="sxs-lookup"><span data-stu-id="8516d-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="8516d-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="8516d-109">Remarks</span></span>
- <span data-ttu-id="8516d-110">Questo elemento non supporta hello `defaultValue` proprietà.</span><span class="sxs-lookup"><span data-stu-id="8516d-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="8516d-111">Per i dettagli sull'implementazione di `constraints`, vedere [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="8516d-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="8516d-112">Se `options.hideConfirmation` è troppo**true**, hello seconda casella di testo per la conferma della password dell'utente hello è nascosto.</span><span class="sxs-lookup"><span data-stu-id="8516d-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="8516d-113">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="8516d-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8516d-114">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="8516d-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="8516d-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8516d-115">Next steps</span></span>
* <span data-ttu-id="8516d-116">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8516d-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8516d-117">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8516d-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8516d-118">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8516d-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
