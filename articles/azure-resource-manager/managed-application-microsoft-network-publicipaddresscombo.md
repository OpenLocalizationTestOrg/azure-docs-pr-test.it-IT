---
title: elemento gestita dell'interfaccia utente dell'applicazione PublicIpAddressCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Network.PublicIpAddressCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Elemento Microsoft.Network.PublicIpAddressCombo dell'interfaccia utente
Gruppo di controlli per la selezione di un indirizzo IP pubblico nuovo o esistente. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Se l'utente di hello seleziona 'None' per l'indirizzo IP pubblico, casella di testo etichetta nome dominio hello è nascosto.
- Se l'utente di hello seleziona un indirizzo IP pubblico esistente, casella di testo etichetta nome dominio hello è disabilitata. Il valore è l'etichetta del nome di dominio dell'indirizzo IP selezionato hello hello.
- aggiornamenti (ad esempio, westus.cloudapp.azure.com) suffisso nome dominio Hello automaticamente in base alla posizione di hello selezionato.

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Osservazioni
- Se `constraints.required.domainNameLabel` è troppo**true**, utente di hello deve fornire un'etichetta del nome di dominio quando si crea un nuovo indirizzo IP pubblico. Gli indirizzi IP pubblici esistenti senza etichetta non sono disponibili per la selezione.
- Se `options.hideNone` è troppo**true**, quindi hello opzione tooselect **Nessuno** per indirizzo IP pubblico hello indirizzo è nascosto. valore predefinito di Hello è **false**.
- Se `options.hideDomainNameLabel` è troppo**true**, quindi la casella di testo hello per l'etichetta del nome di dominio è nascosto. valore predefinito di Hello è **false**.
- Se `options.hideExisting` è true, l'utente hello non sarà in grado di toochoose un indirizzo IP pubblico esistente. valore predefinito di Hello è **false**.

## <a name="sample-output"></a>Output di esempio
Se l'utente di hello non seleziona alcun indirizzo IP pubblico, hello viene visualizzato output seguente:
```json
{
  "newOrExistingOrNone": "none"
}
```

Se l'utente di hello seleziona un indirizzo IP nuovo o esistente, hello viene visualizzato output seguente:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Quando `options.hideNone` è specificato, `newOrExistingOrNone` restituisce sempre **none**.
- Quando `options.hideDomainNameLabel` è specificato, `domainNameLabel` non viene dichiarato.

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
