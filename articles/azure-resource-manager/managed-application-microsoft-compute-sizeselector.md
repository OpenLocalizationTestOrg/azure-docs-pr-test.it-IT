---
title: elemento gestita dell'interfaccia utente dell'applicazione SizeSelector aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Compute.SizeSelector hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Elemento Microsoft.Compute.SizeSelector dell'interfaccia utente
Controllo per la selezione di una dimensione per una o più istanze di macchina virtuale. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Osservazioni
- `recommendedSizes` deve contenere almeno una dimensione. Hello è innanzitutto consigliabile dimensione viene utilizzata come valore predefinito di hello.
- Se una dimensione consigliata non è disponibile nel percorso selezionato hello, dimensioni hello viene ignorata automaticamente. Hello dimensioni consigliate successiva viene invece utilizzata.
- Qualsiasi dimensione non è specificato in hello `constraints.allowedSizes` è nascosto e di qualsiasi dimensione non è specificato `constraints.excludedSizes` viene visualizzato.
`constraints.allowedSizes` e `constraints.excludedSizes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente. elenco di Hello di dimensioni disponibili può essere determinato chiamando [elenco delle dimensioni della macchina virtuale disponibile per una sottoscrizione](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- È necessario specificare `osPlatform`, che può essere **Windows** o **Linux**. I costi di hardware hello toodetermine delle macchine virtuali hello è utilizzato.
- `imageReference` viene omesso per le immagini proprietarie e viene specificato per le immagini di terze parti. I costi di software hello toodetermine delle macchine virtuali hello è utilizzato.
- `count`è moltiplicatore di appropriato hello tooset utilizzato per l'elemento hello. Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').vmCount]`. valore predefinito di Hello è **1**.

## <a name="sample-output"></a>Output di esempio
```json
"Standard_D1"
```

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).
