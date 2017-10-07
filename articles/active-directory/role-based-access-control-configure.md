---
title: Controllo di accesso basato su aaaRole nel portale di Azure hello | Documenti Microsoft
description: Guida introduttiva nella gestione degli accessi in base al ruolo di controllo di accesso in hello portale di Azure. Utilizzare le risorse tooyour le autorizzazioni di ruolo assegnazioni tooassign.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Utilizzo delle risorse di controllo di accesso basato sui ruoli toomanage accesso tooyour sottoscrizione di Azure
> [!div class="op_single_selector"]
> * [Gestire l'accesso per utente o gruppo](role-based-access-control-manage-assignments.md)
> * [Gestire l'accesso per risorsa](role-based-access-control-configure.md)

Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure. Usa tale controllo, è possibile concedere solo quantità di hello di accesso che gli utenti devono tooperform i processi. In questo articolo consente di ottenere attivo e in esecuzione con RBAC in hello portale di Azure. Per altri dettagli sulla gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](role-based-access-control-what-is.md).

All'interno di ogni sottoscrizione, è possibile concedere le assegnazioni di ruolo too2000. 

## <a name="view-access"></a>Visualizzare l'accesso
È possibile vedere chi ha accesso tooa risorsa, gruppo di risorse o sottoscrizione dal pannello principale in hello [portale di Azure](https://portal.azure.com). Ad esempio, è necessario toosee che dispone di accesso tooone i gruppi di risorse:

1. Selezionare **gruppi di risorse** hello sinistra sulla barra di navigazione hello.  
    ![Gruppi di risorse, icona](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Nome hello selezionare hello del gruppo di risorse da hello **gruppi di risorse** blade.
3. Selezionare **Access control (IAM)** dal menu a sinistra di hello.  
4. Pannello di controllo di accesso Hello Elenca tutti gli utenti, gruppi e le applicazioni che sono state concesse gruppo di risorse toohello di accesso.  
   
    ![Screenshot del pannello Utenti: accesso ereditato e assegnato](./media/role-based-access-control-configure/view-access.png)

Si noti che l'ambito di alcuni ruoli sono troppo**questa risorsa** mentre altri sono **Inherited** da un altro ambito. L'accesso è assegnato in modo specifico il gruppo di risorse toohello o ereditato da una sottoscrizione di assegnazione toohello padre.

> [!NOTE]
> Gli amministratori delle sottoscrizioni classico e coamministratori sono considerati proprietari della sottoscrizione hello nel nuovo modello di RBAC hello.

## <a name="add-access"></a>Aggiungere un accesso
È concedere accesso dall'interno sottoscrizione ambito hello hello assegnazione di ruolo, gruppo di risorse o risorse hello.

1. Selezionare **Aggiungi** nel Pannello di controllo di accesso hello.  
2. Ruolo selezionare hello che si desidera tooassign da hello **selezionare un ruolo** blade.
3. Selezionare hello utente, gruppo o dell'applicazione nella directory che si desidera toogrant accesso a. È possibile cercare la directory hello con i nomi visualizzati, indirizzi di posta elettronica e gli identificatori di oggetto.  
   
    ![Screenshot del pannello Aggiungi utenti: casella di ricerca](./media/role-based-access-control-configure/grant-access2.png)
4. Selezionare **OK** assegnazione hello toocreate. Hello **aggiunta utente** popup tiene traccia dell'avanzamento di hello.  
    ![Indicatore di stato dell'aggiunta di utenti, schermata](./media/role-based-access-control-configure/addinguser_popup.png)

Dopo aver aggiunto correttamente un'assegnazione di ruolo, che verrà visualizzata nella hello **utenti** blade.

## <a name="remove-access"></a>Rimuovere un accesso
1. Posiziona il cursore sul nome hello di assegnazione di hello che si desidera tooremove. Una casella di controllo viene visualizzato il nome toohello successivo.
2. Utilizzare hello caselle di controllo tooselect uno o più assegnazioni di ruolo.
2. Selezionare **Rimuovi**.  
3. Selezionare **Sì** rimozione hello tooconfirm.

Le assegnazioni ereditate non possono essere rimosse. Se è necessario tooremove un'assegnazione ereditata, è necessario toodo in hello ambito in cui è stato creato l'assegnazione di ruolo hello. In hello **ambito** colonna, accanto troppo**Inherited** è presente un collegamento che consente di passare toohello risorse in cui è stato assegnato questo ruolo. Passare toohello risorse elencate assegnazione di ruolo tooremove hello.

![Screenshot del pannello Utenti: l'accesso ereditato disabilita il pulsante Rimuovi](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Accesso toomanage altri strumenti
È possibile assegnare i ruoli e gestire l'accesso con i comandi di Azure RBAC in strumenti diversi da hello portale di Azure.  Seguire hello collegamenti toolearn informazioni sui prerequisiti hello e iniziare a utilizzare i comandi di Azure RBAC hello.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md)
* [API REST](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Passaggi successivi
* [Creare un report della cronologia delle modifiche relative all'accesso](role-based-access-control-access-change-history-report.md)
* Vedere hello [ruoli predefiniti RBAC](role-based-access-built-in-roles.md)
* Definire i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)

