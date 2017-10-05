---
title: Controllo degli accessi in base al ruolo con REST - Azure AD | Microsoft Docs
description: Gestione del controllo degli accessi in base al ruolo con l'API REST
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="46872-103">Gestione del controllo degli accessi in base al ruolo con l'API REST</span><span class="sxs-lookup"><span data-stu-id="46872-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46872-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46872-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="46872-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="46872-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="46872-106">API REST</span><span class="sxs-lookup"><span data-stu-id="46872-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="46872-107">Il controllo degli accessi in base al ruolo nel portale di Azure e nell'API di Azure Resource Manager aiuta a gestire l'accesso alla sottoscrizione e alle risorse a un livello estremamente specifico.</span><span class="sxs-lookup"><span data-stu-id="46872-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="46872-108">Con questa funzionalità è possibile concedere l'accesso a utenti, gruppi o entità servizio di Active Directory assegnando loro dei ruoli in un determinato ambito.</span><span class="sxs-lookup"><span data-stu-id="46872-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="46872-109">Elencare tutte le assegnazioni di ruolo</span><span class="sxs-lookup"><span data-stu-id="46872-109">List all role assignments</span></span>
<span data-ttu-id="46872-110">Elenca tutte le assegnazioni di ruolo all'ambito specificato e agli ambiti secondari.</span><span class="sxs-lookup"><span data-stu-id="46872-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="46872-111">Per elencare le assegnazioni di ruolo, è necessario avere accesso all'operazione `Microsoft.Authorization/roleAssignments/read` nell'ambito.</span><span class="sxs-lookup"><span data-stu-id="46872-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="46872-112">L'accesso a questa operazione viene concesso a tutti i ruoli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="46872-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="46872-113">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-114">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-114">Request</span></span>
<span data-ttu-id="46872-115">Usare il metodo **GET** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="46872-116">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-117">Sostituire *{scope}* con l'ambito per il quale elencare le assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="46872-118">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-119">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-120">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-121">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-122">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="46872-123">Sostituire *{filter}* con la condizione da applicare per filtrare l'elenco di assegnazioni di ruolo:</span><span class="sxs-lookup"><span data-stu-id="46872-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="46872-124">Elencare le assegnazioni di ruolo solo per l'ambito specificato, senza includere le assegnazioni di ruolo negli ambiti secondari: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="46872-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="46872-125">Elencare le assegnazioni di ruolo solo per l'utente, il gruppo o l'applicazione specifici: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="46872-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="46872-126">Elencare le assegnazioni di ruolo per un utente specifico, incluse quelle ereditate dai gruppi | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="46872-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="46872-127">Response</span><span class="sxs-lookup"><span data-stu-id="46872-127">Response</span></span>
<span data-ttu-id="46872-128">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="46872-129">Ottenere informazioni su un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="46872-129">Get information about a role assignment</span></span>
<span data-ttu-id="46872-130">È possibile ottenere informazioni su una singola assegnazione di ruolo specificata dall'identificatore di assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="46872-131">Per ottenere informazioni su un'assegnazione di ruolo, è necessario avere accesso all'operazione `Microsoft.Authorization/roleAssignments/read` .</span><span class="sxs-lookup"><span data-stu-id="46872-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="46872-132">L'accesso a questa operazione viene concesso a tutti i ruoli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="46872-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="46872-133">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-134">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-134">Request</span></span>
<span data-ttu-id="46872-135">Usare il metodo **GET** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="46872-136">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-137">Sostituire *{scope}* con l'ambito per il quale elencare le assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="46872-138">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-139">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-140">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-141">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-142">Sostituire *{role-assignment-id}* con l'identificatore GUID dell'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="46872-143">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="46872-144">Response</span><span class="sxs-lookup"><span data-stu-id="46872-144">Response</span></span>
<span data-ttu-id="46872-145">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="46872-146">Creare un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="46872-146">Create a Role Assignment</span></span>
<span data-ttu-id="46872-147">È possibile creare un'assegnazione di ruolo nell'ambito specificato per l'entità specificata, concedendo il ruolo specificato.</span><span class="sxs-lookup"><span data-stu-id="46872-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="46872-148">Per creare un'assegnazione di ruolo, è necessario avere accesso all'operazione `Microsoft.Authorization/roleAssignments/write` .</span><span class="sxs-lookup"><span data-stu-id="46872-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="46872-149">Tra i ruoli predefiniti, l'accesso a questa operazione viene concesso soltanto ai ruoli *Proprietario* e *Amministratore Accesso utenti*.</span><span class="sxs-lookup"><span data-stu-id="46872-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="46872-150">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-151">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-151">Request</span></span>
<span data-ttu-id="46872-152">Usare il metodo **PUT** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="46872-153">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-154">Sostituire *{scope}* con l'ambito in cui creare le assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="46872-155">Quando si crea un'assegnazione di ruolo in un ambito padre, tutti gli ambiti figlio ereditano la stessa assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="46872-156">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-157">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-158">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="46872-159">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-160">Sostituire *{role-assignment-id}* con un nuovo GUID, che diventa l'identificatore GUID della nuova assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="46872-161">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="46872-162">Per il corpo della richiesta, specificare i valori nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="46872-163">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="46872-163">Element Name</span></span> | <span data-ttu-id="46872-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="46872-164">Required</span></span> | <span data-ttu-id="46872-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="46872-165">Type</span></span> | <span data-ttu-id="46872-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="46872-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46872-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="46872-167">roleDefinitionId</span></span> |<span data-ttu-id="46872-168">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-168">Yes</span></span> |<span data-ttu-id="46872-169">String</span><span class="sxs-lookup"><span data-stu-id="46872-169">String</span></span> |<span data-ttu-id="46872-170">Identificatore del ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-170">The identifier of the role.</span></span> <span data-ttu-id="46872-171">Il formato dell'identificatore è: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="46872-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="46872-172">principalId</span><span class="sxs-lookup"><span data-stu-id="46872-172">principalId</span></span> |<span data-ttu-id="46872-173">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-173">Yes</span></span> |<span data-ttu-id="46872-174">String</span><span class="sxs-lookup"><span data-stu-id="46872-174">String</span></span> |<span data-ttu-id="46872-175">objectId dell'entità di Azure AD (utente, gruppo o entità servizio) a cui deve essere assegnato il ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="46872-176">Response</span><span class="sxs-lookup"><span data-stu-id="46872-176">Response</span></span>
<span data-ttu-id="46872-177">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="46872-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="46872-178">Eliminare un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="46872-178">Delete a Role Assignment</span></span>
<span data-ttu-id="46872-179">È possibile eliminare un'assegnazione di ruolo nell'ambito specificato.</span><span class="sxs-lookup"><span data-stu-id="46872-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="46872-180">Per eliminare un'assegnazione di ruolo, è necessario avere accesso all'operazione `Microsoft.Authorization/roleAssignments/delete` .</span><span class="sxs-lookup"><span data-stu-id="46872-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="46872-181">Tra i ruoli predefiniti, l'accesso a questa operazione viene concesso soltanto ai ruoli *Proprietario* e *Amministratore Accesso utenti*.</span><span class="sxs-lookup"><span data-stu-id="46872-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="46872-182">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-183">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-183">Request</span></span>
<span data-ttu-id="46872-184">Usare il metodo **DELETE** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="46872-185">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-186">Sostituire *{scope}* con l'ambito in cui creare le assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="46872-187">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-188">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-189">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-190">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-191">Sostituire *{role-assignment-id}* con l'identificatore GUID dell'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="46872-192">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="46872-193">Response</span><span class="sxs-lookup"><span data-stu-id="46872-193">Response</span></span>
<span data-ttu-id="46872-194">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="46872-195">Elencare tutti i ruoli</span><span class="sxs-lookup"><span data-stu-id="46872-195">List all Roles</span></span>
<span data-ttu-id="46872-196">Elenca tutti i ruoli disponibili per l'assegnazione nell'ambito specificato.</span><span class="sxs-lookup"><span data-stu-id="46872-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="46872-197">Per elencare i ruoli, è necessario avere accesso all'operazione `Microsoft.Authorization/roleDefinitions/read` nell'ambito.</span><span class="sxs-lookup"><span data-stu-id="46872-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="46872-198">L'accesso a questa operazione viene concesso a tutti i ruoli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="46872-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="46872-199">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-200">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-200">Request</span></span>
<span data-ttu-id="46872-201">Usare il metodo **GET** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="46872-202">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-203">Sostituire *{scope}* con l'ambito per il quale elencare i ruoli.</span><span class="sxs-lookup"><span data-stu-id="46872-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="46872-204">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-205">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-206">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-207">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-208">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="46872-209">Sostituire *{filter}* con la condizione da applicare per filtrare l'elenco di ruoli:</span><span class="sxs-lookup"><span data-stu-id="46872-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="46872-210">Elencare i ruoli disponibili per l'assegnazione nell'ambito specificato e in tutti i relativi ambiti figlio: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="46872-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="46872-211">Cercare un ruolo usando l'esatto nome visualizzato: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="46872-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="46872-212">Usare il form con codifica URL dell'esatto nome visualizzato del ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="46872-213">Ad esempio: `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="46872-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="46872-214">Response</span><span class="sxs-lookup"><span data-stu-id="46872-214">Response</span></span>
<span data-ttu-id="46872-215">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="46872-216">Ottenere informazioni su un ruolo</span><span class="sxs-lookup"><span data-stu-id="46872-216">Get information about a Role</span></span>
<span data-ttu-id="46872-217">È possibile ottenere informazioni su un singolo ruolo specificato dall'identificatore di definizione.</span><span class="sxs-lookup"><span data-stu-id="46872-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="46872-218">Per ottenere informazioni su un singolo ruolo usando il relativo nome visualizzato, vedere [Elencare tutti i ruoli](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="46872-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="46872-219">Per ottenere informazioni su un ruolo, è necessario avere accesso all'operazione `Microsoft.Authorization/roleDefinitions/read` .</span><span class="sxs-lookup"><span data-stu-id="46872-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="46872-220">L'accesso a questa operazione viene concesso a tutti i ruoli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="46872-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="46872-221">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-222">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-222">Request</span></span>
<span data-ttu-id="46872-223">Usare il metodo **GET** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="46872-224">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-225">Sostituire *{scope}* con l'ambito per il quale elencare le assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="46872-226">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-227">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-228">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-229">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-230">Sostituire *{role-definition-id}* con l'identificatore GUID della definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="46872-231">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="46872-232">Response</span><span class="sxs-lookup"><span data-stu-id="46872-232">Response</span></span>
<span data-ttu-id="46872-233">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="46872-234">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="46872-234">Create a Custom Role</span></span>
<span data-ttu-id="46872-235">È possibile creare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-235">Create a custom role.</span></span>

<span data-ttu-id="46872-236">Per creare un ruolo personalizzato, è necessario avere accesso all'operazione `Microsoft.Authorization/roleDefinitions/write` in tutti i `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="46872-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="46872-237">Tra i ruoli predefiniti, l'accesso a questa operazione viene concesso soltanto ai ruoli *Proprietario* e *Amministratore Accesso utenti*.</span><span class="sxs-lookup"><span data-stu-id="46872-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="46872-238">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-239">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-239">Request</span></span>
<span data-ttu-id="46872-240">Usare il metodo **PUT** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="46872-241">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-242">Sostituire *{scope}* con il primo *AssignableScope* del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="46872-243">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="46872-244">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-245">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-246">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-247">Sostituire *{role-definition-id}* con un nuovo GUID, che diventa l'identificatore GUID del nuovo ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="46872-248">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="46872-249">Per il corpo della richiesta, specificare i valori nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-249">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="46872-250">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="46872-250">Element Name</span></span> | <span data-ttu-id="46872-251">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="46872-251">Required</span></span> | <span data-ttu-id="46872-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="46872-252">Type</span></span> | <span data-ttu-id="46872-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="46872-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46872-254">name</span><span class="sxs-lookup"><span data-stu-id="46872-254">name</span></span> |<span data-ttu-id="46872-255">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-255">Yes</span></span> |<span data-ttu-id="46872-256">String</span><span class="sxs-lookup"><span data-stu-id="46872-256">String</span></span> |<span data-ttu-id="46872-257">Identificatore GUID del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="46872-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="46872-258">properties.roleName</span></span> |<span data-ttu-id="46872-259">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-259">Yes</span></span> |<span data-ttu-id="46872-260">String</span><span class="sxs-lookup"><span data-stu-id="46872-260">String</span></span> |<span data-ttu-id="46872-261">Nome visualizzato del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-261">Display name of the custom role.</span></span> <span data-ttu-id="46872-262">La dimensione massima è di 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="46872-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="46872-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="46872-263">properties.description</span></span> |<span data-ttu-id="46872-264">No</span><span class="sxs-lookup"><span data-stu-id="46872-264">No</span></span> |<span data-ttu-id="46872-265">String</span><span class="sxs-lookup"><span data-stu-id="46872-265">String</span></span> |<span data-ttu-id="46872-266">Descrizione del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-266">Description of the custom role.</span></span> <span data-ttu-id="46872-267">La dimensione massima è di 1024 caratteri.</span><span class="sxs-lookup"><span data-stu-id="46872-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="46872-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="46872-268">properties.type</span></span> |<span data-ttu-id="46872-269">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-269">Yes</span></span> |<span data-ttu-id="46872-270">String</span><span class="sxs-lookup"><span data-stu-id="46872-270">String</span></span> |<span data-ttu-id="46872-271">Impostare su "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="46872-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="46872-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="46872-272">properties.permissions.actions</span></span> |<span data-ttu-id="46872-273">sì</span><span class="sxs-lookup"><span data-stu-id="46872-273">Yes</span></span> |<span data-ttu-id="46872-274">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-274">String[]</span></span> |<span data-ttu-id="46872-275">Matrice di stringhe di azione che specifica le operazioni concesse dal ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="46872-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="46872-276">properties.permissions.notActions</span></span> |<span data-ttu-id="46872-277">No</span><span class="sxs-lookup"><span data-stu-id="46872-277">No</span></span> |<span data-ttu-id="46872-278">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-278">String[]</span></span> |<span data-ttu-id="46872-279">Matrice di stringhe di azione che specifica le operazioni da escludere dalle operazioni concesse dal ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="46872-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="46872-280">properties.assignableScopes</span></span> |<span data-ttu-id="46872-281">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-281">Yes</span></span> |<span data-ttu-id="46872-282">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-282">String[]</span></span> |<span data-ttu-id="46872-283">Matrice di ambiti in cui il ruolo personalizzato può essere usato.</span><span class="sxs-lookup"><span data-stu-id="46872-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="46872-284">Response</span><span class="sxs-lookup"><span data-stu-id="46872-284">Response</span></span>
<span data-ttu-id="46872-285">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="46872-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="46872-286">Aggiornare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="46872-286">Update a Custom Role</span></span>
<span data-ttu-id="46872-287">È possibile modificare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-287">Modify a custom role.</span></span>

<span data-ttu-id="46872-288">Per modificare un ruolo personalizzato, è necessario avere accesso all'operazione `Microsoft.Authorization/roleDefinitions/write` in tutti i `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="46872-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="46872-289">Tra i ruoli predefiniti, l'accesso a questa operazione viene concesso soltanto ai ruoli *Proprietario* e *Amministratore Accesso utenti*.</span><span class="sxs-lookup"><span data-stu-id="46872-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="46872-290">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-291">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-291">Request</span></span>
<span data-ttu-id="46872-292">Usare il metodo **PUT** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="46872-293">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-294">Sostituire *{scope}* con il primo *AssignableScope* del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="46872-295">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-296">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-297">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-298">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-299">Sostituire *{role-definition-id}* con l'identificatore GUID del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="46872-300">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="46872-301">Per il corpo della richiesta, specificare i valori nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-301">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="46872-302">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="46872-302">Element Name</span></span> | <span data-ttu-id="46872-303">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="46872-303">Required</span></span> | <span data-ttu-id="46872-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="46872-304">Type</span></span> | <span data-ttu-id="46872-305">Descrizione</span><span class="sxs-lookup"><span data-stu-id="46872-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46872-306">name</span><span class="sxs-lookup"><span data-stu-id="46872-306">name</span></span> |<span data-ttu-id="46872-307">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-307">Yes</span></span> |<span data-ttu-id="46872-308">String</span><span class="sxs-lookup"><span data-stu-id="46872-308">String</span></span> |<span data-ttu-id="46872-309">Identificatore GUID del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="46872-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="46872-310">properties.roleName</span></span> |<span data-ttu-id="46872-311">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-311">Yes</span></span> |<span data-ttu-id="46872-312">String</span><span class="sxs-lookup"><span data-stu-id="46872-312">String</span></span> |<span data-ttu-id="46872-313">Nome visualizzato del ruolo personalizzato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="46872-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="46872-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="46872-314">properties.description</span></span> |<span data-ttu-id="46872-315">No</span><span class="sxs-lookup"><span data-stu-id="46872-315">No</span></span> |<span data-ttu-id="46872-316">String</span><span class="sxs-lookup"><span data-stu-id="46872-316">String</span></span> |<span data-ttu-id="46872-317">Descrizione del ruolo personalizzato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="46872-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="46872-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="46872-318">properties.type</span></span> |<span data-ttu-id="46872-319">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-319">Yes</span></span> |<span data-ttu-id="46872-320">String</span><span class="sxs-lookup"><span data-stu-id="46872-320">String</span></span> |<span data-ttu-id="46872-321">Impostare su "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="46872-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="46872-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="46872-322">properties.permissions.actions</span></span> |<span data-ttu-id="46872-323">sì</span><span class="sxs-lookup"><span data-stu-id="46872-323">Yes</span></span> |<span data-ttu-id="46872-324">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-324">String[]</span></span> |<span data-ttu-id="46872-325">Matrice di stringhe di azione che specifica le operazioni alle quali il ruolo personalizzato aggiornato concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="46872-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="46872-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="46872-326">properties.permissions.notActions</span></span> |<span data-ttu-id="46872-327">No</span><span class="sxs-lookup"><span data-stu-id="46872-327">No</span></span> |<span data-ttu-id="46872-328">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-328">String[]</span></span> |<span data-ttu-id="46872-329">Matrice di stringhe di azione che specifica le operazioni da escludere dalle operazione alle quali il ruolo personalizzato aggiornato concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="46872-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="46872-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="46872-330">properties.assignableScopes</span></span> |<span data-ttu-id="46872-331">Sì</span><span class="sxs-lookup"><span data-stu-id="46872-331">Yes</span></span> |<span data-ttu-id="46872-332">String[]</span><span class="sxs-lookup"><span data-stu-id="46872-332">String[]</span></span> |<span data-ttu-id="46872-333">Matrice di ambiti in cui il ruolo personalizzato aggiornato può essere usato.</span><span class="sxs-lookup"><span data-stu-id="46872-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="46872-334">Response</span><span class="sxs-lookup"><span data-stu-id="46872-334">Response</span></span>
<span data-ttu-id="46872-335">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="46872-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="46872-336">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="46872-336">Delete a Custom Role</span></span>
<span data-ttu-id="46872-337">È possibile eliminare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-337">Delete a custom role.</span></span>

<span data-ttu-id="46872-338">Per eliminare un ruolo personalizzato, è necessario avere accesso all'operazione `Microsoft.Authorization/roleDefinitions/delete` in tutti i `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="46872-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="46872-339">Tra i ruoli predefiniti, l'accesso a questa operazione viene concesso soltanto ai ruoli *Proprietario* e *Amministratore Accesso utenti*.</span><span class="sxs-lookup"><span data-stu-id="46872-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="46872-340">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="46872-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="46872-341">Richiesta</span><span class="sxs-lookup"><span data-stu-id="46872-341">Request</span></span>
<span data-ttu-id="46872-342">Usare il metodo **DELETE** con l'URI seguente:</span><span class="sxs-lookup"><span data-stu-id="46872-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="46872-343">All'interno dell'URI, apportare le sostituzioni seguenti per personalizzare la richiesta:</span><span class="sxs-lookup"><span data-stu-id="46872-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="46872-344">Sostituire *{scope}* con l'ambito in cui eliminare la definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="46872-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="46872-345">Gli esempi seguenti illustrano come specificare l'ambito per livelli differenti:</span><span class="sxs-lookup"><span data-stu-id="46872-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="46872-346">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="46872-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="46872-347">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="46872-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="46872-348">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="46872-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="46872-349">Sostituire *{role-definition-id}* con l'identificatore GUID della definizione di ruolo del ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46872-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="46872-350">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="46872-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="46872-351">Response</span><span class="sxs-lookup"><span data-stu-id="46872-351">Response</span></span>
<span data-ttu-id="46872-352">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="46872-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="46872-353">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46872-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
