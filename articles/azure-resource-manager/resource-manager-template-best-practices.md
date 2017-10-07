---
title: aaaBest procedure consigliate per la creazione di modelli di gestione risorse | Documenti Microsoft
description: Linee guida per la semplificazione dei modelli di Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Procedure consigliate per la creazione di modelli di Azure Resource Manager
Queste linee guida consentono di creare modelli di Azure Resource Manager toouse semplice e affidabile. linee guida di Hello sono solo suggerimenti. e non come requisiti assoluti, salvo diversa indicazione. Lo scenario potrebbe richiedere una variante di uno di hello seguenti approcci o esempi.

## <a name="resource-names"></a>Nomi di risorse
In genere vengono usati tre tipi di nomi di risorse in Resource Manager:

* Nomi di risorse che devono essere univoci.
* I nomi delle risorse che non sono necessari toobe univoco, ma si sceglie un nome che può aiutarti a identificare una risorsa in base al contesto tooprovide.
* Nomi di risorse che possono essere generici.

 Per informazioni sulle restrizioni relative ai nomi di risorse, vedere [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenzioni di denominazione consigliate per le risorse di Azure).

### <a name="unique-resource-names"></a>Nomi di risorse univoci
È necessario fornire un nome univoco per qualsiasi tipo di risorsa con un endpoint di accesso ai dati. Alcuni tipi di risorse comuni che richiedono un nome univoco includono:

* Archiviazione di Azure<sup>1</sup> 
* Funzionalità app Web del servizio app di Azure
* SQL Server
* Insieme di credenziali chiave Azure
* Cache Redis di Azure
* Azure Batch
* Gestione traffico di Azure
* Ricerca di Azure
* HDInsight di Azure

<sup>1</sup> I nomi di account di archiviazione devono essere formati da lettere minuscole, un massimo di 24 caratteri e non devono includere alcun segno meno.

Se si fornisce un parametro per un nome di risorsa, è necessario fornire un nome univoco, quando si distribuiscono risorse hello. Facoltativamente, è possibile creare una variabile che utilizza hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nome di funzione. 

È anche possibile desidera tooadd un prefisso o suffisso toohello **uniqueString** risultato. Modifica nome univoco di hello può identificare più facilmente il tipo di risorsa hello dal nome hello. Ad esempio, è possibile generare un nome univoco per un account di archiviazione tramite hello segue variabile:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Nomi di risorse per l'identificazione
Alcuni tipi di risorsa potrebbe essere necessario tooname, ma i relativi nomi non devono toobe univoco. Per questi tipi di risorsa, è possibile fornire un nome che identifica il contesto di risorsa hello sia il tipo di risorsa hello. Specificare un nome descrittivo che consente di identificare risorse hello in un elenco di risorse. Se è necessario un nome di risorsa diverso per distribuzioni diverse toouse, è possibile utilizzare un parametro per il nome di hello:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Se non è necessario toopass in un nome durante la distribuzione, è possibile utilizzare una variabile: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

In alternativa si può usare un valore hardcoded:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Nomi di risorse generici
Per i tipi di risorse per lo più accessibile tramite una risorsa diversa, è possibile utilizzare un nome generico che è hardcoded nel modello di hello. Ad esempio, è possibile impostare un nome generico e standard per le regole del firewall in SQL server:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>parameters
Hello informazioni seguenti possono essere utili quando si utilizzano parametri:

* Ridurre al minimo l'uso di parametri. Se possibile, usare una variabile o un valore letterale. Specificare parametri solo per questi scenari:
   
   * Impostazioni che si desidera toouse variazioni di base tooenvironment (SKU, dimensioni e dalla capacità).
   * Nomi delle risorse che si desidera toospecify per facilitare l'identificazione.
   * Valori di uso frequente toocomplete altre attività (ad esempio, un nome utente di amministratore).
   * Segreti (ad esempio password).
   * numero di Hello o una matrice di valori toouse quando si creano più istanze di un tipo di risorsa.
* Usare la notazione Camel per i nomi dei parametri.
* Fornire una descrizione di ogni parametro nei metadati hello:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Definire i valori predefiniti per i parametri (ad eccezione delle password e delle chiavi SSH):
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Usare **SecureString** per tutte le password e i segreti: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Quando possibile, non utilizzare un percorso di toospecify di parametro. Utilizzare invece hello **percorso** proprietà hello del gruppo di risorse. Utilizzando hello **gruppo di risorse () .location** espressione per tutte le risorse, le risorse nel modello hello vengono distribuite in hello stesso percorso del gruppo di risorse hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Se un tipo di risorsa è supportato in solo un numero limitato di percorsi, è un percorso valido direttamente nel modello di hello toospecify. Se è necessario utilizzare un **percorso** parametro condividere tale valore del parametro quanto possibile con le risorse che sono probabilmente toobe in hello nello stesso percorso. Questo riduce il numero di hello di volte in cui gli utenti vengono richiesto di informazioni sul percorso tooprovide.
* Evitare di utilizzare un parametro o una variabile per la versione API hello per un tipo di risorsa. I valori e le proprietà delle risorse possono variare in base al numero di versione. In un editor di codice IntelliSense non può determinare schema corretto hello quando è impostato versione API hello tooa parametro o variabile. Livello di codice hello invece la versione API nel modello di hello.

## <a name="variables"></a>variables
Hello seguenti informazioni possono essere utili quando si utilizzano variabili:

* Utilizzare le variabili per i valori necessari toouse più volte in un modello. Se un valore viene utilizzato una sola volta, un valore a livello di codice rende il tooread più semplice del modello.
* Non è possibile utilizzare hello [riferimento](resource-group-template-functions-resource.md#reference) funzione hello **variabili** sezione del modello di hello. Hello **riferimento** funzione deriva il relativo valore dallo stato di runtime della risorsa hello. Tuttavia, le variabili vengono risolti durante l'analisi del modello di hello iniziale hello. Costruire valori che devono hello **riferimento** funzione direttamente in hello **risorse** o **restituisce** sezione del modello di hello.
* Includere le variabili per i nomi di risorse che devono essere univoci, come illustrato in [Nomi di risorse](#resource-names).
* È possibile raggruppare le variabili in oggetti complessi. Hello utilizzare **variable.subentry** formato tooreference un valore da un oggetto complesso. Il raggruppamento delle variabili consente di tenere traccia delle variabili correlate Inoltre, migliora la leggibilità del modello di hello. Ad esempio:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Un oggetto complesso non può contenere un'espressione che fa riferimento a un valore da un oggetto complesso. A questo scopo, definire una variabile separata.
   > 
   > 
   
     Per esempi avanzati di uso di oggetti complessi come variabili, vedere [Condividere lo stato tra modelli di Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="resources"></a>Risorse
Hello seguenti informazioni possono essere utili quando si lavora con risorse:

* toohelp altri collaboratori comprendere hello scopo della risorsa hello, specificare **commenti** per ogni risorsa nel modello hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* È possibile usare tag tooadd metadati tooresources. Utilizzare i metadati tooadd informazioni sulle risorse. Ad esempio, è possibile aggiungere metadati toorecord i dettagli di fatturazione per una risorsa. Per ulteriori informazioni, vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md).
* Se si utilizza un *endpoint pubblico* nel modello (ad esempio, un Blob di Azure storage endpoint pubblico), *eseguire hardcoded* hello dello spazio dei nomi. Hello utilizzare **riferimento** toodynamically funzione recuperare hello dello spazio dei nomi. È possibile utilizzare gli ambienti di spazio dei nomi pubblici questo approccio toodeploy hello modello toodifferent senza modificare manualmente l'endpoint di hello nel modello di hello. Impostare hello API versione toohello stessa versione in uso per l'account di archiviazione hello nel modello:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Se l'account di archiviazione hello viene distribuito in hello stesso modello che si sta creando, non è necessario spazio dei nomi del provider di hello toospecify quando si fa riferimento a risorse hello. Questa è la sintassi semplificata hello:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Se si dispone di altri valori nel modello toouse configurato uno spazio dei nomi pubblico, modificare questi valori tooreflect hello stesso **riferimento** (funzione). Ad esempio, è possibile impostare hello **storageUri** proprietà del profilo di diagnostica della macchina virtuale hello:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   È anche possibile fare riferimento a un account di archiviazione in un gruppo di risorse diverso:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Assegnare pubblica macchina di virtuale tooa di indirizzi IP solo quando richiesto da un'applicazione. tooconnect tooa macchina virtuale (VM) per il debug o per la gestione o a scopi amministrativi, utilizzare le regole NAT in ingresso, un gateway di rete virtuale o un jumpbox.
   
     Per ulteriori informazioni sulla connessione toovirtual macchine, vedere:
   
   * [Eseguire macchine virtuali per un'architettura a più livelli in Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Consentire l'accesso esterno tooyour VM usando hello portale di Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Consentire l'accesso esterno tooyour VM tramite PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Consentire l'accesso esterno tooyour VM Linux tramite CLI di Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Hello **domainNameLabel** proprietà per gli indirizzi IP pubblici devono essere univoci. Hello **domainNameLabel** valore deve essere compresa tra 3 e 63 caratteri e seguire le regole di hello specificate da questa espressione regolare: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Poiché hello **uniqueString** funzione genera una stringa di 13 caratteri, hello **dnsPrefixString** parametro è limitato too50 caratteri:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Quando si aggiunge un'estensione di uno script personalizzato tooa password, utilizzare hello **commandToExecute** proprietà hello **protectedSettings** proprietà:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure che informazioni riservate vengono crittografate quando vengono passati come parametri tooVMs ed estensioni, utilizzare hello **protectedSettings** proprietà delle estensioni di hello pertinente.
   > 
   > 

## <a name="outputs"></a>outputs
Se si utilizzano un modello toocreate gli indirizzi IP pubblici, includere un **restituisce** sezione che restituisce i dettagli di indirizzo IP hello e il nome di dominio completo hello (FQDN). Dopo la distribuzione, è possibile utilizzare output valori tooeasily recuperare dettagli pubblica gli indirizzi IP e nomi di dominio completi. Quando si fa riferimento a risorse hello, utilizzare una versione di hello API utilizzate toocreate è: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Modello singolo o modelli annidati
toodeploy la soluzione, è possibile utilizzare un singolo modello o un modello principale con più modelli annidati. I modelli annidati sono comuni per scenari più avanzati. Utilizzo di un consente di modello nidificato hello seguenti vantaggi:

* È possibile scomporre la soluzione in componenti di destinazione.
* È possibile riusare i modelli annidati con modelli principali diversi.

Se si sceglie di modelli annidati toouse, hello alle linee guida consentono di standardizzare schema del modello. Queste linee guida si basano sui [criteri di progettazione per modelli di Azure Resource Manager](best-practices-resource-manager-design-templates.md). È consigliabile una progettazione con hello seguenti modelli:

* **Modello principale** (azuredeploy.json). Utilizzo per i parametri di input hello.
* **Modello di risorse condivise**. Le risorse che utilizzano tutte le altre risorse sono condivise toodeploy utilizzare (ad esempio, virtuale rete e la disponibilità set). Hello utilizzare **dependsOn** espressione tooensure che questo modello viene distribuito prima di altri modelli.
* **Modello di risorse facoltative**. Utilizzare tooconditionally distribuire risorse in base a un parametro (ad esempio, un jumpbox).
* **Modello di risorse membro**. Ogni tipo di istanza all'interno di un livello di applicazione prevede una propria configurazione. All'interno di un livello, è possibile definire diversi tipi di istanza. (Ad esempio, hello prima istanza di viene creato un cluster e istanze aggiuntive vengono aggiunte cluster esistente toohello.) Ogni tipo di istanza avrà un proprio modello di distribuzione.
* **Script**. Per ogni tipo di istanza sono applicabili script ampiamente riutilizzabili, come ad esempio quelli di inizializzazione e formattazione di dischi aggiuntivi. Gli script personalizzati creati per uno scopo specifico di personalizzazione sono diversi, in base al tipo di istanza hello.

![Modello annidato](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Per altre informazioni, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Collegare in modo condizionale toonested modelli
È possibile utilizzare modelli di toonested un parametro tooconditionally collegamento. il parametro Hello diventa parte di hello URI per il modello di hello:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Formato del modello
È una buona norma toopass il modello tramite un validator JSON. Un validator può aiutare a rimuovere virgole, parentesi e parentesi quadre estranee che potrebbero causare un errore durante la distribuzione. Provare [JSONlint](http://jsonlint.com/) o un pacchetto linter per l'ambiente di modifica preferito (Visual Studio Code, Atom, Sublime Text, Visual Studio).

È anche una buona idea tooformat il file JSON per una migliore leggibilità. È possibile usare un pacchetto formattatore JSON per l'editor locale. In Visual Studio, il documento di hello tooformat, premere **Ctrl + K, Ctrl + D**. In Visual Studio Code, usare **Alt+Shift+F**. Se l'editor locale non Formatta documento hello, è possibile utilizzare un [formattatore online](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Passaggi successivi
* Per indicazioni sull'architettura della soluzione per le macchine virtuali, vedere [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Eseguire una macchina virtuale Windows in Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Eseguire una macchina virtuale Linux in Azure).
* Per indicazioni sulla configurazione di un account di archiviazione, vedere l'[elenco di controllo di prestazioni e scalabilità per Archiviazione di Azure](../storage/common/storage-performance-checklist.md).
* toolearn su come usare un'azienda tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise: governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

