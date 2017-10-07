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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="f4c11-103">Utilizzare valore di parametro secure toopass insieme di credenziali chiave durante la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f4c11-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="f4c11-104">Quando è necessario un valore sicuro (ad esempio una password) toopass come parametro durante la distribuzione, è possibile recuperare il valore di hello da un [insieme credenziali chiavi Azure](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4c11-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="f4c11-105">Per recuperare il valore di hello facendo riferimento a insieme di credenziali chiave hello e il segreto nel file di parametro.</span><span class="sxs-lookup"><span data-stu-id="f4c11-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="f4c11-106">il valore di Hello non viene mai esposta in quanto si fa riferimento solo al relativo ID insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f4c11-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="f4c11-107">Non è necessario toomanually immettere il valore di hello per segreto hello ogni volta che si distribuisce risorse hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="f4c11-108">insieme di credenziali chiave Hello può essere presente in una sottoscrizione diversa rispetto a gruppo di risorse hello che a cui si sta distribuendo.</span><span class="sxs-lookup"><span data-stu-id="f4c11-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="f4c11-109">Quando si fa riferimento a insieme di credenziali chiave di hello, includere hello ID di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f4c11-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="f4c11-110">Quando si crea l'insieme di credenziali chiave di hello, impostare hello *enabledForTemplateDeployment* proprietà troppo*true*.</span><span class="sxs-lookup"><span data-stu-id="f4c11-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="f4c11-111">Impostando questo valore tootrue, è consentire l'accesso dai modelli di gestione delle risorse durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f4c11-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="f4c11-112">Distribuire un insieme di credenziali chiave e una chiave privata</span><span class="sxs-lookup"><span data-stu-id="f4c11-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="f4c11-113">toocreate un insieme di credenziali chiave e il segreto, utilizzare CLI di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4c11-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="f4c11-114">Si noti che insieme di credenziali chiave di hello è abilitata per la distribuzione dei modelli.</span><span class="sxs-lookup"><span data-stu-id="f4c11-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="f4c11-115">Per l'interfaccia della riga di comando di Azure usare:</span><span class="sxs-lookup"><span data-stu-id="f4c11-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="f4c11-116">Per PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="f4c11-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="f4c11-117">Abilitare il segreto toohello accesso</span><span class="sxs-lookup"><span data-stu-id="f4c11-117">Enable access toohello secret</span></span>

<span data-ttu-id="f4c11-118">Se si utilizza un insieme di credenziali chiave nuova o esistente, verificare che hello distribuzione modello hello consente l'accesso segreto hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="f4c11-119">distribuzione di un modello che fa riferimento a una chiave privata utente di Hello deve avere hello `Microsoft.KeyVault/vaults/deploy/action` l'autorizzazione per l'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="f4c11-120">Hello [proprietario](../active-directory/role-based-access-built-in-roles.md#owner) e [collaboratore](../active-directory/role-based-access-built-in-roles.md#contributor) entrambi i ruoli di concedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f4c11-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="f4c11-121">È inoltre possibile creare un [ruolo personalizzato](../active-directory/role-based-access-control-custom-roles.md) che concede l'autorizzazione e aggiungere hello utente toothat ruolo.</span><span class="sxs-lookup"><span data-stu-id="f4c11-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="f4c11-122">Per informazioni sull'aggiunta di un ruolo di utente tooa, vedere [assegnare un utente tooadministrator ruoli in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4c11-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="f4c11-123">Fare riferimento a un segreto con un ID statico</span><span class="sxs-lookup"><span data-stu-id="f4c11-123">Reference a secret with static ID</span></span>

<span data-ttu-id="f4c11-124">modello di Hello che riceve un segreto dell'insieme di credenziali chiave è come qualsiasi altro modello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="f4c11-125">Ciò accade perché **hello chiave dell'insieme di credenziali nel file di parametro hello, modello di hello non si fa riferimento.**</span><span class="sxs-lookup"><span data-stu-id="f4c11-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="f4c11-126">Ad esempio, hello seguente modello consente di distribuire un database SQL che include una password di amministratore.</span><span class="sxs-lookup"><span data-stu-id="f4c11-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="f4c11-127">il parametro password Hello è impostato la stringa sicura tooa.</span><span class="sxs-lookup"><span data-stu-id="f4c11-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="f4c11-128">Tuttavia, modello hello non specifica la provenienza di tale valore.</span><span class="sxs-lookup"><span data-stu-id="f4c11-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="f4c11-129">A questo punto, creare un file di parametro per hello modello precedente.</span><span class="sxs-lookup"><span data-stu-id="f4c11-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="f4c11-130">Nel file di parametro hello, specificare un parametro che corrisponde al nome del parametro hello nel modello hello hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="f4c11-131">Valore del parametro hello, fare riferimento a hello segreto dall'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="f4c11-132">Fare riferimento a segreto hello passando l'identificatore di risorsa hello dell'insieme di credenziali chiave hello e il nome di hello del segreto hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="f4c11-133">Nell'esempio seguente di hello, segreto dell'insieme di credenziali chiave hello deve esistere e fornire un valore statico per l'ID di risorsa.</span><span class="sxs-lookup"><span data-stu-id="f4c11-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="f4c11-134">Fare riferimento a un segreto con un ID dinamico</span><span class="sxs-lookup"><span data-stu-id="f4c11-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="f4c11-135">la sezione precedente di Hello è stato illustrato come toopass un ID di risorsa statica per la chiave di hello archivio segreto.</span><span class="sxs-lookup"><span data-stu-id="f4c11-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="f4c11-136">Tuttavia, in alcuni scenari, è necessario un segreto dell'insieme di credenziali chiave che varia in base a una distribuzione corrente di hello tooreference.</span><span class="sxs-lookup"><span data-stu-id="f4c11-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="f4c11-137">In tal caso, non è possibile codificare hello ID di risorsa nel file dei parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="f4c11-138">Purtroppo, è possibile generare in modo dinamico hello ID di risorsa nel file dei parametri hello poiché le espressioni del modello non sono consentite nel file dei parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="f4c11-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="f4c11-139">toodynamically generare ID di risorsa hello per un segreto dell'insieme di credenziali chiave, è necessario spostare le risorse hello necessarie segreto hello in un modello annidato.</span><span class="sxs-lookup"><span data-stu-id="f4c11-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="f4c11-140">Nel modello principale, aggiungere modelli annidati hello e passare un parametro che contiene l'ID di risorsa hello generato dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="f4c11-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f4c11-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4c11-141">Next steps</span></span>
* <span data-ttu-id="f4c11-142">Per informazioni generali sugli insiemi di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4c11-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="f4c11-143">Per esempi completi di segreti di riferimento alle chiavi private, vedere [Esempi di insiemi di credenziali chiave](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="f4c11-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

