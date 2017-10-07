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
# <a name="microsoftcommontextbox-ui-element"></a>Elemento Microsoft.Common.TextBox dell'interfaccia utente
Un controllo che può essere utilizzati tooedit testo non formattato. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Osservazioni
- Se `constraints.required` è troppo**true**, quindi la casella di testo hello deve contenere un valore toovalidate correttamente. valore predefinito di Hello è **false**.
- `constraints.regex` è un modello di espressione regolare di JavaScript. Se specificato, quindi il valore della casella di testo hello deve corrispondere hello modello toovalidate correttamente. Il valore predefinito è **null**.
- `constraints.validationMessage`è una stringa di toodisplay quando il valore della casella di testo hello convalida ha esito negativo. Se non specificato, hello i messaggi vengono utilizzati la convalida predefinita della casella di testo. valore predefinito di Hello è **null**.
- È possibile toospecify un valore per `constraints.regex` quando `constraints.required` è troppo**false**. In questo scenario, un valore non è stato necessario per toovalidate casella di testo hello. Se è specificata, deve corrispondere al criterio di espressione regolare hello.

## <a name="sample-output"></a>Output di esempio

```json
"foobar"
```

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
