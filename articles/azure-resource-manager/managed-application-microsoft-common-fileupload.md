---
title: elemento gestita dell'interfaccia utente dell'applicazione FileUpload aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.FileUpload hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Elemento Microsoft.Common.FileUpload dell'interfaccia utente
Un controllo che consente a un utente toospecify uno o più file tooupload. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Osservazioni
- `constraints.accept`Specifica i tipi di file vengono visualizzati nella finestra di dialogo del browser hello file hello. Vedere hello [specifica HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) per i valori consentiti. valore predefinito di Hello è **null**.
- Se `options.multiple` è troppo**true**, hello autorizzato tooselect più di un file nella finestra di dialogo del browser hello file. valore predefinito di Hello è **false**.
- Questo elemento consente di caricare file in due modalità in base al valore di hello di `options.uploadMode`. Se **file** viene specificato, l'output di hello hello contenuto del file hello come blob. Se **url** viene specificato, il file hello è percorso temporaneo tooa caricato e output di hello contiene hello URL del blob hello. I BLOB temporanei verranno eliminati dopo 24 ore. valore predefinito di Hello è **file**.
- valore di Hello `options.openMode` determina la modalità di lettura file hello. Se il file hello è testo normale previsto toobe, specificare **testo**; in caso contrario, specificare **binario**. valore predefinito di Hello è **testo**.
- Se `options.uploadMode` è troppo**file** e `options.openMode` è troppo**binario**, output di hello è con codifica base64.
- `options.encoding`Specifica toouse codifica hello durante la lettura del file hello. valore predefinito di Hello è **UTF-8**e viene utilizzato solo quando `options.openMode` è troppo**testo**.

## <a name="sample-output"></a>Output di esempio
Se è false options.multiple e options.uploadMode è file, l'output contiene contenuto hello del file hello come una stringa JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Se è true options.multiple and'options.uploadMode è file, quindi l'output contiene contenuto hello del file hello come matrice JSON:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Se options.multiple è false e options.uploadMode è url, l'output include un URL sotto forma di stringa JSON:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Se options.multiple è true e options.uploadMode è url, l'output include un elenco di URL sotto forma di matrice JSON:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Quando si testa un CreateUiDefinition, alcuni browser (ad esempio Google Chrome) troncare URL generati dall'elemento Microsoft.Common.FileUpload hello nella console del browser hello. Potrebbe essere URL completi di clic tooright singoli collegamenti toocopy hello.


## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
