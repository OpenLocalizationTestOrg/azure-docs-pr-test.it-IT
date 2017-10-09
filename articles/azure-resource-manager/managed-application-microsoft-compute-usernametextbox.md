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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Elemento Microsoft.Compute.UserNameTextBox dell'interfaccia utente
Controllo casella di testo con convalida predefinita per i nomi utente di Windows e Linux. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Osservazioni
- Se `constraints.required` è troppo**true**, quindi la casella di testo hello deve contenere un valore toovalidate correttamente. valore predefinito di Hello è **true**.
- È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**.
- `constraints.regex` è un modello di espressione regolare di JavaScript. Se specificato, quindi il valore della casella di testo hello deve corrispondere hello modello toovalidate correttamente. Il valore predefinito è **null**.
- `constraints.validationMessage`è una stringa di toodisplay caso di convalida hello specificata dal valore della casella di testo hello `constraints.regex`. Se non specificato, hello i messaggi vengono utilizzati la convalida predefinita della casella di testo. valore predefinito di Hello è **null**.
- Questo elemento dispone di convalida incorporate che è basata sul valore hello specificato per `osPlatform`. convalida incorporate Hello è utilizzabile con un'espressione regolare personalizzata.
Se un valore per `constraints.regex` viene specificato, entrambi hello predefiniti e vengono attivate le convalide personalizzate.

## <a name="sample-output"></a>Output di esempio
```json
"tabrezm"
```

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
