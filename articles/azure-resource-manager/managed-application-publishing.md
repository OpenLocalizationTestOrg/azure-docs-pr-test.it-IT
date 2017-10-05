---
title: Creare e pubblicare un'applicazione gestita del catalogo dei servizi di Azure | Microsoft Docs
description: Questo articolo descrive come creare un'applicazione gestita di Azure studiata per i membri della propria organizzazione.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="73097-103">Pubblicare un'applicazione gestita per uso interno</span><span class="sxs-lookup"><span data-stu-id="73097-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="73097-104">È possibile creare e pubblicare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="73097-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="73097-105">Un reparto IT può, ad esempio, pubblicare applicazioni gestite che garantiscano la conformità agli standard aziendali.</span><span class="sxs-lookup"><span data-stu-id="73097-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="73097-106">Queste applicazioni gestite sono disponibili nel catalogo dei servizi, non in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="73097-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="73097-107">Per pubblicare un'applicazione gestita per il catalogo dei servizi, è necessario:</span><span class="sxs-lookup"><span data-stu-id="73097-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="73097-108">Creare un pacchetto con estensione zip contenente i tre file modello necessari.</span><span class="sxs-lookup"><span data-stu-id="73097-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="73097-109">Decidere quali utenti, gruppi o applicazioni devono accedere al gruppo di risorse nella sottoscrizione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="73097-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="73097-110">Creare la definizione di applicazione gestita che punta al pacchetto con estensione zip e richiede l'accesso per l'identità.</span><span class="sxs-lookup"><span data-stu-id="73097-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="73097-111">Creare un pacchetto dell'applicazione gestita</span><span class="sxs-lookup"><span data-stu-id="73097-111">Create a managed application package</span></span>

<span data-ttu-id="73097-112">Il primo passaggio consiste nel creare i tre file modello necessari.</span><span class="sxs-lookup"><span data-stu-id="73097-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="73097-113">Creare un pacchetto di tutti e tre i file in un file con estensione zip e caricarlo in una posizione accessibile, ad esempio un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73097-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="73097-114">Passare un collegamento al file con estensione zip quando si crea la definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="73097-115">**applianceMainTemplate.json**: questo file definisce le risorse di Azure di cui viene effettuato il provisioning nell'ambito dell'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="73097-116">Il modello non è diverso da un modello standard di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73097-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="73097-117">Per creare un account di archiviazione tramite un'applicazione gestita, ad esempio, il file applianceMainTemplate.json contiene:</span><span class="sxs-lookup"><span data-stu-id="73097-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="73097-118">**mainTemplate.json**: gli utenti distribuiscono questo modello durante la creazione dell'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="73097-119">Il modello definisce la risorsa di applicazione gestita, che è un tipo di risorsa Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="73097-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="73097-120">Questo file contiene tutti i parametri necessari per le risorse in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="73097-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="73097-121">In questo modello si impostano due proprietà importanti.</span><span class="sxs-lookup"><span data-stu-id="73097-121">You set two important properties in this template.</span></span> <span data-ttu-id="73097-122">La prima proprietà è **applianceDefinitionId** che rappresenta l'ID della definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="73097-123">La definizione verrà creata più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="73097-123">You create the definition later in this topic.</span></span> <span data-ttu-id="73097-124">Quando si imposta questo valore, è necessario decidere quale gruppo di risorse e sottoscrizione usare per archiviare le definizioni dell'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="73097-125">È inoltre necessario decidere un nome per la definizione.</span><span class="sxs-lookup"><span data-stu-id="73097-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="73097-126">L'ID è nel formato:</span><span class="sxs-lookup"><span data-stu-id="73097-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="73097-127">La seconda proprietà è **managedResourceGroupId** che rappresenta l'ID del gruppo di risorse in cui vengono create le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="73097-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="73097-128">È possibile assegnare un valore per il nome di questo gruppo di risorse o lasciare che sia l'utente a specificarne uno.</span><span class="sxs-lookup"><span data-stu-id="73097-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="73097-129">Il formato dell'ID è:</span><span class="sxs-lookup"><span data-stu-id="73097-129">The format of the ID is:</span></span>

  <span data-ttu-id="73097-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="73097-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="73097-131">L'esempio seguente illustra un file mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="73097-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="73097-132">Specifica un gruppo di risorse per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="73097-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="73097-133">L'ID della definizione è impostato per usare una definizione denominata **storageApp** in un gruppo di risorse denominato **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="73097-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="73097-134">È possibile modificare questi valori se si desidera usare altri nomi.</span><span class="sxs-lookup"><span data-stu-id="73097-134">You can change these values to use different names.</span></span> <span data-ttu-id="73097-135">Immettere il proprio ID sottoscrizione nell'ID della definizione.</span><span class="sxs-lookup"><span data-stu-id="73097-135">Provide your own subscription ID in the definition ID.</span></span>

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

* <span data-ttu-id="73097-136">**applianceCreateUiDefinition.json**: il portale di Azure usa questo file per generare l'interfaccia utente per gli utenti che creano l'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="73097-137">È possibile definire la modalità con cui gli utenti inseriscono l'input per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="73097-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="73097-138">È possibile usare opzioni come un elenco a discesa, una casella di testo, una casella per la password e altri strumenti di input.</span><span class="sxs-lookup"><span data-stu-id="73097-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="73097-139">Per informazioni sulla creazione di un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="73097-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="73097-140">L'esempio seguente illustra un file applianceCreateUiDefinition.json che consente agli utenti di specificare il prefisso del nome dell'account di archiviazione tramite una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="73097-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
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

<span data-ttu-id="73097-141">Dopo che tutti i file necessari sono pronti, inserirli in un pacchetto con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="73097-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="73097-142">I tre file devono essere a livello di radice nel file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="73097-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="73097-143">Se li si inserisce in una cartella, durante la creazione della definizione di applicazione gestita viene visualizzato un errore che indica che i file necessari non sono presenti.</span><span class="sxs-lookup"><span data-stu-id="73097-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="73097-144">Caricare il pacchetto in una posizione accessibile da dove può essere usato.</span><span class="sxs-lookup"><span data-stu-id="73097-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="73097-145">Nel resto di questo articolo si presuppone che il file con estensione zip sia presente in un contenitore di BLOB di archiviazione accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="73097-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="73097-146">Creare un'applicazione o un gruppo di utenti Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73097-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="73097-147">Il secondo passaggio consiste nel selezionare un gruppo di utenti o un'applicazione per gestire le risorse per conto del cliente.</span><span class="sxs-lookup"><span data-stu-id="73097-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="73097-148">Questo gruppo di utenti o questa applicazione dispone di autorizzazioni per il gruppo di risorse gestito in base al ruolo assegnato.</span><span class="sxs-lookup"><span data-stu-id="73097-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="73097-149">Il ruolo può essere un ruolo di controllo degli accessi in base al ruolo predefinito, ad esempio Proprietario o Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="73097-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="73097-150">È anche possibile concedere a un singolo utente l'autorizzazione per gestire le risorse, ma in genere si assegna questa autorizzazione a un gruppo utenti.</span><span class="sxs-lookup"><span data-stu-id="73097-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="73097-151">Per creare un nuovo gruppo di utenti di Active Directory, vedere [Creare un gruppo e aggiungere membri in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73097-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="73097-152">È necessario munirsi dell'ID oggetto del gruppo di utenti da usare per la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="73097-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="73097-153">L'esempio seguente illustra come ottenere l'ID oggetto dal nome visualizzato del gruppo:</span><span class="sxs-lookup"><span data-stu-id="73097-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="73097-154">Il comando di esempio restituisce il seguente output:</span><span class="sxs-lookup"><span data-stu-id="73097-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="73097-155">Per recuperare solo l'ID oggetto, usare:</span><span class="sxs-lookup"><span data-stu-id="73097-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="73097-156">Ottenere l'ID di definizione del ruolo</span><span class="sxs-lookup"><span data-stu-id="73097-156">Get the role definition ID</span></span>

<span data-ttu-id="73097-157">Ora è necessario l'ID di definizione del ruolo Controllo degli accessi in base al ruolo predefinito a cui si vuole concedere l'accesso all'utente, al gruppo utenti o all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73097-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="73097-158">In genere si usa il ruolo Proprietario, Collaboratore o Lettore.</span><span class="sxs-lookup"><span data-stu-id="73097-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="73097-159">Il comando seguente illustra come ottenere l'ID di definizione per il ruolo Proprietario:</span><span class="sxs-lookup"><span data-stu-id="73097-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="73097-160">Questo comando restituisce il seguente output:</span><span class="sxs-lookup"><span data-stu-id="73097-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
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

<span data-ttu-id="73097-161">È necessario il valore della proprietà "name" dell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="73097-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="73097-162">È possibile recuperare solo tale proprietà con:</span><span class="sxs-lookup"><span data-stu-id="73097-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="73097-163">Creare la definizione di applicazione gestita</span><span class="sxs-lookup"><span data-stu-id="73097-163">Create the managed application definition</span></span>

<span data-ttu-id="73097-164">Se non si dispone già di un gruppo di risorse per archiviare la definizione di applicazione gestita, crearne uno ora:</span><span class="sxs-lookup"><span data-stu-id="73097-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="73097-165">Creare a questo punto la definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-165">Now, create the managed application definition resource.</span></span>

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

<span data-ttu-id="73097-166">I parametri usati nell'esempio precedente sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="73097-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="73097-167">**resource-group**: nome del gruppo di risorse in cui viene creata la definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="73097-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="73097-168">**lock-level**: tipo di blocco inserito nel gruppo di risorse gestito.</span><span class="sxs-lookup"><span data-stu-id="73097-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="73097-169">Impedisce al cliente di eseguire operazioni indesiderate su questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="73097-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="73097-170">ReadOnly è attualmente il solo livello di blocco supportato.</span><span class="sxs-lookup"><span data-stu-id="73097-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="73097-171">Quando ReadOnly è specificato, il cliente può solo leggere le risorse presenti nel gruppo di risorse gestito.</span><span class="sxs-lookup"><span data-stu-id="73097-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="73097-172">**authorizations**: indica l'ID dell'entità di sicurezza e l'ID di definizione del ruolo usati per concedere l'autorizzazione al gruppo di risorse gestito.</span><span class="sxs-lookup"><span data-stu-id="73097-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="73097-173">Viene specificato nel formato `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="73097-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="73097-174">Per questa proprietà si possono specificare anche altri valori.</span><span class="sxs-lookup"><span data-stu-id="73097-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="73097-175">Se sono necessari più valori, deve essere specificata nel formato `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="73097-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="73097-176">I valori multipli sono separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="73097-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="73097-177">**package-file-uri**: posizione del pacchetto dell'applicazione gestita contenente i file modello, che può essere un BLOB del servizio Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73097-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73097-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73097-178">Next steps</span></span>

* <span data-ttu-id="73097-179">Per un'introduzione alle applicazioni gestite, vedere [Panoramica delle applicazioni gestite di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="73097-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="73097-180">Per gli esempi dei file, vedere [Managed Application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples) (Esempi di applicazione gestita).</span><span class="sxs-lookup"><span data-stu-id="73097-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="73097-181">Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="73097-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="73097-182">Per informazioni sulla pubblicazione di applicazioni gestite in Azure Marketplace, vedere [Applicazioni gestite di Azure nel Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="73097-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="73097-183">Per informazioni sull'uso di un'applicazione gestita dal Marketplace, vedere [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md) (Uso delle applicazioni gestite di Azure nel Marketplace).</span><span class="sxs-lookup"><span data-stu-id="73097-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="73097-184">Per informazioni sulla creazione di un file di definizione dell'interfaccia utente per un'applicazione gestita, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="73097-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
