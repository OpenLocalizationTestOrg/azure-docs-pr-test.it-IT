---
title: gli errori di distribuzione di Azure comuni aaaTroubleshoot | Documenti Microsoft
description: Viene descritto come tooresolve errori comuni quando si distribuisce tooAzure risorse usando Gestione risorse di Azure.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Errore di distribuzione, distribuzione di azure, distribuire tooazure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager
Questo argomento illustra come risolvere alcuni errori comuni che possono verificarsi durante la distribuzione di risorse in Azure.

in questo argomento viene descritti i Hello codici di errore seguente:

* [AccountNameInvalid](#accountnameinvalid)
* [Authorization failed](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Questo codice di errore indica un errore di distribuzione generale, ma non è il codice di errore hello necessario toostart risoluzione dei problemi. codice di errore Hello effettivamente consente di risolvere il problema di hello è in genere un livello di sotto di questo errore. Ad esempio, hello seguente immagine Mostra hello **RequestDisallowedByPolicy** codice di errore che si trova sotto l'errore di distribuzione hello.

![mostra codice di errore](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Quando si distribuisce una risorsa (in genere una macchina virtuale), potrebbe essere visualizzato hello messaggio di errore e codice di errore seguente:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Viene visualizzato questo errore quando hello risorsa SKU selezionato (ad esempio, dimensioni della macchina virtuale) non è disponibile per il percorso di hello selezionato. tooresolve questo problema, è necessario toodetermine SKU disponibili in un'area. È possibile utilizzare PowerShell, portale hello o un toofind operazione REST SKU disponibile.

- Per PowerShell usare [Get AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtrare in base al percorso. È necessario disporre di hello più recente di PowerShell per questo comando.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  risultati di Hello includono un elenco di SKU per la posizione di hello ed eventuali restrizioni per tale SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- hello toouse [portal](https://portal.azure.com), accedi al portale toohello e aggiungere una risorsa tramite l'interfaccia di hello. Quando si impostano i valori hello, vedrai hello SKU disponibili per tale risorsa. Non è necessario distribuzione hello toocomplete.

    ![SKU disponibili](./media/resource-manager-common-deployment-errors/view-sku.png)

- toouse hello API REST per le macchine virtuali, inviare hello seguito richiesta:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Restituisce le SKU e le aree disponibili in hello seguente formato:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Se si è grado toofind uno SKU adatto in tale area o un'area alternativa che soddisfa le esigenze aziendali, inviare un [richiesta SKU](https://aka.ms/skurestriction) tooAzure supporto.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Se si riceve questo errore, si utilizza una sottoscrizione che non è consentito tooaccess tutti i servizi Azure diverso da Azure Active Directory. Questo tipo di sottoscrizione possono verificarsi quando è necessario portale classico di hello tooaccess ma non sono consentiti toodeploy risorse. tooresolve questo problema, è necessario utilizzare una sottoscrizione che dispone dell'autorizzazione toodeploy risorse.  

tooview le sottoscrizioni disponibili con PowerShell, usare:

```powershell
Get-AzureRmSubscription
```

Inoltre, tooset hello abbonamento, utilizzare:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview le sottoscrizioni disponibili con l'interfaccia CLI di Azure 2.0, usare:

```azurecli
az account list
```

Inoltre, tooset hello abbonamento, utilizzare:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Questo errore può essere causato da diversi tipi di errori.

- Errore di sintassi

   Se si riceve un messaggio di errore che indica di convalida del modello non è stato possibile hello, potrebbe essere un problema di sintassi nel modello.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Questo errore è facile toomake perché le espressioni del modello possono essere complesse. Ad esempio, hello seguente assegnazione del nome per un account di archiviazione contiene un set di parentesi, tre funzioni, tre set di parentesi, un set di virgolette singole e una proprietà:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Se non si fornisce la sintassi corrispondente hello, modello hello produce un valore diverso da quello l'intenzione.

   Quando si riceve questo tipo di errore, esaminare attentamente la sintassi dell'espressione hello. È consigliabile usare un editor JSON come [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) o [Visual Studio Code](resource-manager-vs-code.md) che può segnalare gli errori di sintassi.

- Lunghezze di segmenti non valide

   Un altro errore di modello non valido si verifica quando il nome di risorsa hello non è nel formato corretto hello.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Una risorsa di livello radice deve avere un segmento di meno nel nome hello nel tipo di risorsa hello. Ogni segmento si differenzia mediante una barra. Nell'esempio seguente di hello, sono presenti due segmenti di tipo hello e nome hello include un segmento, pertanto è un **valido**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Ma l'esempio successivo hello è **nome non valido** perché contiene hello stesso numero di segmenti di tipo hello.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Per le risorse figlio, necessario hello tipo hello e il nome stesso numero di segmenti. Questo numero di segmenti è utile perché il nome completo di hello e il tipo per l'elemento figlio di hello include hello padre nome e il tipo. Pertanto, nome completo di hello dispone ancora di una minore segmento di tipo completo hello.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Segmenti di hello recupero corretti possono risultare difficile con tipi di gestione risorse che vengono applicati ai provider di risorse. Ad esempio, l'applicazione di un sito web di risorsa lock tooa richiede un tipo con quattro segmenti. Pertanto, il nome di hello è tre segmenti:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Indice di copia non previsto

   Si verifica questo **InvalidTemplate** errore una volta applicata hello **copia** parte tooa elemento del modello di hello che non supporta questo elemento. È possibile applicare solo tipo di risorsa tooa hello Copia elemento. Non è possibile applicare proprietà tooa copia all'interno di un tipo di risorsa. Ad esempio, si applica una macchina virtuale tooa di copia, ma non è possibile applicare i dischi del sistema operativo toohello per una macchina virtuale. In alcuni casi, è possibile convertire un toocreate risorse figlio risorsa tooa padre un ciclo di copia. Per altre informazioni sull'uso di copy, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).

- Parametro non valido

   Se il modello hello specifica valori consentiti per un parametro e specificare un valore che non fa parte di tali valori, viene visualizzato un toohello simile messaggio errore seguente:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Hello verificare i valori consentiti nel modello hello e forniscono uno durante la distribuzione.

- È stata rilevata una dipendenza circolare

   Viene visualizzato questo errore quando risorse dipendono tra loro in modo che impedisce la distribuzione di hello avvio. A causa di una combinazione di interdipendenze, due o più risorse attendono altre risorse che sono a propria volta in attesa. Ad esempio, la risorsa 1 dipende dalla risorsa 3, la risorsa 2 dipende dalla risorsa 1 e la risorsa 3 dipende dalla risorsa 2. È in genere possibile risolvere questo problema rimuovendo le dipendenze non necessarie. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound and ResourceNotFound
Quando il modello include il nome di hello di una risorsa che non può essere risolti, viene visualizzato un errore simile a:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Se si sta tentando di hello toodeploy risorsa nel modello hello mancante, verificare se è necessario tooadd una dipendenza. Azure Resource Manager consente di ottimizzare la distribuzione creando risorse in parallelo, quando ciò è possibile. Se una risorsa deve essere distribuita dopo un'altra risorsa, è necessario hello toouse **dependsOn** hello di elemento del modello di toocreate una dipendenza da un'altra risorsa. Ad esempio, quando si distribuisce un'app web, deve esistere hello piano di servizio App. Se non è stato specificato hello web app dipende dal piano di servizio App hello, Gestione risorse crea entrambe le risorse hello contemporaneamente. Viene visualizzato un errore che informa che hello risorse piano di servizio App non viene trovata, perché non esiste ancora durante il tentativo di una proprietà nell'applicazione web hello tooset. Evitare questo errore impostando dipendenza hello in hello web app.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Per suggerimenti sulla risoluzione degli errori relativi alle dipendenze, vedere [Controllare la sequenza di distribuzione](#check-deployment-sequence).

È inoltre possibile visualizzare questo errore quando la risorsa hello esiste in un gruppo di risorse diverso da quello hello uno vengono distribuite negli. In tal caso, utilizzare hello [funzione resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello il nome completo della risorsa hello.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Se si tenta di hello toouse [riferimento](resource-group-template-functions-resource.md#reference) o [elenco chiavi del](resource-group-template-functions-resource.md#listkeys) funzioni con una risorsa che non possono essere risolti, viene visualizzato il seguente errore hello:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Cercare un'espressione che include hello **riferimento** (funzione). Verificare che i valori di parametro hello siano corretti.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Quando una risorsa è una risorsa di tooanother padre, risorsa padre hello deve esistere prima di creare la risorsa figlio hello. Se non esiste ancora, viene visualizzato il seguente errore hello:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

nome di Hello della risorsa figlio hello include il nome del padre hello. Ad esempio, un database SQL può essere definito come segue:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Tuttavia, se non si specifica una dipendenza sulla risorsa padre hello, risorsa figlio hello può ottenere distribuita prima padre hello. tooresolve questo errore, includere una dipendenza.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists and StorageAccountAlreadyTaken
Per gli account di archiviazione, è necessario fornire un nome per la risorsa hello che è univoco in Azure. Se non si specifica un nome univoco, verrà visualizzato un errore come il seguente:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

È possibile creare un nome univoco concatenando la convenzione di denominazione con risultato hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (funzione).

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Se si distribuisce un account di archiviazione con hello stesso nome di un account di archiviazione esistente nella sottoscrizione, ma fornire un percorso diverso, viene visualizzato un errore che indica che account di archiviazione hello già presente in un percorso diverso. Eliminare l'account di archiviazione esistente hello o fornire hello nello stesso percorso come hello account di archiviazione esistente.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Vedrai hello **AccountNameInvalid** errore durante il tentativo di toogive uno spazio di archiviazione account un nome che include caratteri non consentiti. I nomi degli account di archiviazione devono essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare solo numeri e lettere minuscole. Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funzione restituisce 13 caratteri. Se si concatena toohello un prefisso **uniqueString** provocare, fornire un prefisso di 11 caratteri o meno.

## <a name="badrequest"></a>RichiestaNonValida

Quando per una proprietà si specifica un valore non valido, può comparire lo stato BadRequest. Ad esempio, se si fornisce un valore SKU non corretto per un account di archiviazione, hello distribuzione non riesce. Esaminare i valori validi per la proprietà, toodetermine hello [API REST](/rest/api) per il tipo di risorsa hello si sta distribuendo.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound e MissingSubscriptionRegistration
Durante la distribuzione di risorse, è possibile ricevere hello seguente codice di errore e di messaggio:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

In alternativa, si potrebbe ricevere un messaggio analogo che indica:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Questi errori vengono visualizzati per uno di questi tre motivi:

1. provider di risorse Hello non è stato registrato per la sottoscrizione
2. Versione dell'API non è supportata per il tipo di risorsa hello
3. Percorso non è supportata per il tipo di risorsa hello

messaggio di errore Hello deve contenere suggerimenti per percorsi hello supportato e le versioni dell'API. È possibile modificare il modello tooone di hello valori consigliati. La maggior parte dei provider vengono registrati automaticamente da hello Azure interfaccia della riga di comando di portale o hello in uso, ma non tutte. Se non è stato utilizzato un provider di risorse specifico prima, si potrebbe essere necessario tooregister tale provider. È possibile ottenere altre informazioni sui provider di risorse tramite PowerShell o l'interfaccia della riga di comando di Azure.

**Portale**

È possibile vedere lo stato della registrazione hello e registrare uno spazio dei nomi del provider di risorse tramite il portale di hello.

1. Selezionare **Provider di risorse** per la propria sottoscrizione.

   ![selezionare i provider di risorse](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Esaminare hello elenco di provider di risorse e, se necessario, selezionare hello **registrare** provider di risorse hello tooregister collegamento di tipo hello che si sta tentando di toodeploy.

   ![Elenco di provider di risorse](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee lo stato di registrazione, utilizzare **Get AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister un provider, utilizzare **registro AzureRmResourceProvider** e specificare il nome di hello del provider di risorse hello desiderato tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

percorsi di tooget hello è supportato per un particolare tipo di risorsa, utilizzare:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

hello tooget supportate le versioni dell'API per un particolare tipo di risorsa, utilizzare:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Interfaccia della riga di comando di Azure**

toosee se il provider di hello è registrato, utilizzare hello `azure provider list` comando.

```azurecli
az provider list
```

tooregister un provider di risorse, utilizzare hello `azure provider register` comando e specificare hello *dello spazio dei nomi* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

percorsi supportato hello toosee e le versioni dell'API per un tipo di risorsa, utilizzare:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded e OperationNotAllowed
Alcuni problemi potrebbero verificarsi quando una distribuzione supera una quota specifica per un gruppo di risorse, le sottoscrizioni, gli account o per altri ambiti. Ad esempio, la sottoscrizione potrebbe essere configurato toolimit hello numero di core per un'area. Se si tenta di toodeploy una macchina virtuale con più core di hello consentito quantità, viene visualizzato un errore indicante hello è stato superato.
Per informazioni complete sulle quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).

tooexamine le quote della sottoscrizione per core, è possibile utilizzare hello `azure vm list-usage` comando hello CLI di Azure. per un account di prova è 4, Hello di esempio seguente viene illustrato tale quota di core hello:

```azurecli
az vm list-usage --location "South Central US"
```

Che restituisce:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Se si distribuisce un modello che crea più di quattro core nell'area Stati Uniti occidentali hello, viene visualizzato un errore simile a quello di distribuzione:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

O in PowerShell, è possibile utilizzare hello **Get AzureRmVMUsage** cmdlet.

```powershell
Get-AzureRmVMUsage
```

Che restituisce:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

In questi casi, si deve passare toohello portal e file un tooraise problema supporto la quota per area hello in cui si desidera toodeploy.

> [!NOTE]
> Tenere presente che per gruppi di risorse, la quota hello per le singole aree, non per l'intera sottoscrizione hello. Se è necessario toodeploy 30 core negli Stati Uniti occidentali, è necessario tooask per 30 core di gestione delle risorse negli Stati Uniti occidentali. Se è necessario toodeploy 30 core delle toowhich aree hello è disponibile, è necessario richiedere 30 core di gestione risorse in tutte le aree.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Quando si riceve il messaggio di errore hello:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Si è probabilmente tentato toolink tooa modello nidificato che non è disponibile. Verificare hello URI è fornito per il modello annidato hello. Se il modello di hello esiste in un account di archiviazione, assicurarsi che hello URI sia accessibile. Potrebbe essere necessario toopass un token di firma di accesso condiviso. Per altre informazioni, vedere [Uso di modelli collegati con Gestione risorse di Azure](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Viene visualizzato questo errore quando la sottoscrizione include un criterio che impedisce a un'azione che si sta tentando di tooperform durante la distribuzione di risorse. Nel messaggio di errore hello, cercare l'identificatore hello dei criteri.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

In **PowerShell**, fornire tale identificatore dei criteri come hello **Id** dettagli sui criteri hello bloccati distribuzione tooretrieve del parametro.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

In **CLI di Azure**, specificare il nome di hello della definizione di criteri hello:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Per ulteriori informazioni, vedere hello seguenti articoli:

- [Errore RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Usare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).

## <a name="authorization-failed"></a>L'autorizzazione non è riuscita
Si potrebbe ricevere un errore durante la distribuzione perché hello account o il tentativo di risorse hello toodeploy entità servizio non dispone di accesso tooperform tali azioni. Azure Active Directory consente o l'amministratore toocontrol le identità che possono accedere le risorse con un elevato livello di precisione. Ad esempio, se l'account viene assegnato il ruolo di lettore toohello, non sono in grado di toocreate risorse. In tal caso verrà visualizzato un messaggio di errore che indica che l'autorizzazione non è riuscita.

Per altre informazioni sul controllo degli accessi in base al ruolo, vedere [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Passaggi successivi
* toolearn sul controllo delle azioni, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).
* toolearn sugli errori di hello toodetermine azioni durante la distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
