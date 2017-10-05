---
title: Accesso con privilegi elevati per l'amministratore tenat - Azure AD | Microsoft Docs
description: Questo argomento descrive i ruoli predefiniti per il controllo degli accessi in base al ruolo.
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
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="532d0-103">Accesso con privilegi elevati come amministratore tenant con il Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="532d0-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="532d0-104">Il Controllo degli accessi in base al ruolo consente agli amministratori tenant di ottenere i privilegi elevati temporanei per l'accesso in modo da poter concedere autorizzazioni superiori rispetto al normale.</span><span class="sxs-lookup"><span data-stu-id="532d0-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="532d0-105">Un amministratore tenant può elevare se stesso al ruolo di Amministratore Accesso utenti quando necessario.</span><span class="sxs-lookup"><span data-stu-id="532d0-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="532d0-106">Tale ruolo offre all'amministratore tenant le autorizzazioni per concedere a se stesso o ad altri i ruoli nell'ambito del "/".</span><span class="sxs-lookup"><span data-stu-id="532d0-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="532d0-107">Questa funzionalità è importante perché consente all'amministratore tenant di visualizzare tutte le sottoscrizioni presenti in un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="532d0-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="532d0-108">Consente inoltre alle app di automazione, ad esempio la fatturazione e il controllo, di accedere a tutte le sottoscrizioni e offrire una visualizzazione accurata dello stato dell'organizzazione per la gestione della fatturazione o delle risorse.</span><span class="sxs-lookup"><span data-stu-id="532d0-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="532d0-109">Procedura: usare elevateAccess per concedere l'accesso ai tenant</span><span class="sxs-lookup"><span data-stu-id="532d0-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="532d0-110">Il processo di base funziona con i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="532d0-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="532d0-111">Usando REST, chiamare *elevateAccess*, che concede all'utente il ruolo di Amministratore Accesso utenti nell'ambito "/".</span><span class="sxs-lookup"><span data-stu-id="532d0-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="532d0-112">Creare un'[assegnazione di ruolo](/rest/api/authorization/roleassignments) per assegnare un ruolo in qualsiasi ambito.</span><span class="sxs-lookup"><span data-stu-id="532d0-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="532d0-113">Nell'esempio seguente vengono illustrate le proprietà per l'assegnazione del ruolo di lettore nell'ambito "/":</span><span class="sxs-lookup"><span data-stu-id="532d0-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="532d0-114">Come Amministratore Accesso utenti, è possibile inoltre eliminare le assegnazioni di ruolo nell'ambito "/".</span><span class="sxs-lookup"><span data-stu-id="532d0-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="532d0-115">Revocare i privilegi di Amministratore Accesso utenti fino a quando non saranno di nuovo necessari.</span><span class="sxs-lookup"><span data-stu-id="532d0-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="532d0-116">Procedura per annullare l'azione elevateAccess</span><span class="sxs-lookup"><span data-stu-id="532d0-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="532d0-117">Quando si chiama *elevateAccess* si crea un'assegnazione di ruolo per se stessi in modo da revocare i privilegi necessari per eliminare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="532d0-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="532d0-118">Chiamare [roleDefinition GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) dove roleName = Amministratore Accesso utenti per determinare il nome GUID del ruolo Amministratore Accesso utenti.</span><span class="sxs-lookup"><span data-stu-id="532d0-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="532d0-119">La risposta dovrebbe avere l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="532d0-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
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

    <span data-ttu-id="532d0-120">Salvare il GUID dal parametro *nome*, in questo caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="532d0-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="532d0-121">Chiamare [roleAssignments GET](/rest/api/authorization/roleassignments#RoleAssignments_Get) dove principalId = il proprio ObjectId.</span><span class="sxs-lookup"><span data-stu-id="532d0-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="532d0-122">Questo elenca tutte le assegnazioni nel tenant.</span><span class="sxs-lookup"><span data-stu-id="532d0-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="532d0-123">Cercare quello in cui l'ambito è "/" e il RoleDefinitionId termina con il nome del ruolo GUID individuato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="532d0-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="532d0-124">L'assegnazione del ruolo dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="532d0-124">The role assignment should look like this:</span></span>

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

    <span data-ttu-id="532d0-125">Di nuovo, salvare il GUID dal parametro *nome*, in questo caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="532d0-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="532d0-126">Infine, chiamare [roleAssignments DELETE](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) dove roleAssignmentId = il nome GUID è stato individuato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="532d0-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="532d0-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="532d0-127">Next steps</span></span>

- <span data-ttu-id="532d0-128">Maggiori informazioni sulla [gestione del controllo degli accessi in base al ruolo con REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="532d0-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="532d0-129">[Gestire le assegnazioni di accesso](role-based-access-control-manage-assignments.md) nel Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="532d0-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
