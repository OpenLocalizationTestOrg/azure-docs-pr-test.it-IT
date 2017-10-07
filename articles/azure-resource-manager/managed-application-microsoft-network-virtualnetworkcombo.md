---
title: elemento gestita dell'interfaccia utente dell'applicazione VirtualNetworkCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Network.VirtualNetworkCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Elemento Microsoft.Network.VirtualNetworkCombo dell'interfaccia utente
Gruppo di controlli per la selezione di una rete virtuale nuova o esistente. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- In wireframe superiore hello, utente hello ha selezionato una nuova rete virtuale, in modo da Personalizza il prefisso di nome e l'indirizzo della subnet, ogni utente hello. In questo caso la configurazione delle subnet è facoltativa.
- In hello inferiore wireframe, utente hello è selezionato di una rete virtuale esistente, pertanto è necessario eseguire il mapping utente hello ogni modello di distribuzione hello subnet richiede tooan esistente subnet. In questo caso la configurazione delle subnet è obbligatoria.

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Osservazioni
- Se specificato, hello prima non sovrapposti prefisso dell'indirizzo dimensioni `defaultValue.addressPrefixSize` viene determinato automaticamente in base alle reti virtuali esistenti nella sottoscrizione hello dell'utente.
- il valore predefinito per Hello `defaultValue.name` e `defaultValue.addressPrefixSize` è **null**.
- Specificare `constraints.minAddressPrefixSize`. Qualsiasi rete virtuale esistente con uno spazio di indirizzi più piccolo di quelli hello valore specificato non sono disponibili per la selezione.
- Specificare `subnets` e specificare `constraints.minAddressPrefixSize` per ogni subnet.
- Quando si crea una nuova rete virtuale, viene calcolato automaticamente in base prefisso dell'indirizzo della subnet ogni sul prefisso dell'indirizzo della rete virtuale hello e la rispettiva `addressPrefixSize`.
- Quando si usa una rete virtuale esistente, le subnet di dimensioni inferiori al rispettivo `constraints.minAddressPrefixSize` non sono disponibili per la selezione. Inoltre, se specificato, le subnet che non contengono almeno `minAddressCount` indirizzi disponibili non sono disponibili per la selezione.
valore predefinito di Hello è **0**. tooensure che hello indirizzi disponibili sono contigui, specificare **true** per `requireContiguousAddresses`. valore predefinito di Hello è **true**.
- La creazione di subnet in una rete virtuale esistente non è supportata.
- Se `options.hideExisting` è **true**, utente hello non è possibile scegliere una rete virtuale esistente. valore predefinito di Hello è **false**.

## <a name="sample-output"></a>Output di esempio
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
