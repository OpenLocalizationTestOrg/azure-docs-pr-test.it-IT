---
title: Gestione risorse aaaAzure struttura di modello e la sintassi | Documenti Microsoft
description: "Descrive la struttura hello e le proprietà dei modelli di gestione risorse di Azure utilizzando la sintassi dichiarativa JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Comprendere la struttura di hello e sintassi dei modelli di gestione risorse di Azure
Questo argomento descrive la struttura hello di un modello di gestione risorse di Azure. Presenta diverse sezioni di hello di un modello e hello proprietà che è disponibili in quelle sezioni. modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione. Per un'esercitazione dettagliata sulla creazione di un modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Formato del modello
Nella struttura più semplice, un modello contiene hello seguenti elementi:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--- |:--- |:--- |
| $schema |Sì |Percorso del file di schema hello JSON che descrive una versione di hello hello della lingua del modello. Utilizzare l'URL di hello illustrato nell'esempio sopra riportato hello. |
| contentVersion |Sì |Versione del modello di hello (ad esempio, 1.0.0.0). Questo elemento accetta tutti i valori. Durante la distribuzione di risorse utilizzando il modello di hello, questo valore può essere utilizzato toomake che viene utilizzato il modello di destra hello. |
| parameters |No |I valori forniti durante la distribuzione è eseguita la distribuzione di risorse toocustomize. |
| variables |No |Valori utilizzati come frammenti JSON in espressioni di linguaggio modello toosimplify modello hello. |
| resources |Sì |Tipi di risorse che vengono distribuite o aggiornate in un gruppo di risorse. |
| outputs |No |Valori restituiti dopo la distribuzione. |

Ogni elemento contiene proprietà che è possibile impostare. Hello di esempio seguente contiene una sintassi completa di hello per un modello:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Verranno esaminati sezioni hello del modello di hello in dettaglio più avanti in questo argomento.

## <a name="expressions-and-functions"></a>Espressioni e funzioni
sintassi di base del modello di hello Hello è JSON. Tuttavia, espressioni e funzioni estendono hello JSON i valori disponibili nel modello di hello.  Le espressioni sono scritte in valori letterali stringa JSON il cui primo e ultimo carattere sono tra parentesi quadre hello: `[` e `]`, rispettivamente. il valore di Hello dell'espressione hello viene valutato quando viene distribuito il modello di hello. Durante la scrittura di un valore letterale stringa, il risultato di hello della valutazione di espressione hello può essere di tipo JSON diverso, ad esempio una matrice o un numero intero, a seconda espressione effettiva hello.  una stringa letterale iniziare con una parentesi quadra toohave `[`, ma non viene interpretato come un'espressione, aggiungere una stringa di hello toostart tra parentesi quadre aggiuntive con `[[`.

In genere, si usano espressioni con operazioni tooperform funzioni per la configurazione di distribuzione hello. Proprio come in JavaScript, le chiamate di funzione sono formattate come `functionName(arg1,arg2,arg3)`. Fare riferimento alle proprietà utilizzando gli operatori di hello punto e [index].

Hello di esempio seguente viene illustrato come toouse diverse funzioni durante la costruzione di valori:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Per hello l'elenco completo delle funzioni di modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md). 

## <a name="parameters"></a>parameters
Nella sezione parametri di hello del modello di hello, specificare i valori che è possibile immettere quando si distribuisce hello risorse. Valori di questi parametri consentono di distribuzione hello toocustomize fornendo i valori che sono specifiche per un particolare ambiente (ad esempio sviluppo, test e produzione). Non si dispone tooprovide parametri nel modello, ma senza parametri del modello potrebbe distribuire sempre hello stesse risorse con hello nomi, percorsi e le stesse proprietà.

Definire i parametri con hello seguente struttura:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--- |:--- |:--- |
| parameterName |Sì |Nome del parametro hello. Deve essere un identificatore JavaScript valido. |
| type |Sì |Tipo di valore del parametro hello. Dopo questa tabella, vedere elenco hello dei tipi consentiti. |
| defaultValue |No |Valore predefinito per il parametro hello, se viene fornito alcun valore per il parametro hello. |
| allowedValues |No |Matrice di valori consentiti per toomake parametro hello assicurarsi che venga fornito valore destro hello. |
| minValue |No |valore minimo di Hello per i parametri di tipo int, questo valore è inclusivo. |
| maxValue |No |Hello valore massimo per i parametri di tipo int, questo valore è inclusivo. |
| minLength |No |lunghezza minima di Hello per stringa secureString e parametri di tipo matrice, questo valore è inclusivo. |
| maxLength |No |Hello lunghezza massima consentita per i parametri di tipo matrice, stringa e secureString, questo valore è inclusivo. |
| description |No |Descrizione del parametro hello che viene visualizzata toousers tramite il portale di hello. |

Hello tipi consentiti e i valori sono:

* **string**
* **secureString**
* **int**
* **bool**
* **object** 
* **secureObject**
* **array**

toospecify un parametro come facoltativo, fornire un valore predefinito (può essere una stringa vuota). 

Se si specifica un nome di parametro nel modello che corrisponde a un parametro di modello di hello toodeploy comando hello, sussiste ambiguità sui valori hello forniti. Gestione risorse consente di risolvere questa confusione aggiungendo il suffisso hello **FromTemplate** toohello parametro di modello. Ad esempio, se si include un parametro denominato **ResourceGroupName** nel modello, è in conflitto con hello **ResourceGroupName** parametro hello [ Nuovo AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet. Durante la distribuzione, si è tooprovide richiesto un valore per **ResourceGroupNameFromTemplate**. In generale, si dovrebbe evitare questa confusione, non denominazione dei parametri con hello stesso nome come parametri utilizzati per operazioni di distribuzione.

> [!NOTE]
> Tutte le password, chiavi e altri segreti devono usare hello **secureString** tipo. Se si passano dati sensibili in un oggetto JSON, utilizzare hello **secureObject** tipo. Non è possibile leggere i parametri di modello di tipo secureString o secureObject dopo la distribuzione delle risorse. 
> 
> Ad esempio, hello seguente voce nella cronologia della distribuzione hello Mostra hello valore per una stringa e un oggetto, ma non per secureString e secureObject.
>
> ![visualizzare i valori della distribuzione](./media/resource-group-authoring-templates/show-parameters.png)  
>

Hello seguente esempio viene illustrato come toodefine parametri:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Per il parametro hello tooinput come valori durante la distribuzione, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md). 

## <a name="variables"></a>variables
Nella sezione variabili hello è costruire valori che possono essere utilizzati in tutto il modello. Non è necessario toodefine variabili, ma semplificano spesso il modello riducendo le espressioni complesse.

Definire le variabili con hello seguente struttura:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Hello seguente esempio viene illustrato come toodefine una variabile che viene costruita dai due valori di parametro:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Hello esempio successivo mostra una variabile che è un tipo complesso di JSON e le variabili sono costituite da altre variabili:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Risorse
Nella sezione risorse hello, definire le risorse di hello che vengono distribuite o aggiornate. In questa sezione può diventare complicata perché è necessario comprendere i tipi di hello distribuisce i valori corretti di tooprovide hello. Per hello risorse valori specifici (apiVersion, tipo e proprietà) che è necessario tooset, vedere [definire le risorse nei modelli di Azure Resource Manager](/azure/templates/). 

Si definiscono le risorse con hello seguente struttura:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--- |:--- |:--- |
| condition | No | Valore booleano che indica se la risorsa hello viene distribuita. |
| apiVersion |Sì |Versione di hello toouse di API REST per la creazione di risorse hello. |
| type |Sì |Tipo di risorsa hello. Questo valore è una combinazione di spazio dei nomi hello del provider di risorse hello e il tipo di risorsa hello (ad esempio **Microsoft.Storage/storageAccounts**). |
| name |Sì |Nome della risorsa hello. nome di Hello deve rispettare le restrizioni dei componenti URI definite in RFC3986. Inoltre, servizi di Azure che espongono parti toooutside nome risorsa di hello convalidare toomake nome hello che non sia un tentativo toospoof un'altra identità. |
| location |Variabile |Posizioni geografiche supportate di hello forniva risorse. È possibile selezionare una delle posizioni disponibili hello, ma in genere rende toopick senso che gli utenti tooyour Chiudi. In genere, è anche consigliabile tooplace risorse che interagiscono tra loro hello stessa area. La maggior parte dei tipi di risorsa richiede una posizione, ma alcuni tipi (ad esempio un'assegnazione di ruolo) non la richiedono. Vedere [Impostare la posizione delle risorse nei modelli di Azure Resource Manager](resource-manager-template-location.md). |
| tags |No |Tag associati a risorse hello. Vedere [Applicare i tag alle risorse nei modelli di Azure Resource Manager](resource-manager-template-tags.md). |
| commenti |No |Le note per documentare le risorse di hello nel modello |
| copy |No |Se è necessaria più di un'istanza, hello numero di risorse toocreate. modalità predefinita di Hello è parallela. Specificare la modalità seriale quando non si desidera che tutti o hello toodeploy risorse in hello contemporaneamente. Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |No |Risorse da distribuire prima della distribuzione di questa risorsa. Gestione risorse valuta hello le dipendenze tra le risorse e li distribuisce nell'ordine corretto hello. Quando le risorse non sono interdipendenti, vengono distribuite in parallelo. Hello valore può essere un elenco delimitato da virgole di una risorsa di nomi o gli identificatori univoci di risorse. Elencare solo le risorse distribuite in questo modello. Le risorse non definite in questo modello devono essere già esistenti. Evitare di aggiungere dipendenze non necessarie perché possono rallentare la distribuzione e creare dipendenze circolari. Per indicazioni sull'impostazione delle dipendenze, vedere l'articolo relativo alla [definizione delle dipendenze nei modelli di Azure Resource Manager](resource-group-define-dependencies.md). |
| properties |No |Impostazioni di configurazione specifiche delle risorse. i valori Hello per le proprietà di hello sono hello stesso come valori hello forniti nel corpo della richiesta hello per hello API REST (metodo PUT) toocreate hello risorsa. È inoltre possibile specificare un toocreate matrice copia più istanze di una proprietà. Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md). |
| resources |No |Risorse figlio che dipendono dalla risorsa hello da definire. Specificare solo i tipi di risorse che sono consentiti dallo schema hello della risorsa padre hello. Hello nome completo del tipo di risorsa figlio hello include tipo di risorsa padre hello, ad esempio **Microsoft.Web/sites/extensions**. Dipendenza dalla risorsa padre hello non è implicita. È necessario definirla in modo esplicito. |

sezione delle risorse Hello contiene una matrice di hello toodeploy di risorse. All'interno di ogni risorsa è anche possibile definire una matrice di risorse figlio. La sezione resources potrebbe quindi avere una struttura simile a questa:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Per altre informazioni sulla definizione delle risorse figlio, vedere [Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager](resource-manager-template-child-resource.md).

Hello **condizione** elemento specifica se la risorsa hello è distribuita. un valore per questo elemento Hello risolve tootrue o false. Ad esempio, toospecify se viene distribuito un nuovo account di archiviazione, utilizzare:

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

toospecify se una macchina virtuale viene distribuita con una password o chiave SSH, definire due versioni della macchina virtuale hello nel modello e utilizzare **condizione** toodifferentiate utilizzo. Passare un parametro che specifica quali toodeploy scenario.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Per un esempio di utilizzo di una password o una macchina virtuale di toodeploy chiave SSH, vedere [nome utente o SSH modello condizione](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>outputs
Nella sezione di output di hello, specificare i valori restituiti dalla distribuzione. Ad esempio, è possibile restituire hello URI tooaccess una risorsa distribuita.

Hello seguente illustra la struttura hello di una definizione di output:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--- |:--- |:--- |
| outputName |Sì |Nome del valore di output di hello. Deve essere un identificatore JavaScript valido. |
| type |Sì |Tipo di valore di output di hello. I valori di output supportano hello stesso tipi come parametri di input di modello. |
| value |Sì |Espressione del linguaggio di modello valutata e restituita come valore di output. |

Hello esempio seguente mostra un valore che viene restituito nella sezione di output di hello.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Per altre informazioni sull'utilizzo dell'output, vedere [Condivisione dello stato in modelli di Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Limiti del modello

Limita le dimensioni di hello di too1 il modello file KB too64 MB e ogni parametro. limite di 1 MB Hello applica lo stato finale di toohello del modello di hello dopo che è stato espanso con definizioni di risorse iterativo e i valori di variabili e parametri. 

Si è anche limitati a:

* 256 parametri
* 256 variabili
* 800 risorse (incluso il conteggio copie)
* 64 valori di output
* 24.576 caratteri in un'espressione di modello

È possibile superare alcuni limiti del modello usando un modello annidato. Per altre informazioni, vedere [Uso di modelli collegati nella distribuzione di risorse di Azure](resource-group-linked-templates.md). numero di hello tooreduce di parametri, variabili o output, è possibile combinare più valori in un oggetto. Per altre informazioni, vedere [Oggetti come parametri](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Passaggi successivi
* modelli completo di tooview per molti tipi diversi di soluzioni, vedere hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).
* Per informazioni dettagliate sulle funzioni hello è possibile usare dall'interno di un modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md).
* toocombine più modelli durante la distribuzione, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* Potrebbe essere necessario toouse risorse esistenti all'interno di un gruppo di risorse diverso. Questo scenario è comune quando si usano account di archiviazione o reti virtuali condivisi tra più gruppi di risorse. Per ulteriori informazioni, vedere hello [funzione resourceId](resource-group-template-functions-resource.md#resourceid).
