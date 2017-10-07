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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Accesso con privilegi elevati come amministratore tenant con il Controllo degli accessi in base al ruolo

Il Controllo degli accessi in base al ruolo consente agli amministratori tenant di ottenere i privilegi elevati temporanei per l'accesso in modo da poter concedere autorizzazioni superiori rispetto al normale. Un amministratore tenant possa elevare il livello stesso ruolo di amministratore di accesso utente toohello quando necessario. Tale ruolo consente di hello toogrant le autorizzazioni di amministratore del tenant stesso o da altri ruoli hello ambito "/".

Questa funzionalità è importante perché consente tenant hello toosee admin che tutti hello sottoscrizioni presenti in un'organizzazione. Inoltre, consente tutte le sottoscrizioni di hello tooaccess App (ad esempio, la fatturazione e di controllo) di automazione e forniscono una visualizzazione accurata dello stato di hello dell'organizzazione hello per la gestione fatturazione o asset.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Come toouse elevateAccess toogive tenant l'accesso

il processo di base Hello funziona con hello alla procedura seguente:

1. Uso di REST, chiamare *elevateAccess*, che concede si hello ruolo di amministratore di accesso utente "o" ambito.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Creare un [assegnazione di ruolo](/rest/api/authorization/roleassignments) tooassign qualsiasi ruolo in qualsiasi ambito. Hello di esempio seguente mostra le proprietà di hello per l'assegnazione di ruolo di lettore hello "/" ambito:

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

3. Come Amministratore Accesso utenti, è possibile inoltre eliminare le assegnazioni di ruolo nell'ambito "/".

4. Revocare i privilegi di Amministratore Accesso utenti fino a quando non saranno di nuovo necessari.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Come tooundo hello elevateAccess azione

Quando si chiama *elevateAccess* si crea un'assegnazione di ruolo per se stessi, in modo toorevoke quelli privilegi è necessario toodelete hello assegnazione.

1.  Chiamare [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) dove roleName = nome di amministratore di accesso utente toodetermine hello GUID del ruolo di amministratore di accesso utente hello. risposta Hello dovrebbe essere simile al seguente:

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

    Salvare hello GUID da hello *nome* parametro, in questo caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Chiamare [roleAssignments GET](/rest/api/authorization/roleassignments#RoleAssignments_Get) dove principalId = il proprio ObjectId. Elenca tutte le assegnazioni nel tenant di hello. Cercare hello uno in ambito hello è "/" e il nome di hello RoleDefinitionId termina con il ruolo di hello GUID trovato nel passaggio 1. assegnazione di ruolo Hello dovrebbe essere simile al seguente:

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

    Salvare nuovamente, hello GUID da hello *nome* parametro, in questo caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Infine, chiamare [roleAssignments DELETE](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) dove roleAssignmentId = nome hello GUID trovato nel passaggio 2.

## <a name="next-steps"></a>Passaggi successivi

- Maggiori informazioni sulla [gestione del controllo degli accessi in base al ruolo con REST](role-based-access-control-manage-access-rest.md)

- [Gestire le assegnazioni di accesso](role-based-access-control-manage-assignments.md) in hello portale di Azure
