---
title: criteri delle risorse aaaAzure | Documenti Microsoft
description: Viene descritto come toouse Azure Resource Manager criteri tooensure risorse coerente vengono impostate durante la distribuzione. I criteri possono essere applicati a hello sottoscrizione o gruppi di risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Cenni preliminari sui criteri delle risorse
Criteri di risorse consentono di convenzioni tooestablish per le risorse dell'organizzazione. Definendo le convenzioni, è possibile controllare i costi e gestire più facilmente le risorse. È ad esempio possibile specificare che vengano consentiti solo determinati tipi di macchine virtuali. In alternativa, è possibile richiedere che tutte le risorse abbiano un tag specifico. I criteri vengono ereditati da tutte le risorse figlio. Se il criterio viene applicato tooa gruppo di risorse, è pertanto applicabile tooall risorse di hello in tale gruppo di risorse.

Esistono due concetti toounderstand sui criteri:

* definizione dei criteri - descrivono criteri quando hello e quali tootake azione
* assegnazione di criteri - si applica hello definizione tooa ambito dei criteri (sottoscrizione o gruppo di risorse)

In questo argomento viene illustrata la definizione di criteri. Per informazioni sull'assegnazione di criteri, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md) o [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).

I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).

> [!NOTE]
> Attualmente, criteri non restituiscono i tipi di risorsa che non supportano i tag, tipo e posizione, ad esempio il tipo di risorsa Microsoft.Resources/deployments hello. Il supporto di questo tipo di risorsa verrà aggiunto in futuro. problemi di compatibilità con le versioni precedenti di tooavoid, sarà necessario specificare tipo in modo esplicito durante la creazione di criteri. A tutti i tipi viene ad esempio applicato un criterio per i tag che non specifica i tipi, In tal caso, una distribuzione modello potrebbe non riuscire se è presente una risorsa annidata che non supporta i tag e tipo di risorsa distribuzione hello è stato aggiunto toopolicy valutazione. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Quali sono le differenze rispetto al controllo degli accessi in base al ruolo?
Esistono differenze importanti tra i criteri e il controllo degli accessi in base al ruoli (RBAC). Il Controllo degli accessi in base al ruolo è incentrato sulle azioni dell'**utente** in ambiti diversi. Ad esempio, vengono aggiunti il ruolo di collaboratore toohello per un gruppo di risorse nell'ambito di hello desiderato, pertanto è possibile apportare le modifiche toothat gruppo di risorse. I criteri si concentrano sulle proprietà delle **risorse** durante la distribuzione. Ad esempio, tramite i criteri, è possibile controllare i tipi di hello delle risorse che è possono effettuare il provisioning. In alternativa, è possibile limitare i percorsi di hello in cui è possono effettuare il provisioning di risorse hello. A differenza del controllo degli accessi in base al ruolo, i criteri rappresentano un sistema con autorizzazioni predefinite e negazione esplicita. 

toouse criteri, è necessario che l'autenticazione tramite RBAC. In particolare, per l'account sono necessari:

* `Microsoft.Authorization/policydefinitions/write`autorizzazione toodefine un criterio
* `Microsoft.Authorization/policyassignments/write`autorizzazione tooassign un criterio 

Queste autorizzazioni non sono incluse in hello **collaboratore** ruolo.

## <a name="built-in-policies"></a>Criteri predefiniti

Azure offre alcune definizioni di criteri predefiniti che possono ridurre il numero di hello dei criteri è toodefine. Prima di procedere con le definizioni dei criteri, è necessario considerare se un criterio incorporato fornisce già definizione hello che è necessario. le definizioni dei criteri predefiniti di Hello sono:

* Percorsi consentiti
* Tipi di risorse consentiti
* SKU degli account di archiviazione consentiti
* SKU delle macchine virtuali consentiti
* Applicare il tag e il valore predefinito
* Applicare il tag e il valore
* Tipi di risorse non consentiti
* Richiedere SQL Server versione 12.0
* Richiedere la crittografia dell'account di archiviazione

È possibile assegnare uno di questi criteri tramite hello [portale](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), o [CLI di Azure](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Struttura delle definizioni di criteri
Utilizzare JSON toocreate una definizione dei criteri. definizione dei criteri Hello contiene elementi per:

* parameters
* nome visualizzato
* description
* regola dei criteri
  * valutazione logica
  * effetto

Hello di esempio seguente viene illustrato un criterio che limiti in cui vengono distribuite le risorse:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>parameters
Utilizzo di parametri consente di semplificare la gestione dei criteri, riducendo il numero di hello di definizioni dei criteri. Si definisce un criterio per una proprietà della risorsa (ad esempio limitando i percorsi di hello in cui le risorse possono essere distribuite) e includono i parametri nella definizione di hello. Quindi, riutilizzare tale definizione dei criteri per i diversi scenari passando valori diversi (ad esempio specificando un insieme di località per una sottoscrizione) quando l'assegnazione di criteri di hello.

I parametri vengono dichiarati quando si creano le definizioni dei criteri.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

tipo di Hello di un parametro può essere stringa o matrice. proprietà dei metadati Hello viene utilizzato per strumenti come informazioni descrittive toodisplay portale Azure. 

Nella regola dei criteri di hello, fare riferimento ai parametri con hello la seguente sintassi: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nome visualizzato e descrizione

Utilizzare hello **displayName** e **descrizione** tooidentify hello definizione dei criteri e forniscono un contesto per l'utilizzo.

## <a name="policy-rule"></a>Regola dei criteri

regola dei criteri di Hello costituita **se** e **quindi** blocchi. In hello **se** blocco, si definiscono una o più condizioni che specificano i criteri quando hello. È possibile applicare le condizioni di operatori logici toothese tooprecisely definire scenario hello per un criterio. In hello **quindi** blocco, è definire l'effetto di hello quando hello **se** condizioni sono soddisfatte.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Operatori logici
operatori logici Hello supportato sono:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Hello **non** sintassi inverte il risultato di hello della condizione di hello. Hello **tutto** sintassi (simile toohello logico **e** operazione) richiede tutte true toobe di condizioni. Hello **anyOf** sintassi (simile toohello logico **o** operazione) richiede uno o più true toobe condizioni.

È possibile annidare gli operatori logici. Hello seguente esempio viene illustrato un **non** operazione nidificato all'interno di un **tutto** operazione. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Condizioni
condizione Hello valuta se un **campo** soddisfa determinati criteri. le condizioni di Hello supportato sono:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Quando si utilizza hello **come** condizione, è possibile specificare un carattere jolly (*) nel valore hello.

Quando si utilizza hello **corrispondono** condizione, fornire `#` toorepresent una cifra, `?` per una lettera e qualsiasi altro carattere toorepresent tale carattere effettivo. Per gli esempi, vedere [Applicare criteri delle risorse per nomi e testo](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Fields
Le condizioni vengono formate usando i campi. Un campo rappresenta le proprietà nel payload di richiesta di risorsa hello ovvero toodescribe utilizzati hello stato della risorsa hello.  

è supportato i seguenti campi Hello:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* alias delle proprietà; per un elenco, vedere [alias](#aliases).

### <a name="effect"></a>Effetto
Il criterio supporta tre tipi di effetto: `deny`, `audit` e `append`. 

* **Negare** genera un evento nel Registro di controllo hello e si verifica un errore di richiesta di hello
* **Controllo** genera un evento di avviso nel Registro di controllo ma non viene interrotta richiesta hello
* **Aggiungere** aggiunge hello definito set di campi toohello richiesta 

Per **aggiungere**, è necessario fornire hello seguenti dettagli:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

il valore di Hello può essere una stringa o un oggetto formato JSON. 

## <a name="aliases"></a>Alias

Utilizzare gli alias tooaccess specifici delle proprietà per un tipo di risorsa. Gli alias consentono di toorestrict quali i valori consentiti per una proprietà su una risorsa. Ogni alias esegue il mapping toopaths in versioni diverse di API per un tipo di risorsa specificato. Durante la valutazione dei criteri, il motore dei criteri di hello Ottiene percorso della proprietà hello per la versione API.

**Microsoft.Cache/Redis**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Impostato se la porta server Redis non ssl di hello (6379) è abilitato. |
| Microsoft.Cache/Redis/shardCount | Impostare il numero di hello di partizioni toobe creato in una Cache di Cluster Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Impostare dimensioni hello del hello Redis cache toodeploy.  |
| Microsoft.Cache/Redis/sku.family | Impostare toouse famiglia di SKU hello. |
| Microsoft.Cache/Redis/sku.name | Impostare il tipo di hello di Cache Redis toodeploy. |

**Microsoft.Cdn/profiles**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Impostare il nome di hello del livello di prezzo hello. |

**Microsoft.Compute/disks**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine. |


**Microsoft.Compute/virtualMachines**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Compute/imageId | Impostare l'identificatore hello della macchina virtuale di hello immagine usata toocreate hello. |
| Microsoft.Compute/imageOffer | Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/licenseType | Impostare l'immagine di hello o su disco è concesso in licenza in locale. Questo valore viene utilizzato solo per le immagini che contengono hello del sistema operativo di Windows Server.  |
| Microsoft.Compute/virtualMachines/imageOffer | Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imagePublisher | Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imageSku | Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imageVersion | Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Impostare hello vhd URI. |
| Microsoft.Compute/virtualMachines/sku.name | Impostare dimensioni hello della macchina virtuale hello. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Impostare il nome di hello del server di pubblicazione dell'estensione hello. |
| Microsoft.Compute/virtualMachines/extensions/type | Impostare il tipo di hello di estensione. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Impostare la versione di hello dell'estensione hello. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Compute/imageId | Impostare l'identificatore hello della macchina virtuale di hello immagine usata toocreate hello. |
| Microsoft.Compute/imageOffer | Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine. |
| Microsoft.Compute/licenseType | Impostare l'immagine di hello o su disco è concesso in licenza in locale. Questo valore viene utilizzato solo per le immagini che contengono hello del sistema operativo di Windows Server. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Impostare prefisso del nome di computer per tutte le macchine virtuali hello hello in set di scalabilità hello. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Impostare l'URI del blob hello per l'immagine utente. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Impostare gli URL del contenitore hello che vengono utilizzati toostore dischi del sistema operativo per il set di scalabilità di hello. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Impostare dimensioni hello delle macchine virtuali in un set di scalabilità. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Impostare il livello di hello di macchine virtuali in un set di scalabilità. |
  
**Microsoft.Network/applicationGateways**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Impostare dimensioni hello del gateway hello. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Impostare il tipo di hello del gateway di rete virtuale. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Nome SKU di gateway hello del set. |

**Microsoft.Sql/servers**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Impostare la versione hello del server di hello. |

**Microsoft.Sql/databases**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Impostare hello edition del database hello. |
| Microsoft.Sql/servers/databases/elasticPoolName | Nome hello del set di database di hello hello pool elastico è in. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Set hello configurato ID obiettivo livello di servizio del database hello. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Impostare il nome di hello dell'obiettivo del livello di servizio configurato hello del database hello.  |

**Microsoft.Sql/elasticpools**

| Alias | Descrizione |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Totale hello set condivisa DTU per il pool elastico di hello database. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Impostare edition hello del pool elastico hello. |

**Microsoft.Storage/storageAccounts**

| Alias | Descrizione |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Livello di accesso hello set utilizzato per la fatturazione. |
| Microsoft.Storage/storageAccounts/accountType | Impostare il nome SKU hello. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Specificare se il servizio hello crittografa i dati di hello archiviato nel servizio di archiviazione blob di hello. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Specificare se il servizio hello crittografa i dati di hello archiviato nel servizio di archiviazione di file hello. |
| Microsoft.Storage/storageAccounts/sku.name | Impostare il nome SKU hello. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Impostare tooallow solo https servizio toostorage del traffico. |


## <a name="policy-examples"></a>Esempi di criteri

Hello seguenti argomenti contenga esempi di criteri:

* Per gli esempi di criteri di tag, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).
* Per alcuni esempi di modelli di denominazione e di testo, vedere [Apply resource policies for names and text](resource-manager-policy-naming-convention.md) (Applicare criteri di risorse per nomi e testo).
* Per esempi di criteri di archiviazione, vedere [si applicano agli account delle risorse criteri toostorage](resource-manager-policy-storage.md).
* Per esempi di criteri di macchina virtuale, vedere [applicare i criteri di risorse tooLinux macchine virtuali](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [applicare i criteri di risorse tooWindows macchine virtuali](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Passaggi successivi
* Dopo aver definito una regola dei criteri, assegnare tooa ambito. criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md). criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).
* schema dei criteri di Hello è pubblicato nella [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

