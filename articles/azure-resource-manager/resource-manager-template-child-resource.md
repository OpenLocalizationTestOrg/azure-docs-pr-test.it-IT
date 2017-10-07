---
title: la risorsa aaaDefine figlio nel modello di Azure | Documenti Microsoft
description: Viene illustrato come tooset hello tipo di risorsa e il nome per la risorsa figlio in un modello di gestione risorse di Azure
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager
Quando si crea un modello, spesso necessario tooinclude una risorsa figlio risorsa padre tooa correlati. Il modello, ad esempio, potrebbe includere un'istanza di SQL Server e un database. Hello SQL server è risorsa padre hello e database hello è la risorsa figlio hello. 

formato Hello hello figlio del tipo di risorsa è:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

formato Hello hello figlio del nome di risorsa è:`{parent-resource-name}/{child-resource-name}`

È tuttavia specificare hello tipo e il nome in un modello in modo diverso in base è annidata all'interno di risorsa padre hello oppure autonomamente al primo livello hello. Questo argomento viene illustrato come si avvicina toohandle entrambi.

Quando si crea una risorsa di riferimento completo tooa, hello ordine toocombine segmenti dal tipo hello e nome non è semplicemente una concatenazione di due hello.  Dopo aver hello dello spazio dei nomi, utilizzare invece una sequenza di *nome/tipo* le coppie meno specifico toomost specifico:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

ad esempio:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` è corretto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` non è corretto

## <a name="nested-child-resource"></a>Risorsa figlio annidata
toodefine modo più semplice di Hello una risorsa figlio è toonest in risorsa padre hello. Hello esempio seguente viene illustrato un database SQL annidato in un Server SQL.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Per una risorsa figlio hello tipo hello è troppo`databases` ma il tipo di risorsa completo `Microsoft.Sql/servers/databases`. Non si specifica `Microsoft.Sql/servers/` perché si presuppone dal tipo di risorsa padre hello. nome di risorsa figlio Hello impostato troppo`exampledatabase` ma il nome completo di hello include il nome del padre hello. Non si specifica `exampleserver` perché si presuppone dalla risorsa padre hello.

## <a name="top-level-child-resource"></a>Risorsa figlio di primo livello
È possibile definire la risorsa figlio hello al primo livello hello. È possibile utilizzare questo approccio se risorsa padre hello non viene distribuito nella hello stesso modello o se desidera toouse `copy` toocreate più risorse figlio. Con questo approccio, è necessario fornire il tipo di risorsa completo hello e includono nome della risorsa padre di hello nel nome di risorsa figlio hello.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

database Hello è un server di toohello risorse figlio, anche se sono definiti in hello stesso livello nel modello di hello.

## <a name="next-steps"></a>Passaggi successivi
* Per indicazioni su come toocreate modelli, vedere [procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).
* Per un esempio della creazione di più risorse figlio, vedere [Distribuire più istanze delle risorse nei modelli di Azure Resource Manager](resource-group-create-multiple.md).
