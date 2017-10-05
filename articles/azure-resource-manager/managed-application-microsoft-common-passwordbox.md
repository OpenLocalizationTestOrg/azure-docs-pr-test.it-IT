---
title: Elemento PasswordBox dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Common.PasswordBox dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="eba12-103">Elemento Microsoft.Common.PasswordBox dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="eba12-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="eba12-104">Controllo che può essere usato per fornire e confermare una password.</span><span class="sxs-lookup"><span data-stu-id="eba12-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="eba12-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="eba12-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="eba12-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="eba12-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="eba12-108">Schema</span><span class="sxs-lookup"><span data-stu-id="eba12-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="eba12-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="eba12-109">Remarks</span></span>
- <span data-ttu-id="eba12-110">Questo elemento non supporta la proprietà `defaultValue`.</span><span class="sxs-lookup"><span data-stu-id="eba12-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="eba12-111">Per i dettagli sull'implementazione di `constraints`, vedere [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="eba12-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="eba12-112">Se la proprietà `options.hideConfirmation` è impostata su **true**, la seconda casella di testo per la conferma della password dell'utente è nascosta.</span><span class="sxs-lookup"><span data-stu-id="eba12-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="eba12-113">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="eba12-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="eba12-114">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="eba12-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="eba12-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eba12-115">Next steps</span></span>
* <span data-ttu-id="eba12-116">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eba12-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="eba12-117">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eba12-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="eba12-118">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="eba12-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
