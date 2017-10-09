---
title: le assegnazioni di accesso di aaaView risorse di Azure | Documenti Microsoft
description: Visualizzare e gestire tutte le assegnazioni di controllo di accesso basato sui ruoli hello per qualsiasi utente o gruppo in hello portale di Azure
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Visualizzare le assegnazioni di accesso per utenti e gruppi in hello portale di Azure
> [!div class="op_single_selector"]
> * [Gestire l'accesso per utente o gruppo](role-based-access-control-manage-assignments.md)
> * [Gestire l'accesso per risorsa](role-based-access-control-configure.md)

Controllo di accesso basato sui ruoli (RBAC) in hello Azure Active Directory (Azure AD), è possibile gestire l'accesso tooyour Azure le risorse. 

Accesso assegnato con RBAC è accurato perché è possibile limitare le autorizzazioni di hello in due modi:

* **Ambito:** le assegnazioni di ruolo RBAC sono tooa con ambito specifico sottoscrizione, gruppo di risorse o risorse. Un utente con accesso tooa singola risorsa non è possibile accedere alle altre risorse hello stessa sottoscrizione.
* **Ruolo:** nell'ambito di hello di assegnazione di hello, l'accesso è limitato, ulteriormente tramite l'assegnazione di un ruolo. I ruoli possono essere di livello superiore, ad esempio quello di proprietario, o specifici, ad esempio quello di lettore di macchina virtuale.

Ruoli possono essere assegnati solo all'interno di sottoscrizione hello, gruppo di risorse o risorse che sono hello ambito per l'assegnazione di hello. Ma è possibile visualizzare tutte le assegnazioni di hello accesso per un determinato utente o gruppo in un'unica posizione. È possibile disporre le assegnazioni di ruolo too2000 in ogni sottoscrizione. 

Ottenere altre informazioni su come troppo[utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Visualizzare le assegnazioni di accesso
toolook le assegnazioni di hello accesso per un singolo utente o gruppo, di avviare in Azure Active Directory hello [portale di Azure](http://portal.azure.com).

1. Selezionare **Azure Active Directory**. Se questa opzione non è visibile nell'elenco di navigazione, selezionare **più servizi** e quindi scorrere verso il basso toofind **Azure Active Directory**.
2. Selezionare **Utenti e gruppi** e **Tutti gli utenti** o **Tutti i gruppi**. Questo esempio si incentra sui singoli utenti.
    ![Gestire utenti e gruppi in Azure Active Directory - Schermata](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Ricerca per utente hello in base al nome o il nome utente.
4. Selezionare **risorse di Azure** nel pannello utente hello. Vengono visualizzate tutte le assegnazioni di accesso hello per tale utente.

### <a name="read-permissions-tooview-assignments"></a>Tooview assegnazioni delle autorizzazioni di lettura
Questa pagina Mostra solo le assegnazioni di accesso hello di disporre dell'autorizzazione tooread. Ad esempio, si hanno accesso in lettura toosubscription A e passare toohello risorse di Azure blade toocheck assegnazioni dell'utente. Vengono visualizzate le assegnazioni di accesso per la sottoscrizione A, ma non sarà possibile vedere che l'utente dispone di assegnazioni di accesso per la sottoscrizione B.

## <a name="delete-access-assignments"></a>Eliminare le assegnazioni di accesso
Questo pannello, è possibile eliminare le assegnazioni di accesso che sono state assegnate direttamente tooa utente o gruppo. Se l'assegnazione di accesso hello è stata ereditata da un gruppo padre, è necessario toogo toohello risorse o una sottoscrizione e gestire l'assegnazione di hello non esiste.

1. Selezionare hello uno desiderato toodelete hello elenco di tutte le assegnazioni di hello accesso per un utente o gruppo.
2. Selezionare **rimuovere** e quindi **Sì** tooconfirm.
    ![Rimuovere un'assegnazione di accesso - Schermata](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Passaggi successivi

* Introduzione a controllo di accesso basato sui ruoli troppo[utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](role-based-access-control-configure.md)
* Vedere hello [ruoli predefiniti RBAC](role-based-access-built-in-roles.md)

