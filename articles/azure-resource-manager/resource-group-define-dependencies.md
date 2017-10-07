---
title: ordine di distribuzione aaaSet per le risorse di Azure | Documenti Microsoft
description: Viene descritto come tooset una risorsa come dipendente da un'altra risorsa durante le risorse tooensure distribuzione vengono distribuiti nell'ordine corretto hello.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Definire l'ordine di hello per la distribuzione delle risorse nei modelli di gestione risorse di Azure
Per una determinata risorsa, possono essere presenti altre risorse che devono essere presente prima di distribuire risorse hello. Ad esempio, un server SQL deve esistere prima di tentare di toodeploy un database SQL. Per definire questa relazione, contrassegnare una risorsa come hello dipendente da un'altra risorsa. Si definisce una dipendenza con hello **dependsOn** elemento, o tramite hello **riferimento** (funzione). 

Gestione risorse valuta hello le dipendenze tra le risorse e li distribuisce in base all'ordine dipendenti. Quando le risorse non sono interdipendenti, Resource Manager le distribuisce in parallelo. È necessario solo toodefine dipendenze per le risorse distribuite in hello stesso modello. 

## <a name="dependson"></a>dependsOn
All'interno di un modello di elemento dependsOn hello consente toodefine una risorsa come dipendente in una o più risorse. Il valore può essere un elenco delimitato da virgole di nomi di risorse. 

Hello esempio seguente viene illustrato un set di scalabilità della macchina virtuale che dipende da un servizio di bilanciamento del carico di rete virtuale e un ciclo che crea più account di archiviazione. Queste altre risorse non sono visualizzate nel seguente esempio hello, ma è necessario tooexist in un' posizione nel modello di hello.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

In hello sopra riportato, una dipendenza è incluso nelle risorse hello che vengono create tramite un ciclo di copia denominato **storageLoop**. Per avere un esempio, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).

Quando si definiscono le dipendenze, è possibile includere hello resource provider dello spazio dei nomi e delle risorse tipo tooavoid ambiguità. Tooclarify, ad esempio, un servizio di bilanciamento del carico e la rete virtuale che può avere hello che nomi identici rispetto alle altre risorse, utilizzare hello seguente formato:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Sebbene sia toouse inclinata dependsOn toomap relazioni tra le risorse, è importante toounderstand perché si sta eseguendo. Ad esempio, come le risorse sono collegate tra loro, toodocument dependsOn non approccio giusto hello. È possibile eseguire query quali risorse sono state definite nell'elemento dependsOn hello dopo la distribuzione. L'uso di dependsOn potrebbe influire sul tempo necessario per la distribuzione perché Resource Manager non esegue la distribuzione simultanea di due risorse con dipendenza. toodocument relazioni tra le risorse, utilizzare invece [collegamento delle risorse](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Risorse figlio
proprietà di risorse Hello consente toospecify risorse figlio correlate toohello risorsa che viene definita. Le risorse figlio possono essere solo definite da cinque livelli. È importante toonote che non è una relazione implicita creata tra una risorsa di figlio e padre hello. Se è necessario hello toobe risorse figlio distribuiti dopo la risorsa padre hello, è necessario dichiarare in modo esplicito tale dipendenza con proprietà dependsOn hello. 

Ogni risorsa padre accetta solo determinati tipi di risorse come risorse figlio. Hello accettati vengono specificati i tipi di risorse in hello [schema del modello](https://github.com/Azure/azure-resource-manager-schemas) della risorsa padre hello. nome di Hello del tipo di risorsa figlio include il nome di hello del tipo di risorsa padre hello, ad esempio **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** sono entrambe le risorse figlio di hello  **Microsoft.Web/sites**.

Hello di esempio seguente viene illustrato un SQL server e database SQL. Si noti che una dipendenza esplicita viene definita tra il database SQL hello e SQL server, anche se il database di hello è un elemento figlio di server hello.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>funzione di riferimento
Hello [fanno riferimento a funzione](resource-group-template-functions-resource.md#reference) consente a un'espressione tooderive il relativo valore da altre coppie nome / valore JSON o risorse di runtime. Le Espressioni di riferimento in modo implicito dichiarano che una risorsa dipende da un altro. formato generale Hello è:

```json
reference('resourceName').propertyPath
```

Nell'esempio seguente di hello, un endpoint rete CDN dipende dal profilo CDN hello in modo esplicito e in modo implicito dipende da un'app web.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

È possibile utilizzare questo elemento oppure hello dependsOn elemento toospecify le dipendenze, ma non è necessario toouse entrambi per hello stessa risorsa dipendente. Se possibile, utilizzare tooavoid un riferimento implicito aggiunta di una dipendenza non necessaria.

vedere, più toolearn [fanno riferimento a funzione](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Raccomandazioni per l'impostazione delle dipendenze

Quando si decide quali tooset dipendenze, usare hello alle linee guida:

* Impostare il minor numero possibile di dipendenze.
* Impostare una risorsa figlio come dipendente dalla risorsa padre.
* Hello utilizzare **riferimento** funzione tooset dipendenze implicito tra le risorse che devono tooshare una proprietà. Non aggiungere una dipendenza esplicita (**dependsOn**) quando è già stata definita una dipendenza implicita. Questo approccio riduce il rischio di hello di dipendenze non necessari. 
* Impostare una dipendenza quando una risorsa non può essere **creata** senza le funzionalità di un'altra risorsa. Non impostare una dipendenza se le risorse di hello interagiscono solo dopo la distribuzione.
* Consentire la propagazione a catena delle dipendenze senza impostarle esplicitamente. Ad esempio, la macchina virtuale dipende da un'interfaccia di rete virtuale e l'interfaccia di rete virtuale hello dipende da una rete virtuale e gli indirizzi IP pubblici. Pertanto, la macchina virtuale di hello è distribuite dopo che tutte le tre risorse, ma non imposta in modo esplicito macchina virtuale hello come dipendente da tutte e tre le risorse. Questo approccio è illustrata l'ordine di dipendenza hello e rende più semplice modello di hello toochange in un secondo momento.
* Se un valore può essere determinato prima della distribuzione, provare a distribuire risorse hello senza una dipendenza. Ad esempio, se un valore di configurazione deve nome hello di un'altra risorsa, non è una dipendenza. Questa Guida non sempre funziona perché alcune risorse di verificare l'esistenza hello hello altra risorsa. Se viene visualizzato un errore, aggiungere una dipendenza. 

Resource Manager identifica le dipendenze circolari durante la convalida del modello. Se si riceve un errore che informa che è presente una dipendenza circolare, valutare il modello toosee se tutte le dipendenze non sono necessari e possono essere rimossi. Se la rimozione di dipendenze non funziona, è possibile evitare dipendenze circolari spostando alcune operazioni di distribuzione in risorse figlio che vengono distribuite dopo le risorse di hello che dispongono di una dipendenza circolare hello. Si supponga, ad esempio, si distribuiscono due macchine virtuali, ma è necessario impostare proprietà su ciascuna di esse che fanno riferimento altri toohello. È possibile distribuirli in hello seguente ordine:

1. VM 1
2. VM 2
3. L'estensione in VM 1 dipende da VM 1 e VM 2. estensione Hello imposta valori per vm1 ottenute da vm2.
4. L'estensione in VM 2 dipende da VM 1 e VM 2. estensione Hello imposta valori per vm2 ottenute da vm1.

Per informazioni sulla valutazione di ordine di distribuzione hello e risoluzione degli errori di dipendenza, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla risoluzione dei problemi di dipendenze durante la distribuzione, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sulla creazione di modelli di gestione risorse di Azure, vedere [creazione di modelli](resource-group-authoring-templates.md). 
* Per un elenco di funzioni disponibili di hello in un modello, vedere [funzioni di modello](resource-group-template-functions.md).

