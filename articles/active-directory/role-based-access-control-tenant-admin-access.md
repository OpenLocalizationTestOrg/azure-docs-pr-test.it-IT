---
title: amministrazione aaaTenant elevare l'accesso, Azure AD | Documenti Microsoft
description: Questo argomento descrive hello compilato nei ruoli per il controllo di accesso basato sui ruoli (RBAC).
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="21768-103">Accesso con privilegi elevati come amministratore tenant con il Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="21768-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="21768-104">Il Controllo degli accessi in base al ruolo consente agli amministratori tenant di ottenere i privilegi elevati temporanei per l'accesso in modo da poter concedere autorizzazioni superiori rispetto al normale.</span><span class="sxs-lookup"><span data-stu-id="21768-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="21768-105">Un amministratore tenant possa elevare il livello stesso ruolo di amministratore di accesso utente toohello quando necessario.</span><span class="sxs-lookup"><span data-stu-id="21768-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="21768-106">Tale ruolo consente di hello toogrant le autorizzazioni di amministratore del tenant stesso o da altri ruoli hello ambito "/".</span><span class="sxs-lookup"><span data-stu-id="21768-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="21768-107">Questa funzionalità è importante perché consente tenant hello toosee admin che tutti hello sottoscrizioni presenti in un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="21768-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="21768-108">Inoltre, consente tutte le sottoscrizioni di hello tooaccess App (ad esempio, la fatturazione e di controllo) di automazione e forniscono una visualizzazione accurata dello stato di hello dell'organizzazione hello per la gestione fatturazione o asset.</span><span class="sxs-lookup"><span data-stu-id="21768-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="21768-109">Come toouse elevateAccess toogive tenant l'accesso</span><span class="sxs-lookup"><span data-stu-id="21768-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="21768-110">il processo di base Hello funziona con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="21768-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="21768-111">Uso di REST, chiamare *elevateAccess*, che concede si hello ruolo di amministratore di accesso utente "o" ambito.</span><span class="sxs-lookup"><span data-stu-id="21768-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="21768-112">Creare un [assegnazione di ruolo](/rest/api/authorization/roleassignments) tooassign qualsiasi ruolo in qualsiasi ambito.</span><span class="sxs-lookup"><span data-stu-id="21768-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="21768-113">Hello di esempio seguente mostra le proprietà di hello per l'assegnazione di ruolo di lettore hello "/" ambito:</span><span class="sxs-lookup"><span data-stu-id="21768-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="21768-114">Come Amministratore Accesso utenti, è possibile inoltre eliminare le assegnazioni di ruolo nell'ambito "/".</span><span class="sxs-lookup"><span data-stu-id="21768-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="21768-115">Revocare i privilegi di Amministratore Accesso utenti fino a quando non saranno di nuovo necessari.</span><span class="sxs-lookup"><span data-stu-id="21768-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="21768-116">Come tooundo hello elevateAccess azione</span><span class="sxs-lookup"><span data-stu-id="21768-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="21768-117">Quando si chiama *elevateAccess* si crea un'assegnazione di ruolo per se stessi, in modo toorevoke quelli privilegi è necessario toodelete hello assegnazione.</span><span class="sxs-lookup"><span data-stu-id="21768-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="21768-118">Chiamare [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) dove roleName = nome di amministratore di accesso utente toodetermine hello GUID del ruolo di amministratore di accesso utente hello.</span><span class="sxs-lookup"><span data-stu-id="21768-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="21768-119">risposta Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="21768-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="21768-120">Salvare hello GUID da hello *nome* parametro, in questo caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="21768-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="21768-121">Chiamare [roleAssignments GET](/rest/api/authorization/roleassignments#RoleAssignments_Get) dove principalId = il proprio ObjectId.</span><span class="sxs-lookup"><span data-stu-id="21768-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="21768-122">Elenca tutte le assegnazioni nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="21768-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="21768-123">Cercare hello uno in ambito hello è "/" e il nome di hello RoleDefinitionId termina con il ruolo di hello GUID trovato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="21768-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="21768-124">assegnazione di ruolo Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="21768-124">hello role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="21768-125">Salvare nuovamente, hello GUID da hello *nome* parametro, in questo caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="21768-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="21768-126">Infine, chiamare [roleAssignments DELETE](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) dove roleAssignmentId = nome hello GUID trovato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="21768-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21768-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21768-127">Next steps</span></span>

- <span data-ttu-id="21768-128">Maggiori informazioni sulla [gestione del controllo degli accessi in base al ruolo con REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="21768-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="21768-129">[Gestire le assegnazioni di accesso](role-based-access-control-manage-assignments.md) in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="21768-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
