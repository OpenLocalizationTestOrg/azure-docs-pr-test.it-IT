---
title: aaaCreate e pubblicare un'applicazione di servizio di Azure gestito catalogo | Documenti Microsoft
description: Viene illustrato come toocreate di Azure gestiti applicazione che deve essere parte della propria organizzazione.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Pubblicare un'applicazione gestita per uso interno

È possibile creare e pubblicare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione. Un reparto IT può, ad esempio, pubblicare applicazioni gestite che garantiscano la conformità agli standard aziendali. Queste applicazioni gestite sono disponibili tramite catalogo servizi hello, non hello Azure Marketplace.

un'applicazione gestita per il catalogo di servizi di hello toopublish, è necessario:

* Creare un pacchetto con estensione zip che contiene tre file di modello richiesti hello.
* Decidere quale utente, gruppo o l'applicazione deve accedere a toohello gruppo di risorse nella sottoscrizione hello dell'utente.
* Creare una definizione dell'applicazione hello gestito che punta pacchetto con estensione zip toohello e richiede l'accesso per l'identità di hello.

## <a name="create-a-managed-application-package"></a>Creare un pacchetto dell'applicazione gestita

primo passaggio Hello è toocreate hello tre modello richiesto file. Tutti e tre i file del pacchetto in un file zip e caricarlo percorso accessibile tooan, ad esempio un account di archiviazione. Passare un file con estensione zip toothis di collegamento quando la creazione di hello gestiti definizione dell'applicazione.

* **applianceMainTemplate.json**: questo file definisce hello Azure le risorse che vengono effettuato il provisioning come parte di hello applicazione gestita. modello di Hello non è diversa rispetto a un modello di gestione risorse regolari. Ad esempio, un account di archiviazione tramite un'applicazione gestita toocreate, applianceMainTemplate.json contiene:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: gli utenti di distribuire questo modello quando la creazione di hello applicazione gestita. Definisce una risorsa dell'applicazione hello gestito, ovvero un tipo di risorsa Microsoft.Solutions/appliances. Questo file contiene tutti i parametri di hello che è necessario per le risorse di hello applianceMainTemplate.json.

  In questo modello si impostano due proprietà importanti. In primo luogo, hello **applianceDefinitionId** proprietà è ID hello hello gestito dalla definizione dell'applicazione. Creare la definizione di hello più avanti in questo argomento. Quando si imposta questo valore, è necessario decidere quali sottoscrizioni e toouse gruppo di risorse per l'archiviazione hello definizioni delle applicazioni gestite. E, è necessario scegliere un nome per la definizione di hello. ID Hello è nel formato di hello:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  In secondo luogo, hello **managedResourceGroupId** proprietà è ID hello hello del gruppo di risorse in cui hello Azure le risorse vengono create. È possibile assegnare un valore per il nome di questo gruppo di risorse o consentire all'utente di hello consente di specificare un nome. l'ID hello formato hello è:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Hello di esempio seguente viene illustrato un file mainTemplate.json. Specifica un gruppo di risorse per le risorse di hello distribuito. ID definizione Hello è toouse set denominata di una definizione di **storageApp** in un gruppo di risorse denominato **managedApplicationGroup**. È possibile modificare questi nomi di valori toouse diversi. Fornire il proprio ID sottoscrizione in hello ID di definizione.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: hello portale di Azure utilizza questo file toogenerate hello interfaccia utente per gli utenti che creano hello applicazione gestita. È possibile definire la modalità con cui gli utenti inseriscono l'input per ogni parametro. È possibile usare opzioni come un elenco a discesa, una casella di testo, una casella per la password e altri strumenti di input. toolearn toocreate un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Hello esempio seguente viene illustrato un file applianceCreateUiDefinition.json che consente agli utenti toospecify hello archiviazione account prefisso del nome e una casella di testo.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

Una volta pronti tutti i file hello necessita, inserirle in un pacchetto come file con estensione zip. Hello tre file dovranno essere a livello di radice hello del file con estensione zip hello. Se li si inserisce in una cartella, viene visualizzato un errore quando la creazione di hello gestiti definizione dell'applicazione che dichiara hello necessari file non sono presenti. Caricare hello tooan accessibile percorso del pacchetto da dove possono essere utilizzato. resto Hello di questo articolo si presuppone file con estensione zip hello in un contenitore di blob di archiviazione accessibile pubblicamente.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Creare un'applicazione o un gruppo di utenti Azure Active Directory

secondo passaggio Hello è tooselect un gruppo di utenti o un'applicazione per la gestione delle risorse di hello per conto cliente hello. Il gruppo di utenti o l'applicazione dispone di autorizzazioni hello risorsa gestita gruppo secondo toohello ruolo assegnato. ruolo di Hello può essere qualsiasi ruolo di controllo di accesso basato sui ruoli (RBAC) incorporato come proprietario o collaboratore. È anche possibile fornire un singolo utente autorizzazione toomanage hello di risorse, ma in genere è assegnare questo gruppo di utenti tooa di autorizzazione. toocreate un nuovo gruppo di utenti di Active Directory, vedere [creare un gruppo e aggiungere membri in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

ID di oggetto hello di hello utente gruppo toouse è necessario per la gestione delle risorse di hello. Hello di esempio seguente viene illustrato come tooget hello ID di oggetto dal nome visualizzato del gruppo di hello:

```azurecli-interactive
az ad group show --group exampleGroupName
```

comando di esempio Hello restituisce hello seguente output:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

ID di oggetto hello solo tooretrieve, utilizzare:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Ottenere l'ID di definizione del ruolo hello

Successivamente, è necessario l'ID di definizione di ruolo hello di hello ruolo incorporato e RBAC desiderato toogrant accesso toohello utente, gruppo di utenti o applicazioni. In genere, si usa hello proprietario o ruolo di collaboratore o lettore. Hello comando seguente viene illustrato come tooget hello ID di definizione del ruolo per il ruolo di proprietario hello:


```azurecli-interactive
az role definition list --name owner
```

Tale comando restituisce hello seguente output:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

È necessario il valore di hello della proprietà "name" hello hello sopra riportato. È possibile recuperare solo tale proprietà con:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Creare la definizione di applicazione hello gestito

Se non si dispone già di un gruppo di risorse per archiviare la definizione di applicazione gestita, crearne uno ora:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Questo punto, creare una risorsa di definizione dell'applicazione hello gestito.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

parametri di Hello utilizzati nel precedente esempio hello sono:

* **gruppo di risorse**: hello nome del gruppo di risorse hello definizione di applicazione gestita da hello in cui viene creato.
* **a livello di blocco**: tipo hello di blocco inserita nel gruppo di risorse gestite hello. Cliente hello impedisce operazioni indesiderati in questo gruppo di risorse. Attualmente, ReadOnly è hello è supportato solo il livello di blocco. Quando viene specificato ReadOnly, cliente hello può leggere solo risorse hello presenti nel gruppo di risorse gestite hello.
* **autorizzazioni**: descrive ID entità hello e ID di definizione del ruolo hello che appartengono al gruppo di risorse gestite toohello autorizzazione toogrant utilizzato. È specificato nel formato hello `<principalId>:<roleDefinitionId>`. Per questa proprietà si possono specificare anche altri valori. Se sono necessari più valori, deve essere specificati nel modulo hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. I valori multipli sono separati da uno spazio.
* **uri di file di pacchetto**: hello posizione del pacchetto di applicazione gestita hello che contiene i file di modello hello, che possono essere un blob di archiviazione di Azure.

## <a name="next-steps"></a>Passaggi successivi

* Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).
* Per esempi di file hello, vedere [gestiti esempi di applicazioni](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).
* Per informazioni sulla pubblicazione applicazioni gestite toohello Azure Marketplace, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).
* Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).
* toolearn toocreate un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
