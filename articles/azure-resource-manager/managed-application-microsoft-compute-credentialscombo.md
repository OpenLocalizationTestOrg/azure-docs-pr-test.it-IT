---
title: elemento gestita dell'interfaccia utente dell'applicazione CredentialsCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Compute.CredentialsCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="92d1e-103">Elemento Microsoft.Compute.CredentialsCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="92d1e-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="92d1e-104">Si tratta di un gruppo di controlli con convalida predefinita per le chiavi pubbliche SSH e le password di Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="92d1e-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="92d1e-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="92d1e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="92d1e-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="92d1e-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="92d1e-108">Schema</span><span class="sxs-lookup"><span data-stu-id="92d1e-108">Schema</span></span>
<span data-ttu-id="92d1e-109">Se `osPlatform` è **Windows**, hello nello schema seguente viene utilizzata:</span><span class="sxs-lookup"><span data-stu-id="92d1e-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="92d1e-110">Se `osPlatform` è **Linux**, hello nello schema seguente viene utilizzata:</span><span class="sxs-lookup"><span data-stu-id="92d1e-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="92d1e-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="92d1e-111">Remarks</span></span>
- <span data-ttu-id="92d1e-112">È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="92d1e-113">Se `constraints.required` è troppo**true**, quindi hello password o le caselle di testo di chiave pubblica SSH devono contenere valori toovalidate correttamente.</span><span class="sxs-lookup"><span data-stu-id="92d1e-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="92d1e-114">valore predefinito di Hello è **true**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-114">hello default value is **true**.</span></span>
- <span data-ttu-id="92d1e-115">Se `options.hideConfirmation` è troppo**true**, quindi hello seconda casella di testo per la conferma della password dell'utente hello è nascosto.</span><span class="sxs-lookup"><span data-stu-id="92d1e-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="92d1e-116">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-116">hello default value is **false**.</span></span>
- <span data-ttu-id="92d1e-117">Se `options.hidePassword` è troppo**true**, quindi l'autenticazione di password toouse opzione hello è nascosto.</span><span class="sxs-lookup"><span data-stu-id="92d1e-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="92d1e-118">È possibile usarla solo quando `osPlatform` è **Linux**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="92d1e-119">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-119">The default value is **false**.</span></span>
- <span data-ttu-id="92d1e-120">Vincoli aggiuntivi sugli hello consentiti password può essere implementata usando hello `customPasswordRegex` proprietà.</span><span class="sxs-lookup"><span data-stu-id="92d1e-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="92d1e-121">stringa in Hello `customValidationMessage` viene visualizzato quando una password si verifica un errore di convalida personalizzata.</span><span class="sxs-lookup"><span data-stu-id="92d1e-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="92d1e-122">Hello valore predefinito per entrambe le proprietà è **null**.</span><span class="sxs-lookup"><span data-stu-id="92d1e-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="92d1e-123">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="92d1e-123">Sample output</span></span>
<span data-ttu-id="92d1e-124">Se `osPlatform` è **Windows**, o utente hello fornita una password anziché con una chiave pubblica SSH, quindi hello viene visualizzato output seguente:</span><span class="sxs-lookup"><span data-stu-id="92d1e-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="92d1e-125">Se una chiave pubblica SSH è fornito dall'utente di hello, quindi hello viene visualizzato output seguente:</span><span class="sxs-lookup"><span data-stu-id="92d1e-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="92d1e-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="92d1e-126">Next steps</span></span>
* <span data-ttu-id="92d1e-127">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92d1e-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="92d1e-128">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92d1e-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="92d1e-129">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="92d1e-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
