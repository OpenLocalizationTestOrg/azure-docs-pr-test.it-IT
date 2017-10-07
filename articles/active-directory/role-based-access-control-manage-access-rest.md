---
title: Controllo degli accessi basato su aaaRole con altre, Azure AD | Documenti Microsoft
description: La gestione del controllo di accesso basato sui ruoli con hello API REST
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
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="b676a-103">Controllare l'accesso basato sui ruoli con hello API REST</span><span class="sxs-lookup"><span data-stu-id="b676a-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b676a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b676a-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="b676a-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b676a-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="b676a-106">API REST</span><span class="sxs-lookup"><span data-stu-id="b676a-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="b676a-107">Role-Based Access controllo (RBAC) nel portale di Azure hello e API di gestione risorse di Azure consente di gestire l'accesso tooyour sottoscrizione e le risorse a un livello con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="b676a-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="b676a-108">Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.</span><span class="sxs-lookup"><span data-stu-id="b676a-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="b676a-109">Elencare tutte le assegnazioni di ruolo</span><span class="sxs-lookup"><span data-stu-id="b676a-109">List all role assignments</span></span>
<span data-ttu-id="b676a-110">Elenca tutte le assegnazioni di ruolo hello in hello specificato ambito e subscopes.</span><span class="sxs-lookup"><span data-stu-id="b676a-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="b676a-111">le assegnazioni di ruolo toolist, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/read` operazione nell'ambito di hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="b676a-112">Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="b676a-113">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-114">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-114">Request</span></span>
<span data-ttu-id="b676a-115">Hello utilizzare **ottenere** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="b676a-116">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-117">Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="b676a-118">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-119">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-120">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-121">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-122">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b676a-123">Sostituire *{filter}* con condizione hello che si desidera l'elenco di assegnazione di ruolo di tooapply toofilter hello:</span><span class="sxs-lookup"><span data-stu-id="b676a-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="b676a-124">Elenco di assegnazioni di ruolo per solo hello specificato ambito, escluse le assegnazioni di ruolo hello in subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="b676a-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="b676a-125">Elencare le assegnazioni di ruolo solo per l'utente, il gruppo o l'applicazione specifici: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="b676a-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="b676a-126">Elencare le assegnazioni di ruolo per un utente specifico, incluse quelle ereditate dai gruppi | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="b676a-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="b676a-127">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-127">Response</span></span>
<span data-ttu-id="b676a-128">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="b676a-129">Ottenere informazioni su un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="b676a-129">Get information about a role assignment</span></span>
<span data-ttu-id="b676a-130">Ottiene informazioni su una singola assegnazione di ruolo specificata dall'identificatore di assegnazione di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="b676a-131">tooget informazioni su un'assegnazione di ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/read` operazione.</span><span class="sxs-lookup"><span data-stu-id="b676a-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="b676a-132">Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="b676a-133">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-134">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-134">Request</span></span>
<span data-ttu-id="b676a-135">Hello utilizzare **ottenere** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b676a-136">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-137">Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="b676a-138">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-139">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-140">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-141">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-142">Sostituire *{role-assignment-id}* con identificatore GUID hello hello assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="b676a-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="b676a-143">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b676a-144">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-144">Response</span></span>
<span data-ttu-id="b676a-145">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="b676a-146">Creare un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="b676a-146">Create a Role Assignment</span></span>
<span data-ttu-id="b676a-147">Creare un ruolo di assegnazione di hello specificato ambito per hello specificato principale concessione hello del ruolo specificato.</span><span class="sxs-lookup"><span data-stu-id="b676a-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="b676a-148">toocreate un'assegnazione di ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/write` operazione.</span><span class="sxs-lookup"><span data-stu-id="b676a-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="b676a-149">Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="b676a-150">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-151">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-151">Request</span></span>
<span data-ttu-id="b676a-152">Hello utilizzare **inserire** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b676a-153">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-154">Sostituire *{scope}* con ambito hello in corrispondenza del quale si desiderano toocreate le assegnazioni di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="b676a-155">Quando si crea un'assegnazione di ruolo a un ambito padre, tutti gli ambiti figlio ereditano hello assegnazione di ruolo stesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="b676a-156">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-157">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-158">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="b676a-159">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-160">Sostituire *{role-assignment-id}* con un nuovo GUID, che diventa l'identificatore GUID hello hello nuova assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="b676a-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="b676a-161">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b676a-162">Corpo della richiesta hello, fornire valori hello hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="b676a-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="b676a-163">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="b676a-163">Element Name</span></span> | <span data-ttu-id="b676a-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b676a-164">Required</span></span> | <span data-ttu-id="b676a-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="b676a-165">Type</span></span> | <span data-ttu-id="b676a-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b676a-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b676a-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="b676a-167">roleDefinitionId</span></span> |<span data-ttu-id="b676a-168">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-168">Yes</span></span> |<span data-ttu-id="b676a-169">String</span><span class="sxs-lookup"><span data-stu-id="b676a-169">String</span></span> |<span data-ttu-id="b676a-170">Identificatore Hello del ruolo di hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-170">hello identifier of hello role.</span></span> <span data-ttu-id="b676a-171">formato Hello dell'identificatore hello è:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="b676a-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="b676a-172">principalId</span><span class="sxs-lookup"><span data-stu-id="b676a-172">principalId</span></span> |<span data-ttu-id="b676a-173">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-173">Yes</span></span> |<span data-ttu-id="b676a-174">String</span><span class="sxs-lookup"><span data-stu-id="b676a-174">String</span></span> |<span data-ttu-id="b676a-175">objectId dell'entità hello Azure AD (utente, gruppo o entità servizio) viene assegnato il ruolo di hello toowhich.</span><span class="sxs-lookup"><span data-stu-id="b676a-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="b676a-176">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-176">Response</span></span>
<span data-ttu-id="b676a-177">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="b676a-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="b676a-178">Eliminare un'assegnazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="b676a-178">Delete a Role Assignment</span></span>
<span data-ttu-id="b676a-179">Elimina un'assegnazione di ruolo hello specificato ambito.</span><span class="sxs-lookup"><span data-stu-id="b676a-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="b676a-180">toodelete un'assegnazione di ruolo, è necessario disporre di accesso toohello `Microsoft.Authorization/roleAssignments/delete` operazione.</span><span class="sxs-lookup"><span data-stu-id="b676a-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="b676a-181">Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="b676a-182">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-183">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-183">Request</span></span>
<span data-ttu-id="b676a-184">Hello utilizzare **eliminare** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b676a-185">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-186">Sostituire *{scope}* con ambito hello in corrispondenza del quale si desiderano toocreate le assegnazioni di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="b676a-187">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-188">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-189">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-190">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-191">Sostituire *{role-assignment-id}* con l'id di assegnazione di ruolo hello GUID.</span><span class="sxs-lookup"><span data-stu-id="b676a-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="b676a-192">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b676a-193">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-193">Response</span></span>
<span data-ttu-id="b676a-194">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="b676a-195">Elencare tutti i ruoli</span><span class="sxs-lookup"><span data-stu-id="b676a-195">List all Roles</span></span>
<span data-ttu-id="b676a-196">Elenca tutti i ruoli di hello che sono disponibili per l'assegnazione hello specificato ambito.</span><span class="sxs-lookup"><span data-stu-id="b676a-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="b676a-197">i ruoli toolist, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/read` operazione nell'ambito di hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="b676a-198">Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="b676a-199">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-200">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-200">Request</span></span>
<span data-ttu-id="b676a-201">Hello utilizzare **ottenere** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="b676a-202">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-203">Sostituire *{scope}* con ambito hello per i quali si desiderano toolist ruoli hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="b676a-204">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-205">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-206">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-207">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-208">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b676a-209">Sostituire *{filter}* con condizione hello che si desidera tooapply toofilter hello elenco ruoli:</span><span class="sxs-lookup"><span data-stu-id="b676a-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="b676a-210">Elenco di ruoli disponibili per l'assegnazione hello specificato ambito e i relativi ambiti figlio:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="b676a-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="b676a-211">Cercare un ruolo usando l'esatto nome visualizzato: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="b676a-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="b676a-212">Nome visualizzato hello del ruolo hello nel formato con codifica URL hello utilizzare.</span><span class="sxs-lookup"><span data-stu-id="b676a-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="b676a-213">Ad esempio: `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="b676a-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="b676a-214">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-214">Response</span></span>
<span data-ttu-id="b676a-215">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="b676a-216">Ottenere informazioni su un ruolo</span><span class="sxs-lookup"><span data-stu-id="b676a-216">Get information about a Role</span></span>
<span data-ttu-id="b676a-217">Ottiene informazioni su un singolo ruolo specificato dall'identificatore hello della definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="b676a-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="b676a-218">informazioni tooget su un singolo ruolo usando il nome visualizzato, vedere [l'elenco di tutti i ruoli](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="b676a-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="b676a-219">tooget informazioni su un ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/read` operazione.</span><span class="sxs-lookup"><span data-stu-id="b676a-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="b676a-220">Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="b676a-221">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-222">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-222">Request</span></span>
<span data-ttu-id="b676a-223">Hello utilizzare **ottenere** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b676a-224">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-225">Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="b676a-226">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-227">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-228">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-229">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-230">Sostituire *{role-definition-id}* con identificatore GUID hello hello definizione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="b676a-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="b676a-231">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b676a-232">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-232">Response</span></span>
<span data-ttu-id="b676a-233">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="b676a-234">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="b676a-234">Create a Custom Role</span></span>
<span data-ttu-id="b676a-235">È possibile creare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-235">Create a custom role.</span></span>

<span data-ttu-id="b676a-236">toocreate un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/write` operazione su tutti hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b676a-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="b676a-237">Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="b676a-238">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-239">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-239">Request</span></span>
<span data-ttu-id="b676a-240">Hello utilizzare **inserire** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b676a-241">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-242">Sostituire *{scope}* con hello prima *AssignableScope* di ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="b676a-243">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli.</span><span class="sxs-lookup"><span data-stu-id="b676a-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="b676a-244">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-245">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-246">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-247">Sostituire *{role-definition-id}* con un nuovo GUID, che diventa l'identificatore GUID hello del nuovo ruolo personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="b676a-248">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b676a-249">Corpo della richiesta hello, fornire valori hello hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="b676a-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="b676a-250">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="b676a-250">Element Name</span></span> | <span data-ttu-id="b676a-251">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b676a-251">Required</span></span> | <span data-ttu-id="b676a-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="b676a-252">Type</span></span> | <span data-ttu-id="b676a-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b676a-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b676a-254">name</span><span class="sxs-lookup"><span data-stu-id="b676a-254">name</span></span> |<span data-ttu-id="b676a-255">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-255">Yes</span></span> |<span data-ttu-id="b676a-256">String</span><span class="sxs-lookup"><span data-stu-id="b676a-256">String</span></span> |<span data-ttu-id="b676a-257">Identificatore GUID del ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="b676a-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b676a-258">properties.roleName</span></span> |<span data-ttu-id="b676a-259">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-259">Yes</span></span> |<span data-ttu-id="b676a-260">String</span><span class="sxs-lookup"><span data-stu-id="b676a-260">String</span></span> |<span data-ttu-id="b676a-261">Nome visualizzato del ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-261">Display name of hello custom role.</span></span> <span data-ttu-id="b676a-262">La dimensione massima è di 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b676a-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="b676a-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="b676a-263">properties.description</span></span> |<span data-ttu-id="b676a-264">No</span><span class="sxs-lookup"><span data-stu-id="b676a-264">No</span></span> |<span data-ttu-id="b676a-265">String</span><span class="sxs-lookup"><span data-stu-id="b676a-265">String</span></span> |<span data-ttu-id="b676a-266">Descrizione del ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-266">Description of hello custom role.</span></span> <span data-ttu-id="b676a-267">La dimensione massima è di 1024 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b676a-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="b676a-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="b676a-268">properties.type</span></span> |<span data-ttu-id="b676a-269">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-269">Yes</span></span> |<span data-ttu-id="b676a-270">String</span><span class="sxs-lookup"><span data-stu-id="b676a-270">String</span></span> |<span data-ttu-id="b676a-271">Impostare troppo "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="b676a-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="b676a-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b676a-272">properties.permissions.actions</span></span> |<span data-ttu-id="b676a-273">sì</span><span class="sxs-lookup"><span data-stu-id="b676a-273">Yes</span></span> |<span data-ttu-id="b676a-274">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-274">String[]</span></span> |<span data-ttu-id="b676a-275">Una matrice di azione di stringhe che specifica le operazioni di hello concesse dal ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="b676a-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b676a-276">properties.permissions.notActions</span></span> |<span data-ttu-id="b676a-277">No</span><span class="sxs-lookup"><span data-stu-id="b676a-277">No</span></span> |<span data-ttu-id="b676a-278">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-278">String[]</span></span> |<span data-ttu-id="b676a-279">Una matrice di stringhe di azione specifica hello operazioni tooexclude da operazioni di hello concesse dal ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="b676a-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b676a-280">properties.assignableScopes</span></span> |<span data-ttu-id="b676a-281">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-281">Yes</span></span> |<span data-ttu-id="b676a-282">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-282">String[]</span></span> |<span data-ttu-id="b676a-283">Matrice di ambiti in cui hello può essere utilizzato un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b676a-284">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-284">Response</span></span>
<span data-ttu-id="b676a-285">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="b676a-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="b676a-286">Aggiornare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="b676a-286">Update a Custom Role</span></span>
<span data-ttu-id="b676a-287">È possibile modificare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-287">Modify a custom role.</span></span>

<span data-ttu-id="b676a-288">toomodify un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/write` operazione su tutti hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b676a-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="b676a-289">Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="b676a-290">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-291">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-291">Request</span></span>
<span data-ttu-id="b676a-292">Hello utilizzare **inserire** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b676a-293">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-294">Sostituire *{scope}* con hello prima *AssignableScope* di ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="b676a-295">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-296">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-297">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-298">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-299">Sostituire *{role-definition-id}* con identificatore GUID hello di ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="b676a-300">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b676a-301">Corpo della richiesta hello, fornire valori hello hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="b676a-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="b676a-302">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="b676a-302">Element Name</span></span> | <span data-ttu-id="b676a-303">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b676a-303">Required</span></span> | <span data-ttu-id="b676a-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="b676a-304">Type</span></span> | <span data-ttu-id="b676a-305">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b676a-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b676a-306">name</span><span class="sxs-lookup"><span data-stu-id="b676a-306">name</span></span> |<span data-ttu-id="b676a-307">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-307">Yes</span></span> |<span data-ttu-id="b676a-308">String</span><span class="sxs-lookup"><span data-stu-id="b676a-308">String</span></span> |<span data-ttu-id="b676a-309">Identificatore GUID del ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="b676a-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b676a-310">properties.roleName</span></span> |<span data-ttu-id="b676a-311">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-311">Yes</span></span> |<span data-ttu-id="b676a-312">String</span><span class="sxs-lookup"><span data-stu-id="b676a-312">String</span></span> |<span data-ttu-id="b676a-313">Nome visualizzato del ruolo personalizzata aggiornata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="b676a-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="b676a-314">properties.description</span></span> |<span data-ttu-id="b676a-315">No</span><span class="sxs-lookup"><span data-stu-id="b676a-315">No</span></span> |<span data-ttu-id="b676a-316">String</span><span class="sxs-lookup"><span data-stu-id="b676a-316">String</span></span> |<span data-ttu-id="b676a-317">Descrizione di hello aggiornamento ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="b676a-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="b676a-318">properties.type</span></span> |<span data-ttu-id="b676a-319">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-319">Yes</span></span> |<span data-ttu-id="b676a-320">String</span><span class="sxs-lookup"><span data-stu-id="b676a-320">String</span></span> |<span data-ttu-id="b676a-321">Impostare troppo "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="b676a-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="b676a-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b676a-322">properties.permissions.actions</span></span> |<span data-ttu-id="b676a-323">sì</span><span class="sxs-lookup"><span data-stu-id="b676a-323">Yes</span></span> |<span data-ttu-id="b676a-324">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-324">String[]</span></span> |<span data-ttu-id="b676a-325">Una matrice di stringhe di azione specifica hello toowhich operazioni di hello aggiornato personalizzato ruolo concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="b676a-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b676a-326">properties.permissions.notActions</span></span> |<span data-ttu-id="b676a-327">No</span><span class="sxs-lookup"><span data-stu-id="b676a-327">No</span></span> |<span data-ttu-id="b676a-328">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-328">String[]</span></span> |<span data-ttu-id="b676a-329">Una matrice di azione stringhe specificando tooexclude di operazioni di hello dalle operazioni hello quali hello aggiornato concessioni di ruoli personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="b676a-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b676a-330">properties.assignableScopes</span></span> |<span data-ttu-id="b676a-331">Sì</span><span class="sxs-lookup"><span data-stu-id="b676a-331">Yes</span></span> |<span data-ttu-id="b676a-332">String[]</span><span class="sxs-lookup"><span data-stu-id="b676a-332">String[]</span></span> |<span data-ttu-id="b676a-333">Matrice di ambiti in cui hello può essere usato ruolo personalizzato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b676a-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b676a-334">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-334">Response</span></span>
<span data-ttu-id="b676a-335">Codice di stato: 201</span><span class="sxs-lookup"><span data-stu-id="b676a-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="b676a-336">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="b676a-336">Delete a Custom Role</span></span>
<span data-ttu-id="b676a-337">È possibile eliminare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b676a-337">Delete a custom role.</span></span>

<span data-ttu-id="b676a-338">toodelete un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/delete` operazione su tutti hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b676a-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="b676a-339">Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="b676a-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="b676a-340">Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b676a-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b676a-341">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b676a-341">Request</span></span>
<span data-ttu-id="b676a-342">Hello utilizzare **eliminare** metodo con hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="b676a-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b676a-343">All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:</span><span class="sxs-lookup"><span data-stu-id="b676a-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="b676a-344">Sostituire *{scope}* con ambito hello in corrispondenza del quale si desidera definizione di ruolo toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="b676a-345">Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:</span><span class="sxs-lookup"><span data-stu-id="b676a-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="b676a-346">Sottoscrizione: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b676a-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b676a-347">Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b676a-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b676a-348">Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b676a-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b676a-349">Sostituire *{role-definition-id}* con id di definizione di ruolo hello GUID del ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b676a-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="b676a-350">Sostituire *{api-version}* con 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b676a-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b676a-351">Response</span><span class="sxs-lookup"><span data-stu-id="b676a-351">Response</span></span>
<span data-ttu-id="b676a-352">Codice di stato: 200</span><span class="sxs-lookup"><span data-stu-id="b676a-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b676a-353">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b676a-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
