---
title: Segreto dell'insieme di credenziali delle chiavi con il modello di Resource Manager | Microsoft Docs
description: Viene illustrato come passare una chiave privata da un insieme di credenziali chiave come parametro durante la distribuzione.
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
ms.openlocfilehash: 1ca72599e67e79d42a3d430dbb13e89ea7265334
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="76b76-103">Usare Key Vault per passare un valore del parametro protetto durante la distribuzione</span><span class="sxs-lookup"><span data-stu-id="76b76-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="76b76-104">Quando è necessario passare un valore protetto (ad esempio una password) come parametro durante la distribuzione, è possibile recuperare il valore da [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76b76-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="76b76-105">Il valore viene recuperato facendo riferimento all'insieme di credenziali delle chiavi e alla chiave privata nel file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="76b76-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="76b76-106">Il valore non viene mai esposto, in quanto si fa riferimento solo all'ID dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="76b76-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="76b76-107">Non è necessario immettere manualmente il valore segreto ogni volta che si distribuisce le risorse.</span><span class="sxs-lookup"><span data-stu-id="76b76-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="76b76-108">L'insieme di credenziali delle chiavi può essere presente in una sottoscrizione diversa rispetto al gruppo di risorse in cui si sta eseguendo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="76b76-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="76b76-109">Quando si fa riferimento all'insieme di credenziali delle chiavi, includere l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="76b76-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="76b76-110">Quando di crea l'insieme di credenziali delle chiavi, impostare la proprietà *enabledForTemplateDeployment* su *true*.</span><span class="sxs-lookup"><span data-stu-id="76b76-110">When creating the key vault, set the *enabledForTemplateDeployment* property to *true*.</span></span> <span data-ttu-id="76b76-111">Impostando questo valore su true, si consente l'accesso dai modelli di Resource Manager durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="76b76-111">By setting this value to true, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="76b76-112">Distribuire un insieme di credenziali chiave e una chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b76-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="76b76-113">Per creare un insieme di credenziali delle chiavi e un segreto, usare l'interfaccia della riga di comando di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76b76-113">To create a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="76b76-114">Si noti che l'insieme di credenziali delle chiavi viene abilitato per la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="76b76-114">Notice that the key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="76b76-115">Per l'interfaccia della riga di comando di Azure usare:</span><span class="sxs-lookup"><span data-stu-id="76b76-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="76b76-116">Per PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="76b76-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="76b76-117">Abilitare l'accesso alla chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b76-117">Enable access to the secret</span></span>

<span data-ttu-id="76b76-118">Indipendentemente dal fatto che si usi un insieme di credenziali delle chiavi nuovo o già esistente, assicurarsi che l'utente che distribuisce il modello possa accedere alla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b76-118">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="76b76-119">L'utente che distribuisce un modello che fa riferimento a una chiave privata deve disporre dell'autorizzazione `Microsoft.KeyVault/vaults/deploy/action` per l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76b76-119">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="76b76-120">Entrambi i ruoli [Proprietario](../active-directory/role-based-access-built-in-roles.md#owner) e [Collaboratore](../active-directory/role-based-access-built-in-roles.md#contributor) possono concedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="76b76-120">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="76b76-121">È inoltre possibile creare un [ruolo personalizzato](../active-directory/role-based-access-control-custom-roles.md) che conceda l'autorizzazione e aggiunga l'utente a questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="76b76-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="76b76-122">Per informazioni sull'aggiunta di un utente a un ruolo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="76b76-122">For information about adding a user to a role, see [Assign a user to administrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="76b76-123">Fare riferimento a un segreto con un ID statico</span><span class="sxs-lookup"><span data-stu-id="76b76-123">Reference a secret with static ID</span></span>

<span data-ttu-id="76b76-124">Il modello che riceve un segreto dell'insieme di credenziali delle chiavi è come qualsiasi altro modello.</span><span class="sxs-lookup"><span data-stu-id="76b76-124">The template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="76b76-125">Infatti **si fa riferimento all'insieme di credenziali delle chiavi nel file dei parametri, non nel modello**.</span><span class="sxs-lookup"><span data-stu-id="76b76-125">That's because **you reference the key vault in the parameter file, not the template.**</span></span> <span data-ttu-id="76b76-126">Il modello seguente, ad esempio, distribuisce un database SQL che include una password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="76b76-126">For example, the following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="76b76-127">Il parametro della password è impostato su una stringa sicura,</span><span class="sxs-lookup"><span data-stu-id="76b76-127">The password parameter is set to a secure string.</span></span> <span data-ttu-id="76b76-128">ma il modello non specifica la provenienza di tale valore.</span><span class="sxs-lookup"><span data-stu-id="76b76-128">But, the template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="76b76-129">Creare ora un file dei parametri per il modello precedente.</span><span class="sxs-lookup"><span data-stu-id="76b76-129">Now, create a parameter file for the preceding template.</span></span> <span data-ttu-id="76b76-130">Nel file dei parametri specificare un parametro corrispondente al nome del parametro nel modello.</span><span class="sxs-lookup"><span data-stu-id="76b76-130">In the parameter file, specify a parameter that matches the name of the parameter in the template.</span></span> <span data-ttu-id="76b76-131">Per il valore del parametro, fare riferimento al segreto dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76b76-131">For the parameter value, reference the secret from the key vault.</span></span> <span data-ttu-id="76b76-132">Si fa riferimento alla chiave privata passando l'identificatore della risorsa dell'insieme di credenziali chiave e il nome della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b76-132">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="76b76-133">Nell'esempio seguente il segreto dell'insieme di credenziali delle chiavi deve esistere già e si deve fornire un valore statico per il relativo ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="76b76-133">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="76b76-134">Fare riferimento a un segreto con un ID dinamico</span><span class="sxs-lookup"><span data-stu-id="76b76-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="76b76-135">La sezione precedente ha illustrato come passare un ID risorsa statico per il segreto dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="76b76-135">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="76b76-136">In alcuni scenari, tuttavia, è necessario fare riferimento a un segreto dell'insieme di credenziali delle chiavi che varia a seconda della distribuzione corrente.</span><span class="sxs-lookup"><span data-stu-id="76b76-136">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="76b76-137">In questo caso non è possibile impostare come hardcoded l'ID risorsa nel file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="76b76-137">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="76b76-138">Non è sfortunatamente possibile generare in modo dinamico l'ID risorsa nel file dei parametri, perché le espressioni del modello non sono consentite nel file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="76b76-138">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="76b76-139">Per generare in modo dinamico l'ID risorsa per un segreto dell'insieme di credenziali delle chiavi, è necessario spostare la risorsa che necessita del segreto in un modello annidato.</span><span class="sxs-lookup"><span data-stu-id="76b76-139">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="76b76-140">Nel modello principale aggiungere il modello annidato e passare un parametro che include l'ID risorsa generato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="76b76-140">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="76b76-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76b76-141">Next steps</span></span>
* <span data-ttu-id="76b76-142">Per informazioni generali sugli insiemi di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76b76-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="76b76-143">Per esempi completi di segreti di riferimento alle chiavi private, vedere [Esempi di insiemi di credenziali chiave](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="76b76-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

