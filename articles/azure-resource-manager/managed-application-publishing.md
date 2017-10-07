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
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="e020c-103">Pubblicare un'applicazione gestita per uso interno</span><span class="sxs-lookup"><span data-stu-id="e020c-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="e020c-104">È possibile creare e pubblicare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e020c-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="e020c-105">Un reparto IT può, ad esempio, pubblicare applicazioni gestite che garantiscano la conformità agli standard aziendali.</span><span class="sxs-lookup"><span data-stu-id="e020c-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="e020c-106">Queste applicazioni gestite sono disponibili tramite catalogo servizi hello, non hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e020c-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="e020c-107">un'applicazione gestita per il catalogo di servizi di hello toopublish, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e020c-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="e020c-108">Creare un pacchetto con estensione zip che contiene tre file di modello richiesti hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="e020c-109">Decidere quale utente, gruppo o l'applicazione deve accedere a toohello gruppo di risorse nella sottoscrizione hello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e020c-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="e020c-110">Creare una definizione dell'applicazione hello gestito che punta pacchetto con estensione zip toohello e richiede l'accesso per l'identità di hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="e020c-111">Creare un pacchetto dell'applicazione gestita</span><span class="sxs-lookup"><span data-stu-id="e020c-111">Create a managed application package</span></span>

<span data-ttu-id="e020c-112">primo passaggio Hello è toocreate hello tre modello richiesto file.</span><span class="sxs-lookup"><span data-stu-id="e020c-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="e020c-113">Tutti e tre i file del pacchetto in un file zip e caricarlo percorso accessibile tooan, ad esempio un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e020c-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="e020c-114">Passare un file con estensione zip toothis di collegamento quando la creazione di hello gestiti definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e020c-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="e020c-115">**applianceMainTemplate.json**: questo file definisce hello Azure le risorse che vengono effettuato il provisioning come parte di hello applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="e020c-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="e020c-116">modello di Hello non è diversa rispetto a un modello di gestione risorse regolari.</span><span class="sxs-lookup"><span data-stu-id="e020c-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="e020c-117">Ad esempio, un account di archiviazione tramite un'applicazione gestita toocreate, applianceMainTemplate.json contiene:</span><span class="sxs-lookup"><span data-stu-id="e020c-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="e020c-118">**mainTemplate.json**: gli utenti di distribuire questo modello quando la creazione di hello applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="e020c-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="e020c-119">Definisce una risorsa dell'applicazione hello gestito, ovvero un tipo di risorsa Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="e020c-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="e020c-120">Questo file contiene tutti i parametri di hello che è necessario per le risorse di hello applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="e020c-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="e020c-121">In questo modello si impostano due proprietà importanti.</span><span class="sxs-lookup"><span data-stu-id="e020c-121">You set two important properties in this template.</span></span> <span data-ttu-id="e020c-122">In primo luogo, hello **applianceDefinitionId** proprietà è ID hello hello gestito dalla definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e020c-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="e020c-123">Creare la definizione di hello più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="e020c-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="e020c-124">Quando si imposta questo valore, è necessario decidere quali sottoscrizioni e toouse gruppo di risorse per l'archiviazione hello definizioni delle applicazioni gestite.</span><span class="sxs-lookup"><span data-stu-id="e020c-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="e020c-125">E, è necessario scegliere un nome per la definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="e020c-126">ID Hello è nel formato di hello:</span><span class="sxs-lookup"><span data-stu-id="e020c-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="e020c-127">In secondo luogo, hello **managedResourceGroupId** proprietà è ID hello hello del gruppo di risorse in cui hello Azure le risorse vengono create.</span><span class="sxs-lookup"><span data-stu-id="e020c-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="e020c-128">È possibile assegnare un valore per il nome di questo gruppo di risorse o consentire all'utente di hello consente di specificare un nome.</span><span class="sxs-lookup"><span data-stu-id="e020c-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="e020c-129">l'ID hello formato hello è:</span><span class="sxs-lookup"><span data-stu-id="e020c-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="e020c-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="e020c-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="e020c-131">Hello di esempio seguente viene illustrato un file mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="e020c-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="e020c-132">Specifica un gruppo di risorse per le risorse di hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="e020c-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="e020c-133">ID definizione Hello è toouse set denominata di una definizione di **storageApp** in un gruppo di risorse denominato **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="e020c-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="e020c-134">È possibile modificare questi nomi di valori toouse diversi.</span><span class="sxs-lookup"><span data-stu-id="e020c-134">You can change these values toouse different names.</span></span> <span data-ttu-id="e020c-135">Fornire il proprio ID sottoscrizione in hello ID di definizione.</span><span class="sxs-lookup"><span data-stu-id="e020c-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="e020c-136">**applianceCreateUiDefinition.json**: hello portale di Azure utilizza questo file toogenerate hello interfaccia utente per gli utenti che creano hello applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="e020c-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="e020c-137">È possibile definire la modalità con cui gli utenti inseriscono l'input per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="e020c-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="e020c-138">È possibile usare opzioni come un elenco a discesa, una casella di testo, una casella per la password e altri strumenti di input.</span><span class="sxs-lookup"><span data-stu-id="e020c-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="e020c-139">toolearn toocreate un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="e020c-140">Hello esempio seguente viene illustrato un file applianceCreateUiDefinition.json che consente agli utenti toospecify hello archiviazione account prefisso del nome e una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e020c-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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

<span data-ttu-id="e020c-141">Una volta pronti tutti i file hello necessita, inserirle in un pacchetto come file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="e020c-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="e020c-142">Hello tre file dovranno essere a livello di radice hello del file con estensione zip hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="e020c-143">Se li si inserisce in una cartella, viene visualizzato un errore quando la creazione di hello gestiti definizione dell'applicazione che dichiara hello necessari file non sono presenti.</span><span class="sxs-lookup"><span data-stu-id="e020c-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="e020c-144">Caricare hello tooan accessibile percorso del pacchetto da dove possono essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e020c-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="e020c-145">resto Hello di questo articolo si presuppone file con estensione zip hello in un contenitore di blob di archiviazione accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="e020c-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="e020c-146">Creare un'applicazione o un gruppo di utenti Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e020c-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="e020c-147">secondo passaggio Hello è tooselect un gruppo di utenti o un'applicazione per la gestione delle risorse di hello per conto cliente hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="e020c-148">Il gruppo di utenti o l'applicazione dispone di autorizzazioni hello risorsa gestita gruppo secondo toohello ruolo assegnato.</span><span class="sxs-lookup"><span data-stu-id="e020c-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="e020c-149">ruolo di Hello può essere qualsiasi ruolo di controllo di accesso basato sui ruoli (RBAC) incorporato come proprietario o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="e020c-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="e020c-150">È anche possibile fornire un singolo utente autorizzazione toomanage hello di risorse, ma in genere è assegnare questo gruppo di utenti tooa di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e020c-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="e020c-151">toocreate un nuovo gruppo di utenti di Active Directory, vedere [creare un gruppo e aggiungere membri in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="e020c-152">ID di oggetto hello di hello utente gruppo toouse è necessario per la gestione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="e020c-153">Hello di esempio seguente viene illustrato come tooget hello ID di oggetto dal nome visualizzato del gruppo di hello:</span><span class="sxs-lookup"><span data-stu-id="e020c-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="e020c-154">comando di esempio Hello restituisce hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="e020c-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="e020c-155">ID di oggetto hello solo tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="e020c-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="e020c-156">Ottenere l'ID di definizione del ruolo hello</span><span class="sxs-lookup"><span data-stu-id="e020c-156">Get hello role definition ID</span></span>

<span data-ttu-id="e020c-157">Successivamente, è necessario l'ID di definizione di ruolo hello di hello ruolo incorporato e RBAC desiderato toogrant accesso toohello utente, gruppo di utenti o applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e020c-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="e020c-158">In genere, si usa hello proprietario o ruolo di collaboratore o lettore.</span><span class="sxs-lookup"><span data-stu-id="e020c-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="e020c-159">Hello comando seguente viene illustrato come tooget hello ID di definizione del ruolo per il ruolo di proprietario hello:</span><span class="sxs-lookup"><span data-stu-id="e020c-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="e020c-160">Tale comando restituisce hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="e020c-160">That command returns hello following output:</span></span>

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

<span data-ttu-id="e020c-161">È necessario il valore di hello della proprietà "name" hello hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="e020c-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="e020c-162">È possibile recuperare solo tale proprietà con:</span><span class="sxs-lookup"><span data-stu-id="e020c-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="e020c-163">Creare la definizione di applicazione hello gestito</span><span class="sxs-lookup"><span data-stu-id="e020c-163">Create hello managed application definition</span></span>

<span data-ttu-id="e020c-164">Se non si dispone già di un gruppo di risorse per archiviare la definizione di applicazione gestita, crearne uno ora:</span><span class="sxs-lookup"><span data-stu-id="e020c-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="e020c-165">Questo punto, creare una risorsa di definizione dell'applicazione hello gestito.</span><span class="sxs-lookup"><span data-stu-id="e020c-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="e020c-166">parametri di Hello utilizzati nel precedente esempio hello sono:</span><span class="sxs-lookup"><span data-stu-id="e020c-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="e020c-167">**gruppo di risorse**: hello nome del gruppo di risorse hello definizione di applicazione gestita da hello in cui viene creato.</span><span class="sxs-lookup"><span data-stu-id="e020c-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="e020c-168">**a livello di blocco**: tipo hello di blocco inserita nel gruppo di risorse gestite hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="e020c-169">Cliente hello impedisce operazioni indesiderati in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e020c-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="e020c-170">Attualmente, ReadOnly è hello è supportato solo il livello di blocco.</span><span class="sxs-lookup"><span data-stu-id="e020c-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="e020c-171">Quando viene specificato ReadOnly, cliente hello può leggere solo risorse hello presenti nel gruppo di risorse gestite hello.</span><span class="sxs-lookup"><span data-stu-id="e020c-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="e020c-172">**autorizzazioni**: descrive ID entità hello e ID di definizione del ruolo hello che appartengono al gruppo di risorse gestite toohello autorizzazione toogrant utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e020c-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="e020c-173">È specificato nel formato hello `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="e020c-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="e020c-174">Per questa proprietà si possono specificare anche altri valori.</span><span class="sxs-lookup"><span data-stu-id="e020c-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="e020c-175">Se sono necessari più valori, deve essere specificati nel modulo hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="e020c-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="e020c-176">I valori multipli sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="e020c-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="e020c-177">**uri di file di pacchetto**: hello posizione del pacchetto di applicazione gestita hello che contiene i file di modello hello, che possono essere un blob di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e020c-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e020c-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e020c-178">Next steps</span></span>

* <span data-ttu-id="e020c-179">Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e020c-180">Per esempi di file hello, vedere [gestiti esempi di applicazioni](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="e020c-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="e020c-181">Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="e020c-182">Per informazioni sulla pubblicazione applicazioni gestite toohello Azure Marketplace, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="e020c-183">Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="e020c-184">toolearn toocreate un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e020c-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
