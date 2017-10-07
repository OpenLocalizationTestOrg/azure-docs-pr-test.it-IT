---
title: il segreto dell'insieme di credenziali aaaKey con modello di gestione risorse | Documenti Microsoft
description: Viene illustrato come toopass un segreto da una chiave dell'insieme di credenziali come parametro durante la distribuzione.
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Utilizzare valore di parametro secure toopass insieme di credenziali chiave durante la distribuzione

Quando è necessario un valore sicuro (ad esempio una password) toopass come parametro durante la distribuzione, è possibile recuperare il valore di hello da un [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md). Per recuperare il valore di hello facendo riferimento a insieme di credenziali chiave hello e il segreto nel file di parametro. il valore di Hello non viene mai esposta in quanto si fa riferimento solo al relativo ID insieme di credenziali chiave. Non è necessario toomanually immettere il valore di hello per segreto hello ogni volta che si distribuisce risorse hello. insieme di credenziali chiave Hello può essere presente in una sottoscrizione diversa rispetto a gruppo di risorse hello che a cui si sta distribuendo. Quando si fa riferimento a insieme di credenziali chiave di hello, includere hello ID di sottoscrizione.

Quando si crea l'insieme di credenziali chiave di hello, impostare hello *enabledForTemplateDeployment* proprietà troppo*true*. Impostando questo valore tootrue, è consentire l'accesso dai modelli di gestione delle risorse durante la distribuzione.  

## <a name="deploy-a-key-vault-and-secret"></a>Distribuire un insieme di credenziali chiave e una chiave privata

toocreate un insieme di credenziali chiave e il segreto, utilizzare CLI di Azure o PowerShell. Si noti che insieme di credenziali chiave di hello è abilitata per la distribuzione dei modelli. 

Per l'interfaccia della riga di comando di Azure usare:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Per PowerShell, usare:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Abilitare il segreto toohello accesso

Se si utilizza un insieme di credenziali chiave nuova o esistente, verificare che hello distribuzione modello hello consente l'accesso segreto hello. distribuzione di un modello che fa riferimento a una chiave privata utente di Hello deve avere hello `Microsoft.KeyVault/vaults/deploy/action` l'autorizzazione per l'insieme di credenziali chiave hello. Hello [proprietario](../active-directory/role-based-access-built-in-roles.md#owner) e [collaboratore](../active-directory/role-based-access-built-in-roles.md#contributor) entrambi i ruoli di concedere l'accesso. È inoltre possibile creare un [ruolo personalizzato](../active-directory/role-based-access-control-custom-roles.md) che concede l'autorizzazione e aggiungere hello utente toothat ruolo. Per informazioni sull'aggiunta di un ruolo di utente tooa, vedere [assegnare un utente tooadministrator ruoli in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Fare riferimento a un segreto con un ID statico

modello di Hello che riceve un segreto dell'insieme di credenziali chiave è come qualsiasi altro modello. Ciò accade perché **hello chiave dell'insieme di credenziali nel file di parametro hello, modello di hello non si fa riferimento.** Ad esempio, hello seguente modello consente di distribuire un database SQL che include una password di amministratore. il parametro password Hello è impostato la stringa sicura tooa. Tuttavia, modello hello non specifica la provenienza di tale valore.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

A questo punto, creare un file di parametro per hello modello precedente. Nel file di parametro hello, specificare un parametro che corrisponde al nome del parametro hello nel modello hello hello. Valore del parametro hello, fare riferimento a hello segreto dall'insieme di credenziali chiave hello. Fare riferimento a segreto hello passando l'identificatore di risorsa hello dell'insieme di credenziali chiave hello e il nome di hello del segreto hello. Nell'esempio seguente di hello, segreto dell'insieme di credenziali chiave hello deve esistere e fornire un valore statico per l'ID di risorsa.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Fare riferimento a un segreto con un ID dinamico

la sezione precedente di Hello è stato illustrato come toopass un ID di risorsa statica per la chiave di hello archivio segreto. Tuttavia, in alcuni scenari, è necessario un segreto dell'insieme di credenziali chiave che varia in base a una distribuzione corrente di hello tooreference. In tal caso, non è possibile codificare hello ID di risorsa nel file dei parametri di hello. Purtroppo, è possibile generare in modo dinamico hello ID di risorsa nel file dei parametri hello poiché le espressioni del modello non sono consentite nel file dei parametri di hello.

toodynamically generare ID di risorsa hello per un segreto dell'insieme di credenziali chiave, è necessario spostare le risorse hello necessarie segreto hello in un modello annidato. Nel modello principale, aggiungere modelli annidati hello e passare un parametro che contiene l'ID di risorsa hello generato dinamicamente.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni generali sugli insiemi di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).
* Per esempi completi di segreti di riferimento alle chiavi private, vedere [Esempi di insiemi di credenziali chiave](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

